# GitHub Copilot setup

Start with [the user guide](USER_GUIDE.md) for the complete walkthrough and example prompts.

Copy `.github/` and `docs/` into the repository while preserving unrelated configuration. Include the supplied root `SOURCES.md`, `CHANGES.md` and `MIGRATION_MAP.md`, merging existing documentation if necessary, because relative links use them. Keep your framework README. Relative references must move with the instructions. Follow [migration](MIGRATION.md) when replacing an earlier package.

| Surface | Entry point |
|---|---|
| Repository-wide guidance | `.github/copilot-instructions.md` |
| File-scoped guidance | Three `.github/instructions/*.instructions.md` files |
| Task skills | Four `.github/skills/<name>/SKILL.md` files |
| Supported IDE prompt picker | Four `.github/prompts/*.prompt.md` files |
| Custom-agent picker | Planner, generator, healer and reviewer under `.github/agents/` |

Confirm file discovery and tool availability in the actual Copilot surface/version. If its picker does not load a workflow, explicitly ask Copilot to read the relevant SKILL.md. Prompt files are IDE entry points, not invented Copilot CLI subcommands.

## CLI-only browser integration

Follow [CLI setup](java/reference/cli-browser.md). Use an approved Node.js/Playwright CLI installation and an environment that can actually reach private OMC. No MCP server, MCP configuration or native Playwright Test agent tool is required. Do not add an MCP fallback when CLI is unavailable; record the missing capability and deliver unverified work honestly.

The planner, generator and healer declare Copilot's `read`, `search`, `edit` and `execute` aliases. They need shell execution for CLI; the generator/healer also compile and run Java through Gradle. The planner's edits are limited by instructions to plans/review documents, although its shell tools are technically capable of broader writes. Configure actual permissions in the host. Unknown aliases may be ignored by a surface: verify the available execution tool rather than claiming a capability from YAML alone.

The reviewer remains read/search-only and checks supplied evidence. No model pin, credentials, auto-approval setting, browser installation or organization policy is embedded. Private access, host execution permissions and CI/repository controls require their real environment configuration.

## Review entry points

1. Select `bdd-planner` / the plan prompt and prepare G1.
2. After G1 is satisfied, select `java-bdd-generator` / the generation prompt and prepare G2.
3. For a failure, select `java-bdd-healer` / the existing diagnosis prompt and prepare G3. Request diagnosis only or authorize repair explicitly as appropriate.
4. Select `java-bdd-reviewer` / the review prompt for a separate review pass; retain real owner acceptance and repository checks.

See [gate decisions and evidence](java/reference/review-gates.md). Existing explicit approval counts; a generated approval field does not. These profiles do not automatically dispatch one another or enforce a merge gate.

Sources: [repository instructions](https://docs.github.com/en/copilot/how-tos/configure-custom-instructions/add-repository-instructions), [custom agents and tool aliases](https://docs.github.com/en/copilot/reference/custom-agents-configuration), [skills](https://docs.github.com/en/copilot/concepts/agents/about-agent-skills), [prompt files](https://docs.github.com/en/copilot/tutorials/customization-library/prompt-files), [Playwright CLI](https://playwright.dev/agent-cli/introduction).
