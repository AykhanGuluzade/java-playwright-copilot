# Complete original-file migration map

All 115 reviewed Markdown files are retired/replaced, rewritten or consolidated as listed. New task skills and references replace repeated prose; a retired role does not need a compatibility stub that silently reintroduces the old instructions. Paths below are relative to the repository/package root.

| Original reviewed file | New destination | Disposition |
|---|---|---|
| `.cline/agents/README.md` | [docs/COPILOT_SETUP.md](docs/COPILOT_SETUP.md) | Replaced Cline setup with Copilot-supported formats and surface notes. |
| `.cline/agents/acceptance-criteria-reader.md` | [.github/skills/plan-coverage/SKILL.md](.github/skills/plan-coverage/SKILL.md) | Consolidated requirements/coverage planning; no unimplemented schemas or handoffs. |
| `.cline/agents/acceptance-criteria.md` | [.github/skills/plan-coverage/SKILL.md](.github/skills/plan-coverage/SKILL.md) | Consolidated requirements/coverage planning; no unimplemented schemas or handoffs. |
| `.cline/agents/accessibility-locator.md` | [.github/skills/generate-java-bdd/SKILL.md](.github/skills/generate-java-bdd/SKILL.md) | Consolidated into Java generation with real lifecycle and templates. |
| `.cline/agents/allure-generator.md` | [docs/java/reference/reporting.md](docs/java/reference/reporting.md) | Configuration/lifecycle responsibility, not a separate service agent. |
| `.cline/agents/api-helper.md` | [docs/java/reference/api-testing.md](docs/java/reference/api-testing.md) | Java API guidance; no imaginary helper implementation. |
| `.cline/agents/architecture-generator.md` | [docs/java/reference/architecture.md](docs/java/reference/architecture.md) | Document implemented runtime instead of simulated agent catalog. |
| `.cline/agents/assertion-generator.md` | [.github/skills/generate-java-bdd/SKILL.md](.github/skills/generate-java-bdd/SKILL.md) | Consolidated into Java generation with real lifecycle and templates. |
| `.cline/agents/changelog-generator.md` | [docs/java/reference/maintenance.md](docs/java/reference/maintenance.md) | On-demand maintenance/documentation guidance; real tooling and explicit publication scope. |
| `.cline/agents/component-builder.md` | [.github/skills/generate-java-bdd/SKILL.md](.github/skills/generate-java-bdd/SKILL.md) | Consolidated into Java generation with real lifecycle and templates. |
| `.cline/agents/component-generator.md` | [.github/skills/generate-java-bdd/SKILL.md](.github/skills/generate-java-bdd/SKILL.md) | Consolidated into Java generation with real lifecycle and templates. |
| `.cline/agents/css-locator.md` | [.github/skills/generate-java-bdd/SKILL.md](.github/skills/generate-java-bdd/SKILL.md) | Consolidated into Java generation with real lifecycle and templates. |
| `.cline/agents/debugging-agent.md` | [.github/skills/diagnose-java-failures/SKILL.md](.github/skills/diagnose-java-failures/SKILL.md) | Bounded evidence-based diagnosis with preserved expectations. |
| `.cline/agents/documentation-agent.md` | [docs/java/reference/maintenance.md](docs/java/reference/maintenance.md) | On-demand maintenance/documentation guidance; real tooling and explicit publication scope. |
| `.cline/agents/duplicate-code-detector.md` | [.github/skills/review-java-bdd/SKILL.md](.github/skills/review-java-bdd/SKILL.md) | Consolidated review; actual build tools enforce deterministic checks. |
| `.cline/agents/dynamic-locator-generator.md` | [.github/skills/generate-java-bdd/SKILL.md](.github/skills/generate-java-bdd/SKILL.md) | Consolidated into Java generation with real lifecycle and templates. |
| `.cline/agents/execution-agent.md` | [docs/java/reference/bdd-runner.md](docs/java/reference/bdd-runner.md) | Actual Java runner and verification tasks replace prose-only runner. |
| `.cline/agents/feature-generator.md` | [.github/skills/generate-java-bdd/SKILL.md](.github/skills/generate-java-bdd/SKILL.md) | Gherkin creation is part of a complete Java BDD slice rather than a separate simulated agent. |
| `.cline/agents/feature-writer.md` | [.github/skills/generate-java-bdd/SKILL.md](.github/skills/generate-java-bdd/SKILL.md) | Gherkin creation is part of a complete Java BDD slice rather than a separate simulated agent. |
| `.cline/agents/fixture-generator.md` | [.github/skills/generate-java-bdd/SKILL.md](.github/skills/generate-java-bdd/SKILL.md) | Consolidated into Java generation with real lifecycle and templates. |
| `.cline/agents/github-actions-agent.md` | [docs/java/reference/maintenance.md](docs/java/reference/maintenance.md) | On-demand maintenance/documentation guidance; real tooling and explicit publication scope. |
| `.cline/agents/hooks-generator.md` | [.github/skills/generate-java-bdd/SKILL.md](.github/skills/generate-java-bdd/SKILL.md) | Consolidated into Java generation with real lifecycle and templates. |
| `.cline/agents/locator-builder.md` | [.github/skills/generate-java-bdd/SKILL.md](.github/skills/generate-java-bdd/SKILL.md) | Consolidated into Java generation with real lifecycle and templates. |
| `.cline/agents/locator-generator.md` | [.github/skills/generate-java-bdd/SKILL.md](.github/skills/generate-java-bdd/SKILL.md) | Consolidated into Java generation with real lifecycle and templates. |
| `.cline/agents/maintenance-agent.md` | [docs/java/reference/maintenance.md](docs/java/reference/maintenance.md) | On-demand maintenance/documentation guidance; real tooling and explicit publication scope. |
| `.cline/agents/method-builder.md` | [.github/skills/generate-java-bdd/SKILL.md](.github/skills/generate-java-bdd/SKILL.md) | Consolidated into Java generation with real lifecycle and templates. |
| `.cline/agents/naming-reviewer.md` | [.github/skills/review-java-bdd/SKILL.md](.github/skills/review-java-bdd/SKILL.md) | Consolidated review; actual build tools enforce deterministic checks. |
| `.cline/agents/orchestrator.md` | [docs/java/reference/agentic-extension.md](docs/java/reference/agentic-extension.md) | Retired unimplemented orchestration; use selectable Copilot profiles/workflows. |
| `.cline/agents/outline-writer.md` | [.github/skills/generate-java-bdd/SKILL.md](.github/skills/generate-java-bdd/SKILL.md) | Gherkin creation is part of a complete Java BDD slice rather than a separate simulated agent. |
| `.cline/agents/page-object-builder.md` | [.github/skills/generate-java-bdd/SKILL.md](.github/skills/generate-java-bdd/SKILL.md) | Consolidated into Java generation with real lifecycle and templates. |
| `.cline/agents/page-object-generator.md` | [.github/skills/generate-java-bdd/SKILL.md](.github/skills/generate-java-bdd/SKILL.md) | Consolidated into Java generation with real lifecycle and templates. |
| `.cline/agents/planner.md` | [.github/skills/plan-coverage/SKILL.md](.github/skills/plan-coverage/SKILL.md) | Consolidated requirements/coverage planning; no unimplemented schemas or handoffs. |
| `.cline/agents/playwright-reviewer.md` | [.github/skills/review-java-bdd/SKILL.md](.github/skills/review-java-bdd/SKILL.md) | Consolidated review; actual build tools enforce deterministic checks. |
| `.cline/agents/pom-reviewer.md` | [.github/skills/review-java-bdd/SKILL.md](.github/skills/review-java-bdd/SKILL.md) | Consolidated review; actual build tools enforce deterministic checks. |
| `.cline/agents/readme-generator.md` | [docs/java/reference/maintenance.md](docs/java/reference/maintenance.md) | On-demand maintenance/documentation guidance; real tooling and explicit publication scope. |
| `.cline/agents/refactoring-agent.md` | [docs/java/reference/maintenance.md](docs/java/reference/maintenance.md) | On-demand maintenance/documentation guidance; real tooling and explicit publication scope. |
| `.cline/agents/reporting-agent.md` | [docs/java/reference/reporting.md](docs/java/reference/reporting.md) | Configuration/lifecycle responsibility, not a separate service agent. |
| `.cline/agents/requirement-reader.md` | [.github/skills/plan-coverage/SKILL.md](.github/skills/plan-coverage/SKILL.md) | Consolidated requirements/coverage planning; no unimplemented schemas or handoffs. |
| `.cline/agents/requirement.md` | [.github/skills/plan-coverage/SKILL.md](.github/skills/plan-coverage/SKILL.md) | Consolidated requirements/coverage planning; no unimplemented schemas or handoffs. |
| `.cline/agents/review-agent.md` | [.github/skills/review-java-bdd/SKILL.md](.github/skills/review-java-bdd/SKILL.md) | Consolidated review; actual build tools enforce deterministic checks. |
| `.cline/agents/risk-analyzer.md` | [.github/skills/plan-coverage/SKILL.md](.github/skills/plan-coverage/SKILL.md) | Consolidated requirements/coverage planning; no unimplemented schemas or handoffs. |
| `.cline/agents/scenario-writer.md` | [.github/skills/generate-java-bdd/SKILL.md](.github/skills/generate-java-bdd/SKILL.md) | Gherkin creation is part of a complete Java BDD slice rather than a separate simulated agent. |
| `.cline/agents/screenshot-manager.md` | [docs/java/reference/reporting.md](docs/java/reference/reporting.md) | Configuration/lifecycle responsibility, not a separate service agent. |
| `.cline/agents/step-definition-generator.md` | [.github/skills/generate-java-bdd/SKILL.md](.github/skills/generate-java-bdd/SKILL.md) | Consolidated into Java generation with real lifecycle and templates. |
| `.cline/agents/story-analyzer-subagent.md` | [.github/skills/plan-coverage/SKILL.md](.github/skills/plan-coverage/SKILL.md) | Consolidated requirements/coverage planning; no unimplemented schemas or handoffs. |
| `.cline/agents/story-analyzer.md` | [.github/skills/plan-coverage/SKILL.md](.github/skills/plan-coverage/SKILL.md) | Consolidated requirements/coverage planning; no unimplemented schemas or handoffs. |
| `.cline/agents/tag-generator.md` | [.github/skills/generate-java-bdd/SKILL.md](.github/skills/generate-java-bdd/SKILL.md) | Gherkin creation is part of a complete Java BDD slice rather than a separate simulated agent. |
| `.cline/agents/test-coverage-analyzer.md` | [.github/skills/plan-coverage/SKILL.md](.github/skills/plan-coverage/SKILL.md) | Consolidated requirements/coverage planning; no unimplemented schemas or handoffs. |
| `.cline/agents/test-data-generator.md` | [.github/skills/generate-java-bdd/SKILL.md](.github/skills/generate-java-bdd/SKILL.md) | Consolidated into Java generation with real lifecycle and templates. |
| `.cline/agents/trace-manager.md` | [docs/java/reference/reporting.md](docs/java/reference/reporting.md) | Configuration/lifecycle responsibility, not a separate service agent. |
| `.cline/agents/typescript-reviewer.md` | [.github/skills/review-java-bdd/SKILL.md](.github/skills/review-java-bdd/SKILL.md) | Consolidated review; actual build tools enforce deterministic checks. |
| `.cline/agents/video-manager.md` | [docs/java/reference/reporting.md](docs/java/reference/reporting.md) | Configuration/lifecycle responsibility, not a separate service agent. |
| `.cline/agents/website-analyzer.md` | [.github/skills/generate-java-bdd/SKILL.md](.github/skills/generate-java-bdd/SKILL.md) | Consolidated into Java generation with real lifecycle and templates. |
| `.cline/agents/xpath-optimizer.md` | [.github/skills/generate-java-bdd/SKILL.md](.github/skills/generate-java-bdd/SKILL.md) | Consolidated into Java generation with real lifecycle and templates. |
| `.cline/prompts/debug.md` | [.github/prompts/diagnose-java-failures.prompt.md](.github/prompts/diagnose-java-failures.prompt.md) | Merged into a native Copilot task prompt; detailed domain guidance retained in docs. |
| `.cline/prompts/generate-architecture-template.md` | [.github/prompts/generate-java-bdd.prompt.md](.github/prompts/generate-java-bdd.prompt.md) | Merged into a native Copilot task prompt; detailed domain guidance retained in docs. |
| `.cline/prompts/generate-component.md` | [.github/prompts/generate-java-bdd.prompt.md](.github/prompts/generate-java-bdd.prompt.md) | Merged into a native Copilot task prompt; detailed domain guidance retained in docs. |
| `.cline/prompts/generate-feature.md` | [.github/prompts/generate-java-bdd.prompt.md](.github/prompts/generate-java-bdd.prompt.md) | Merged into a native Copilot task prompt; detailed domain guidance retained in docs. |
| `.cline/prompts/generate-fixtures.md` | [.github/prompts/generate-java-bdd.prompt.md](.github/prompts/generate-java-bdd.prompt.md) | Merged into a native Copilot task prompt; detailed domain guidance retained in docs. |
| `.cline/prompts/generate-hooks-template.md` | [.github/prompts/generate-java-bdd.prompt.md](.github/prompts/generate-java-bdd.prompt.md) | Merged into a native Copilot task prompt; detailed domain guidance retained in docs. |
| `.cline/prompts/generate-hooks.md` | [.github/prompts/generate-java-bdd.prompt.md](.github/prompts/generate-java-bdd.prompt.md) | Merged into a native Copilot task prompt; detailed domain guidance retained in docs. |
| `.cline/prompts/generate-locators.md` | [.github/prompts/generate-java-bdd.prompt.md](.github/prompts/generate-java-bdd.prompt.md) | Merged into a native Copilot task prompt; detailed domain guidance retained in docs. |
| `.cline/prompts/generate-page.md` | [.github/prompts/generate-java-bdd.prompt.md](.github/prompts/generate-java-bdd.prompt.md) | Merged into a native Copilot task prompt; detailed domain guidance retained in docs. |
| `.cline/prompts/generate-readme-template.md` | [.github/prompts/generate-java-bdd.prompt.md](.github/prompts/generate-java-bdd.prompt.md) | Merged into a native Copilot task prompt; detailed domain guidance retained in docs. |
| `.cline/prompts/generate-report.md` | [.github/prompts/generate-java-bdd.prompt.md](.github/prompts/generate-java-bdd.prompt.md) | Merged into a native Copilot task prompt; detailed domain guidance retained in docs. |
| `.cline/prompts/generate-scenarios-from-snapshot.md` | [.github/prompts/generate-java-bdd.prompt.md](.github/prompts/generate-java-bdd.prompt.md) | Merged into a native Copilot task prompt; detailed domain guidance retained in docs. |
| `.cline/prompts/generate-step.md` | [.github/prompts/generate-java-bdd.prompt.md](.github/prompts/generate-java-bdd.prompt.md) | Merged into a native Copilot task prompt; detailed domain guidance retained in docs. |
| `.cline/prompts/generate-test-data-template.md` | [.github/prompts/generate-java-bdd.prompt.md](.github/prompts/generate-java-bdd.prompt.md) | Merged into a native Copilot task prompt; detailed domain guidance retained in docs. |
| `.cline/prompts/refactor.md` | [.github/prompts/generate-java-bdd.prompt.md](.github/prompts/generate-java-bdd.prompt.md) | Merged into a native Copilot task prompt; detailed domain guidance retained in docs. |
| `.cline/prompts/review.md` | [.github/prompts/review-java-bdd.prompt.md](.github/prompts/review-java-bdd.prompt.md) | Merged into a native Copilot task prompt; detailed domain guidance retained in docs. |
| `.cline/skills/accessibility/skill.md` | [docs/java/reference/accessibility.md](docs/java/reference/accessibility.md) | Domain reference consolidated; native discovery now uses the four .github/skills SKILL.md files. |
| `.cline/skills/allure/skill.md` | [docs/java/reference/reporting.md](docs/java/reference/reporting.md) | Domain reference consolidated; native discovery now uses the four .github/skills SKILL.md files. |
| `.cline/skills/api/skill.md` | [docs/java/reference/api-testing.md](docs/java/reference/api-testing.md) | Domain reference consolidated; native discovery now uses the four .github/skills SKILL.md files. |
| `.cline/skills/assertions/skill.md` | [docs/java/reference/architecture.md](docs/java/reference/architecture.md) | Domain reference consolidated; native discovery now uses the four .github/skills SKILL.md files. |
| `.cline/skills/component-object-model/skill.md` | [docs/java/reference/architecture.md](docs/java/reference/architecture.md) | Domain reference consolidated; native discovery now uses the four .github/skills SKILL.md files. |
| `.cline/skills/cucumber/skill.md` | [docs/java/reference/bdd-runner.md](docs/java/reference/bdd-runner.md) | Domain reference consolidated; native discovery now uses the four .github/skills SKILL.md files. |
| `.cline/skills/debugging/skill.md` | [docs/java/reference/reporting.md](docs/java/reference/reporting.md) | Domain reference consolidated; native discovery now uses the four .github/skills SKILL.md files. |
| `.cline/skills/fixtures/skill.md` | [docs/java/reference/test-data.md](docs/java/reference/test-data.md) | Domain reference consolidated; native discovery now uses the four .github/skills SKILL.md files. |
| `.cline/skills/gherkin/skill.md` | [docs/java/reference/bdd-runner.md](docs/java/reference/bdd-runner.md) | Domain reference consolidated; native discovery now uses the four .github/skills SKILL.md files. |
| `.cline/skills/github-actions/skill.md` | [docs/java/reference/maintenance.md](docs/java/reference/maintenance.md) | Domain reference consolidated; native discovery now uses the four .github/skills SKILL.md files. |
| `.cline/skills/hooks/skill.md` | [docs/java/reference/bdd-runner.md](docs/java/reference/bdd-runner.md) | Domain reference consolidated; native discovery now uses the four .github/skills SKILL.md files. |
| `.cline/skills/locator/skill.md` | [docs/java/reference/java-style.md](docs/java/reference/java-style.md) | Domain reference consolidated; native discovery now uses the four .github/skills SKILL.md files. |
| `.cline/skills/logging/skill.md` | [docs/java/reference/reporting.md](docs/java/reference/reporting.md) | Domain reference consolidated; native discovery now uses the four .github/skills SKILL.md files. |
| `.cline/skills/page-object-model/skill.md` | [docs/java/reference/architecture.md](docs/java/reference/architecture.md) | Domain reference consolidated; native discovery now uses the four .github/skills SKILL.md files. |
| `.cline/skills/performance/skill.md` | [docs/java/reference/parallel-execution.md](docs/java/reference/parallel-execution.md) | Domain reference consolidated; native discovery now uses the four .github/skills SKILL.md files. |
| `.cline/skills/playwright/skill.md` | [docs/java/reference/architecture.md](docs/java/reference/architecture.md) | Domain reference consolidated; native discovery now uses the four .github/skills SKILL.md files. |
| `.cline/skills/refactoring/skill.md` | [docs/java/reference/maintenance.md](docs/java/reference/maintenance.md) | Domain reference consolidated; native discovery now uses the four .github/skills SKILL.md files. |
| `.cline/skills/review/skill.md` | [docs/java/reference/review-checklist.md](docs/java/reference/review-checklist.md) | Domain reference consolidated; native discovery now uses the four .github/skills SKILL.md files. |
| `.cline/skills/security/skill.md` | [docs/java/reference/test-data.md](docs/java/reference/test-data.md) | Domain reference consolidated; native discovery now uses the four .github/skills SKILL.md files. |
| `.cline/skills/test-data/skill.md` | [docs/java/reference/test-data.md](docs/java/reference/test-data.md) | Domain reference consolidated; native discovery now uses the four .github/skills SKILL.md files. |
| `.cline/skills/typescript/skill.md` | [docs/java/reference/java-style.md](docs/java/reference/java-style.md) | Domain reference consolidated; native discovery now uses the four .github/skills SKILL.md files. |
| `.cline/templates/architecture.md` | [docs/java/templates/architecture.md](docs/java/templates/architecture.md) | Rewritten with Java/runtime-accurate content and related-file guidance. |
| `.cline/templates/component.md` | [docs/java/templates/component.md](docs/java/templates/component.md) | Rewritten with Java/runtime-accurate content and related-file guidance. |
| `.cline/templates/feature.md` | [docs/java/templates/feature.md](docs/java/templates/feature.md) | Rewritten with Java/runtime-accurate content and related-file guidance. |
| `.cline/templates/fixture.md` | [docs/java/templates/fixture.md](docs/java/templates/fixture.md) | Rewritten with Java/runtime-accurate content and related-file guidance. |
| `.cline/templates/hooks.md` | [docs/java/templates/hooks.md](docs/java/templates/hooks.md) | Rewritten with Java/runtime-accurate content and related-file guidance. |
| `.cline/templates/page-object.md` | [docs/java/templates/page-object.md](docs/java/templates/page-object.md) | Rewritten with Java/runtime-accurate content and related-file guidance. |
| `.cline/templates/readme.md` | [docs/java/templates/readme.md](docs/java/templates/readme.md) | Rewritten with Java/runtime-accurate content and related-file guidance. |
| `.cline/templates/scenario-outline.md` | [docs/java/templates/scenario-outline.md](docs/java/templates/scenario-outline.md) | Rewritten with Java/runtime-accurate content and related-file guidance. |
| `.cline/templates/scenario.md` | [docs/java/templates/scenario.md](docs/java/templates/scenario.md) | Rewritten with Java/runtime-accurate content and related-file guidance. |
| `.cline/templates/test-data.md` | [docs/java/templates/test-data.md](docs/java/templates/test-data.md) | Rewritten with Java/runtime-accurate content and related-file guidance. |
| `.clinerules/architecture.md` | [docs/java/reference/architecture.md](docs/java/reference/architecture.md) | Replaced aspirational architecture and inconsistent layout. |
| `.clinerules/coding-standards.md` | [.github/instructions/java-playwright.instructions.md](.github/instructions/java-playwright.instructions.md) | Consolidated and corrected for Java; detailed examples moved to docs. |
| `.clinerules/component-model.md` | [.github/instructions/java-playwright.instructions.md](.github/instructions/java-playwright.instructions.md) | Consolidated and corrected for Java; detailed examples moved to docs. |
| `.clinerules/cucumber.md` | [.github/instructions/cucumber.instructions.md](.github/instructions/cucumber.instructions.md) | Corrected runner/lifecycle and unified assertion policy. |
| `.clinerules/folder-structure.md` | [docs/java/reference/architecture.md](docs/java/reference/architecture.md) | Replaced aspirational architecture and inconsistent layout. |
| `.clinerules/git-workflow.md` | [.github/instructions/build-ci.instructions.md](.github/instructions/build-ci.instructions.md) | Replaced assumed branch policies with real CI/review controls. |
| `.clinerules/human-approval.md` | [.github/copilot-instructions.md](.github/copilot-instructions.md) | Meaningful scope/review/data boundaries; no simulated approval service. |
| `.clinerules/locator-rules.md` | [.github/instructions/java-playwright.instructions.md](.github/instructions/java-playwright.instructions.md) | Consolidated and corrected for Java; detailed examples moved to docs. |
| `.clinerules/naming-conventions.md` | [.github/instructions/java-playwright.instructions.md](.github/instructions/java-playwright.instructions.md) | Consolidated and corrected for Java; detailed examples moved to docs. |
| `.clinerules/page-object-model.md` | [.github/instructions/java-playwright.instructions.md](.github/instructions/java-playwright.instructions.md) | Consolidated and corrected for Java; detailed examples moved to docs. |
| `.clinerules/playwright.md` | [.github/instructions/java-playwright.instructions.md](.github/instructions/java-playwright.instructions.md) | Consolidated and corrected for Java; detailed examples moved to docs. |
| `.clinerules/review-checklist.md` | [docs/java/reference/review-checklist.md](docs/java/reference/review-checklist.md) | Removed contradictory checklist requirements. |
| `.clinerules/security.md` | [.github/copilot-instructions.md](.github/copilot-instructions.md) | Meaningful scope/review/data boundaries; no simulated approval service. |
| `.clinerules/typescript.md` | [.github/instructions/java-playwright.instructions.md](.github/instructions/java-playwright.instructions.md) | Consolidated and corrected for Java; detailed examples moved to docs. |
