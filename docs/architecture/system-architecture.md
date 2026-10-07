# System Architecture

## 1. High-Level Architecture Overview

The Enterprise Partner & Operations Portal is designed as a cloud-native, multi-tier web application built on modular services, relational persistence, secure object storage, and an integration layer connecting to Ouch!'s existing core systems.

```text
+-----------------------------------------------------------------------------------+
|                                Presentation Layer                                 |
|                         Responsive Web Application (React.js)                     |
|     (Partner Portal, Operations Portal, Dashboards, Workflow & Request Views)     |
+------------------------------------------+----------------------------------------+
                                           | HTTPS / REST / JSON
                                           v
+-----------------------------------------------------------------------------------+
|                               API / Application Layer                             |
|                           Backend (.NET Core or Node.js)                          |
|                                                                                   |
|  +--------------------+  +----------------------+  +---------------------------+  |
|  | Partner Management |  | Document Management  |  |    Request Management     |  |
|  +--------------------+  +----------------------+  +---------------------------+  |
|  +--------------------+  +----------------------+  +---------------------------+  |
|  |   Workflow Engine  |  | Dashboard & Reporting|  |  User & Access Management |  |
|  |  (Routing & SLAs)  |  |      (Analytics)     |  |       (RBAC & MFA)        |  |
|  +--------------------+  +----------------------+  +---------------------------+  |
|  +-----------------------------------------------------------------------------+  |
|  |                           API Integration Layer                             |  |
|  +-----------------------------------------------------------------------------+  |
+------------------------+-------------------------------+--------------------------+
                         |                               |
        +----------------+---------------+               | Object Storage
        | Relational Data                | Storage       | (Presigned URLs / Direct)
        v                                v               v
+-------------------+            +--------------------------------------------------+
|    PostgreSQL     |            | Cloud Object Storage (Azure Blob / Amazon S3)    |
| (Entities, State, |            | (Agreements, Uploaded Documents, Evidence Files) |
| RBAC, Audit Logs) |            +--------------------------------------------------+
+-------------------+
        ^
        | Integration Connectors
        v
+-----------------------------------------------------------------------------------+
|                          External & Existing Systems                              |
|  +---------------------+   +---------------------+   +--------------------------+ |
|  | Core Insurance Plat.|   |     CRM System      |   | Identity Provider (IdP)  | |
|  +---------------------+   +---------------------+   +--------------------------+ |
|  +---------------------+                                                          |
|  |    Email Services   |                                                          |
|  +---------------------+                                                          |
+-----------------------------------------------------------------------------------+
```

---

## 2. Technology Stack & Architectural Decision Status

| Layer | Confirmed Technology | Alternatives Under Evaluation (Discovery Phase) |
| :--- | :--- | :--- |
| **Frontend** | React.js (SPA / Responsive Web) | Confirmed |
| **Backend API** | RESTful Architecture | **.NET Core** vs. **Node.js** (Decision pending Discovery) |
| **Database** | PostgreSQL | Confirmed |
| **Object Storage**| Cloud Object Storage | **Azure Blob Storage** vs. **Amazon S3** (Depends on cloud) |
| **Cloud Provider**| Cloud-Native Platform | **Microsoft Azure** vs. **AWS** (Decision pending Discovery) |
| **Auth Protocol** | OAuth 2.0 / OpenID Connect | Confirmed |

*Note: The choice between .NET Core vs Node.js and Azure vs AWS will be confirmed during the Discovery phase based on Ouch!'s existing infrastructure, internal skills, and total cost of ownership.*

---

## 3. Layer Responsibilities

### Frontend Layer (`frontend/`)
* **Technology**: React.js.
* **Responsibilities**:
  * Single, responsive web interface for both external users (partners, brokers, corporate clients) and internal users (operations, customer support, managers).
  * Form management and client-side validation (registration, request creation, document submission).
  * Real-time dashboard visualizations, operational queue management, and analytics rendering.
  * Role-aware UI rendering according to granted RBAC privileges.
  * Secure token handling and redirection flows with the Identity Provider.

### Backend / API Layer (`backend/`)
* **Technology**: .NET Core or Node.js (RESTful APIs).
* **Responsibilities**:
  * Business logic execution for partner onboarding, request lifecycle, document validation, and workflow state machines.
  * Role-Based Access Control enforcement and MFA verification on every endpoint.
  * Task workflow automation: rule-based queue routing, SLA monitoring timers, reminders, and escalation handlers.
  * Audit logging: recording tamper-evident entries for operational actions.
  * Secure mediation for document upload/download with cloud storage.
  * Integration gateway abstracting communication with existing external systems.

### Persistence & Storage Layer
* **PostgreSQL Database**:
  * Relational store for partner accounts, user profiles, RBAC configurations, request state tracking, SLA metadata, and audit records.
  * Strict schema integrity, foreign keys, and transaction management.
* **Cloud Object Storage (Azure Blob / AWS S3)**:
  * Encrypted storage for document binaries, contracts, agreement PDFs, and uploaded evidence.
  * Access managed via time-limited, signed URLs or backend mediation.

---

## 4. Architectural Constraints & Boundaries
1. **Existing Systems Preservation**: No re-platforming or replacing existing core systems (Core Insurance, CRM, IdP). The portal acts as an integration consumer and operational gateway.
2. **Device Scope**: Strict focus on responsive web browsers; native mobile wrappers or apps are out of scope.
3. **Multi-Tenant Segregation**: Logical segregation at application and query level ensuring external partners have access exclusively to their own organization's records.
4. **Stateless API Design**: The backend REST APIs must remain stateless to support horizontal scaling in the cloud.
