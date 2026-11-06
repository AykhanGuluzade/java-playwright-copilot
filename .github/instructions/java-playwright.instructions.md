---
applyTo: "src/test/java/**/*.java"
---
# Java and Playwright implementation

Use Java 17-compatible source unless the repository explicitly selects another version. Match existing package names. Use PascalCase Java files/classes, camelCase methods/fields and UPPER_SNAKE_CASE constants. Prefer final fields, clear types and records for small immutable data objects. Explain non-obvious decisions; avoid boilerplate comments on every method or locator.

Initialize Page-backed locators in the constructor, never in a field initializer that runs before Page assignment. Do not copy TypeScript `await`, fixture-extension objects, `expect`, `test.describe`, or `playwright.config.ts` into Java.

Prefer `getByRole` with an accessible name or `getByLabel`. Use `getByTestId` when the application has a stable test-ID contract; configure custom attributes through `playwright.selectors().setTestIdAttribute(...)`. Scope within components and check ambiguous matches. Positional selectors require a meaningful, stable ordering contract.

Use actions' auto-waiting and retrying assertions in assertion helpers. Do not default navigation to NETWORKIDLE or add `Thread.sleep`/`waitForTimeout` to make a test pass. Wait for the relevant UI or response condition. Register response/navigation waits before the triggering action where required by the Java API.

Playwright Java is not thread-safe. Scenario-owned objects must remain on the same thread. Do not add global shared pages to improve speed. Reuse browsers only after a thread-owned lifecycle is implemented and verified.

Keep HTTP clients separate from page objects and dispose APIRequestContext resources. Validate response bodies with actual schemas if the project has them; do not invent schema files or claim type declarations validate JSON at runtime.

See [architecture](../../docs/java/reference/architecture.md), [Java style](../../docs/java/reference/java-style.md), and [parallel execution](../../docs/java/reference/parallel-execution.md).

Use [CLI evidence](../../docs/java/reference/cli-browser.md) to author locators. Temporary CLI refs are not durable Java selectors. CLI-generated snippets must be integrated with this scenario lifecycle and verified through Gradle/Cucumber.
