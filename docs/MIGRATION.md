# Migration from the reviewed Cline / TypeScript package

## Scope

The source review covered commit `8ce831781436b81b329c4fe6addaf9d255ba192d`. This replacement regenerates the instruction/documentation layer for GitHub Copilot and Java. Existing TypeScript implementations, GitHub settings, secrets and internal services are not changed by copying Markdown.

## Instruction migration

1. Save the current repository state in version control or a local backup.
2. Consult [the complete map](../MIGRATION_MAP.md). Retire the 115 reviewed Markdown files from active `.cline/` and `.clinerules/` locations. Keep any archive outside automatically discovered instruction directories.
3. Preserve files added after the reviewed commit, personal settings and unrelated project configuration. Reconcile any new instructions deliberately; do not delete the entire `.github` directory.
4. Copy this package's `.github/` and `docs/` trees, plus the supporting root `SOURCES.md`, `CHANGES.md` and `MIGRATION_MAP.md`. Reconcile existing documentation and preserve relative links. Keep your framework README and link it to [the user guide](USER_GUIDE.md), or adapt the [project README template](java/templates/readme.md) after the Java runtime works.
5. Confirm the repository instruction file, three scoped instruction files, four skills, four prompt files and four custom profiles appear where your Copilot surface supports them.

Replace or archive the original root README's Cline commands and the old `agentic-framework-for-cline-pw-bdd-pom.md` guide as part of this documentation migration. Leaving those instructions as current usage documentation would reintroduce the unsupported workflow.

## Runtime migration

Materialize the exact target files listed in [the template index](java/templates/index.md). The baseline is Java 17-compatible source, Gradle 9.8.2, Playwright Java 1.64.0, Cucumber-JVM 8.0.4 and JUnit 6.1.3. These are explicit reference pins, not enterprise-approved versions or an instruction to upgrade an existing managed framework.

- Establish an approved Java 17+ JDK and Gradle distribution. Generate and commit the wrapper using `gradle wrapper --gradle-version 9.8.2 --distribution-type bin --gradle-distribution-sha256-sum 21bd5da2de49b642904077f38c0efdc7778e92b3ed0889392dca61b97e389607`.
- Copy the build, suite, properties, scenario session, hooks, page, assertion helper, data record, steps and sample feature from the templates. Keep package names and glue settings consistent when renaming.
- Compile with `./gradlew testClasses`. Install Chromium with `./gradlew playwrightInstall` (Linux workers can use `-PwithDeps=true`). Set `BASE_URL` to the authorized non-production application.
- Adapt the example's `/login`, Email, Continue and status-message contract to real approved behavior. The example is a fixture demonstration, not a verified OMC login implementation.
- Execute `./gradlew test -Dcucumber.filter.tags=@smoke`. Confirm actual scenarios and steps ran and the reports are fresh. Prove a deliberately incorrect expected outcome fails in an isolated validation copy, then restore it.
- Move other scenarios incrementally and preserve their requirement mappings. Retire Node/TypeScript sources/configuration only as a reviewed runtime migration; do not leave both runners claiming to execute the same feature inventory.

## Enterprise migration

FAST may own the runner, dependency versions or lifecycle. Preserve those contracts and adapt the reference where required. Validate the smallest OMC scenario through Gradle, the approved image, FAST Run Service and TURBO publication before claiming the integration works. See [enterprise integration](java/reference/enterprise-integration.md).

## Updating the earlier Copilot package

Replace the package-owned instructions, prompts, skills and references with this revision. Remove the earlier `.github/agents/java-bdd-engineer.agent.md` after preserving any personal changes: its roles now live in `java-bdd-generator.agent.md` and `java-bdd-healer.agent.md`. Keep `bdd-planner` and `java-bdd-reviewer`, with their updated instructions. The four existing skill/prompt names remain stable, including `diagnose-java-failures` for healing.

Configure an approved Playwright CLI installation and materialize the example JSON in [CLI setup](java/reference/cli-browser.md) if needed. No Playwright MCP server is used. Preserve organization-managed versions; CLI authoring tools do not replace the Gradle/Cucumber runner or install Java runtime dependencies. Apply [G1/G2/G3](java/reference/review-gates.md) to the actual plan, implementation and repair evidence.
