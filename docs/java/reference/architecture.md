# Java automation architecture

The executable path is **Gradle Test -> JUnit Platform suite -> Cucumber engine -> Java glue -> page/actions and assertion helpers -> Playwright Java -> application**.

Copilot supports authorship and diagnosis outside this runtime. Skills, prompts and custom profiles provide instructions; they do not add a dispatcher, scheduler, `run()` method, persistent state schema, or approval service. User-selected work can proceed within the authorized scope without simulating handoffs for every locator.

## Responsibilities

| Layer | Responsibility |
|---|---|
| `runner` | Feature discovery, engine selection and glue configuration |
| `hooks` / `support` | Scenario ownership, browser lifecycle and diagnostics |
| `steps` | Bind Gherkin to business actions/verifications |
| `pages` / `components` | Application interaction and scoped locators |
| `assertions` | Business expectations using retrying Java assertions |
| `data` | Immutable synthetic inputs and explicit overrides |

Initialize Page-backed fields only after receiving the Page. Share scenario objects using PicoContainer constructor injection. Do not share mutable state between scenarios. The initial implementation creates a browser per scenario for clarity; a later optimization may reuse a browser per owning thread after measuring and verifying isolation.

One assertion-placement policy applies across instructions, samples and reviews. Dedicated assertion helpers are a project convention, not a restriction imposed by Playwright itself. A component is justified by reusable UI behavior, not by a requirement to wrap every element in a class.

[Template index](../templates/index.md), [runner](bdd-runner.md), [parallelism](parallel-execution.md), [enterprise integration](enterprise-integration.md).
