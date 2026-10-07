# Ouch! Enterprise Partner & Operations Portal

A centralized, cloud-based platform connecting insurance/takaful partners, corporate clients, brokers, affiliates, and internal operations teams.

---

## 1. Project Overview

The Enterprise Partner & Operations Portal centralizes partner onboarding, document management, request handling, workflow automation, and operational analytics into a single digital platform, integrating directly with Ouch!'s existing core systems.

* **Target Timeline**: 4–5 months (~17 weeks across Discovery, Development, Testing, Deployment).
* **Target ROI**: 12–18 months post go-live.
* **Core Objectives**:
  * Reduce partner onboarding time from 5–10 days down to 1–2 days.
  * Reduce manual document handling by ~80%.
  * Reduce email-based coordination by ~70%.
  * Accelerate policy issuance turnaround by 30–40%.
  * Automate real-time operational reporting.

---

## 2. Documentation Map

* **AI Agent Instructions**: [AGENTS.md](AGENTS.md)
* **Requirements**:
  * [business-requirements.md](docs/requirements/business-requirements.md) — Scope, objectives, user personas, KPIs, and acceptance criteria.
  * [functional-requirements.md](docs/requirements/functional-requirements.md) — The 7 core modules, features, and business logic.
  * [non-functional-requirements.md](docs/requirements/non-functional-requirements.md) — Security (MFA, RBAC), compliance, scalability, and performance.
* **Architecture**:
  * [system-architecture.md](docs/architecture/system-architecture.md) — Multi-tier cloud architecture, component layers, and responsibilities.
  * [integrations.md](docs/architecture/integrations.md) — Integration touchpoints (Core Insurance, CRM, IdP, Email, Storage).
* **API Contracts**:
  * [api-overview.md](docs/api/api-overview.md) — REST API boundaries and pending contract specifications.
* **Data Model**:
  * [domain-entities.md](docs/data-model/domain-entities.md) — Conceptual domain entities, ER diagram, and open schema items.
* **Architecture Decisions**:
  * [ADR-0001-confirmed-technical-baseline.md](docs/decisions/ADR-0001-confirmed-technical-baseline.md) — Confirmed technical baseline.
  * [ADR-0002-open-architecture-decisions.md](docs/decisions/ADR-0002-open-architecture-decisions.md) — Open choices pending Discovery (.NET vs Node.js, Azure vs AWS).
* **Development & Governance**:
  * [process-and-guidelines.md](docs/development/process-and-guidelines.md) — Delivery phases, testing strategy, security, and governance.
* **Task Backlog**:
  * [task-backlog.md](tasks/task-backlog.md) — Implementation task breakdown and milestone guides.

---

## 3. Project Structure

```text
/
├── AGENTS.md                  # Operating instructions and guidelines for AI agents
├── README.md                  # Project overview and documentation index
│
├── docs/                      # Core project documentation and specifications
│   ├── requirements/          # Business, functional, and non-functional requirements
│   ├── architecture/          # High-level architecture, diagrams, and integration touchpoints
│   ├── api/                   # REST API boundaries and contracts
│   ├── data-model/            # Conceptual domain entities and schema definitions
│   ├── decisions/             # Architecture Decision Records (ADRs)
│   └── development/           # Development process, QA, security, and governance
│
├── tasks/                     # Dependency-ordered task backlog across phases
│
├── frontend/                  # React.js client application source code
│
└── backend/                   # REST API backend source code (.NET Core or Node.js)
```

---

## 4. Level 2 Git Workflow

```text
AI implements task
      ↓
Run relevant tests
      ↓
Review changes / git diff
      ↓
Create commit
      ↓
Push feature branch
      ↓
Developer review
```

* The AI coding agent can perform local Git operations as part of completing a task.
* The agent should run relevant tests before committing.
* The agent should review the Git diff before committing.
* The agent can create a descriptive commit after successful verification.
* The agent can push the current feature branch when permitted.
* The agent must never push directly to `main`.
* The agent must not commit secrets, credentials, `.env` files, or other sensitive files.
* If tests or Git operations fail, the agent should report the failure instead of claiming the task is complete.
