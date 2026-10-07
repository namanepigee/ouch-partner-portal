# 007 - External Integrations Layer

## Overview
* **Status**: Pending
* **Milestone**: Enterprise System Integration
* **Dependencies**: [001-foundation.md](001-foundation.md), [005-request-management.md](005-request-management.md), [006-task-workflow-engine.md](006-task-workflow-engine.md)

---

## 1. Why the Feature Exists
Duplicate manual entry across disconnected spreadsheets and internal systems causes high operational overhead, delays policy issuance, and introduces data entry errors. This integration layer bridges the portal with Ouch!'s existing core systems, ensuring automated data exchange without requiring replacement or re-platforming of legacy applications.

---

## 2. Who Uses It & Which Organizations/Users Are Involved
* **Ouch! Operations & Engineering Teams**: Benefit from automated system synchronization between the portal and back-office insurance systems.
* **External Organizations (Indirectly)**: External partners (e.g., ABC Insurance) whose requests and approved profiles are automatically synchronized with core systems without manual back-office re-keying.

---

## 3. Important User Journeys & System Touchpoints

### Touchpoint 7.1: Core Insurance Platform Connector
* **Context**: Once a policy issuance request is approved in the portal, it must be synchronized with Ouch!'s core insurance platform.
* **Journey**:
  1. Portal request reaches approved status for policy issuance.
  2. Integration adapter transforms the portal request payload, including the external organization reference (e.g., Partner: ABC Insurance) and attached documents.
  3. Payload is submitted to the core platform API.
  4. Core platform returns external policy reference ID or asynchronous callback.
  5. Portal updates request status and stores the core reference ID for tracking.

### Touchpoint 7.2: CRM Partner Synchronization
* **Context**: Maintain a unified 360-degree partner profile between Ouch!'s CRM and the portal.
* **Journey**:
  1. An organization onboarding application (e.g., ABC Insurance) is approved by Ouch! operations.
  2. Integration adapter pushes organization details, key contacts, and agreement status to the CRM.
  3. Updates made in CRM (such as account manager assignments) synchronize back to the portal organization record.

### Touchpoint 7.3: Transactional Email Service
* **Context**: Dispatch automated emails for onboarding, workflow assignments, SLA warnings, and reminders.
* **Journey**:
  1. Workflow engine triggers an email event.
  2. Integration adapter applies appropriate localized templates, sets recipient headers, and dispatches via SMTP or transactional email API (e.g., SendGrid, AWS SES, or Azure Communication Services).
  3. Delivery status and failure events are logged.

### Touchpoint 7.4: Identity Provider (IdP) & Cloud Storage Integration
* **Context**: Standardize authentication verification (OAuth 2.0 / OIDC) and secure object persistence across Azure/AWS storage clients.

---

## 4. Business Rules & Organization/Data Isolation Considerations
* **Organization Context in Integration Payloads**: All data sent to the Core Insurance Platform and CRM must explicitly carry the originating organization's identifier to maintain accurate attribution.
* **Resilience & Fault Tolerance**: Failures in external systems must not block portal operations or corrupt request state; asynchronous queues and retry policies must handle temporary third-party downtimes gracefully.
* **Security & Secret Management**: No credentials, API tokens, or secrets for external systems may be hardcoded or exposed to client-side code.

---

## 5. Dependencies
* [001-foundation.md](001-foundation.md) (Sandbox access credentials verified during Discovery).
* [005-request-management.md](005-request-management.md) (Policy issuance request lifecycle).
* [006-task-workflow-engine.md](006-task-workflow-engine.md) (Workflow trigger events).

---

## 6. Open Questions & Discovery Items
* *Open Requirement / Discovery Question*: Are the Core Insurance Platform APIs synchronous (instant response) or asynchronous (polling / webhooks for policy issuance completion)?
* *Open Requirement / Discovery Question*: Will external organization users authenticate against Ouch!'s central IdP, or is the IdP strictly used for Ouch! internal users?
* *Open Requirement / Discovery Question*: What is the exact data mapping and schema specification between portal organization entities and CRM account entities?
* *Open Requirement / Discovery Question*: What are the rate limits and SLA availability commitments of the existing core systems?

---

## 7. Expected Outcome & Deliverables
* Resilient API connectors for Core Insurance Platform, CRM, Email, IdP, and Cloud Storage.
* Background queue handlers with exponential backoff and retry policies for external calls.
* Integration health check endpoints and monitoring logs.

---

## 8. Verification & Acceptance Checklist
- [ ] Approved policy issuance requests synchronize cleanly to the staging core insurance platform.
- [ ] Core insurance policy reference numbers reflect accurately on the portal request view.
- [ ] Organization profiles synchronize between portal and CRM without manual data duplication.
- [ ] Transactional emails deliver reliably with correct event-driven template contents.
- [ ] Transient integration outages are retried without losing request data or crashing portal services.

---

## 9. Explicitly Out of Scope
* Modifying, refactoring, or re-platforming existing core insurance systems or CRM applications.
* Building a real-time event broker (e.g., Kafka) unless explicitly justified during Discovery.
