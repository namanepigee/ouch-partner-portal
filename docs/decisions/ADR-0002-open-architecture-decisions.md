# ADR-0002: Open Architecture Decisions (Pending Discovery)

* **Status**: Proposed / Under Evaluation (Open for Stakeholder Input)
* **Target Resolution**: End of Phase 1 (Discovery)

---

## 1. Decision Item 1: Backend Framework (.NET Core vs. Node.js)

### Context
The source document leaves the backend runtime explicitly open between **.NET Core** and **Node.js**. The decision must be confirmed during the Discovery phase based on Ouch!'s existing infrastructure, in-house technical skills, and total cost of ownership (TCO).

### Options Considered
* **Option A: .NET Core (C#)**
  * *Pros*: Strongly-typed enterprise environment, high performance, enterprise tooling, tight integration with Microsoft ecosystem (Active Directory/Azure).
  * *Cons*: Requires C# / .NET skillsets, different runtime paradigm from React frontend.
* **Option B: Node.js (TypeScript)**
  * *Pros*: Full-stack JavaScript/TypeScript alignment with React frontend, rich asynchronous I/O ecosystem, shared types/DTO patterns.
  * *Cons*: Requires disciplined architecture patterns for enterprise workflow state machines.

### Action / Input Required
Ouch! Solution Architect and Engineering leadership to review internal team skills and confirm backend runtime.

---

## 2. Decision Item 2: Cloud Platform & Object Storage (Azure vs. AWS)

### Context
The target cloud platform is left open between **Microsoft Azure** and **Amazon Web Services (AWS)**. Storage selection is coupled directly to the chosen provider (**Azure Blob Storage** vs. **Amazon S3**).

### Options Considered
* **Option A: Microsoft Azure**
  * *Compute*: Azure App Services / Azure Container Apps.
  * *Database*: Azure Database for PostgreSQL (Flexible Server).
  * *Storage*: Azure Blob Storage.
  * *Identity*: Azure AD / Entra ID B2B / B2C integration.
* **Option B: Amazon Web Services (AWS)**
  * *Compute*: AWS ECS / App Runner.
  * *Database*: Amazon RDS for PostgreSQL.
  * *Storage*: Amazon S3 with SSE encryption.
  * *Identity*: AWS Cognito or enterprise IdP federation.

### Action / Input Required
Ouch! IT / Infrastructure team to confirm existing cloud subscription footprint, corporate hosting policies, and cost preferences.

---

## 3. Decision Item 3: Core Insurance Platform Integration Protocol & Latency

### Context
The source document notes that the existing core insurance platform exposes APIs or can be made to expose APIs. Whether policy issuance requests should be processed synchronously or asynchronously (via webhooks or event queues) remains to be defined during Discovery.

### Action / Input Required
Ouch! IT to provide API documentation, staging access, and SLA characteristics of the core insurance system.
