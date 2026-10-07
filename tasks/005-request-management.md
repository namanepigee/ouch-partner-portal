# 005 - Request Management Module

## Overview
* **Status**: Pending
* **Milestone**: Core Business Services
* **Dependencies**: [002-user-and-access-management.md](002-user-and-access-management.md), [003-document-management.md](003-document-management.md), [004-partner-management.md](004-partner-management.md)

---

## 1. Why the Feature Exists
Today, request collaboration occurs via unstructured emails and messaging, creating delayed policy issuance, lack of visibility into open items, and duplicate manual entry. This module centralizes request submission, document attachment, and real-time status tracking for policy issuance requests, product enquiries, and claims support requests, accelerating turnaround by 30–40% and reducing email coordination by ~70%.

---

## 2. Who Uses It & Which Organizations/Users Are Involved
* **External Organization Users (e.g., ABC User, XYZ User)**: Create requests, upload required documents, view open items, track status changes, and respond to requests for additional information.
* **Organization Admins (e.g., ABC Admin)**: Oversee all requests submitted by their organization, monitor resolution timelines, and submit escalations when needed.
* **Ouch! Internal Operations Teams**: Receive policy issuance requests, validate submitted data, progress requests through operational stages, coordinate underwriting, and issue policy confirmations.
* **Ouch! Customer Support Teams**: Receive product enquiries and claims support requests, coordinate responses, and handle operational support.

---

## 3. Important User Journeys

### Journey 5.1: External Organization Request Submission Flow
1. **Initiate Request**: ABC User clicks "Create Request" in the portal.
2. **Select Request Type**: User chooses from in-scope categories:
   * *Policy Issuance Request* (submission of policy underwriting requests and schedules).
   * *Product Enquiry* (questions regarding insurance/takaful products and coverage guidelines).
   * *Claims Support Request* (assistance with claims handling and documentation).
3. **Enter Information**: User completes structured fields specific to the request category.
4. **Attach Documents**: User uploads required evidentiary documents (leveraging [003-document-management.md](003-document-management.md)).
5. **Submit**: Request is validated and submitted to Ouch! operations.

### Journey 5.2: Ouch! Internal Processing & Lifecycle State Progression
1. **Intake**: Ouch! Operations team receives the submitted request in their operational queue (routed via [006-task-workflow-engine.md](006-task-workflow-engine.md)).
2. **Review & Action**: Operations officer reviews request details and attached files.
3. **Status Update**: Officer updates request status:
   * Requests additional details or document revisions (moving status to `Pending Info`).
   * Approves and processes the request (moving status to `In Review` -> `Approved` -> `Issued`).
   * Rejects with documented explanation.
4. **Downstream Sync**: Validated policy issuance requests trigger synchronization with Ouch!'s Core Insurance Platform (via [007-external-integrations.md](007-external-integrations.md)).

### Journey 5.3: Real-Time Status Tracking & Escalations
1. ABC User and ABC Admin track request progress in real time via their organization's request list view.
2. If processing is delayed or an urgent issue arises, user or operations officer can trigger an escalation.
3. System logs escalation reason, highlights request in operational queues, and notifies assigned stakeholders.

---

## 4. Business Rules & Organization/Data Isolation Considerations
* **Strict Organization Isolation**: ABC users must only access requests belonging to ABC Organization. XYZ Insurance users must never view, list, or track ABC requests.
* **Ouch! Operations Cross-Organization View**: Ouch! operations officers can access requests across organizations according to their assigned operational queues and role permissions.
* **Audit Trail**: Every status change, comment, document attachment, and escalation must be immutably recorded with actor ID, organization context, and timestamp.

---

## 5. Dependencies
* [002-user-and-access-management.md](002-user-and-access-management.md) (Authentication, user identity, and tenant context).
* [003-document-management.md](003-document-management.md) (Document upload and versioning for request attachments).
* [004-partner-management.md](004-partner-management.md) (Organization record association).

---

## 6. Open Questions & Discovery Items
* *Open Requirement / Discovery Question*: What are the exact mandatory and optional input fields per request type (Policy Issuance vs. Product Enquiry vs. Claims Support)?
* *Open Requirement / Discovery Question*: What are the exact lifecycle workflow states and valid transitions per request category (e.g., `Draft`, `Submitted`, `In Review`, `Pending Info`, `Approved`, `Issued`, `Closed`)?
* *Open Requirement / Discovery Question*: Does an Organization Admin have a pre-submission review/approval gate before an ABC User's request is submitted to Ouch!?
* *Open Requirement / Discovery Question*: What are the intra-organization visibility rules (can an ABC User see all ABC requests, or only requests they personally created)?
* *Open Requirement / Discovery Question*: What criteria and thresholds define when a request can be escalated manually vs. automatically?

---

## 7. Expected Outcome & Deliverables
* Dynamic request creation forms tailored by request category with document attachment support.
* External organization request list and tracking view with real-time status indicators.
* Internal operations request management console with status transition controls and escalation triggers.
* Comprehensive audit logging for all request lifecycle events.

---

## 8. Verification & Acceptance Checklist
- [ ] ABC User can create, attach documents to, and submit policy issuance, product enquiry, and claims requests.
- [ ] ABC User and ABC Admin can track the real-time status of submitted requests.
- [ ] XYZ Organization users cannot see or access ABC requests (isolation verified).
- [ ] Ouch! Operations team can review requests, transition status, and request additional information.
- [ ] Manual and automated escalations flag requests prominently in operational views.
- [ ] Audit log captures all request creations, updates, and status changes.

---

## 9. Explicitly Out of Scope
* Automatic policy underwriting calculation engines (underwriting calculations reside in the existing Core Insurance Platform).
* Retail consumer claims filing (portal is strictly for enterprise partners, brokers, corporate clients, and operations).
