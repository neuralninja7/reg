

## 🟩 **In Scope (Aligned to Solution & RFP)**

### 1. **AI Platform Enablement (Core Scope)**

* Establishment of a **centralized AI Platform** integrating the seven value streams (VS1–VS7).
* **AI Gateway** as a single controlled access layer for all models, APIs, and data tools.
* **Agentic AI Runtime** to execute multi-step reasoning workflows, support human-in-the-loop approvals, and tool integration.
* **Self-service RAG Builder & AI Companion tools** enabling business users to build domain-specific assistants securely.
* **Model Registry, Evaluation & Deployment Framework** with versioning, rollbacks, and automated benchmarking.
* **Data.AI Fabric Integration**—structured/unstructured data unification through Dremio, Milvus, and metadata graph.
* **AIOps/MLOps backbone**—observability, CI/CD, monitoring, cost governance, and failover automation.
* **Responsible AI & Governance layer** with policy registry, compliance automation, and audit reporting.

---

### 2. **Program Execution and Delivery**

* Platform setup, configuration, and onboarding of initial use cases (pilot and scaled rollout).
* Design and deployment of **agentic workflows and connectors** aligned with PromProm business units.
* **User onboarding and AI literacy enablement**, including training sessions and reference playbooks.
* **Multi-environment setup (Dev, QA, UAT, Prod)** including CI/CD pipelines.
* Documentation: architecture, APIs, governance policies, operating model, and handover artefacts.

---

### 3. **Security, Compliance, and Data Management**

* Implementation of **identity federation, access control, and token governance**.
* End-to-end **auditability, logging, and observability integration** (e.g., ServiceNow, Splunk).
* **Encryption, data masking, and PII handling** within AI interactions.
* **Alignment with GxP, HIPAA, and data localization standards.**

---

### 4. **Engagement, Governance & Support**

* **Joint governance model** with PromProm for approvals, design reviews, and policy updates.
* **Project management and agile delivery**, including sprint planning and milestone tracking.
* **Support and knowledge transition** at completion of implementation.

---

## 🟥 **Out of Scope (Explicit & Implied Exclusions)**

### 1. **Product Development Beyond Platform**

* Creation of **standalone business applications or products** outside the AI platform boundaries.
* Development of **custom LLMs or proprietary foundation models** beyond tuning, selection, or evaluation.
* **Data annotation or manual labeling** services at scale.
* **Third-party licensing, SaaS procurement, or infrastructure provisioning** costs outside agreed platform tools.

---

### 2. **Operational Responsibilities**

* 24×7 production support post-handover (to be transitioned to PromProm operations).
* **Change management or process reengineering** across business units beyond the AI enablement initiative.
* **Non-AI systems integration** (e.g., ERP, MES, LIMS) unless specifically part of a defined use case.

---

### 3. **Extended Deliverables**

* **Hardware provisioning, on-prem infrastructure**, or datacenter management.
* Development of **non-AI analytics dashboards or reporting portals**.
* **Regulatory filings or clinical data submissions** beyond compliance readiness.

---

### 4. **Commercial Exclusions**

* **Licenses, cloud consumption, and GPU costs** borne by PromProm.
* **Travel or third-party expenses** not pre-approved in the SOW.
* **Future extensions or follow-on phases** unless separately contracted.

---

## 🧩 **Summary Cross-Mapping to Value Streams**

| Value Stream            | In-Scope Focus                        | Out-of-Scope Boundary                   |
| ----------------------- | ------------------------------------- | --------------------------------------- |
| VS1 – Gateway           | Design, control, and API management   | Commercial licensing of external APIs   |
| VS2 – Agentic Platform  | Agent orchestration, HITL integration | Building unrelated automation bots      |
| VS3 – RAG Builder       | UI and orchestration                  | New UX frameworks or enterprise app dev |
| VS4 – Model Engineering | Registry, evaluation, deployment      | Training new foundation models          |
| VS5 – AIOps/MLOps       | Observability, CI/CD, resilience      | Production infra ownership              |
| VS6 – Data.AI           | Data access, lineage, embeddings      | Data warehousing modernization          |
| VS7 – Governance        | Policy automation, audit, literacy    | Broader org-level training programs     |

---

