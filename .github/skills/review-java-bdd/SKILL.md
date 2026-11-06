---
name: review-java-bdd
description: Independently review CLI-based Java Playwright/Cucumber plans, generated tests or repairs against their review gates and execution evidence.
---

# Review Java BDD

Inspect the relevant plan, actual diff and surrounding runtime. Read [review gates](../../../docs/java/reference/review-gates.md) and [the checklist](../../../docs/java/reference/review-checklist.md). Identify whether this is a G1 plan review, G2 generation review or G3 repair review. Use an actual approval source; a prefilled template or author claim is not an independent approval.

- G1: Check requirement references, expected results, business risks, role/data assumptions and which flows were actually explored through CLI. Observed UI behavior alone cannot establish correctness.
- G2: Trace planned outcomes through Gherkin bindings, scenario state, page actions and Java assertion helpers. Verify that locators come from evidence and remain durable, Java APIs are valid, and fresh Gradle reports cover the intended scenarios. CLI snippets or snapshots alone are insufficient execution evidence.
- G3: Compare original failure, cause, repair attempts, changed lines and reruns. Reject weakened checks, suppressed failures, unsupported expectation changes or exhausted repair loops. Shared-step/page changes need adjacent coverage evidence.

Report actionable findings with severity, exact file/line, trigger and consequence. State which checks ran, what was supplied and what remains unverified. Return a concrete disposition: ready for acceptance, changes required, or blocked on named evidence/decision. Do not claim human acceptance, actual tool execution or enforced merge protection that has not happened.

This read/search-only reviewer does not edit or run Gradle/CLI commands. Request missing execution evidence from the author or an authorized execution role; inspect it before changing the review disposition. Actual host permissions, CI checks and repository review controls enforce the boundary.
