# Maintenance and documentation

Use one maintained source for commands and versions: the actual Gradle build/wrapper. Update referenced commands after executing them. Document current architecture and operational limitations, not an aspirational catalog of agents or missing schemas.

Put deterministic checks in declared build tasks and CI. Prefer an existing compiler, formatter, static analyzer or duplicate detector over a separate conversational agent that claims an unimplemented AST engine. For requirement coverage, report reviewed links from source criteria to executable scenarios; keyword matches are suggestions, not verified coverage.

Audit dependencies with an approved configured tool. Separate diagnosis from dependency modification. Never use a forced automatic upgrade as an audit command. A dependency update needs compatibility review, lock/wrapper verification where used, and an actual affected test run.

Keep changes small. Compare behavior before/after refactoring and retain assertion strength. Generate a changelog from real version-control history when requested; do not fabricate scheduled maintenance, release automation, branch protection or a GitHub publishing capability.

A slow scenario deserves measurement of application response, setup and infrastructure. Do not impose an arbitrary five-second budget or shorten waits to two seconds merely to satisfy generic prose. Retries are diagnostic/operational settings, not a replacement for correcting flaky tests.

Ordinary test evidence belongs in CI artifacts, not `.github/copilot-instructions.md` or tracked orchestration state. Document review decisions in the actual PR or approved process.

The agent browser CLI has its own approved version and release-specific command surface. Review its installed help and [CLI guidance](cli-browser.md) when upgrading. Keep the four Copilot roles and [review gates](review-gates.md) consistent; do not regenerate native MCP-dependent agents over this Java adaptation.
