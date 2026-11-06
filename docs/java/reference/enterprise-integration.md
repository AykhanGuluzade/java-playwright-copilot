# OMC / FAST / Lightspeed / FAST Run Service / TURBO

The supplied screenshots describe FAST's Cucumber basis, Lightspeed pipelines, image-based FAST Run Service execution and parallel pods, and TURBO standardized reporting. They do not establish the exact OMC adapter, dependency matrix, authentication contract or JTS schema. This package must not invent those details.

Preserve an existing FAST-provided Java runner or lifecycle where required; do not layer two independent Before/After browser owners over one scenario. Resolve the supported Cucumber, JUnit and Java versions with framework owners before adopting the standalone pins. Replace the sample session or suite through a tested adapter rather than claiming they are already integrated.

Validate one approved OMC scenario through these contracts:

| Boundary | Evidence needed |
|---|---|
| Gradle / FAST | Real entry task, lifecycle ownership, dependency compatibility and nonzero scenario count |
| Lightspeed / image | Approved build trigger, registry/image digest, matching browser/JDK/OS dependencies |
| FAST Run Service | Supported invocation, tag/environment selection, sharding, exit/status contract and artifact retrieval |
| TURBO | Actual JTS mapping/schema, scenario/run IDs, failed/skipped semantics, artifact links and publication result |

Keep a versioned, reviewed field mapping based on the real schema when supplied. A local mapping draft or JSON file is not a successful TURBO publication. Never add dummy internal URLs, credentials or fabricated CLI commands to make the guide look complete.

Acceptance includes a known-pass and known-failure run, isolated parallel data, complete artifacts and preserved failures across aggregation. Platform onboarding, service permissions and production access are external setup, not capabilities provided by these Markdown files.
