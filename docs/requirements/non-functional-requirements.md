# Non-Functional Requirements (NFRs)

This document outlines the architectural, security, performance, and operational constraints derived from the project source document.

---

## 1. Security & Compliance

1. **Authentication & Identity Standards**
   - Industry-standard OAuth 2.0 / OpenID Connect (OIDC) protocols.
   - Mandatory Multi-Factor Authentication (MFA) across all external and internal user roles.
2. **Access Control & Multi-Tenancy / Segregation**
   - Role-Based Access Control (RBAC) enforced at API and database query levels.
   - Strict tenant/partner data isolation: Partners and corporate clients must never access another partner's records, documents, or requests.
3. **Data Protection & Privacy**
   - Compliance with financial and insurance data privacy standards (PII protection).
   - Encryption in transit (TLS 1.2+ mandatory across all endpoints).
   - Encryption at rest for relational database (PostgreSQL) and object storage (Azure Blob / AWS S3).
4. **Auditability & Traceability**
   - Immutable audit logs for all critical actions: document uploads/views, status modifications, approval decisions, and authentication events.
   - Audit trail must record timestamp, actor ID, action type, IP address, and target entity.

---

## 2. Performance & Scalability

1. **Cloud-Native Scalability**
   - System must support horizontal scaling in the chosen cloud environment (Azure or AWS) to handle concurrent partner request volume.
2. **Turnaround & Response Times**
   - Target 30–40% turnaround acceleration in policy issuance request processing.
   - Web application responsiveness under expected concurrent user load (to be validated in Phase 3 Performance Testing).
3. **Document Handling Capacity**
   - Performant handling of document uploads and downloads without blocking core portal APIs (e.g., using direct-to-cloud signed/presigned URLs).

---

## 3. Reliability & Availability

1. **Resilience**
   - Cloud deployment with automated failover and managed database backup/point-in-time recovery for PostgreSQL.
   - Graceful degradation when external integrations (CRM, core platform) experience temporary downtime or network latency.
2. **Fault Tolerance & Async Processing**
   - Asynchronous queuing/background processing for notifications, reminders, and external API sync to avoid blocking user interactions.

---

## 4. Usability & Client Compatibility

1. **Responsive Web Application**
   - Delivered as a modern, responsive web application (React.js) compatible with standard modern desktop and mobile browsers.
   - Native mobile applications (iOS/Android) are explicitly out of scope.
2. **User Experience**
   - Intuitive, frictionless workflows designed to reduce onboarding time from 5–10 days down to 1–2 days and reduce email coordination by ~70%.

---

## 5. Integration Constraints

1. **Integration with Existing Systems**
   - Integrates with Ouch!'s existing core insurance platform, CRM, and identity provider without requiring replacement or re-platforming of legacy systems.
   - RESTful API communication across integration boundaries.
