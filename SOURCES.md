# Source and version references

Reviewed input: [CrazyDevo/agentic-fw-v01](https://github.com/CrazyDevo/agentic-fw-v01/tree/8ce831781436b81b329c4fe6addaf9d255ba192d), commit `8ce831781436b81b329c4fe6addaf9d255ba192d`.

Regenerated for Java Playwright/Cucumber and GitHub Copilot on 2026-11-02; CLI-only workflow revision on 2026-11-04. Runtime reference pins are unchanged.

## Public reference stack

| Item | Explicit pin | Published source |
|---|---|---|
| Java source compatibility | 17 | Project baseline, not a claim to select the newest JDK |
| Gradle distribution | 9.8.2 | https://services.gradle.org/versions/current |
| Playwright Java | 1.64.0 | https://repo.maven.apache.org/maven2/com/microsoft/playwright/playwright/1.64.0/ |
| Cucumber BOM | 8.0.4 | https://repo.maven.apache.org/maven2/io/cucumber/cucumber-bom/8.0.4/ |
| JUnit BOM | 6.1.3 | https://repo.maven.apache.org/maven2/org/junit/junit-bom/6.1.3/ |
| Cucumber JSON provider | Jackson Databind 3.2.4 | https://repo.maven.apache.org/maven2/tools/jackson/core/jackson-databind/3.2.4/ |

The selected Cucumber engine POM aligns JUnit 6.1.3. The reference pins are not security certification or enterprise support approval. Preserve the organization-managed FAST dependency matrix when it differs and validate the adapter.

Gradle binary ZIP SHA-256: `21bd5da2de49b642904077f38c0efdc7778e92b3ed0889392dca61b97e389607`, checked against the official checksum endpoint.

## Primary documentation

- [Copilot repository instructions](https://docs.github.com/en/copilot/how-tos/configure-custom-instructions/add-repository-instructions)
- [Copilot custom agents](https://docs.github.com/en/copilot/reference/custom-agents-configuration)
- [Copilot skills](https://docs.github.com/en/copilot/concepts/agents/about-agent-skills)
- [Copilot prompt files](https://docs.github.com/en/copilot/tutorials/customization-library/prompt-files)
- [Playwright Java test runners](https://playwright.dev/java/docs/test-runners)
- [Playwright Java assertions](https://playwright.dev/java/docs/test-assertions)
- [Playwright Java multithreading](https://playwright.dev/java/docs/multithreading)
- [Playwright Java locators](https://playwright.dev/java/docs/locators)
- [Playwright Java trace viewer](https://playwright.dev/java/docs/trace-viewer)
- [Playwright Java videos](https://playwright.dev/java/docs/videos)
- [Playwright Java API testing](https://playwright.dev/java/docs/api-testing)
- [Playwright Java accessibility testing](https://playwright.dev/java/docs/accessibility-testing)
- [Cucumber scenario state](https://cucumber.io/docs/cucumber/state/)
- [Cucumber JUnit Platform engine](https://github.com/cucumber/cucumber-jvm/tree/main/cucumber-junit-platform-engine)
- [Gradle Java testing](https://docs.gradle.org/current/userguide/java_testing.html)
- [Native Playwright Test Agents](https://playwright.dev/docs/test-agents)

Internal integration context comes from the user's supplied screenshots and requirements, not public claims about internal APIs or compatibility.

## CI action pins

| Action | Release | Commit |
|---|---|---|
| actions/checkout | [v7.0.1](https://github.com/actions/checkout/releases/tag/v7.0.1) | `3d3c42e5aac5ba805825da76410c181273ba90b1` |
| actions/setup-java | [v6.1.0](https://github.com/actions/setup-java/releases/tag/v6.1.0) | `b843ebf9b913146b38da2eaa7aeddf76074ae1ad` |
| actions/upload-artifact | [v7.0.2](https://github.com/actions/upload-artifact/releases/tag/v7.0.2) | `cf430e030ddbb5b0abf93d22962f4752f3646cd9` |

## CLI workflow sources

Checked on 2026-11-04. The user's environment permits Playwright CLI and excludes Playwright MCP. The installed CLI release must be checked against these current docs; the package does not install or invent a CLI version pin.

- [CLI installation and Node prerequisite](https://playwright.dev/agent-cli/installation)
- [CLI browser configuration and Java code output](https://playwright.dev/agent-cli/configuration)
- [Snapshots and temporary refs](https://playwright.dev/agent-cli/snapshots)
- [Browser interaction](https://playwright.dev/agent-cli/commands/interaction)
- [Code generation and workflow patterns](https://playwright.dev/agent-cli/commands/codegen)
- [Attach/detach lifecycle](https://playwright.dev/agent-cli/commands/attach)
- [Playwright Test-specific CLI debugging](https://playwright.dev/agent-cli/commands/test-debugging)
- [Java Browser.bind API, added in 1.59](https://playwright.dev/java/docs/api/class-browser#browser-bind)

The instructions and review gates are this package's Java/Cucumber adaptation. They do not claim native Cucumber generation/healing support from the Playwright Test agents. No Microsoft agent instructions were copied verbatim into these profiles.

## User guide sources

The setup portions of [the user guide](docs/USER_GUIDE.md) were checked on 2026-11-06 against the official [CLI installation](https://playwright.dev/agent-cli/installation), [CLI configuration](https://playwright.dev/agent-cli/configuration), [VS Code custom-agent](https://code.visualstudio.com/docs/agent-customization/custom-agents) and [GitHub agent-configuration](https://docs.github.com/en/copilot/reference/custom-agents-configuration) documentation. Runtime reference pins were not changed or presented as newly validated releases.
