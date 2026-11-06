---
name: plan-coverage
description: Explore an authorized application with Playwright CLI and plan requirement-linked Java Playwright/Cucumber coverage for review.
---

# CLI planner

Read the repository instructions, supplied acceptance criteria and existing features. Load [CLI guidance](../../../docs/java/reference/cli-browser.md) and [review gates](../../../docs/java/reference/review-gates.md). Identify actual requirement references; do not manufacture IDs or derive business expectations solely from the current UI.

1. Confirm the authorized target, role, starting state, data/reset needs and scope of permitted interactions. Check the installed CLI/version and its help. If CLI or application access is unavailable, produce a clearly marked requirements-only draft and record the blocked browser checks.
2. Explore with a dedicated CLI session using snapshots, navigation and permitted interactions. Map critical user journeys and relevant validation/boundary paths. Use synthetic data and reversible operations within scope. Record observations, fresh evidence paths, unexpected behavior and questions that affect correctness.
3. Produce `docs/test-plans/<task-slug>.md` when file writing is available, otherwise return the complete plan in chat. Include source criteria, scenario titles, preconditions/data, actions, expected results, positive/negative cases, requirement mapping, existing coverage to reuse, affected pages and intended Gradle selection. Separate observed facts, approved requirements and proposed cases.
4. Present the concrete plan at **G1**. Record the actual approval source or pending decision. Existing explicit approval of a sufficiently detailed task can satisfy G1. Do not proceed with dependent generation where expected business behavior remains unresolved; continue independent work within scope.

Planning edits are limited to plan/review documentation and local evidence, not Java implementation or feature changes. Close your own CLI session, or detach from an attached external browser, after collecting evidence. Use [architecture](../../../docs/java/reference/architecture.md) and [feature guidance](../../../docs/java/templates/feature.md) as needed.
