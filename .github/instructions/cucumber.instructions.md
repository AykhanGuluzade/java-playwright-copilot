---
applyTo: "src/test/resources/features/**/*.feature,src/test/java/**/steps/**/*.java,src/test/java/**/hooks/**/*.java,src/test/java/**/runner/**/*.java,src/test/resources/junit-platform.properties"
---
# Cucumber-JVM behavior and lifecycle

Gherkin describes business outcomes, preconditions and actions. Link scenarios to real acceptance criteria through agreed IDs. Do not equate one scenario per visible UI element, keyword similarity, or a scenario count with verified requirement coverage. Keep secrets and unnecessary selectors/URLs out of feature text.

Reuse parameterized steps where the business meaning matches. Avoid giant generic steps and duplicate expressions. Use Background only for genuinely shared preconditions and Scenario Outline only for meaningful variations. Every example must have a verifiable expected outcome.

Put glue in `com.omc.automation` subpackages and use `io.cucumber.java` annotations. Share BrowserSession and scenario data through PicoContainer constructor injection. Create page objects after the Before hook has started the session. Do not mix Cucumber hooks with JUnit/Node Playwright Test fixtures.

Steps delegate to pages/actions and assertion helpers. Assertions belong to assertion helpers, including real negative-path assertions. Hooks do not contain test assertions. Browser-context cleanup must run after failures and partial setup; diagnostic failures must not replace the original scenario failure.

Use the JUnit Platform suite and properties in [runner setup](../../docs/java/reference/bdd-runner.md). Forward tag/parallel properties through Gradle explicitly. Verify feature discovery, all step bindings and nonzero executed scenarios. Do not rely on a Playwright Test command to execute `.feature` files.

CLI exploration informs the scenario but does not define its expected business result. Preserve G1 acceptance criteria through G2 generation and G3 repair; see [review gates](../../docs/java/reference/review-gates.md).
