# Java conventions

Use package paths matching Java declarations, PascalCase `.java` classes, camelCase methods/fields and UPPER_SNAKE_CASE constants. Keep Gherkin filenames in kebab-case. Environment variables use UPPER_SNAKE_CASE. These conventions replace conflicting JavaScript/TypeScript naming rules.

Favor final fields, constructor injection and immutable records for test inputs. Avoid raw collections and unchecked casts. Use explicit null/blank validation at configuration boundaries. Prefer small cohesive actions; do not add inheritance, builders or wrappers without a concrete reuse need.

Explain contracts or surprising behavior in comments. Javadoc is useful for maintained APIs; every locator and trivial method does not need a generated paragraph. Keep source examples compiling against the selected Java release and actual dependency versions.

Java Playwright calls are synchronous. Do not transliterate TypeScript `await`, Node fixture objects, `expect` or `test.describe`. Use `com.microsoft.playwright.assertions.PlaywrightAssertions.assertThat` for UI checks in assertion helpers. Use ordinary assertion libraries for pure domain calculations only when actually declared in the build.

`Page`, `BrowserContext` and Playwright instances must remain on their owner thread. Avoid async executors around page actions. Close allocated resources even when setup or a scenario fails.

Compiler checks and declared quality tools enforce what they can. Do not claim Checkstyle, Spotless, PMD or a Java formatter is configured unless its task and configuration actually exist. The reference build provides compiler and scenario verification, not imaginary lint tasks.
