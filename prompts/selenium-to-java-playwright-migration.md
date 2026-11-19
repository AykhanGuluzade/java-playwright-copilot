# Devin Prompt — Migrate an Existing Selenium Automation Repository to Java Playwright

## Role and mission

Act as a **Principal SDET, Java Test Automation Architect, and Legacy Automation Migration Engineer**.

You have access to:
- **SOURCE_SELENIUM_REPO**: the existing Selenium automation repository (read-only during this assignment).
- **TARGET_PLAYWRIGHT_REPO**: a separate repository where the migrated **Java + Playwright** framework and tests will live.
- Optional Confluence pages, CI/CD documentation, test environment details, and business requirements.

Discover the actual repositories from the Devin session context. If either repository is missing or ambiguous, document the blocker; **never assume this prompt repository is the migration destination**.

**Goal:** migrate the existing Selenium automation suite to idiomatic, reliable Java Playwright in the separate target repository while preserving verified business coverage, assertions, test data behavior, reporting, and CI compatibility. Do not simply replace Selenium method calls one-to-one.

## Non-negotiable guardrails

1. Treat the Selenium repository as the **source of truth for current test intent**, but distinguish its assertions from incidental implementation and potential bugs.
2. Do **not modify, delete, or push to the Selenium source repository**.
3. Work in the **target Playwright repository only**, on a dedicated feature branch; do not force-push or overwrite existing work. If branch creation or write access is unavailable, deliver migration artifacts and report the limitation.
4. Inspect the target first. **Reuse existing Gradle, Java, Cucumber, Playwright, FAST, TURBO, FAST Run Service, reporting, and CI conventions where present**. Do not introduce these tools just because they are named here.
5. Never expose secrets, copy credentials, download production customer information, bypass enterprise authentication, or execute destructive actions in any environment.
6. Prefer stable, maintainable Playwright locators and assertions. Avoid blanket sleeps, brittle positional XPath, unnecessary JavaScript injection, and manually reimplementing Playwright's auto-waiting.
7. Preserve test behavior only when it matches documented expected behavior; flag questionable legacy assertions for review, never silently change their business meaning.
8. Do not declare a scenario migrated or passing without actual execution evidence.

## Phase 1 — Discover and inventory the Selenium suite

Read the source repository and inventory:
- Build system, Java version, dependencies, test runner (JUnit/TestNG/Cucumber), and test organization.
- Selenium WebDriver initialization, browser options, remote/grid execution, driver lifecycle, and parallelization.
- Feature files, glue/step definitions, page objects, base classes, custom wrappers, wait utilities, hooks, listeners, data providers, fixtures, and shared helpers.
- Tagging, test suites, parameterization, screenshots, tracing/logging, reporting, reruns, CI jobs, environment configuration, secrets references, and external service interactions.
- Tests involving frames, shadow DOM, multiple windows/tabs, dialogs, file uploads/downloads, tables, grids, dynamic elements, authentication, API calls, and asynchronous UI state.
- Duplicate, flaky, disabled, obsolete, and high-value scenarios, using evidence rather than guesswork.

Create `migration/01-source-inventory.md` and a scenario matrix with source file, scenario name, tags, business purpose, dependencies, assertions, risk, estimated migration complexity, and priority.

## Phase 2 — Inspect the target repository and design the migration

Check whether TARGET_PLAYWRIGHT_REPO already has a functional Java Playwright project. Identify what must be preserved or improved.

Recommend architecture for:
- Gradle project structure and version compatibility.
- Java Playwright browser/context/page lifecycle, isolation, and safe parallelism.
- Cucumber integration if used by the source or required by the target.
- Page Object Model versus reusable component objects and workflow abstractions.
- Configuration and secrets references, multi-environment runs, test data, and cleanup.
- Browser artifacts: screenshots, traces, videos when supported, and failure diagnostics.
- API setup and backend verification where appropriate.
- CI execution, tagging, selective suites, reporting, and flaky-test handling.

Write `migration/02-target-architecture.md`, an explicit Selenium-to-Playwright migration mapping, and a prioritized phased plan. **Do not copy legacy Selenium abstractions if Playwright has a better native approach.**

## Phase 3 — Define conversion rules

Use these principles consistently:

| Legacy Selenium pattern | Preferred Java Playwright approach |
|---|---|
| WebDriver and driver manager | Playwright + Browser + isolated BrowserContext + Page |
| `findElement` and chained WebElements | `Locator` with user-facing role/label/text/test-id selectors where appropriate |
| Implicit/explicit polling and `Thread.sleep` | Playwright auto-waiting, `Locator` assertions, explicit condition waits only when needed |
| Selenium `click`/`sendKeys` | `Locator.click()`, `fill()`, `press()`, etc. |
| Selenium assertions around WebElements | Playwright `assertThat(locator)` and Java assertions for business data |
| `switchTo().frame` | `FrameLocator` |
| Window handles | Page/context popup handling |
| JavaScript executors | Native Playwright features first; evaluate scripting only when justified |
| Selenium screenshots | Playwright screenshot and trace facilities |
| Shared static driver | Scenario/test-scoped context and page objects, thread-safe execution |

Adapt to **the Java Playwright API actually installed**, not TypeScript-only examples. Check version-specific APIs and do not invent methods. Handle dialogs, downloads, retries, timeouts, and navigation without arbitrary sleeps.

Preserve existing Gherkin text/tags and business assertions where valid; update step implementation underneath. Only edit feature text if necessary, explaining the change.

## Phase 4 — Implement incrementally in the separate target repository

1. Establish a minimal buildable, runnable Java Playwright foundation in TARGET_PLAYWRIGHT_REPO, aligned with its existing conventions.
2. Migrate a **representative vertical slice** first: one simple smoke scenario, one complex workflow, and one scenario requiring special UI interaction or test data.
3. Run compilation, static checks, and available tests. Record environment/access blockers clearly.
4. After the vertical slice is validated, migrate remaining scenarios in small, reviewable batches prioritized by business criticality, stability, reuse, and complexity.
5. Improve locator resilience, diagnostic artifacts, and scenario isolation as you migrate.
6. Do not delete obsolete source tests automatically. Flag candidates for owner approval.
7. Create small commits, report each batch, and prepare a target-repository pull request **only if permitted in the session**. Never merge without authorization.

If live application access or credentials are unavailable, you may implement and compile tests, but explicitly mark their execution as **not verified**.

## Phase 5 — Verify behavioral parity

Build `migration/03-parity-matrix.md` containing, for each original scenario:
- Selenium source path and scenario identifier.
- New Playwright path and scenario identifier.
- Preserved business rules and expected assertions.
- Test data, fixtures, environment dependencies, and tags.
- Status: Not started / Implemented / Compiles / Executed passing / Blocked / Requires business review.
- Execution evidence (commands, environment, date, logs/artifact locations).
- Any intentional differences and reason.

Compare assertion coverage, scenario coverage, browser/environment compatibility, parallel execution, and runtime where measured; **do not invent speed or flakiness improvements**. Validate both positive and negative paths and cleanup behavior.

## Phase 6 — CI/CD and operational handover

Propose or implement, when authorized, CI changes in the target repository for:
- Gradle test tasks and parameterized environments.
- Smoke, regression, and tagged runs; Cucumber tags if applicable.
- Browser installation/cache strategy consistent with enterprise security controls.
- Parallel workers with isolated contexts/test data.
- Report and trace artifact capture and retention.
- Credentials via approved secret management, not source code.
- Clearly separated compile, test, and environment-dependent execution results.

Provide `migration/04-ci-handover.md` with commands that have actually been verified, troubleshooting guidance, and manual setup prerequisites.

## Required final deliverables

In the **target repository**, produce:
1. A working Java Playwright framework aligned to target conventions.
2. Migrated tests organized for long-term maintenance.
3. `migration/01-source-inventory.md`
4. `migration/02-target-architecture.md`
5. `migration/03-parity-matrix.md`
6. `migration/04-ci-handover.md`
7. `migration/05-open-risks-and-decisions.md`
8. A concise `migration/MIGRATION-SUMMARY.md` including implemented count, executed-pass count, blocked count, outstanding source scenarios, notable design decisions, and evidence links.

For important claims reference source and target repository paths and relevant symbols/lines. Classify conclusions as **Verified**, **Inferred**, or **Unknown**. Explain any missing information.

## Definition of done

Migration is complete only when the agreed in-scope scenarios have source-to-target traceability, their business assertions are preserved or explicitly approved as changed, the target compiles, required environments have successfully run the tests, reporting/CI is documented, and remaining blockers are accepted. Otherwise report an accurate partial migration with next steps.

## Initial action

Start by identifying and confirming SOURCE_SELENIUM_REPO and TARGET_PLAYWRIGHT_REPO from the connected Devin workspace. Inspect both repositories, provide the inventory and phased migration plan, and then proceed with the smallest representative vertical slice. Do not begin with a blind bulk conversion.
