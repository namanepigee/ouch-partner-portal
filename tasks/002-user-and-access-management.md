# 002 - User & Access Management Module

## Overview
* **Status**: Pending
* **Milestone**: Core Security & Identity
* **Dependencies**: [001-foundation.md](001-foundation.md)

---

## 1. Why the Feature Exists
The Ouch! Portal is a shared enterprise application serving both Ouch! internal teams and multiple distinct external organizations (e.g., ABC Insurance, XYZ Insurance, corporate clients, brokers). Secure authentication, mandatory multi-factor authentication (MFA), role-based access control (RBAC), and strict multi-organization data isolation are necessary to protect confidential insurance records, maintain regulatory compliance, and ensure users only see data belonging to their own organization context.

---

## 2. Who Uses It & Which Organizations/Users Are Involved

### 1. Ouch! Internal Users
* Operate from the Ouch! side across all or designated partner organizations.
* Manage organizations, external accounts, workflow queues, and operational configurations.
* *Note*: Exact internal role hierarchy and permissions are NOT finalized.

### 2. Organization Admins (e.g., ABC Admin, XYZ Admin)
* Administrator of their specific external organization within the Ouch! platform (e.g., ABC Insurance).
* Conceptually responsible for managing their organization's users and assigning permitted roles/access.
* Not an Ouch! platform administrator; has zero administrative authority over other organizations or Ouch! internal operations.
* *Note*: Exact permissions and management capabilities are NOT finalized.

### 3. Normal Organization Users (e.g., ABC User, XYZ User)
* External users operating strictly within their organization's context.
* Create and manage permitted requests, upload required documents, and track status.
* Must never access another organization's data or administrative settings.

---

## 3. Important User Journeys

### Journey 2.1: User Authentication & Context Establishment
1. User enters credentials via the configured authentication mechanism.
2. User completes mandatory Multi-Factor Authentication (MFA) challenge.
3. Upon successful validation, the system establishes:
   * Identity context (User ID, Name, Contact).
   * Organization context (e.g., Organization: ABC Insurance, or Internal: Ouch!).
   * Effective role and permission set.
4. The client application adapts its navigation and views to the user's role and organization boundary.

### Journey 2.2: Organization User Administration (Conceptual)
1. Organization Admin (e.g., ABC Admin) navigates to their organization's user management screen.
2. Admin creates/invites a new user (e.g., ABC User) or modifies existing user access within ABC Insurance.
3. The newly provisioned user receives access instructions and onboards into ABC Insurance's context.
4. Admin cannot view, invite, or manage users belonging to XYZ Insurance or Ouch! internal teams.

### Journey 2.3: Ouch! Internal User Administration
1. Ouch! administrator provisions or configures internal staff accounts.
2. Roles determine operational scope (e.g., viewing cross-organization operational queues, reviewing onboarding cases, managing system settings).

---

## 4. Business Rules & Organization/Data Isolation Considerations
* **Strict Organization Separation**: ABC users must never access, query, or mutate XYZ data, requests, documents, or users, unless explicitly authorized by an eventual cross-organization permission model.
* **Query-Level Multi-Tenancy**: All backend data queries and mutations for organization resources must enforce organization scoping at the persistence layer, not solely in UI presentation.
* **MFA Mandatory**: Multi-Factor Authentication is mandatory across all external and internal user categories.
* **Auditability**: All authentication attempts, privilege elevations, and user management actions must generate immutable audit log entries.

---

## 5. Dependencies
* [001-foundation.md](001-foundation.md) (Database scaffolding and discovery alignment on identity models).
* Availability of Identity Provider / credential management architecture decisions from Discovery.

---

## 6. Open Questions & Discovery Items
* *Open Requirement / Discovery Question*: What is the exact Ouch! internal role hierarchy (e.g., Operations Officer, Team Lead, Operations Manager, Support Agent, System Admin)?
* *Open Requirement / Discovery Question*: What is the exact RBAC permission matrix for internal and external actions?
* *Open Requirement / Discovery Question*: What are the exact Organization Admin capabilities (can they invite users directly, reset credentials, or assign custom sub-roles)?
* *Open Requirement / Discovery Question*: How are user credentials created and managed (manual provisioning by Ouch!, self-serve invitation links, or an external Identity Provider like Azure AD / Okta / Cognito)?
* *Open Requirement / Discovery Question*: Will external organization users authenticate against Ouch!'s central IdP, federate with their own corporate SSO, or use portal-managed credentials?
* *Open Requirement / Discovery Question*: Are there any legitimate cross-organization visibility scenarios (e.g., a master broker managing multiple corporate client entities)?

---

## 7. Expected Outcome & Deliverables
* Authentication service and session management supporting MFA.
* Authorization middleware enforcing organization boundary checks and role permissions on every API request.
* User management interfaces and endpoints tailored for Organization Admins and Ouch! Internal Users.
* Security audit logging recording actor, action, organization ID, timestamp, and IP address.

---

## 8. Verification & Acceptance Checklist
- [ ] User authentication flow successfully authenticates internal and external users.
- [ ] MFA challenge is strictly enforced; bypassing MFA prevents access to protected APIs.
- [ ] External organization user (ABC) attempting to read or modify XYZ data receives 403 Forbidden.
- [ ] Organization Admin can only view and manage users within their assigned organization.
- [ ] Ouch! internal users operate according to their assigned internal role without leaking data between external tenants.
- [ ] Security audit log records every login, failure, and permission change.

---

## 9. Explicitly Out of Scope
* Self-service customer registration for retail insurance consumers (portal is strictly for partner organizations and Ouch! internal teams).
* Finalizing unverified permission schemas before Discovery workshops conclude.
