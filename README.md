# AI Collaborative Development Standard

A reusable, evidence-driven standard for AI-assisted collaborative software development, parallel task coordination, independent verification, controlled task closure, and evidence-based execution recovery.

**Current mainline baseline:** V1.0 — Released for Validation.  
**V1.1 status:** Candidate for Validation, currently on branch `v1.1/blocked-task-lifecycle`; not yet approved as the default standard. The original V1.0 documents remain unchanged as historical baselines.

## Standards

### V1.1 candidate

1. [Controller & Task Orchestration Standard V1.1](docs/01-controller-task-orchestration-standard-v1.1.md) — dependency readiness, parallel scheduling, incremental-change safeguards, controller decisions for continue/replan/suspend/seal/cancel, and controlled recovery.
2. [Middle-Layer Execution & Closure Standard V1.1](docs/02-middle-layer-task-coordination-closure-standard-v1.1.md) — required blocker escalation, route correction, dependency checks, stop/retry rules, and recovery handoff.
3. [Shared Protocol & Templates V1.1](docs/03-shared-protocol-and-templates-v1.1.md) — separated lifecycle/delivery/dependency states, blocker decisions, recovery gates, evidence, and continuous improvement.

### V1.0 historical baseline

1. [Controller & Task Orchestration Standard V1.0](docs/01-controller-task-orchestration-standard-v1.0.md)
2. [Middle-Layer Task Coordination & Closure Standard V1.0](docs/02-middle-layer-task-coordination-closure-standard-v1.0.md)
3. [Shared Protocol & Templates V1.0](docs/03-shared-protocol-and-templates-v1.0.md)

V1.0 is preserved for traceability. V1.1 should replace it as the operating default only after conflict review, template consistency checks, real-task trials, regression-case validation, and explicit approval.

## Copy-ready templates

- [Task Contract Template](templates/task-contract.md) — authorization, scope, dependencies, stop conditions, deliverables, and objective acceptance criteria.
- [Task Dependency & Incremental-Change Impact Template](templates/task-dependency-and-change-impact.md) — verifies module maturity, upstream/downstream dependencies, old-version behavior, compatibility risks, and parallel boundaries.
- [Blocker, Pause & Resume Template](templates/blocker-pause-resume.md) — records direct evidence, work-item triage, recovery gates, and the controller decision.
- [Task Closeout & Acceptance Record Template](templates/task-closeout.md) — separates execution facts, independent review, controller decision, and formal closure.
- [Workspace Inventory & Provenance Template](templates/workspace-inventory-provenance.md) — records file/workspace provenance and protects unknown artifacts.

## Operating model

The collaboration has **three responsibility levels, not four**:

- **Controller:** owns project-level decisions, authorization, cross-group coordination, task lifecycle decisions, final acceptance, and integration decisions.
- **Middle layer / parallel work group:** turns authorized work into executable contracts, checks dependencies and evidence, coordinates coding tools, corrects technical routes within authorization, and promptly escalates blockers.
- **Coding tool:** implements the explicit contract, performs implementation-level self-checks, and reports actual evidence and blockers.

The middle layer must not silently change project goals or make unauthorized lifecycle decisions. It must also not keep retrying a failed route merely because the original plan is fixed. When execution cannot make effective progress, it reports the specific cause, actual state, evidence, impact, safe independent work, blocked work, options, risks, and recovery conditions. The controller then records a clear decision.

## Core principles

- **Stable goals, adaptable routes:** authorization, safety, evidence and acceptance rules stay stable; implementation order, decomposition and methods may change when evidence invalidates the original plan.
- **Dependencies are facts, not assumptions:** planned modules are not implemented modules; mocks and temporary adapters are not real end-to-end proof.
- **Old-version incrementality:** identify affected existing behavior, interfaces, data, permissions, configuration and regression boundaries before changing a mature baseline.
- **Explicit blocker escalation:** BLOCKED is a factual condition; ON HOLD and SEALED are controller-authorized lifecycle decisions.
- **Recovery must be evidence-based:** no automatic resume due only to elapsed time, retry count or assumption. Recheck prerequisites and obtain authorized approval.
- **No infinite retries:** a retry must produce new evidence, a validated change, a clear difference or a decision. Otherwise stop and escalate.
- **Evidence over self-report:** distinguish implementation, self-verification, independent verification, commit, push, integration and formal acceptance.
- **Protect accepted work and unknown artifacts:** do not redo accepted work without cause; do not delete, move or overwrite unknown files without authorization.
- **3–5 rounds is an escalation target, not a quality waiver.**
- **Record durable status:** decisions, evidence, blockers, recovery conditions and remaining work must live outside conversational memory.

## Validation and release policy

V1.1 remains a candidate until reviewed and exercised in real tasks. For each trial, record task type/risk, correction rounds, blockers and controller response time, dependency-related rework, evidence completeness, independent findings, escaped defects, regression catches, and execution cost. Metrics must include their denominator and observation window. Fewer rounds alone do not prove improvement if escaped defects or risk increase.

Formal release status changes require documented review and authorization. Adding documents or passing a single task is not proof of maturity.

## Language

Normative documents are maintained in Chinese first. English titles are for discoverability and do not alter the normative meaning.
