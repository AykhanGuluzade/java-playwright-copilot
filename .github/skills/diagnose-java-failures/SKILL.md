---
name: diagnose-java-failures
description: Diagnose Java Playwright/Cucumber failures using Gradle artifacts and Playwright CLI, make bounded authorized repairs, and prepare evidence for review.
---

# CLI healer for Java BDD

Read repository instructions, the failed scenario, approved business expectation, current diff and original execution evidence. Load [CLI guidance](../../../docs/java/reference/cli-browser.md), [reporting](../../../docs/java/reference/reporting.md) and [review gates](../../../docs/java/reference/review-gates.md).

1. Preserve the original failure, reports and artifact paths before a rerun clears them. Identify the failed action/assertion and classify the cause as a test defect, product defect, data/environment issue or unresolved. If needed, reproduce only the affected selection through the real Gradle runner.
2. Use a dedicated CLI session to reproduce the same role/data/flow and collect snapshots, locator evidence, relevant console/network details and the observed result. Label a separate reproduction as such. The baseline closes the Java browser after each scenario; do not claim CLI attached to that failed browser. Use the optional Java attachment route only if it has actually been implemented and verified.
3. For a supported test defect within an authorized fix request, make the smallest candidate repair. At most **two candidate repair attempts for the same failure per task**. Record the hypothesis, changed lines and before/after evidence for each. An identical retry, agent switch or new CLI session does not reset this bound. Further work needs new evidence or an explicitly revised instruction.
4. Rerun the affected and relevant adjacent Java/Cucumber scenarios through Gradle; inspect fresh counts, statuses, exit codes and the diff. A passing rerun does not by itself prove a correct repair. Preserve the expected business outcome and meaningful negative checks.
5. Prepare **G3**: diagnosis, original failure, attempt history, minimal diff, rerun evidence and separate review disposition. Product defects remain visible; data/environment problems get a specific corrective recommendation. Stop candidate edits when the cause remains uncertain or the bound is reached.

Do not weaken/remove assertions, alter expected business values, add skip tags/fixme, swallow exceptions, add arbitrary sleeps, broaden locators or increase retries/timeouts merely to pass. A business expectation change returns to G1 for explicit acceptance. Diagnosis-only requests do not authorize edits. Complete authorized local verification before acceptance review; never auto-merge. Close/detach the CLI session.
