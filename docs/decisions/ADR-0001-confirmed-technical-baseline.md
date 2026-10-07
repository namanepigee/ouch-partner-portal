# ADR-0001: Baseline Architectural Decisions

* **Status**: Accepted (Derived from Primary Source Document)
* **Date**: Phase 1 / Inception

---

## 1. Context
Ouch! requires an Enterprise Partner & Operations Portal to streamline partner onboarding, request handling, document management, and workflow automation across insurance partners, corporate clients, brokers, affiliates, and internal teams. The system must integrate with Ouch!'s existing IT estate.

---

## 2. Decisions Explicitly Confirmed in Project Scope

### 2.1 Presentation Tier
* **Decision**: Implement the client application using **React.js** as a responsive web application.
* **Scope Constraint**: Native mobile applications (iOS/Android) are explicitly out of scope.

### 2.2 Relational Database
* **Decision**: Adopt **PostgreSQL** as the core relational database.
* **Rationale**: Strong ACID guarantees, rich indexing, mature enterprise cloud managed offerings (Azure Database for PostgreSQL or Amazon RDS), and relational support for complex entity workflows and RBAC.

### 2.3 Authentication & Authorization
* **Decision**: Enforce **OAuth 2.0 / OpenID Connect (OIDC)** with **Multi-Factor Authentication (MFA)** and **Role-Based Access Control (RBAC)** across all user personas.
* **Rationale**: Necessary to satisfy financial and insurance sector data privacy standards (PII) and protect partner-segregated data.

### 2.4 API Communication Style
* **Decision**: Expose and consume **RESTful services** over HTTPS with JSON payloads.

### 2.5 Integration Boundary
* **Decision**: Integrate with the existing Core Insurance Platform, CRM, and Identity Provider in their current state.
* **Scope Constraint**: No re-platforming or replacing legacy systems in this project phase.

---

## 3. Consequences
* The architecture provides a clean separation of concerns between client (React) and backend REST services.
* Requires secure API mediation and strict tenant segregation at the database and API authorization layers.
