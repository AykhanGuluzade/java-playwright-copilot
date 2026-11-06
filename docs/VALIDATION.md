# Validation record

## User guide revision — 2026-11-06

- 55 Markdown files, with the new guide discoverable from the README and Copilot setup page.
- Guide links, navigation anchors, code fences, Java CLI JSON example and package coverage checked. Every Markdown document in the package has a link in the guide's explanations.
- All existing skill metadata, profile/prompt routing, legacy migration mappings and template targets rechecked. Profile/skill definitions and Java runtime examples are unchanged in this revision.
- ZIP contents verified against the final Markdown folder, with no extra platform metadata or work files included.

Setup guidance was checked against current official Copilot and Playwright CLI documentation. These are documentation/archive checks; no live Copilot, CLI browser, Java scenario or internal-service integration was executed for this revision. Historical results and limits below remain applicable.

## CLI documentation revision — 2026-11-04

- 54 Markdown files, including four Copilot profiles, four skills, four prompts and three scoped instruction files.
- Relative links and code fences checked; YAML discovery metadata and prompt-to-agent routing verified. Planner/generator/healer have execution aliases; the reviewer remains read/search-only. No MCP tool/server configuration is included.
- All four skills pass the skill metadata validator. All 115 reviewed legacy-file mappings still resolve.
- Thirteen Java/Gradle/properties/Gherkin target blocks remain identical to the previously compiled validation fixture. The CLI revision changes instructions and references, not these runtime targets.
- The CLI JSON example parses and selects Java output, an isolated browser and a local evidence directory. Command patterns were checked against current official documentation, with installed-version checks required on adoption.
- Static workflow review covered missing CLI/access, unresolved business expectations, product defects, zero/skipped execution evidence, bounded repairs, existing approval and reviewer tool limits. This is instruction review, not a live Copilot behavioral test.

Node, npm and playwright-cli were unavailable on this validation host's PATH. No CLI browser session, CLI Java output, private OMC access or Java-browser attachment was executed. The optional Browser.bind debug adapter is documented but not implemented by the baseline. Copilot discovery/tool permissions, human review controls and enterprise services need validation in the target environment.

## Retained Java reference checks — 2026-11-02

The unchanged reference classes compiled with Gradle 9.8.2, OpenJDK 19 and `--release 17` against [the explicit pins](../SOURCES.md). Resolved baseline dependency classes required no newer than Java 17, excluding multi-release overlays. A Java 17 CI run remains an adoption check. The CI YAML and full action SHAs were checked; the workflow was not executed on GitHub.

A separate browser-free Cucumber harness with the same runner/reporting configuration verified:

| Check | Actual outcome |
|---|---|
| Known-good scenarios | Two passed, exit 0 |
| Deliberately wrong expectation | One failed, one passed, exit 1 |
| Two-way parallel execution | Two passed with fresh PicoContainer state, exit 0 |
| Tag selection matching no scenarios | Zero executed; evidence gate failed the build, exit 1 |

These checks validate runner semantics, not application interactions. They exposed and corrected the Cucumber JSON provider requirement. Browser installation remains explicit; test JVMs disable implicit browser downloads.

The real browser sample was attempted, but macOS blocked Chromium startup with a process permission error before application steps ran. The original failure stayed visible. Successful browser actions, screenshot/trace output and parallel browser lifecycle were not verified. Those checks were not repeated for this instruction-only revision.

FAST, Lightspeed Enterprise, FAST Run Service, TURBO publication and optional reporting/accessibility adapters were not executed. Copying this Markdown package does not change the GitHub repository, install dependencies or migrate TypeScript runtime sources.
