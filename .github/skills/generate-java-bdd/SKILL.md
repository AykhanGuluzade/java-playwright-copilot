---
name: generate-java-bdd
description: Use Playwright CLI evidence to generate Java Playwright/Cucumber tests from an accepted plan and prepare their diff and Gradle results for review.
---

# CLI generator for Java BDD

Read the repository instructions, accepted plan and relevant implementation. Load [CLI guidance](../../../docs/java/reference/cli-browser.md) and [review gates](../../../docs/java/reference/review-gates.md). Check G1's actual decision/source; resolve any expected-result ambiguity before implementing dependent scenarios. Reuse existing business steps, page objects and assertion helpers.

1. Start an isolated CLI session with the planned role, environment and data. Replay every planned action and inspect the planned result. Retain an evidence path and observed result for each important verification. CLI actions succeeding alone do not verify the business outcome. Record contradictions as potential defects; do not change expected behavior to match a broken UI.
2. Use Java CLI code output and observed role/name, label or test-ID locators as authoring inputs. Refresh stale refs. If the installed CLI lacks Java output, translate the observed action/locator deliberately and validate the Java API; never paste TypeScript runner constructs or ephemeral `eNN` refs into framework selectors. Mark any inaccessible flow unverified.
3. Build a vertical BDD slice: `.feature`, scenario-scoped data/state, page/component actions, dedicated assertion helpers and thin Cucumber glue. Follow [the complete templates](../../../docs/java/templates/index.md) and preserve FAST-managed versions/lifecycle. Configure [the Java runner](../../../docs/java/reference/bdd-runner.md) if this task includes runtime migration.
4. Compile and run the affected scenarios through Gradle. Inspect fresh reports, intended selection, nonzero executed counts, all step bindings and exit status. Check adjacent cases affected by reused steps or page objects. For a newly established runtime, also demonstrate a deliberate assertion failure in an isolated fixture, then restore it.
5. Prepare **G2** with the diff, plan-to-feature mapping, CLI evidence and actual execution results. A separate reviewer checks intent, false-pass risks and evidence completeness. Missing access or runtime failures keep execution unverified; they do not become a pass or a waived gate.

Complete authorized local implementation and checks before acceptance review. Do not commit, push, merge or publish without the relevant authorization. Close/detach your CLI session. Generation is complete only when its actual state and remaining review decisions are reported honestly.
