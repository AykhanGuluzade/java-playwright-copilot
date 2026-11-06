# Executable BDD runner

The reference build aligns Cucumber artifacts with `cucumber-bom:8.0.4`, JUnit with `junit-bom:6.1.3`, and uses `playwright:1.64.0`. It declares Jackson Databind 3.2.4 as the JSON provider required by Cucumber 8 reporting. The JUnit Platform suite selects the `features` resource package and glue `com.omc.automation`. Cucumber root-engine discovery is disabled to prevent a second run beside the suite. The Gradle test filter selects the suite class.

Required files are [build](../templates/gradle-build.md), [suite](../templates/runner.md), [properties](../templates/junit-platform-properties.md), [session/settings](../templates/fixture.md) and [hooks](../templates/hooks.md). PicoContainer gives hooks and steps the same BrowserSession within one scenario and a different instance for the next scenario.

## Commands after materializing the Java runtime

```sh
./gradlew testClasses
./gradlew playwrightInstall
./gradlew test
./gradlew test -Dcucumber.filter.tags=@smoke
./gradlew test -Dcucumber.filter.name='Display the submitted'
```

`BASE_URL` is required for execution, not compilation. Set it through an approved environment mechanism. The sample does not assume a dotenv dependency or read `.env` automatically. The Gradle test task sets `PLAYWRIGHT_SKIP_BROWSER_DOWNLOAD=1`: browsers are installed explicitly, so scenario startup does not silently download additional engines. The suite supports Chromium by default; Firefox/WebKit selection requires their binaries to be installed through the Java CLI task after adding the required installation arguments. Use the same `PLAYWRIGHT_BROWSERS_PATH` for installation and execution if you customize the browser cache.

The build forwards tag, name and selected parallel properties explicitly into the test JVM. A property on the Gradle launcher is not automatically a property inside that JVM. Do not add an unsupported feature-file argument to a Node test command.

A finalized verification task requires fresh JSON evidence and at least one executed scenario. A filtered-empty run must fail. Undefined/pending/ambiguous steps and failed assertions remain unsuccessful executions; reporting must preserve that result. Binding-only dry runs are not passing browser tests.

Source: [Cucumber JUnit Platform engine](https://github.com/cucumber/cucumber-jvm/tree/main/cucumber-junit-platform-engine), [Gradle Java testing](https://docs.gradle.org/current/userguide/java_testing.html).

Agent browser exploration and failure reproduction use [Playwright CLI](cli-browser.md). Its sessions do not replace this runner. Preserve original reports before another test run clears them, and distinguish CLI reproduction from actual Java scenario execution.
