# Business Requirements & Project Scope

## 1. Executive Summary & Project Purpose
Ouch! is expanding its network of insurance and takaful partners, corporate clients, brokers, affiliates, and internal operations teams. Currently, collaboration occurs via informal and fragmented channels: email threads, shared spreadsheets, shared drives, and messaging apps.

The **Enterprise Partner & Operations Portal** is a single, secure, cloud-based platform that centralizes partner onboarding, document handling, request management, workflow automation, and operational reporting, integrated with Ouch!'s existing insurance systems.

* **Project Duration**: 4–5 months (~17 weeks across 4 phases).
* **Expected ROI**: Within 12–18 months of go-live.

---

## 2. Business Problem & Current Pain Points
Interactions with external and internal stakeholders suffer from:
* **Slow Partner Onboarding**: Typically takes 5–10 days.
* **Manual Document Collection**: Fragmented storage across email and shared drives with no central repository.
* **Duplicate Data Entry**: Re-entering the same information across disparate systems and teams.
* **Limited Request Visibility**: Lack of tracking for open requests, statuses, approvals, and escalations.
* **Delayed Policy Issuance**: Caused by asynchronous back-and-forth communication.
* **Elevated Operational Cost**: Driven by manual handling, coordination overhead, and rework.

---

## 3. Project Objectives & Success Metrics (Target KPIs)

| KPI | Current State | Target State |
| :--- | :--- | :--- |
| **Partner Onboarding Time** | 5–10 days | 1–2 days |
| **Manual Document Handling** | High | Reduced by ~80% |
| **Email-based Requests / Coordination**| High | Reduced by ~70% |
| **Request Visibility** | Limited | Real-time dashboards & status tracking |
| **Processing Turnaround (Policy Issuance)** | Baseline | 30–40% faster turnaround |
| **Operational Reporting** | Manual | Automated real-time dashboards & exports |

---

## 4. User Roles & Stakeholders

### Stakeholder Groups & Personas
1. **Insurance / Takaful Partners**: Underwriters and partner institutions managing distribution agreements and policy reviews.
2. **Corporate Clients**: Enterprise clients submitting requests, managing corporate policy documentation, and tracking status.
3. **Brokers & Affiliates**: Intermediaries submitting partner registration, enquiries, and policy issuance requests.
4. **Internal Operations Teams**: Case officers and operations managers reviewing onboarding submissions, processing policy issuance requests, managing documents, and tracking SLA compliance.
5. **Customer Support**: Support agents handling product enquiries and claims support requests.
6. **Project Sponsor (Ouch!)**: Overall accountability, budget approval, escalation resolution.
7. **Business Owner / Product Owner (Ouch!)**: Requirements sign-off, UAT coordination, prioritization decisions.
8. **IT / Infrastructure (Ouch!)**: Cloud environment provisioning, access to existing systems for integration.

---

## 5. Scope of Work

### In-Scope Core Modules
The portal comprises seven core modules integrated with Ouch!'s existing systems:
1. **Module 1 — Partner Management**: Partner registration, digital onboarding workflow, approval workflows, partner profile management, agreement repository.
2. **Module 2 — Document Management**: Secure document upload, version control, document validation, digital acknowledgements, audit trail.
3. **Module 3 — Request Management**: Policy issuance requests, product enquiries, claims support requests, escalation workflows, status tracking.
4. **Module 4 — Task Workflow Engine**: Automated routing, SLA monitoring, approval workflows, email notifications, reminder automation.
5. **Module 5 — Dashboard & Reporting**: Pending requests view, partner performance metrics, processing time analytics, operational KPIs, exportable reports.
6. **Module 6 — User & Access Management**: Role-based access control (RBAC), multi-factor authentication (MFA), audit logs, secure authentication.
7. **Module 7 — API Integration Layer**: Integration with Core insurance platform, CRM, Email services, Identity provider, and Cloud document storage.

### Out-of-Scope (Explicitly Excluded)
* **Native Mobile Applications (iOS/Android)**: The portal is delivered strictly as a responsive web application.
* **Replacement or Re-platforming**: No replacement of the core insurance system, CRM, or identity provider; the portal integrates with existing systems as they exist today.
* **Historical Data Migration**: No migration of historical partner data beyond the minimum required for go-live.
* **Multi-Language / Localization**: No localization beyond the primary operating language unless explicitly scoped and agreed during Discovery.
* **Public-Facing Customer Self-Service Portal**: The portal is strictly for partner, corporate client, broker, affiliate, and internal operations users—not retail end-customers.
* **Post-Hypercare Enhancements**: Enhancements following the hypercare window are managed under a separate change request process.

---

## 6. Project Acceptance Criteria
The project is complete and accepted when:
1. All seven core modules are deployed to production and functioning per signed-off requirements.
2. API integrations with the core insurance platform, CRM, email services, identity provider, and document storage are live and validated.
3. System, UAT, security, and performance test cycles are completed with all critical/high defects resolved.
4. Role-based access control (RBAC) and multi-factor authentication (MFA) are enforced for all user roles.
5. User training has been delivered and technical/user documentation handed over to Ouch!.
6. The hypercare support period has concluded with no open Severity-1 issues.

---

## 7. Governance, Change Management & Dependencies

### Governance
* Weekly project status meetings during Discovery, Development, and Testing.
* Daily standups during the 2-week Deployment / Go-Live phase.
* Any scope, timeline, or budget adjustment requires a formal Change Request signed off by the Project Sponsor.
* Contingency allocation (USD 2,000, ~4.5%) is reserved for unforeseen integration complexities or Discovery refinements.

### Critical Dependencies & Assumptions
* **System Access**: Availability of test/staging credentials for the core insurance platform, CRM, and IdP by the start of Phase 2 (Development).
* **Infrastructure**: Timely provisioning of cloud environment (Azure or AWS) ahead of Phase 2.
* **Key Decisions**: Confirmation of backend framework (.NET Core vs Node.js) and cloud provider (Azure vs AWS) at the conclusion of Phase 1 (Discovery).
* **Personnel**: Ouch! provides timely access to SMEs for Discovery workshops and a dedicated, empowered Business Owner for sign-offs.
