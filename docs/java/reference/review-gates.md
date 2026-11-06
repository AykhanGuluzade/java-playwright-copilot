# Review gates and evidence

Use three concrete review boundaries. A review gate records what has been reviewed, by whom and against which evidence; it is not an implemented approval service. Preserve existing explicit authorization. Do not request another approval for every local locator edit, compile or test run.

| Gate | Evidence to prepare | Decision and stopping condition |
|---|---|---|
| G1: plan and expectations | Source criteria; scenario mapping; role/data/start state; actions and expected outcomes; CLI observations and gaps; intended selection | The owner accepts the plan, or an existing explicit task already accepts those details. Resolve missing or conflicting business expectations before dependent generation. |
| G2: generated change | Accepted plan; actual Java/feature diff; CLI verification evidence; compiler result; fresh affected/adjacent Cucumber runs | A separate review pass checks coverage, lifecycle and false-pass risks. Present concrete work for owner/repository acceptance. Failures or missing execution evidence prevent a verified-ready result. |
| G3: repair | Original failure; cause classification; candidate history; minimal diff; before/after and adjacent reruns | Review whether the cause is fixed while preserving the test's purpose. Product defects remain failures; changed business expectations return to G1. Stop unsupported edits or after two candidates without new evidence. |

A sufficiently detailed, authorized implementation request may satisfy G1 without another question. If only planning was requested, deliver the plan for acceptance before generation. A fix request authorizes ordinary local candidate repairs and verification; final acceptance concerns the concrete diff and evidence. Review does not itself authorize commit, push, merge, publication or production actions.

## Plan record

Save plans under `docs/test-plans/<task-slug>.md`, or return the same content in chat when writing is unavailable. Include:

- Scope, source requirement references and baseline revision where available.
- Environment, application role, initial/auth state, synthetic data and reset/cleanup needs.
- Scenario-to-requirement mapping, actions and explicit expected outcomes, including relevant negative/boundary cases.
- Existing feature/step/page reuse and intended Gradle tags or name selection.
- CLI observations with evidence paths; requirements-only or unverified portions marked clearly.
- G1 status: accepted, pending, or changes required; actual decision source/actor/date. Do not prefill accepted status.

## Implementation or repair evidence

Use the PR/review record or an approved local review note. Keep raw run artifacts under an ignored `build/agent-evidence/<run-id>/` directory. Include:

- Gate and state: prepared, changes required, blocked on named evidence, or accepted with a real decision reference.
- Plan/requirement links and actual diff/revision; distinguish new generation from repair.
- CLI version, session/environment, role/data, actions, expected versus observed results and artifact paths. A command's success is not an assertion of the business result.
- Gradle command, exit code, selected scope and fresh report path; discovered, executed, passed, failed, skipped and undefined/pending counts as available. Explain any unavailable count or mismatch. Zero execution, partial skips or missing reports cannot be called fully passed.
- For repairs: preserve the original failure; record each candidate's hypothesis, changed lines and rerun result. Do not overwrite earlier failure evidence.
- Review findings, remaining limitations and actual reviewer/owner decision. Author self-review does not establish independent review or human acceptance.

If CLI, private application access or test execution is unavailable, deliver the prepared work with a blocked/unverified state and the specific missing capability. Do not manufacture browser evidence, successful runs or approval. Branch protection, required checks and platform permissions remain the real enforcement mechanisms.
