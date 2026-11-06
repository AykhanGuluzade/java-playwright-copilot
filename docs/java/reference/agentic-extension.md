# CLI-based planner, generator and healer

The Copilot profiles and skills implement an authoring workflow for Java Playwright/Cucumber. Browser interaction uses Playwright CLI shell commands; execution uses Gradle/JUnit Platform/Cucumber-JVM. Playwright MCP is unavailable and is not a fallback. The Java CLI tasks in the build install Java-version browser binaries and open traces; they are distinct from the agent browser CLI.

| Stage | Input | Output and gate |
|---|---|---|
| Planner | Requirements, existing coverage, authorized target | CLI observations, requirement-linked plan, G1 decision |
| Generator | Accepted plan and existing framework | Java/BDD diff, live browser evidence, Gradle results, G2 review |
| Healer | Original failed Java execution and expected outcome | Cause classification, bounded candidate diff, reruns, G3 review |
| Reviewer | The relevant plan/diff and evidence | Separate review disposition and unresolved findings |

Read [CLI usage](cli-browser.md) for sessions, Java output, evidence and optional attachment. Read [review gates](review-gates.md) for decisions and stopping conditions. An accepted, sufficiently detailed task can establish G1; copying an approval template cannot.

This adapts the useful explore/verify/reproduce patterns of the native Playwright agents. It does not claim that their Playwright Test-specific setup, write-test, run or debug tools execute Java/Cucumber. Do not invoke those tools or use `npx playwright test` to validate Java features. CLI-generated Java snippets still require scenario lifecycle, reusable glue, assertions, compilation and execution in this framework.

Profiles can be selected independently. Handoffs consist of actual Markdown plans, diffs and evidence references; no dispatcher, approval agent, `run()` API or background orchestration state is assumed. No automatic merge or publication is included. Actual host permissions, CI checks and human review govern acceptance.

Sources: [CLI introduction](https://playwright.dev/agent-cli/introduction), [CLI authoring workflow](https://playwright.dev/agent-cli/commands/codegen), [native Playwright Test Agents](https://playwright.dev/docs/test-agents).
