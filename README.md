# AI Collaborative Development Standard

A reusable, evidence-driven standard for AI-assisted collaborative software development, parallel task coordination, independent verification, and controlled task closure.

**Current release status: Released for Validation (V1.0 draft).**  
This repository is a working standard under validation, not a claim of proven maturity. Status may be upgraded only after the standards have been exercised in real tasks and the evidence is recorded.

## Standards

1. [Controller & Task Orchestration Standard V1.0](docs/01-controller-task-orchestration-standard-v1.0.md) — project goals, authorization, prioritization, parallel coordination, shared status ledger, integration decisions, and final acceptance.
2. [Middle-Layer Task Coordination & Closure Standard V1.0](docs/02-middle-layer-task-coordination-closure-standard-v1.0.md) — task decomposition, executable coding-tool contracts, implementation coordination, independent verification, consolidated corrections, and handoff.
3. [Shared Protocol & Templates V1.0](docs/03-shared-protocol-and-templates-v1.0.md) — common terminology, task identifiers, evidence rules, status vocabulary, and reusable templates.

## Operating model

The collaboration has **three responsibility levels, not four**:

- **Controller:** owns project-level decisions, authorization, cross-group coordination, final acceptance, and integration decisions.
- **Middle layer / parallel work group:** turns authorized work into executable contracts, coordinates coding tools, checks evidence independently, and reports results or blockers.
- **Coding tool:** implements the explicit contract and performs implementation-level self-checks.

The controller may delegate execution and verification tasks but retains final project authority. The middle layer may resolve technical details within its authorization, but may not silently change project goals, acceptance criteria, shared contracts, or cross-group resource decisions.

## Core principles

- Define the target, scope, deliverables, dependencies, exclusions, and acceptance criteria before implementation.
- Prefer evidence from the actual repository, executed tests, remote state, and concrete artifacts over self-reported completion.
- Keep implementation, self-verification, independent verification, commit, push, integration, and final acceptance as distinct states.
- Treat previously accepted work as a baseline; revisit it only for a regression, contract conflict, security issue, current-task blocker, or explicit authorization.
- Use a 3–5 interaction target to control iteration cost, not to weaken acceptance criteria. Escalate or re-plan when progress stalls.
- Record durable status outside conversational memory.
- Do not claim PASS without actual verification evidence.

## Validation policy

Each real-world trial should record the task contract, number of correction rounds, evidence, unresolved issues, and whether the standard prevented ambiguity or rework. Keep this release at **Released for Validation** until a documented validation review authorizes a status change.

## Language

The normative documents are maintained in Chinese first. English titles are provided for discoverability; translations may be added without changing the normative meaning.
