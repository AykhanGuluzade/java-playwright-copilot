# Architecture documentation template

Describe the implemented system using this outline:

1. Runner and actual command: Gradle, JUnit Platform suite, Cucumber engine.
2. Test layers: feature resources, glue, scenario state, page/actions, assertion helpers.
3. Lifecycle: owner thread, context isolation, diagnostic capture, cleanup.
4. Configuration: declared variables, dependency pins, browser revisions and secrets source.
5. Reporting: actual plugins, output directories and verified publication adapters.
6. CI/containers: real jobs, image contract, data/shard allocation and resource limits.
7. Copilot support: recognized instruction files, optional skills/prompts/profiles and actual available tools.
8. Known gaps: unimplemented integrations and the evidence needed to close them.

Use [the reference architecture](../reference/architecture.md) as a starting point. Draw only implemented runtime relationships. Do not add a scheduler, agent dispatcher, schemas, Allure listeners or approval service because an old document named one.
