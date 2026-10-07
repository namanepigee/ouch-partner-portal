# AI Agent Operating Guidelines — Ouch! Enterprise Portal

This file defines the mandatory protocols, engineering workflows, and rules of engagement for AI coding agents operating in this repository.

---

## 1. Core Operating Principles

1. **Context-First & Spec-Driven**
   - **Never invent missing requirements, endpoints, or data models.**
   - Before writing or modifying code, you **MUST** read and cross-reference:
     * Requirements: [business-requirements.md](docs/requirements/business-requirements.md), [functional-requirements.md](docs/requirements/functional-requirements.md), [non-functional-requirements.md](docs/requirements/non-functional-requirements.md)
     * Architecture: [system-architecture.md](docs/architecture/system-architecture.md), [integrations.md](docs/architecture/integrations.md)
     * API Contracts: [api-overview.md](docs/api/api-overview.md)
     * Data Model: [domain-entities.md](docs/data-model/domain-entities.md)
     * Architectural Decisions: [ADR-0001-confirmed-technical-baseline.md](docs/decisions/ADR-0001-confirmed-technical-baseline.md), [ADR-0002-open-architecture-decisions.md](docs/decisions/ADR-0002-open-architecture-decisions.md)
     * Task Backlog: [task-backlog.md](tasks/task-backlog.md)

2. **Flag Ambiguities & Open Choices**
   - If a specification is ambiguous, contradictory, or underspecified, **stop and request clarification**. Do NOT guess.
   - Do NOT unilaterally choose between open technical options (e.g., .NET Core vs. Node.js, Azure vs. AWS) unless an accepted ADR records the stakeholder choice.

3. **Single Source of Truth**
   - Architectural decisions live in `docs/decisions/` (ADRs).
   - Data structures and schemas live in `docs/data-model/`.
   - API endpoints and interface contracts live in `docs/api/`.
   - Any architectural deviation must be preceded by an updated specification or ADR.

4. **Testing, Verification & Quality**
   - Every implementation must include appropriate tests (unit, integration, or contract tests).
   - Verify code locally before declaring a task complete.
   - Maintain strict separation of concerns between `frontend/` (React.js) and `backend/` (REST API).

---

## 2. Mandatory Agent Workflow Protocol

When assigned a task, follow this sequential 4-step execution flow:

```text
Step 1: Discover & Align  -->  Step 2: Plan & Propose  -->  Step 3: Implement & Test  -->  Step 4: Verify & Synchronize
```

### Step 1: Discover & Align
1. Review the relevant task definition in [task-backlog.md](tasks/task-backlog.md).
2. Read the corresponding specifications in `docs/requirements/`, `docs/architecture/`, `docs/api/`, `docs/data-model/`, and `docs/decisions/`.
3. Check existing codebase in `frontend/` and `backend/` to understand existing patterns.

### Step 2: Plan & Propose
1. For architectural modifications or API changes, propose updates to the respective docs or create a new ADR under `docs/decisions/`.
2. Confirm that open decisions (such as tech stack choices) have documented resolutions.
3. Formulate a step-by-step checklist before modifying code.

### Step 3: Implement & Test
1. Write clean, modular, and maintainable code strictly adhering to documented contracts.
2. Respect security constraints: Enforce RBAC, multi-tenant isolation, and OAuth 2.0 / OIDC token verification.
3. Write automated unit and integration tests covering business rules and edge cases.

### Step 4: Verify & Synchronize
1. Execute tests and ensure all pass cleanly.
2. Update task status in [task-backlog.md](tasks/task-backlog.md) and the corresponding task file under `tasks/`.
3. Synchronize documentation if implementation details or schemas evolved.

---

## 3. Directory Map & Governance

| Directory | Agent Responsibilities |
| :--- | :--- |
| `docs/requirements/` | Source of truth for scope, features, and NFRs. Read-only unless directed by user. |
| `docs/architecture/` | Reference system boundaries, component designs, and external integrations. |
| `docs/api/` | Reference and maintain REST API boundaries, schemas, and contract specs. |
| `docs/data-model/` | Reference and maintain database schemas, entity relationships, and migrations. |
| `docs/decisions/` | Read accepted ADRs; record new technical proposals and trade-offs. |
| `docs/development/` | Follow guidelines for delivery phases, quality assurance, and security rules. |
| `tasks/` | Track task dependencies, active tasks, and implementation progress. |
| `frontend/` | Implement client-facing interfaces, components, and state management (React.js). |
| `backend/` | Implement REST APIs, workflow engine, domain logic, and integrations. |
