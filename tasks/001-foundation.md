# 001 - Foundation & Discovery

## Overview
* **Status**: Pending Approval / Ready to Start
* **Milestone**: Foundation & Baseline Setup
* **Dependencies**: None (Starting Point)

---

## 1. Why the Feature Exists
Before building application features, the team must align on the core multi-organization domain model, define discovery requirements for user management and onboarding, validate external system touchpoints, establish technical baselines, and scaffold the baseline repository and cloud environments.

---

## 2. Who Uses It & Which Organizations/Users Are Involved
* **Ouch! Project Stakeholders**: Business Owner, Project Sponsor, Operations Team, Customer Support, IT/Infrastructure Team.
* **External Organization Stakeholders (Conceptual)**: Representatives from partner organizations (e.g., Insurance/Takaful partners, Corporate Clients, Brokers, Affiliates) participating in Discovery workshops and process mapping.

---

## 3. Important User Journeys & Discovery Workstreams

### Workstream 1.1: Business Process Mapping & User Journeys
* Map end-to-end user journeys for both sides of the portal:
  * External Organization side: Organization registration/onboarding, user account creation, request creation (policy issuance, enquiry, claims), document upload, and request tracking.
  * Ouch! Internal side: Organization review and approval, operational queue management, document validation, workflow state progression, policy processing, and escalation handling.
* Establish initial turnaround baselines to validate targets (reducing partner onboarding from 5–10 days to 1–2 days; accelerating policy issuance turnaround by 30–40%).

### Workstream 1.2: Multi-Organization Structure & Identity Discovery
* Formulate discovery options for the two administration levels:
  * Ouch! Internal Users (operations officers, managers, support agents, system admins).
  * Organization Admins (e.g., ABC Admin managing ABC users).
  * Normal Organization Users (e.g., ABC User creating requests and uploading documents).
* Investigate organization onboarding mechanisms: self-service registration vs. invitation-based onboarding vs. manual provisioning by Ouch! operations.
* Investigate user authentication models: centralized Identity Provider vs. per-organization SSO federation vs. local credential management with MFA.

### Workstream 1.3: Technical Architecture & Stack Resolution
* Facilitate stakeholder decisions on open technical alternatives recorded in [ADR-0002](../docs/decisions/ADR-0002-open-architecture-decisions.md):
  * Backend runtime: `.NET Core` vs. `Node.js`
  * Cloud platform & storage: `Microsoft Azure` (Blob Storage) vs. `AWS` (Amazon S3)
* Finalize solution architecture document and transition ADR-0002 to Accepted upon stakeholder sign-off.

### Workstream 1.4: External Integration Feasibility & Sandbox Access
* Verify API capabilities, endpoints, and staging credentials for existing systems:
  * Core Insurance Platform
  * CRM
  * Identity Provider (OAuth 2.0 / OIDC)
  * Transactional Email Service

### Workstream 1.5: UI Wireframes & User Journey Sign-Off
* Produce wireframes reflecting organization separation and distinct user perspectives:
  * External Organization Portal: Dashboard, Request submission forms, Document upload/status views, User management (for Org Admins).
  * Ouch! Internal Operations Portal: Multi-organization operational queues, Review checkpoints, SLA monitoring, and KPI reporting.
* Obtain formal sign-off from Ouch! Business Owner.

### Workstream 1.6: Repository Scaffolding & Cloud Environment Setup
* Provision development cloud resources (compute, managed PostgreSQL database, object storage container/bucket).
* Scaffold frontend (`frontend/`) using React.js.
* Scaffold backend (`backend/`) using the selected runtime (.NET Core or Node.js).
* Establish base database migration tooling and CI/CD pipelines.

---

## 4. Business Rules & Organization/Data Isolation Considerations
* The portal is a single shared application serving Ouch! internal teams and multiple distinct external organizations.
* The foundational architecture and database design must treat the organization entity as the primary isolation boundary from Day 1.
* No external organization may view another organization's records, users, or workflows unless explicitly authorized by the eventual permission model.

---

## 5. Dependencies
* Timely access to Ouch! subject matter experts (operations, support, and partner-facing teams).
* Staging/test credentials provided by Ouch! IT for existing integration touchpoints.
* Stakeholder decision on backend framework and cloud provider.

---

## 6. Open Questions & Discovery Items
* *Discovery Question*: What is the finalized Ouch! internal role hierarchy (e.g., Operations Officer vs. Operations Manager vs. Support Agent)?
* *Discovery Question*: What is the approved onboarding mechanism for external organizations (self-service registration vs. invitation link vs. manual back-office creation)?
* *Discovery Question*: How will Organization Admins and normal organization users be authenticated (central Ouch! IdP, dedicated organization SSO, or portal-managed credentials with MFA)?
* *Discovery Question*: How are Organization Admins initially provisioned and authorized?
* *Discovery Question*: What are the exact request workflow states and transition rules between external organizations and Ouch! operations?

---

## 7. Expected Outcome & Deliverables
1. Business process maps and signed-off detailed requirements document.
2. Accepted Architecture Decision Record (ADR) resolving tech stack and cloud hosting.
3. Integration feasibility report and staging sandbox access verification.
4. Signed-off UI wireframe package covering external organization and Ouch! internal views.
5. Functional repository scaffolding with running local/dev environment and base PostgreSQL migrations.

---

## 8. Verification & Acceptance Checklist
- [ ] Process maps signed off by Business Owner.
- [ ] Multi-organization data isolation strategy reviewed and approved in architecture.
- [ ] Backend stack and cloud provider confirmed and documented.
- [ ] Staging API credentials verified for external systems.
- [ ] Wireframes approved by stakeholders.
- [ ] `frontend/` builds and runs cleanly.
- [ ] `backend/` connects to PostgreSQL and passes baseline health checks.

---

## 9. Explicitly Out of Scope
* Implementing functional business application features.
* Finalizing unverified permission matrices or role schemas before discovery workshops conclude.
* Native mobile applications (iOS/Android).
* Re-platforming or replacing existing core systems.
