---
applyTo: "**/*.gradle,**/*.gradle.kts,gradle/**,.github/workflows/**,Dockerfile*"
---
# Gradle, CI and reporting

Use the actual Gradle wrapper and pinned Java/Cucumber/JUnit/Playwright versions. Keep Cucumber artifacts aligned through its BOM and JUnit artifacts through its BOM. Review dependency changes and rerun checks; do not silently replace the organization-managed FAST dependency set with the standalone example pins.

The Java build executes the Cucumber engine via JUnit Platform. Do not invent Node/npm test scripts, Allure tasks, schema validators, formatter tasks or publishing services. Add and verify any task before documenting it as available.

Install browser binaries for the exact Playwright Java version. Linux workers need matching OS dependencies; the reference build exposes `playwrightInstall -PwithDeps=true`. Browser selection beyond Chromium also needs matching binaries installed. Verify image/version compatibility before container execution.

Preserve failing exit codes. Collect existing reports/artifacts in CI with an always-run upload step, including on test failure. A reporting job must not turn an unsuccessful test run green. Configure retention and access restrictions for sensitive artifacts. Keep source trees and agent instructions free of generated run state.

Run compiler checks and actual scenario execution; reject zero executed scenarios. A dry run proves binding/discovery only. Keep Cucumber parallelism, Gradle forks and container shards as separate controls with a documented resource budget and nonoverlapping scenario ownership.

Actual repository protections, required checks and runtime permissions enforce review. Markdown does not implement an approval service. See [CI template](../../docs/java/templates/ci.md), [reporting](../../docs/java/reference/reporting.md), and [enterprise contracts](../../docs/java/reference/enterprise-integration.md).

Agent browser work uses Playwright CLI, separate from the Gradle Java test runner. Keep the approved CLI/Node tool version documented; do not add an MCP service or treat CLI action success as a CI test pass. Apply [review gates](../../docs/java/reference/review-gates.md) to changes and repair evidence.
