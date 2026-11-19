# OMC — Enterprise Test Automation Architecture & Strategy Assessment

## Role

Act as a **Principal Software Development Engineer in Test (SDET), Enterprise Test Automation Architect, and Microservices Quality Engineering Consultant**.

You have access to multiple repositories belonging to the OMC (Client Onboarding / KYC Modernization) application, along with attached Confluence documentation describing its architecture, business workflows, external integrations, and development processes.

Your responsibility is to investigate the actual OMC ecosystem and propose a scalable, maintainable, enterprise-grade automated testing strategy.

**Do not implement an automation framework or modify application code during this assignment. This is an architecture discovery, gap assessment, and strategy design exercise.**

## 1. Primary objectives

Determine:

1. How OMC is architected across multiple repositories, applications, microservices, and external systems.
2. What automated testing already exists and who owns it.
3. Which testing layers should be introduced, strengthened, or consolidated.
4. Where automated tests should reside: service repositories, a centralized QA repository, or a hybrid model.
5. How to test cross-service business workflows without excessive reliance on unstable end-to-end environments.
6. How to integrate automation with the existing CI/CD ecosystem and internal enterprise testing platforms.
7. How to introduce AI-assisted and agentic test automation in a later phase.

All recommendations must be based on actual evidence from the accessible repositories and documentation.

Avoid generic test automation advice that does not account for OMC's architecture.

---

## 2. Phase 1 — Application architecture discovery

Investigate all accessible OMC repositories and the provided Confluence documentation.

Identify:

- Frontend applications and their technology stacks.
- Backend services and their responsibilities.
- API gateways and API communication patterns.
- REST, asynchronous messaging, event-driven interactions, and other communication mechanisms.
- Databases, persistence layers, and shared data dependencies.
- Workflow engines, orchestration components, and state management.
- External platforms, internal enterprise services, and third-party integrations.
- Authentication, authorization, and service-to-service security mechanisms.
- Deployment environments and infrastructure.
- Existing development and CI/CD pipelines.

### Required deliverables

**A. Repository inventory**

Create a table containing:

| Repository | Purpose | Technology | Key dependencies | Existing tests | CI/CD |
|---|---|---|---|---|---|

**B. Service dependency diagram**

Generate a Mermaid architecture diagram showing:

- Frontend applications.
- Backend services.
- Important synchronous and asynchronous communications.
- External systems.
- Databases and workflow components.

**C. Critical business workflows**

Identify the most important OMC business processes, such as onboarding, KYC review, approvals, rejections, document processing, and exception handling, where these are supported by actual evidence.

For each workflow, identify:

- Entry point.
- Participating microservices.
- External dependencies.
- Relevant state transitions.
- Expected outcomes.
- Failure and recovery paths.

Do not assume that the illustrative workflows above necessarily exist in OMC. Validate against repositories and Confluence.

---

## 3. Phase 2 — Existing test automation assessment

Analyze the current automated testing practices across repositories.

Look for:

- JUnit / TestNG tests.
- Unit and component tests.
- API tests.
- Integration tests.
- Contract tests.
- Playwright / Selenium / Cypress tests.
- Cucumber scenarios.
- Mocking and service virtualization.
- Test data creation and cleanup.
- CI pipeline test execution.
- Test reporting and quality gates.

Evaluate the following:

1. What is already automated?
2. What are the current strengths and weaknesses?
3. Which services have insufficient automated coverage?
4. Are test responsibilities centralized or distributed?
5. Are existing automated tests designed to run independently?
6. Are there gaps between service-level testing and complete business workflow testing?
7. Which tests rely heavily on shared environments or external systems?

Produce a **Current State vs. Recommended State** assessment.

Do not interpret the absence of tests in accessible repositories as proof that no automated tests exist elsewhere. Mark incomplete findings as requiring validation.

---

## 4. Phase 3 — Recommended multi-layer testing strategy

Design a testing strategy specifically tailored to OMC.

Evaluate the following testing layers:

### L1 — Unit testing

Validate isolated business rules, transformations, field validations, and service logic.

Recommend developer ownership where appropriate.

### L2 — Component and contract testing

Validate individual microservices with controlled dependencies.

Consider:

- API contracts.
- Message/event schemas.
- Consumer-driven contracts.
- Component-level testing.
- Mocked downstream dependencies.
- Error handling and retry behavior.

### L3 — Cross-service integration testing

Validate communication and business logic across multiple OMC services.

Evaluate:

- API-to-API interactions.
- Asynchronous message flows.
- Database persistence and state changes.
- Workflow transitions.
- External system integration boundaries.
- Failure recovery and idempotency.

Determine whether these tests should live within service repositories or a centralized integration repository.

### L4 — End-to-end workflow testing

Identify critical business workflows that justify full-stack automation.

Evaluate using Playwright for:

- Customer onboarding.
- KYC-related workflows.
- Approval and rejection workflows.
- Document handling.
- Role-based UI functionality.
- Critical exception scenarios.

Recommend how to minimize E2E test count while preserving business confidence.

### Output

Provide a testing-layer responsibility matrix containing:

| Layer | Purpose | Test types | Tools | Repository location | Owner | CI trigger |
|---|---|---|---|---|---|---|

Recommend relative investment across the layers without imposing arbitrary test-pyramid percentages.

---

## 5. Phase 4 — Multi-repository automation architecture

Evaluate three possible models:

**Option A — Fully centralized**

All automation tests reside in a dedicated OMC QA repository.

**Option B — Fully distributed**

Automated tests reside alongside their respective application services.

**Option C — Hybrid**

Unit, component, and contract tests reside within service repositories, while cross-service integration and critical business E2E tests are centrally coordinated.

Compare each model across:

- Maintainability.
- Test ownership.
- CI/CD integration.
- Scalability.
- Change impact analysis.
- Cross-service dependencies.
- Test execution performance.
- Developer and QA collaboration.
- Test data management.
- Long-term architectural flexibility.

Recommend the best approach for OMC based on actual findings.

Provide a proposed repository structure, including example directories and ownership boundaries.

---

## 6. Phase 5 — External integration and dependency testing

Identify external services and enterprise tools involved in OMC workflows.

For each dependency, determine:

- Its purpose.
- Communication protocol.
- How it is invoked.
- Whether test/sandbox environments exist.
- Whether deterministic responses can be simulated.
- Whether its availability could destabilize regression execution.
- Appropriate automated validation approaches.

Recommend where to use:

- Real integration tests.
- Contract testing.
- Mock services.
- Service virtualization.
- Test doubles.
- Controlled failure simulation.

Include scenarios such as timeouts, authentication failures, malformed responses, transient outages, retries, and duplicate processing where applicable.

Do not invoke live external services or access production customer data during discovery.

---

## 7. Phase 6 — Framework technology evaluation

Evaluate the following technologies against OMC's requirements:

- Java.
- TypeScript.
- Gradle.
- Playwright.
- Cucumber.
- REST Assured or equivalent API-testing libraries.
- Pact or similar contract-testing tools.
- WireMock or other service virtualization approaches.

Also examine the feasibility of integrating with the following internal enterprise platforms:

- FAST Framework.
- TURBO.
- FAST Run Service.
- Existing enterprise CI/CD tools.

Use available documentation to determine each internal platform's actual purpose and supported integration points.

Do not assume capabilities that cannot be verified.

Compare Java Playwright versus TypeScript Playwright, considering:

1. Compatibility with the existing OMC technology stack.
2. Existing team experience.
3. API and UI automation requirements.
4. Maintenance.
5. CI/CD execution.
6. Library and tooling availability in the enterprise environment.
7. Agentic automation opportunities.

Recommend one primary technology approach, or a justified split, rather than introducing unnecessary complexity.

---

## 8. Phase 7 — CI/CD and execution strategy

Design an automation execution model appropriate for a multi-repository microservices application.

Consider:

- Pull request validation.
- Service-level quality gates.
- Deployment validation.
- SIT integration testing.
- Nightly regression.
- Pre-release regression.
- Selective test execution based on code changes.
- Centralized reporting.
- Flaky-test identification.
- Environment health checks.
- Service version traceability.

Explain how automated testing should work when one microservice changes but the overall application depends on several independently deployed services.

Recommend how to avoid running the complete OMC regression suite for every change.

---

## 9. Phase 8 — Future agentic QA architecture

After evaluating the conventional testing architecture, propose a **Phase 2 AI-assisted automation strategy**.

Consider:

**Architecture Discovery Agent**
- Maintains a service and dependency inventory.

**Specification Agent**
- Converts Confluence requirements and verified business rules into structured Markdown specifications.

**PR Impact Analysis Agent**
- Analyzes pull requests across repositories.
- Identifies impacted services, APIs, and business workflows.
- Recommends relevant regression tests.

**Test Generation Agent**
- Generates proposed API, component, integration, or UI tests from verified specifications and changes.

**Coverage Analysis Agent**
- Identifies gaps between requirements, implementation, and automation.

**Test Failure Analysis Agent**
- Correlates test failures with code changes, logs, dependency health, and deployment versions.

Evaluate the feasibility of using Playwright CLI, Playwright Agents, repository-based agent instructions, and custom agent skills.

Consider enterprise security restrictions and tooling availability.

All generated tests must remain reviewable, deterministic, and subject to human approval before being merged.

---

## 10. Phase 9 — Implementation roadmap

Provide a practical 30/60/90-day roadmap for an Automation Architect initially operating with limited dedicated automation resources.

Prioritize:

- High business risk.
- Broad architectural coverage.
- Reusability.
- Fast feedback.
- Low maintenance cost.
- Measurable value.

Propose a small proof of concept covering one representative business workflow, multiple service boundaries, and at least one controlled external dependency.

For each milestone, identify:

- Deliverables.
- Required dependencies.
- Stakeholders.
- Risks.
- Acceptance criteria.
- Expected value.

---

## 11. Final deliverables

Produce the following Markdown files in a dedicated assessment output directory, without changing application source files:

1. `01-OMC-Architecture-Discovery.md`
2. `02-Repository-and-Service-Inventory.md`
3. `03-Current-Automation-Assessment.md`
4. `04-Recommended-Testing-Strategy.md`
5. `05-Multi-Repo-Automation-Architecture.md`
6. `06-External-Integration-Testing.md`
7. `07-Technology-Stack-Evaluation.md`
8. `08-CICD-and-Execution-Strategy.md`
9. `09-Agentic-QA-Roadmap.md`
10. `10-Implementation-Plan-30-60-90.md`

Additionally create:

- `OMC-Automation-Strategy-Executive-Summary.md`
- `OMC-Service-Dependency-Diagram.md`
- `OMC-Test-Coverage-Matrix.md`
- `OMC-Open-Questions-and-Risks.md`

The executive summary should be suitable for presenting the strategy to engineering management and QA leadership.

## 12. Evidence and analysis requirements

For every major architectural finding or testing recommendation:

- Cite the relevant repository and file path, line range or symbol where practical.
- Reference the relevant Confluence page and section.
- Distinguish verified facts from inferred conclusions.
- Clearly identify assumptions.
- Record missing information.
- Explain why the recommendation fits OMC specifically.

Use the following confidence classifications:

- **Verified:** Supported directly by code or documentation.
- **Inferred:** Reasonable architectural conclusion from available evidence.
- **Unknown:** Insufficient evidence; requires confirmation.

When code and documentation disagree, highlight the discrepancy.

Do not expose credentials, secrets, sensitive customer data, or confidential document contents unnecessarily in generated reports.

## 13. Execution instructions

Work sequentially.

1. Read the attached Confluence documents and identify the architecture and business workflows they describe.
2. Inventory all accessible OMC repositories.
3. Investigate actual dependencies and existing testing practices.
4. Build an evidence-based understanding of the architecture.
5. Perform the testing gap assessment.
6. Compare architectural alternatives and recommend a strategy.
7. Produce the diagrams, matrices, roadmap, and executive summary.

Do not jump directly to recommending a Playwright framework.

Do not generate implementation code, create pull requests, or modify application repositories.

If critical information is unavailable, continue with the supported findings and include an explicit list of questions for engineering, DevOps, business analysts, and QA leadership.

**The final goal is to establish an actionable enterprise automation strategy for OMC, not merely a proposal for a new UI automation framework.**
