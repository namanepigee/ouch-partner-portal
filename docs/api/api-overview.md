# API Boundaries & Interface Overview

## 1. Architectural Style & Standards

* **Protocol & Format**: RESTful architecture over HTTPS using JSON for payloads.
* **Authentication**: OAuth 2.0 / OpenID Connect (OIDC) Bearer Tokens (JWT).
* **Authorization**: Role-Based Access Control (RBAC) enforced on all private endpoints.
* **Security**: MFA verification claims required on access tokens.

> **CRITICAL RULE**: Exact endpoint paths, request bodies, and response payloads are not fully specified in the primary source document and must be confirmed during the Discovery phase. Do NOT invent hypothetical schemas or mock endpoints until finalized in Discovery workshops.

---

## 2. API Domain Boundaries & Functional Areas

The portal backend exposes REST services organized across the seven core functional areas:

### 1. Partner Management API Boundary
* **Purpose**: Manages partner onboarding, profile information, and agreement associations.
* **Operations Needed**:
  * Submit partner registration.
  * Retrieve and update partner profiles.
  * Process onboarding stage transitions and approval reviews.
  * Manage agreements associated with a partner account.

### 2. Document Management API Boundary
* **Purpose**: Handles file upload authorizations, document metadata, versioning, and validation.
* **Operations Needed**:
  * Request upload authorization / presigned storage URL.
  * Register document metadata (category, version, file hash, linked entity).
  * Retrieve document versions and audit trail.
  * Record digital acknowledgements and approval status.

### 3. Request Management API Boundary
* **Purpose**: Coordinates requests for policy issuance, product enquiries, and claims support.
* **Operations Needed**:
  * Create, view, filter, and track requests (Policy Issuance, Enquiries, Claims Support).
  * Transition request statuses through operational workflows.
  * Trigger manual or automated escalations.

### 4. Task Workflow Engine API Boundary
* **Purpose**: Supports queue routing, SLA monitoring, and automated reminders.
* **Operations Needed**:
  * Retrieve assigned task queues and pending review items.
  * Submit task decisions (Approve, Reject, Request Info).
  * Query SLA timer statuses, warnings, and breach notifications.

### 5. Dashboard & Reporting API Boundary
* **Purpose**: Feeds operational queues, KPI summaries, and export capabilities.
* **Operations Needed**:
  * Aggregate pending requests by priority, status, and SLA.
  * Query partner performance metrics (volume, turnaround, issuance rate).
  * Generate and download exportable reports (CSV, Excel, PDF).

### 6. User & Access Management API Boundary
* **Purpose**: Manages user profiles, role assignments, and session metadata.
* **Operations Needed**:
  * Synchronize user profile context with the external Identity Provider.
  * Query role-permission mappings and tenant context.
  * Log and query security audit events.

### 7. Integration Layer Boundary (External Connectors)
* **Purpose**: Interfacing with existing enterprise systems.
* **Connectors Required**:
  * **Core Insurance Platform**: Submission of policy requests, query product info, poll/webhook policy issuance status.
  * **CRM**: Bi-directional sync of partner organization and contact records.
  * **Email Service**: Dispatch of notification templates, reminder triggers, and alert emails.
  * **Identity Provider**: Token validation, user claims introspection.
  * **Document Storage**: Secure file transfer and URL generation.

---

## 3. Pending Contracts & Discovery Items

The following contracts are explicitly pending and will be documented in this directory once agreed during Phase 1:
1. OpenAPI 3.0 specification definition for all endpoints.
2. Error response structure specification (e.g., RFC 7807 Problem Details).
3. Pagination, filtering, and sorting conventions.
4. Core Insurance Platform and CRM API schemas and webhook contracts.
