# User guide: Java Playwright and Cucumber with GitHub Copilot

Updated: 2026-11-06. Browser workflow: **Playwright CLI**. Test runtime: **Java Playwright + Cucumber-JVM + JUnit Platform + Gradle**.

This guide explains the package, shows how to adopt it in an existing framework, and provides prompts for planning, generation, healing and review. The IDE walkthrough uses VS Code with GitHub Copilot. Other supported Copilot IDEs can use the same files, subject to their actual discovery and tool support.

## Contents

- [How the workflow fits together](#how-the-workflow-fits-together)
- [Package explanations](#package-explanations)
- [Step-by-step setup](#step-by-step-setup)
- [Example prompts and review gates](#example-prompts-and-review-gates)
- [Troubleshooting](#troubleshooting)
- [Validation and sources](#validation-and-sources)

## How the workflow fits together

Copilot reads repository guidance, adopts a selected role and follows the relevant skill. The role uses Playwright CLI to inspect the application and collect browser evidence. Generated Java/Cucumber tests execute through the actual Gradle runner. The reviewer assesses the plan, diff and evidence before owner acceptance.

```text
Requirements -> Planner -> G1: accepted plan
                           |
                           v
                      Generator -> Gradle/Cucumber execution -> G2: reviewed change
                                            |
                                          failure
                                            v
                                        Healer -> rerun -> G3: reviewed repair

Playwright CLI supplies browser observations throughout authoring/investigation.
The reviewer performs a separate review at each relevant gate.
```

CLI commands succeeding do not prove that a Java test passed. Compilation does not prove scenario execution. Acceptance uses actual requirements, the changed code and fresh execution evidence.

The download consists of Markdown instructions and code examples embedded in Markdown. Copying it does not install dependencies, turn examples into Java files, configure internal services or automatically start agents. Playwright MCP is outside this workflow.

## Package explanations

Paths in this section are relative to the extracted `java-playwright-copilot/` folder. After adoption, their relative layout is preserved in the framework repository.

### Root documentation

| File | What it is for |
|---|---|
| [README.md](../README.md) | Starting point: package layout, roles and runtime decisions. |
| [CHANGES.md](../CHANGES.md) | Corrections from the legacy Cline package and the subsequent CLI/user-guide revisions. |
| [MIGRATION_MAP.md](../MIGRATION_MAP.md) | Destination and disposition of all 115 originally reviewed Markdown files. |
| [SOURCES.md](../SOURCES.md) | Documentation sources, explicit reference dependency versions and CI action pins. |

### `.github/copilot-instructions.md`: shared guidance

[The repository instruction file](../.github/copilot-instructions.md) defines the common Java/Cucumber architecture, CLI browser workflow, Gradle execution, assertion policy, scenario isolation, evidence requirements and review boundaries. Keep it consistent with your real framework's package names and commands.

### `.github/instructions/`: file-specific rules

Each file has `applyTo` metadata describing which repository paths it targets.

| File | Responsibility |
|---|---|
| [java-playwright.instructions.md](../.github/instructions/java-playwright.instructions.md) | Java style, constructor-initialized locators, waiting, owner-thread rules and page/component responsibilities. |
| [cucumber.instructions.md](../.github/instructions/cucumber.instructions.md) | Business-focused Gherkin, step reuse, injection, lifecycle and runner wiring. |
| [build-ci.instructions.md](../.github/instructions/build-ci.instructions.md) | Gradle/dependency management, browser installation, CI, reporting and failure propagation. |

### `.github/agents/`, `.github/skills/` and `.github/prompts/`

These folders describe different parts of the same workflow:

- **Agents** define selectable roles and tool aliases.
- **Skills** define the detailed procedure, inputs, evidence and stopping conditions. Each skill folder contains `SKILL.md`.
- **Prompts** provide short IDE entry points that select a profile and load a skill. They are not shell commands.

| Agent profile | Skill | Prompt | Expected result |
|---|---|---|---|
| [bdd-planner](../.github/agents/bdd-planner.agent.md) | [plan-coverage](../.github/skills/plan-coverage/SKILL.md) | [plan-coverage.prompt.md](../.github/prompts/plan-coverage.prompt.md) | Requirement-linked plan and CLI observations for G1. |
| [java-bdd-generator](../.github/agents/java-bdd-generator.agent.md) | [generate-java-bdd](../.github/skills/generate-java-bdd/SKILL.md) | [generate-java-bdd.prompt.md](../.github/prompts/generate-java-bdd.prompt.md) | Java/BDD diff, browser evidence and Gradle results for G2. |
| [java-bdd-healer](../.github/agents/java-bdd-healer.agent.md) | [diagnose-java-failures](../.github/skills/diagnose-java-failures/SKILL.md) | [diagnose-java-failures.prompt.md](../.github/prompts/diagnose-java-failures.prompt.md) | Cause classification, bounded candidate repairs and reruns for G3. |
| [java-bdd-reviewer](../.github/agents/java-bdd-reviewer.agent.md) | [review-java-bdd](../.github/skills/review-java-bdd/SKILL.md) | [review-java-bdd.prompt.md](../.github/prompts/review-java-bdd.prompt.md) | Findings, evidence gaps and a review disposition. |

The first three profiles declare read, search, edit and execution aliases. The planner's permitted edits are limited by its instructions to plan/review documentation and local evidence. The reviewer is read/search-only and does not run tests or edit files. Actual host permissions and supported tools govern execution; a profile is not a background service or a technical approval barrier.

### `docs/`: adoption and verification

| File | Responsibility |
|---|---|
| [USER_GUIDE.md](USER_GUIDE.md) | This complete onboarding guide, package explanations and prompt examples. |
| [COPILOT_SETUP.md](COPILOT_SETUP.md) | Short reference for installation locations, discovery and tool expectations. |
| [MIGRATION.md](MIGRATION.md) | Replacing legacy rules and optionally establishing the Java runtime. |
| [VALIDATION.md](VALIDATION.md) | Checks actually completed, historical runtime results and remaining integration limits. |

### `docs/java/reference/`: detailed framework guidance

These documents supply task-specific context when a skill needs it.

| Guide | What it explains |
|---|---|
| [architecture.md](java/reference/architecture.md) | Layer responsibilities and the executable path through Gradle, Cucumber and Playwright Java. |
| [bdd-runner.md](java/reference/bdd-runner.md) | Feature discovery, glue, JUnit Platform, tag/property forwarding and execution checks. |
| [cli-browser.md](java/reference/cli-browser.md) | CLI setup, Java output, sessions, snapshots, evidence and optional live Java attachment. |
| [agentic-extension.md](java/reference/agentic-extension.md) | How the CLI-based planner, generator, healer and reviewer fit together. |
| [review-gates.md](java/reference/review-gates.md) | G1/G2/G3 decisions, required evidence, acceptance sources and stopping conditions. |
| [review-checklist.md](java/reference/review-checklist.md) | Concrete checks for lifecycle, coverage, assertions, locators, reports and repairs. |
| [java-style.md](java/reference/java-style.md) | Naming, constructor injection, immutable inputs and maintainable Java conventions. |
| [test-data.md](java/reference/test-data.md) | Synthetic data, configuration, scenario isolation, provisioning and cleanup ownership. |
| [parallel-execution.md](java/reference/parallel-execution.md) | Safe concurrency and the distinction between scenario threads, Gradle forks and containers. |
| [reporting.md](java/reference/reporting.md) | Cucumber reports, failure screenshots/traces, optional videos and preservation of evidence. |
| [api-testing.md](java/reference/api-testing.md) | Java API requests, setup/cleanup helpers, response assertions and resource lifecycle. |
| [accessibility.md](java/reference/accessibility.md) | Accessibility-related checks, scanner integration and limits of locator/snapshot evidence. |
| [enterprise-integration.md](java/reference/enterprise-integration.md) | Contracts to verify for FAST, Lightspeed Enterprise, FAST Run Service and TURBO. |
| [maintenance.md](java/reference/maintenance.md) | Dependency changes, documentation upkeep and keeping commands aligned with the real build. |

The enterprise guide records integration boundaries; it does not implement internal adapters or establish a supported dependency matrix.

### `docs/java/templates/`: Java and configuration examples

Each complete code example identifies its intended target file. Materialize related files together when building a new runtime. For an existing framework, adapt only the examples you need and preserve its managed architecture.

The reference Java namespace is `com.omc.automation`. Its packages have these responsibilities:

| Java package | Template | Example classes | Responsibility |
|---|---|---|---|
| `runner` | [runner.md](java/templates/runner.md) | `RunCucumberTest` | Launch Cucumber through the JUnit Platform suite. |
| `hooks` | [hooks.md](java/templates/hooks.md) | `ScenarioHooks` | Start and finish each scenario's browser lifecycle. |
| `support` | [fixture.md](java/templates/fixture.md) | `TestSettings`, `BrowserSession` | Read configuration, own resources, capture diagnostics and clean up. |
| `steps` | [step-definitions.md](java/templates/step-definitions.md) | `LoginSteps` | Connect Gherkin to actions and assertion helpers. |
| `pages` | [page-object.md](java/templates/page-object.md) | `LoginPage` | Hold page locators and application actions. |
| `components` | [component.md](java/templates/component.md) | `NavigationComponent` | Encapsulate a reusable part of the UI. |
| `assertions` | [assertions.md](java/templates/assertions.md) | `LoginAssertions` | Verify business outcomes with retrying Java assertions. |
| `data` | [test-data.md](java/templates/test-data.md) | `UserData` | Hold immutable synthetic scenario input. |

Separate assertion helpers are this package's convention. Playwright itself does not require that particular package structure. The sample login flow is illustrative and must be adapted to actual OMC behavior.

The remaining template documents support execution and documentation:

| Template | Purpose |
|---|---|
| [gradle-build.md](java/templates/gradle-build.md) | Example build/settings, dependencies, Java browser installation and verification tasks. |
| [junit-platform-properties.md](java/templates/junit-platform-properties.md) | Discovery, reporting and baseline execution settings. |
| [feature.md](java/templates/feature.md) | A sample feature connected to the supplied Java implementation. |
| [scenario.md](java/templates/scenario.md) | Business-focused scenario design and an example requiring real criteria/glue. |
| [scenario-outline.md](java/templates/scenario-outline.md) | Data-driven scenario design with explicit expected outcomes. |
| [ci.md](java/templates/ci.md) | Example GitHub Actions workflow for the Java test runtime. |
| [architecture.md](java/templates/architecture.md) | Outline for documenting your implemented architecture. |
| [readme.md](java/templates/readme.md) | Outline for documenting actual setup and execution commands. |
| [index.md](java/templates/index.md) | Navigation and explanation of which template files belong together. |

## Step-by-step setup

### 1. Copy the files into the repository root

Extract `java-playwright-copilot-md.zip`. Copy the contents of its `java-playwright-copilot/` folder into the framework root, preserving this layout:

```text
your-framework/
  .github/
    copilot-instructions.md
    agents/
    instructions/
    prompts/
    skills/
  docs/
    USER_GUIDE.md
    COPILOT_SETUP.md
    MIGRATION.md
    VALIDATION.md
    java/reference/
    java/templates/
  SOURCES.md
  CHANGES.md
  MIGRATION_MAP.md
  build.gradle                 your existing build, if present
  src/                         your existing implementation
```

Merge folders and matching documentation carefully; preserve unrelated CI workflows, settings and instructions. Include the three supporting root Markdown files because relative documentation links use them. Keep your existing project README, optionally linking it to this guide. Do not leave the supplied `.github/` nested inside a separate package subfolder.

On macOS, `.github` may be hidden in Finder; Command-Shift-period toggles hidden files. When replacing the earlier Copilot package, retire `java-bdd-engineer.agent.md` after preserving customizations: its responsibilities now have separate generator/healer profiles. Follow [migration](MIGRATION.md) for the old Cline rules and runtime conversion.

### 2. Match the guidance to your framework

Check package names, feature locations, runner/glue, injection, report locations, environment variables and actual Gradle commands. Update the supplied instructions if your namespace differs from `com.omc.automation`.

Preserve working FAST-managed versions and lifecycle. Do not replace an established runtime merely because the standalone template uses different pins. If a runtime is missing, use [the template index](java/templates/index.md) and [runner guide](java/reference/bdd-runner.md) to establish it deliberately.

The reference commands are:

```sh
./gradlew testClasses
./gradlew test -Dcucumber.filter.tags=@smoke
```

Their availability and tag forwarding depend on the actual build. `playwrightInstall` and `showTrace` exist only after their build tasks have been materialized or equivalent tasks already exist. Windows uses `gradlew.bat`.

### 3. Check prerequisites in the execution environment

Use your approved Java JDK, Gradle wrapper, Node.js 20+ and Playwright CLI. Run from the framework root in the environment Copilot will use:

```sh
java -version
./gradlew --version
node --version
playwright-cli --version
playwright-cli --help
```

If the CLI is not already supplied, replace `VERSION` below with your approved release:

```sh
npm install -g "@playwright/cli@VERSION"
```

Install the CLI's browser binaries when required:

```sh
playwright-cli install-browser
```

This is separate from browser installation for the Playwright Java dependency. The supplied Java build exposes `./gradlew playwrightInstall`; use your framework's actual equivalent. Record both tool versions, especially before attempting optional attachment.

### 4. Create the CLI configuration

Create `config/playwright-cli.json` using the installed release's supported schema:

```json
{
  "codegen": "java",
  "testIdAttribute": "data-testid",
  "browser": {
    "browserName": "chromium",
    "isolated": true,
    "contextOptions": {
      "viewport": { "width": 1280, "height": 720 }
    }
  },
  "outputDir": "build/agent-evidence/cli"
}
```

The JSON is an example to create, not an additional file already installed by the ZIP. Match viewport and test-ID conventions to the application. Keep secrets outside the tracked config. Pass this config explicitly when opening a session and inspect actual output to confirm Java code generation. See [CLI details](java/reference/cli-browser.md).

### 5. Configure access and perform a browser check

Set `BASE_URL` to the approved OMC test environment. Replace the placeholder before running these POSIX-shell examples:

```sh
export BASE_URL='YOUR_APPROVED_OMC_URL'
playwright-cli -s=omc-setup open "$BASE_URL" --config=config/playwright-cli.json --headed
playwright-cli -s=omc-setup snapshot
playwright-cli -s=omc-setup close
```

In PowerShell, environment assignment uses `$env:BASE_URL = 'YOUR_APPROVED_OMC_URL'`; navigation then uses `$env:BASE_URL`. Adapt shell quoting and use `.\gradlew.bat` for Gradle.

Make the variable available to the actual terminal/tool process Copilot starts; an export in an unrelated terminal does not configure every IDE session. The selected workspace environment must reach OMC. A remote/cloud session does not automatically inherit local private-network access.

Complete SSO/2FA manually in a headed browser if needed. Tell the agent to resume only after the resulting state is available. Do not place credentials in prompts or command history.

Keep generated data out of version control. Merge appropriate entries into `.gitignore`, using your actual authentication-state location:

```gitignore
/build/
/.playwright/
/.playwright-cli/
/.auth/
```

### 6. Confirm Copilot discovers the profiles

Open the framework repository root in VS Code and sign in to GitHub Copilot. In Chat, select the Copilot environment if multiple agent environments are offered.

Open the Command Palette, run **Chat: Open Customizations**, and inspect the **Agents** tab. Confirm `bdd-planner`, `java-bdd-generator`, `java-bdd-healer` and `java-bdd-reviewer` are listed without file errors. Select a profile from the Chat agent dropdown.

Verify actual tools: planner/generator/healer need shell execution for CLI; generator/healer also run Gradle. Reviewer activity should be reading/search only. Host permissions still apply. If a profile or prompt is not discovered, check the root folder and metadata, then explicitly ask a supported normal agent to read the appropriate `SKILL.md`. Do not assume discovery proves execution support.

Prompt files are optional entry points where supported. You can select the role and paste the examples below without using a prompt picker. These are Copilot prompts, not terminal commands.

### 7. Run a preflight check

Use a normal Copilot agent with the required read/execution tools for setup diagnosis:

```text
Read .github/copilot-instructions.md and docs/USER_GUIDE.md.
Inspect this framework's actual Gradle/Cucumber setup and the supplied
Copilot profiles. Check available Java, Node and Playwright CLI versions.

Report actual source/feature paths, runner/glue, tag-property forwarding,
report paths, available tools and commands. Confirm BASE_URL is defined
without printing credentials or secret configuration.

Do not edit files, install packages or run application scenarios yet.
Identify concrete setup gaps and the smallest changes needed.
Do not claim that CLI access or Java scenario execution has been verified
unless the relevant check actually ran.
```

Resolve real setup gaps before asking the generator to produce a verified result. Start with one small approved journey and then expand.

## Example prompts and review gates

The examples use an illustrative journey named **Order Search**. They do not assert OMC business rules. Put your actual acceptance criteria in `docs/requirements/order-search.md` and supply the approved account role, synthetic data and reset requirements there. Replace example names and artifact paths as needed.

Attach the referenced files or use your IDE's Add Context feature when they are not already in context. For review, a fresh chat with the reviewer profile helps separate the review from the author's conclusions. Supply the actual plan, diff and execution evidence; do not rely on unstated context from a different chat.

### The three gates

| Gate | What is reviewed | Evidence and decision |
|---|---|---|
| G1 | Scope and expected business outcomes | Requirement-linked plan, observations, data assumptions and real owner acceptance. |
| G2 | Generated implementation | Accepted plan, actual diff, CLI verification, fresh affected/adjacent Gradle results and separate review. |
| G3 | Candidate repair | Original failure, supported cause, bounded candidate history, minimal diff, before/after and adjacent reruns. |

An existing explicit request that already accepts sufficiently detailed scope/expectations can satisfy G1. Do not request duplicate approval for every file or locator. Unresolved business expectations stop dependent implementation. Actual owner/repository decisions govern acceptance; reviewer advice and Markdown fields cannot approve themselves or enforce merge controls. Full rules are in [review gates](java/reference/review-gates.md).

### Planner: prepare G1

Select **bdd-planner**:

```text
Read .github/skills/plan-coverage/SKILL.md.

Plan Java Playwright/Cucumber coverage for Order Search.
Requirements: docs/requirements/order-search.md.
Target: BASE_URL from the configured environment.
Role, synthetic data and reset rules: use those in the requirements.

Explore only the permitted flows using Playwright CLI.
Identify existing features, steps and page objects to reuse.
Include positive, negative and relevant boundary scenarios.
Separate approved requirements from observations and proposed cases.

Save the plan to docs/test-plans/order-search.md.
Include expected outcomes, requirement mapping, data/reset needs,
CLI evidence paths and the intended Gradle test selection.
Prepare Gate G1 for review. Do not implement tests yet.
```

Expected output: a concrete plan and evidence, with unanswered questions visible. The planner can produce a requirements-only draft if access is blocked, but must label unverified flows.

### Reviewer: assess G1

Select **java-bdd-reviewer**:

```text
Read .github/skills/review-java-bdd/SKILL.md.
Review Gate G1.

Requirements: docs/requirements/order-search.md.
Plan: docs/test-plans/order-search.md.

Check requirement coverage, expected outcomes, negative/boundary cases,
role/data assumptions, reuse and what was actually explored through CLI.
Observed UI behavior must not replace approved business expectations.

Do not edit files or execute commands.
Return actionable findings and state whether the plan is ready for my
acceptance, requires changes, or is blocked on a named decision/evidence.
Do not mark human acceptance on my behalf.
```

After reviewing the plan and findings, an owner acceptance message can be:

```text
I accept Gate G1 for the current docs/test-plans/order-search.md,
with its stated scope, data assumptions and expected outcomes.
Use this acceptance when generating the tests.
```

Record actual acceptance only after the decision is made. If the plan changes materially, review the changed scope/expectations.

### Generator: prepare G2

Select **java-bdd-generator** after G1 is satisfied:

```text
Read .github/skills/generate-java-bdd/SKILL.md.

Gate G1 is accepted for docs/test-plans/order-search.md; use the actual
acceptance message/reference supplied with this task.
Implement that plan in the existing Java Playwright/Cucumber framework.

Reuse existing steps, page objects, assertion helpers and scenario
lifecycle. Preserve FAST-managed dependencies and runner contracts.
Verify planned interactions and outcomes with Playwright CLI.
Use durable locators from actual evidence, not temporary snapshot refs.
Use the agreed scenario selection/tag, @order_search if appropriate.

Compile and execute affected scenarios through the actual Gradle runner.
Run relevant adjacent cases affected by reused code.
Prepare Gate G2 with the diff, requirement-to-scenario mapping,
CLI evidence, commands, exit codes and fresh scenario counts/reports.
Mark unavailable checks as unverified. Do not commit, push or merge.
```

With the reference build, typical commands are:

```sh
./gradlew testClasses
./gradlew test -Dcucumber.filter.tags="@order_search"
```

Confirm that selection matches the plan and reaches the test JVM. Inspect executed/passed/failed/skipped/undefined/pending statuses, exit code and fresh reports. Compilation, an empty tag selection or a successful CLI reproduction cannot establish passing Java tests. Do not use `npx playwright test` to execute these Java/Cucumber features.

### Reviewer: assess G2

Select **java-bdd-reviewer** and supply the plan, diff and current evidence:

```text
Read .github/skills/review-java-bdd/SKILL.md.
Review Gate G2 for the current Order Search changes.

Compare docs/test-plans/order-search.md with the actual diff.
Inspect the supplied CLI evidence and fresh Gradle/Cucumber reports.
Check bindings, scenario lifecycle, assertion strength, locator quality,
intended scenario selection and relevant adjacent coverage.

Check that compilation or CLI exploration has not been presented as
successful Java test execution. Identify missing or stale evidence.
Do not edit files or execute commands.
Return findings with file/line references and a readiness disposition
for my acceptance. Do not claim human acceptance or a passing run
that the supplied evidence does not establish.
```

Resolve findings and obtain any missing execution evidence before owner acceptance. An acceptance message can identify the exact reviewed revision/diff:

```text
I accept Gate G2 for the reviewed Order Search diff/revision [reference]
and the attached execution evidence. This acceptance covers the test
change; commit, push and merge follow our repository process.
```

### Healer: prepare G3

Select **java-bdd-healer**. Replace bracketed fields with actual paths:

```text
Read .github/skills/diagnose-java-failures/SKILL.md.

Investigate the failing Order Search scenario [exact title/tag].
Plan: docs/test-plans/order-search.md.
Failure reports: [actual report path].
Diagnostics: [actual screenshot/trace/log paths].

Preserve the original failure reports before rerunning.
Classify the cause as a test defect, product defect,
data/environment issue or unresolved.
Use Playwright CLI to investigate or reproduce the flow.
Distinguish a separate reproduction from the original Java browser.

I authorize minimal local repairs for confirmed test defects,
with at most two candidate attempts for this failure in this task.
Preserve business expectations. Do not weaken assertions, add skips,
swallow failures or repeat until green.

Rerun affected and relevant adjacent Java/Cucumber scenarios.
Prepare Gate G3 with diagnosis, candidate history, minimal diff
and before/after execution evidence. Do not commit, push or merge.
```

For diagnosis without edits, replace the repair authorization with:

```text
Diagnose only. Do not change Java implementation, features or build files.
Return the supported cause, evidence and proposed next action.
```

The default healer inspects saved Java failure artifacts and performs a separately identified CLI reproduction. The baseline After hook closes the Java browser. Attaching to that exact browser requires an additional live debug integration; it is not installed by this Markdown package. See [CLI attachment details](java/reference/cli-browser.md).

### Reviewer: assess G3

Select **java-bdd-reviewer** and provide the original failure and repair evidence:

```text
Read .github/skills/review-java-bdd/SKILL.md.
Review Gate G3 for this repair.

Compare the original failure, approved expected behavior, diagnosis,
candidate history, actual diff and fresh rerun evidence.
Check that the repair addresses the supported cause without weakening
coverage, hiding a product defect or exceeding the candidate bound.
Inspect affected and adjacent scenario results.

Do not edit files or execute commands.
Return actionable findings and state whether the repair is ready for
my acceptance, requires changes, or remains blocked on named evidence.
Changed business expectations require a new G1 decision.
```

An owner acceptance message can be:

```text
I accept Gate G3 for repair [diff/revision reference], based on the
reviewed diagnosis, preserved original failure and supplied reruns.
Use our normal repository process for any commit, push or merge.
```

If the cause remains uncertain or two candidates fail without new evidence, stop candidate edits and report what is needed. A product defect remains visible as a failure; it does not become a skipped test or an altered expected outcome.

## Troubleshooting

| Symptom | What to check |
|---|---|
| Profiles are missing | Open the repository root, confirm `.github/agents/*.agent.md`, check file errors and actual IDE support. Reopen a chat after discovery. |
| A prompt does not appear | Select the profile and explicitly load the corresponding skill. Prompt pickers vary by surface. |
| Copilot cannot run CLI | Check execution-tool availability, host permissions and CLI PATH inside the actual execution environment. Report blocked capability instead of claiming exploration. |
| BASE_URL is unavailable | Set it in the process environment used by the agent's commands; do not assume another terminal's export applies. |
| OMC is unreachable | Verify private-network access in that actual local/remote environment. Resolve access through the approved arrangement. |
| CLI emits TypeScript | Pass the intended config, inspect overrides and verify installed-release support for Java output. Deliberately translate observed snippets if needed, then compile/run Java. |
| No scenarios execute | Check tag forwarding, feature discovery, glue, suite filters and fresh reports. Zero execution is not a passing result. |
| Reviewer asks to run commands | Supply execution evidence from an authorized execution role. Keep the reviewer read/search-only. |
| A repair changes the expected result | Reassess the requirement at G1. A product bug does not authorize weaker expectations. |
| An attachment target has disappeared | The Java scenario may already have cleaned up. Use saved artifacts/separate reproduction unless a verified live debug mode exists. |
| Links break after copying | Preserve `.github/`, `docs/` and supporting root document layout. Reconcile links deliberately if you rename or relocate files. |

## Validation and sources

See [VALIDATION.md](VALIDATION.md) for the checks actually performed. This guide's examples are operational instructions, not evidence of a live Copilot/CLI run against OMC. The package does not claim verified internal-service integration or an installed Java browser-attachment adapter.

Current setup references checked on 2026-11-06:

- [Playwright CLI installation](https://playwright.dev/agent-cli/installation): Node prerequisite, package and browser installation.
- [Playwright CLI configuration](https://playwright.dev/agent-cli/configuration): Java output and browser/session configuration.
- [VS Code custom agents](https://code.visualstudio.com/docs/agent-customization/custom-agents): profile discovery, selection and verification.
- [GitHub custom-agent configuration](https://docs.github.com/en/copilot/reference/custom-agents-configuration): frontmatter and tool aliases.

Further implementation sources and reference versions are maintained in [SOURCES.md](../SOURCES.md).
