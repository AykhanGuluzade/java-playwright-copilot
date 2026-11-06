# Scenario-owned browser session

PicoContainer supplies one BrowserSession to hooks and steps per scenario. The reference creates its Playwright objects on the executing scenario thread.

Target: `src/test/java/com/omc/automation/support/TestSettings.java`

```java
package com.omc.automation.support;

import java.net.URI;

public record TestSettings(String baseUrl, String browser, boolean headless) {
    public static TestSettings fromEnvironment() {
        String url = System.getenv("BASE_URL");
        if (url == null || url.isBlank()) {
            throw new IllegalStateException("BASE_URL must identify the authorized test environment.");
        }
        URI uri = URI.create(url);
        if (uri.getHost() == null || !("https".equals(uri.getScheme()) || "http".equals(uri.getScheme()))) {
            throw new IllegalArgumentException("BASE_URL must be an absolute HTTP(S) URL.");
        }
        String browser = System.getenv().getOrDefault("BROWSER", "chromium");
        String headless = System.getenv().getOrDefault("HEADLESS", "true");
        if (!headless.equals("true") && !headless.equals("false")) {
            throw new IllegalArgumentException("HEADLESS must be true or false.");
        }
        return new TestSettings(url, browser, Boolean.parseBoolean(headless));
    }
}
```

Target: `src/test/java/com/omc/automation/support/BrowserSession.java`

```java
package com.omc.automation.support;

import com.microsoft.playwright.Browser;
import com.microsoft.playwright.BrowserContext;
import com.microsoft.playwright.Page;
import com.microsoft.playwright.Playwright;
import com.microsoft.playwright.Tracing;
import io.cucumber.java.Scenario;

import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.UUID;

public final class BrowserSession implements AutoCloseable {
    private Playwright playwright;
    private Browser browser;
    private BrowserContext context;
    private Page page;
    private Path artifactDirectory;
    private long ownerThread;
    private boolean tracing;

    public void start() throws IOException {
        if (playwright != null) {
            throw new IllegalStateException("The scenario already owns a browser session.");
        }
        ownerThread = Thread.currentThread().getId();
        TestSettings settings = TestSettings.fromEnvironment();
        artifactDirectory = Files.createDirectories(Path.of("build", "artifacts", UUID.randomUUID().toString()));
        playwright = Playwright.create();
        playwright.selectors().setTestIdAttribute("data-testid");
        var launch = new com.microsoft.playwright.BrowserType.LaunchOptions().setHeadless(settings.headless());
        browser = switch (settings.browser()) {
            case "chromium" -> playwright.chromium().launch(launch);
            case "firefox" -> playwright.firefox().launch(launch);
            case "webkit" -> playwright.webkit().launch(launch);
            default -> throw new IllegalArgumentException("BROWSER must be chromium, firefox or webkit.");
        };
        context = browser.newContext(new Browser.NewContextOptions().setBaseURL(settings.baseUrl()));
        context.tracing().start(new Tracing.StartOptions()
            .setScreenshots(true).setSnapshots(true).setSources(false));
        tracing = true;
        page = context.newPage();
    }

    public Page page() {
        checkOwner();
        if (page == null) {
            throw new IllegalStateException("Start the scenario browser session before using its page.");
        }
        return page;
    }

    public void finish(Scenario scenario) {
        checkOwner();
        RuntimeException problem = null;
        if (scenario.isFailed() && page != null && !page.isClosed()) {
            try {
                byte[] screenshot = page.screenshot(new Page.ScreenshotOptions()
                    .setPath(artifactDirectory.resolve("failure.png")));
                scenario.attach(screenshot, "image/png", "failure screenshot");
            } catch (RuntimeException error) {
                problem = error;
            }
        }
        if (tracing && context != null) {
            try {
                if (scenario.isFailed()) {
                    Path trace = artifactDirectory.resolve("trace.zip");
                    context.tracing().stop(new Tracing.StopOptions().setPath(trace));
                    scenario.log("Local trace: " + trace);
                } else {
                    context.tracing().stop();
                }
            } catch (RuntimeException error) {
                problem = combine(problem, error);
            } finally {
                tracing = false;
            }
        }
        try {
            close();
        } catch (RuntimeException error) {
            problem = combine(problem, error);
        }
        if (problem != null) {
            if (scenario.isFailed()) {
                scenario.log("Artifact capture or cleanup also failed: " + problem.getClass().getSimpleName());
            } else {
                throw problem;
            }
        }
    }

    @Override
    public void close() {
        checkOwner();
        RuntimeException problem = null;
        try {
            problem = closeResource(context, problem);
            problem = closeResource(browser, problem);
            problem = closeResource(playwright, problem);
        } finally {
            page = null;
            context = null;
            browser = null;
            playwright = null;
            tracing = false;
        }
        if (problem != null) {
            throw problem;
        }
    }

    private void checkOwner() {
        if (ownerThread != 0 && ownerThread != Thread.currentThread().getId()) {
            throw new IllegalStateException("Playwright objects must stay on their owning scenario thread.");
        }
    }

    private static RuntimeException closeResource(AutoCloseable resource, RuntimeException prior) {
        if (resource == null) {
            return prior;
        }
        try {
            resource.close();
            return prior;
        } catch (Exception error) {
            RuntimeException wrapped = error instanceof RuntimeException runtime
                ? runtime : new IllegalStateException("Browser resource cleanup failed.", error);
            return combine(prior, wrapped);
        }
    }

    private static RuntimeException combine(RuntimeException prior, RuntimeException next) {
        if (prior == null) {
            return next;
        }
        if (prior != next) {
            prior.addSuppressed(next);
        }
        return prior;
    }
}
```

Trace recording starts before actions; failed scenarios retain it, successful ones discard it. Cleanup handles partial setup and preserves the primary failure. A cleanup failure on a passing scenario fails execution. The baseline uses explicit `BASE_URL`, `BROWSER` and `HEADLESS` environment variables; it does not silently load an undeclared dotenv library.
