# Domain Entities & Data Model

This document outlines the core business entities, their conceptual relationships, and items pending detailed schema definition during Phase 1 Discovery.

---

## 1. High-Level Entity Relationship Diagram (Conceptual)

```text
+-------------------+             1..* +-------------------+
|      Partner      |------------------|       User        |
| (Organization)    |                  |  (IdP / RBAC)     |
+-------------------+                  +-------------------+
    |             |                              |
    | 1..*        | 1..*                         | 1..*
    v             v                              v
+-----------+  +-----------+              +---------------+
| Agreement |  |  Request  |              |   AuditLog    |
| (Contract)|  | (Lifecycle|              |  (Immutable)  |
+-----------+  +-----------+              +---------------+
    |             |
    | 1..*        | 1..*
    v             v
+--------------------------+              +---------------+
|         Document         |              | WorkflowTask  |
|      (Versioned)         |              |  & SLA Record |
+--------------------------+              +---------------+
```

---

## 2. Identified Core Domain Entities

### 1. `Partner`
* **Description**: Represents external business entities (Insurance/Takaful Partner, Corporate Client, Broker, Affiliate).
* **Key Attributes**: Entity name, registration number, partner type, status (`Registered`, `Onboarding`, `In Review`, `Approved`, `Active`, `Suspended`), contact information, CRM reference ID.
* **Relationships**:
  * Has many `User` accounts.
  * Has many `Agreement` contracts.
  * Submits many `Request` instances.
  * Has many `Document` records.

### 2. `User`
* **Description**: An authenticated user of the portal (external partner staff or internal Ouch! operations/support staff).
* **Key Attributes**: Identity Provider Subject ID (OAuth/OIDC), email, full name, phone number, MFA status, active status.
* **Relationships**:
  * Belongs to zero or one `Partner` (null for internal Ouch! staff).
  * Has one or more `Role` associations (RBAC).

### 3. `Role` & `Permission`
* **Description**: RBAC model governing portal navigation, data visibility, and API execution.
* **Roles Identified in Source**:
  * Partner User / Administrator
  * Corporate Client User
  * Broker / Affiliate
  * Operations Officer
  * Operations Manager
  * Customer Support Agent
  * System Administrator

### 4. `Agreement`
* **Description**: Legal and distribution agreements governing the partner relationship.
* **Key Attributes**: Agreement type, title, effective date, expiration date, acknowledgement status, version.
* **Relationships**:
  * Belongs to a `Partner`.
  * Associated with versioned `Document` files.

### 5. `Document` & `DocumentVersion`
* **Description**: File assets uploaded into cloud object storage, requiring version control, validation, and audit tracking.
* **Key Attributes**: Title, document type/category (e.g., license, KYC, policy schedule, claim evidence), current version number, validation status (`Pending`, `Valid`, `Invalid`, `Needs Review`), cloud storage path/key, file size, MIME type, file hash.
* **Relationships**:
  * Attached to `Partner`, `Agreement`, or `Request`.
  * Has an audit trail of actions.

### 6. `Request`
* **Description**: Operational items raised by external stakeholders or internal teams.
* **Types Identified**:
  * Policy Issuance Request
  * Product Enquiry
  * Claims Support Request
* **Key Attributes**: Request reference number, request type, priority (`Low`, `Medium`, `High`, `Urgent`), status (`Draft`, `Submitted`, `In Review`, `Pending Info`, `Approved`, `Issued`, `Closed`), submitted by user ID, core system external reference ID.
* **Relationships**:
  * Belongs to a `Partner` and submitter `User`.
  * Associated with one or more `Document` attachments.
  * Associated with one or more `WorkflowTask` steps.

### 7. `WorkflowTask` & `SLAMonitor`
* **Description**: An operational unit of work routed through the Task Workflow Engine.
* **Key Attributes**: Assigned queue, assigned operations officer, task status, due date/time, SLA target duration, SLA status (`Within SLA`, `Warning`, `Breached`), escalation level.
* **Relationships**:
  * Belongs to a `Request` or `Partner` (for onboarding approvals).

### 8. `AuditLog`
* **Description**: Tamper-evident record of actions across the system.
* **Key Attributes**: Timestamp, actor ID (User), action type, target entity type, target entity ID, IP address, payload/state change details.

---

## 3. Items Pending Decision & Discovery Workshop Sign-Off

The following data model specifications must be determined in Phase 1 Discovery:
1. **Concrete Database Schemas**: Detailed PostgreSQL DDL / migration specifications, field constraints, nullability, and foreign key cascading.
2. **Document Metadata Standards**: Strict document type taxonomies and validation rule definitions per document type.
3. **External ID Mapping**: Exact external key attributes linking records to Ouch!'s legacy Core Insurance Platform and CRM.
4. **Historical Data Schema**: Minimum data structure required for initial partner seeding/go-live import.
