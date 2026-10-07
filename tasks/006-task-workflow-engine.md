# 006 - Task Workflow Engine

## Overview
* **Status**: Pending
* **Milestone**: Workflow Automation & Routing
* **Dependencies**: [004-partner-management.md](004-partner-management.md), [005-request-management.md](005-request-management.md)

---

## 1. Why the Feature Exists
To eliminate unstructured email back-and-forth and manual ticket triage, this engine automates task distribution between external organizations and Ouch! operations teams, enforces SLA countdowns, coordinates multi-level approval hierarchies, and sends automated event notifications and reminders.

---

## 2. Who Uses It & Which Organizations/Users Are Involved
* **Ouch! Operations & Customer Support**: Work from automated task queues, claim items, execute approval decisions, and monitor SLA compliance countdowns.
* **External Organization Users & Admins (e.g., ABC User, ABC Admin)**: Receive automated notifications and reminders when action is required (e.g., missing document or review needed) and submit updates that route back to Ouch! teams.

---

## 3. Important User Journeys

### Journey 6.1: Automated Task Routing & Queue Assignment
1. An incoming request (e.g., Policy Issuance Request from ABC Insurance) or partner onboarding application is submitted.
2. The workflow engine evaluates routing rules (e.g., request type, partner tier, line of business) and assigns the item to the appropriate Ouch! operations queue.
3. Operations officers can view queue items and claim or be assigned tasks based on configured distribution rules.

### Journey 6.2: SLA Monitoring & Countdown Tracking
1. A timer starts upon request submission based on the configured SLA for that request category.
2. The engine tracks elapsed time against defined thresholds:
   * `Within SLA` (normal processing state).
   * `Warning Threshold` (e.g., 75% elapsed SLA; alerts assigned officer).
   * `Breached` (SLA exceeded; triggers automated escalation and manager notification).
3. Visual indicators in operational dashboards update in real time.

### Journey 6.3: Two-Way Workflow Movement Between External Org and Ouch!
1. Ouch! Operations officer flags a request as requiring additional details or corrected documents.
2. The workflow engine transitions the item to `Pending Info` and dispatches an automated notification to ABC User.
3. The task context is returned to ABC Organization.
4. ABC User uploads the requested documentation and resubmits.
5. The workflow engine detects the update, advances status back to `In Review`, and re-routes the task to Ouch! operations.

### Journey 6.4: Approval Workflows & Reminder Automation
1. High-value requests or organization onboarding cases require multi-level approval (e.g., Senior Officer -> Operations Manager).
2. Approvers execute decisions (`Approve`, `Reject`, `Request Info`).
3. Scheduled background workers send automated reminders for pending approvals approaching deadline thresholds.

---

## 4. Business Rules & Organization/Data Isolation Considerations
* **Tenant Isolation in Notifications & Tasks**: Notification payloads sent to external users must strictly pertain to their own organization's records and never leak information about other organizations.
* **Internal Operations Boundary**: External organization users cannot view internal operational task queues, internal assignment details, or internal notes across organizations.
* **State Machine Consistency**: State transitions must be validated against permitted transition paths to prevent invalid workflow states.

---

## 5. Dependencies
* [004-partner-management.md](004-partner-management.md) (Organization onboarding workflow triggers).
* [005-request-management.md](005-request-management.md) (Request lifecycle event triggers).

---

## 6. Open Questions & Discovery Items
* *Open Requirement / Discovery Question*: What are the exact SLA duration thresholds and warning alert percentages per request type?
* *Open Requirement / Discovery Question*: What is the approved queue distribution strategy (manual pull from pool, round-robin, load-balanced, or skill-based)?
* *Open Requirement / Discovery Question*: Do external Organization Admins participate as formal approvers in any workflow steps before items reach Ouch!?
* *Open Requirement / Discovery Question*: What is the exact multi-tier internal approval hierarchy at Ouch! for high-value policy issuance requests?
* *Open Requirement / Discovery Question*: What are the configured retry and throttle limits for automated email notifications and reminders?

---

## 7. Expected Outcome & Deliverables
* Configurable rule-based task routing engine.
* Real-time SLA monitoring background service with warning and breach event dispatchers.
* Multi-level approval state machine.
* Automated reminder scheduler and notification dispatcher.

---

## 8. Verification & Acceptance Checklist
- [ ] Submitted requests route to the appropriate internal operations queue based on business rules.
- [ ] SLA timers initiate on submission and accurately reflect remaining time.
- [ ] Warning and breach events trigger alerts in operational views and send notification emails.
- [ ] Task status cycles cleanly between external organization (`Pending Info`) and Ouch! operations (`In Review`).
- [ ] Multi-level approval transitions progress according to defined approval rules.
- [ ] Notifications and reminders never expose data across organization boundaries.

---

## 9. Explicitly Out of Scope
* Complex third-party BPMN workflow suites (e.g., Camunda) unless determined during Discovery (workflow engine is built as an integrated portal service).
