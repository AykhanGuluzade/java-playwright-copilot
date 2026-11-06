# Cucumber Java lifecycle hooks

Cucumber owns the scenario lifecycle, including failure diagnostics and cleanup.

Target: `src/test/java/com/omc/automation/hooks/ScenarioHooks.java`

```java
package com.omc.automation.hooks;

import com.omc.automation.support.BrowserSession;
import io.cucumber.java.After;
import io.cucumber.java.Before;
import io.cucumber.java.Scenario;

import java.io.IOException;

public final class ScenarioHooks {
    private final BrowserSession session;

    public ScenarioHooks(BrowserSession session) {
        this.session = session;
    }

    @Before
    public void startBrowser() throws IOException {
        session.start();
    }

    @After
    public void captureAndClose(Scenario scenario) {
        session.finish(scenario);
    }
}
```

Use with [BrowserSession](fixture.md). These are `io.cucumber.java` hooks, not JUnit hooks or a Node fixture-extension object. Do not add a second browser owner in a FAST-managed lifecycle.
