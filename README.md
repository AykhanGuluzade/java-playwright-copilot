# Java Playwright + Cucumber for GitHub Copilot

Copilot instructions for **Java 17+**, **Playwright Java**, **Cucumber-JVM**, **JUnit Platform** and **Gradle**, with **Playwright CLI** for browser exploration and evidence. No Playwright MCP connection is required or configured.

## Start here

1. Open the [user guide](docs/USER_GUIDE.md) for package explanations, step-by-step setup and copyable planner/generator/healer/reviewer prompts.
2. Use [Copilot setup](docs/COPILOT_SETUP.md) and [CLI setup](docs/java/reference/cli-browser.md) as focused setup references.
3. Read [review gates](docs/java/reference/review-gates.md) before planning, generating or repairing tests.
4. Use [migration](docs/MIGRATION.md) and [the complete original-file map](MIGRATION_MAP.md) to retire the old Cline rules.
5. If the Java runtime is missing, materialize [the reference templates](docs/java/templates/index.md) and adapt the sample business behavior to OMC.

The download contains Markdown instructions and code templates. Copying them does not install CLI/browser binaries, convert TypeScript sources, change GitHub settings or connect internal services.

## Workflows

| Copilot profile | Task skill | Result |
|---|---|---|
| `bdd-planner` | `plan-coverage` | CLI exploration and a requirement-linked plan; Gate G1 |
| `java-bdd-generator` | `generate-java-bdd` | Browser-verified Java/BDD changes and Gradle evidence; Gate G2 |
| `java-bdd-healer` | `diagnose-java-failures` | Evidence-based diagnosis and bounded candidate repairs; Gate G3 |
| `java-bdd-reviewer` | `review-java-bdd` | Separate review of the plan, implementation or repair |

Select the matching prompt/profile where supported, or ask Copilot to read its SKILL.md explicitly. These are selectable roles; they do not run a background orchestration service.

## Package layout

- `.github/copilot-instructions.md`: shared Java/BDD and CLI contract.
- `.github/instructions/`: three file-scoped rule sets.
- `.github/skills/`: four task workflows with discovery metadata.
- `.github/prompts/`: four IDE entry points.
- `.github/agents/`: planner, generator, healer and reviewer profiles.
- `docs/USER_GUIDE.md`: complete onboarding guide, package explanations and example prompts.
- `docs/java/reference/`: CLI usage, review gates and framework guidance.
- `docs/java/templates/`: Java/Gradle examples with exact target paths.

## Runtime decisions

| Concern | Decision |
|---|---|
| Browser authoring and investigation | Playwright CLI shell commands; Java code output where supported |
| Test execution | Cucumber-JVM on JUnit Platform, launched by Gradle |
| Scenario state | PicoContainer injection; fresh state per scenario |
| Browser lifecycle | Scenario-owned Playwright/browser/context/page; same owning thread |
| Assertions | Dedicated assertion helpers called from thin steps |
| Page/component objects | Locators and actions |
| Parallelism | Sequential baseline, then explicitly configured scenario concurrency |
| Reports | Fresh Cucumber JSON, HTML, XML and messages |
| Repairs | At most two candidate attempts per failure per task; preserve business expectations |

CLI snippets and successful exploration are inputs to authoring, not proof that the Java scenario passed. Review uses the actual diff and fresh Gradle/Cucumber execution evidence. See [sources](SOURCES.md), [changes](CHANGES.md) and [validation limits](docs/VALIDATION.md).
