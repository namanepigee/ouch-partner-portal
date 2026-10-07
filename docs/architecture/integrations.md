# External System Integrations

This document defines the integration touchpoints between the Enterprise Partner & Operations Portal and Ouch!'s existing enterprise landscape.

---

## 1. Integration Landscape Overview

Module 7 (API Integration Layer) connects the portal to five external/existing systems:
1. **Core Insurance Platform**
2. **Customer Relationship Management (CRM)**
3. **Email Services**
4. **Identity Provider (IdP)**
5. **Cloud Document Storage**

---

## 2. Integration Touchpoint Details

### 1. Core Insurance Platform
* **Purpose**: Synchronize policy issuance requests, insurance product catalog/enquiry context, and downstream policy issuance statuses.
* **Protocol / Style**: RESTful APIs.
* **Key Interactions**:
  * Submit validated policy issuance requests originated by partners.
  * Retrieve real-time or polled policy issuance status updates to reflect in the portal.
  * Query insurance and takaful product information for product enquiries.
* **Assumptions & Dependencies**:
  * Assumes the core platform provides accessible REST APIs (or can be adapted to expose them).
  * Staging/test credentials must be provided by Ouch! IT before the start of Phase 2 Development.

### 2. CRM System
* **Purpose**: Centralize partner account synchronization and maintain a unified 360-degree partner profile.
* **Protocol / Style**: RESTful APIs / Webhooks.
* **Key Interactions**:
  * Sync approved partner profiles, organization metadata, and primary contacts between the portal and CRM.
  * Eliminate duplicate manual entry across sales, partnership, and operational systems.
* **Assumptions & Dependencies**:
  * Staging credentials and API documentation to be validated during Phase 1 Discovery.

### 3. Email Services
* **Purpose**: Transactional notification dispatch, reminder automation, and escalation alerts.
* **Protocol / Style**: SMTP or Transactional Email API (e.g., SendGrid, AWS SES, or Azure Communication Services).
* **Key Interactions**:
  * Onboarding status updates and confirmation emails.
  * SLA warning alerts and escalation notifications to internal ops teams.
  * Document signature requests and acknowledgement reminders.
  * Password reset and MFA verification notices (if handled via email channel).

### 4. Identity Provider (IdP)
* **Purpose**: Centralized authentication, Single Sign-On (SSO), and Multi-Factor Authentication (MFA).
* **Protocol / Style**: OAuth 2.0 / OpenID Connect (OIDC).
* **Key Interactions**:
  * Authenticate internal and external users.
  * Enforce MFA challenge upon login.
  * Issue JSON Web Tokens (JWT) or session tokens consumed by the portal frontend and backend.
* **Assumptions & Dependencies**:
  * Ouch! will configure or provide client IDs, secret credentials, and OIDC discovery endpoints during Discovery.

### 5. Cloud Document Storage
* **Purpose**: Highly scalable, durable object storage for uploaded files, agreement documents, and evidence.
* **Protocol / Style**: Object Storage SDK / REST (Azure Blob Storage or AWS S3).
* **Key Interactions**:
  * Secure file upload via backend mediation or direct presigned/SAS URL generation.
  * File retrieval with time-limited authorization.
  * Versioned storage of agreement revisions and legal attachments.

---

## 3. Integration Risks & Mitigation Strategies

| Integration Risk | Impact | Documented Mitigation |
| :--- | :--- | :--- |
| **Delayed access or test credentials for core systems** | Schedule slip in Phase 2/3 | Confirm integration credentials and API availability during Phase 1 Discovery; flag early to Ouch! IT. |
| **API specification gaps or missing endpoints in legacy systems** | Rework during development | Conduct technical feasibility review in Discovery; allocate contingency reserve if adapter layers are needed. |
| **Rate limiting or latency in external systems** | Portal responsiveness degradation | Introduce asynchronous background queueing and caching for non-critical synchronization. |
