# Java BDD and CLI workflow review checklist

- The relevant G1/G2/G3 record identifies the actual plan, diff, evidence and decision source; no fabricated approval or self-declared independent acceptance.
- Each scenario verifies a real requirement or is explicitly labelled a proposed case. CLI-observed UI behavior has not replaced approved business expectations.
- Browser work used CLI with an observed version, authorized target, correct role/data and fresh evidence. Separate reproductions are distinguished from actual Java browser attachments.
- Locators match evidence and are durable; no temporary snapshot refs embedded as framework selectors. Ambiguous matches are resolved deliberately.
- Feature discovery, glue, suite filters and injection agree; no missing/ambiguous steps, duplicate suite execution or invented runner commands.
- Java compiles; documented commands and dependencies exist; the agent browser CLI and Java runtime are distinguished.
- Locators initialize after Page assignment. Pages/components act, assertion helpers verify, thin steps delegate and hooks manage lifecycle.
- No removed/weakened assertions, boolean-only substitutes for retrying checks, unauthorized skips/fixme, swallowed failures, sleeps or retries-until-green.
- Scenario resources stay on their owning thread; data and artifacts are isolated; cleanup survives setup and scenario failures.
- Fresh Gradle/Cucumber reports cover the intended nonzero selection. Exit codes and failed/skipped/undefined/pending states remain visible; CLI success is not Java execution evidence.
- Repairs retain the original failure, supported cause, at most two candidate attempts per failure per task and before/after plus adjacent-case evidence. Product defects remain visible.
- Local auth state, generated CLI files and sensitive artifacts are excluded from source control and controlled before sharing. Only the task's own CLI session is closed/detached.
- Required checks, platform permissions and human/repository decisions enforce acceptance; Markdown itself is not an approval service.

Give actionable findings with exact file/line, trigger and consequence. Distinguish confirmed defects from unverified integration assumptions. Read [review gates](review-gates.md) for the full decision/evidence contract.
