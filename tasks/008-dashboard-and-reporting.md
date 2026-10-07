# 008 - Dashboard & Operational Reporting Module

## Overview
* **Status**: Pending
* **Milestone**: Operations Analytics & Dashboards
* **Dependencies**: [004-partner-management.md](004-partner-management.md), [005-request-management.md](005-request-management.md), [006-task-workflow-engine.md](006-task-workflow-engine.md)

---

## 1. Why the Feature Exists
Operational reporting today depends on manually compiling spreadsheets across fragmented teams, resulting in limited visibility, delayed escalations, and high administrative overhead. This module delivers automated real-time dashboards and exportable reports to track pending requests, partner performance metrics, turnaround time analytics, and SLA compliance.

---

## 2. Who Uses It & Which Organizations/Users Are Involved

### 1. Ouch! Operations & Management
* Access multi-organization operational queues, monitor SLA countdowns, track team turnaround times, review partner performance metrics, and export aggregate reports.

### 2. External Organization Admins (e.g., ABC Admin, XYZ Admin)
* Access organization-specific dashboards summarizing ABC's active requests, turnaround metrics, and open action items.
* Never see cross-organization operational queues or performance metrics for other organizations.

### 3. Normal Organization Users (e.g., ABC User)
* View their active request statuses and pending actions within their organization context.

---

## 3. Important User Journeys

### Journey 8.1: Ouch! Operations Queue & SLA Dashboard
1. Operations officer accesses the operational dashboard.
2. View displays open requests across organizations, prioritized by urgency, request type, and remaining SLA time.
3. Visual indicators highlight requests approaching warning thresholds or in breach status.
4. Officer clicks a request to open the request detail view and take action.

### Journey 8.2: External Organization Dashboard View
1. ABC Admin logs into the portal.
2. Dashboard displays ABC Insurance's metrics: total open requests, pending document requests, recently issued policies, and average turnaround time.
3. View is strictly scoped to ABC Insurance data.

### Journey 8.3: Partner Performance & Processing Analytics
1. Ouch! management views partner analytics dashboard to evaluate:
   * Partner submission volume and approval conversion rates.
   * Documentation error and rework rates per partner.
   * End-to-end turnaround times compared to the 30–40% acceleration objective.

### Journey 8.4: Operational Report Exporting
1. Authorized user configures report parameters (date range, request type, status, and organization filter if internal).
2. System generates structured export (CSV, Excel, or PDF).
3. Download is generated with audit logging.

---

## 4. Business Rules & Organization/Data Isolation Considerations
* **Strict Organization Scoping on Dashboards**: External organization users (e.g., ABC Admin) must only view aggregated numbers, charts, and queues belonging strictly to their organization. Under no circumstances may metrics, request counts, or turnaround data from XYZ Insurance be visible.
* **Internal Role-Based Access**: Access to cross-partner performance comparisons is restricted to authorized Ouch! management roles.
* **Query Performance**: Analytical queries must be optimized (e.g., indexed queries or aggregated views in PostgreSQL) to prevent degrading operational transaction performance.

---

## 5. Dependencies
* [004-partner-management.md](004-partner-management.md) (Organization records).
* [005-request-management.md](005-request-management.md) (Request status data and timestamps).
* [006-task-workflow-engine.md](006-task-workflow-engine.md) (SLA metrics and task lifecycle events).

---

## 6. Open Questions & Discovery Items
* *Open Requirement / Discovery Question*: What is the finalized set of dashboard widgets and metrics required for Organization Admins vs. Ouch! Internal Users?
* *Open Requirement / Discovery Question*: What specific calculation formulas are used for partner performance and SLA compliance percentages?
* *Open Requirement / Discovery Question*: Which roles have permission to generate and download exportable reports, and which file formats (CSV, Excel, PDF) are mandatory for MVP?

---

## 7. Expected Outcome & Deliverables
* Role-tailored dashboard views for Ouch! Operations and External Organization Admins.
* Real-time operational queues with live SLA status filters.
* Reporting aggregation API endpoints enforcing multi-organization scoping.
* Export engine producing structured CSV/Excel/PDF downloads.

---

## 8. Verification & Acceptance Checklist
- [ ] Ouch! Operations dashboard displays open requests with live SLA countdowns.
- [ ] External Organization Admin (ABC) dashboard displays only ABC metrics and requests.
- [ ] Multi-tenant isolation verified: ABC Admin cannot see or deduce XYZ metrics or request volume.
- [ ] Processing turnaround analytics reflect elapsed time accurately across workflow stages.
- [ ] Export engine generates correct filtered reports without exposing unauthorized records.
- [ ] Analytics queries execute performantly without locking operational database tables.

---

## 9. Explicitly Out of Scope
* Integration with third-party external BI platforms (e.g., PowerBI / Tableau) unless separately scoped.
* Real-time financial accounting and claims settlement reporting.
