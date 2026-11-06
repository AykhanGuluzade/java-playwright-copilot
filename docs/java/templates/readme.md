# Project README outline

- Explain the application behaviors this Java Playwright/Cucumber suite verifies.
- List the actual JDK, wrapper, Cucumber/JUnit/Playwright versions and supported browsers.
- Explain which template files have been materialized and which integrations remain proposed.
- Document required environment variables without secrets and identify the authorized test environment.
- Give verified compile, browser-install, scenario-selection and execution commands from the real build.
- State the report/artifact paths, expected nonzero scenario count and failure/skip semantics.
- Link the Copilot setup, architecture, data isolation, parallel execution and review guidance.
- Describe actual CI/enterprise contracts, permissions, retention and ownership.

For the supplied reference build, valid commands after setup are:

```sh
./gradlew testClasses
./gradlew playwrightInstall
./gradlew test -Dcucumber.filter.tags=@smoke
```

State that BASE_URL is required for execution and that the sample business flow needs adaptation to the application. Do not invent a license, internal support matrix, publishing destination, Allure task or undocumented Copilot CLI command.

Document [CLI browser setup](../reference/cli-browser.md), Java output configuration and [G1/G2/G3 review gates](../reference/review-gates.md). Distinguish planner/generator/healer shell work from Gradle/Cucumber execution. State that optional Java browser attachment is not installed by the baseline templates.
