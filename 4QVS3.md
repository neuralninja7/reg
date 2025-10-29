# 🧩 **Final Blueprint — VS-3 : Self-Service RAG & Companion Builder**

---

## 🔹 **Quadrant 1 – Our Understanding of the Value Stream**

### 🧠 Client Intent

* Empower business users to **design and deploy RAG-based GenAI applications** through a self-service, governed interface.
* Provide both **guided (wizard) and advanced configuration** modes, supporting varied skill levels.
* Abstract technical complexity — data pipelines, model binding, retrieval logic — while preserving transparency and control.
* Ensure all RAG apps adhere to enterprise policies for data security, model use, and auditability.
* Enable **seamless integration** with AI Gateway (VS-1) for authentication and policy, and with Agentic Runtime (VS-2) for execution.
* Support a **complete lifecycle** from data ingestion → chunking → embedding → retrieval → evaluation → governance feedback.

> **In essence →** VS-3 translates enterprise AI capabilities into a governed self-service studio for knowledge companion creation.

---

## 🔹 **Quadrant 2 – Key Solution Tenets (visual diagram)**

| **Tenet / Principle**                      | **Essence (One-Line Summary)**                                                                          | **Underlying Logical Components Mapped**                      |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| **Data Ingestion & Processing Pipeline**   | Connects to enterprise repositories and performs chunking, metadata enrichment, and vector indexing.    | Data Connectors + Processing Framework + Vector Index Adapter |
| **Model Integration Framework**            | Provides a unified interface to foundation and embedding models with governed access and cost tracking. | Model Router + Embedding Manager + Prompt Template Library    |
| **RAG Pipeline Orchestration**             | Manages retrieval, context assembly and generation flows through configurable DAG patterns.             | Orchestration Engine + Policy Hooks                           |
| **Application Configuration & Versioning** | Maintains source, model, and prompt configurations for repeatable deployments and rollbacks.            | Configuration Registry + Version Controller                   |
| **Dual-Mode UX Builder**                   | Offers wizard-based no-code mode and expert mode for fine-tuned RAG setup.                              | Visual Builder + Advanced Configurator                        |
| **Evaluation & Feedback Environment**      | Enables testing for retrieval accuracy, response quality and traceability.                              | Evaluation Framework + Analytics Layer                        |
| **Security & Governance Controls**         | Applies role-based access, content safety, PII protection and audit logging.                            | IAM Hooks + Policy Registry + Audit Service                   |

**Edge Labels (on diagram):**

* **Inbound →** Data Sources and Gateway (VS-1)
* **Outbound →** Runtime (VS-2) | Telemetry (VS-5) | Model Registry (VS-4)
* **Feedback ←** Governance and Evaluation (VS-7)

---

## 🔹 **Quadrant 3 – Build vs Buy Strategy (AWS-Inclined Deep Analysis)**

| **Capability Area**                        | **Strategy**                                          | **Rationale / AWS-Aligned Decision Factors**                                            |
| ------------------------------------------ | ----------------------------------------------------- | --------------------------------------------------------------------------------------- |
| **Data Ingestion & Processing Pipeline**   | 🟩 **Buy (Glue / AppFlow)**                           | Managed ETL and connectors reduce ops effort; extend only for custom semantic chunking. |
| **Vector Storage & Retrieval**             | 🟩 **Buy (OpenSearch Serverless or Aurora-pgvector)** | Scalable vector search with enterprise security and native hybrid queries.              |
| **Model Integration Framework**            | 🟩 **Buy (Amazon Bedrock)**                           | Central access to multiple foundation and embedding models under one policy plane.      |
| **RAG Pipeline Orchestration**             | 🟨 **Extend (Step Functions + Custom DAG Layer)**     | Use Step Functions for reliability; overlay a portable DAG spec for cross-cloud use.    |
| **Application Configuration & Versioning** | 🟦 **Build (Core IP)**                                | PromProm-specific registry governs templates, models and version control.               |
| **Dual-Mode UX Builder**                   | 🟦 **Build (Core IP)**                                | User experience is key differentiator; build custom UI on Amplify or native framework.  |
| **Evaluation & Feedback Environment**      | 🟩 **Buy (Bedrock Eval / SageMaker Clarify)**         | Managed evaluation pipeline reduces overhead and provides standardized metrics.         |
| **Security & Governance Controls**         | 🟩 **Buy (Config + IAM + Macie)**                     | Native AWS governance and audit stack meets PromProm’s compliance needs.                |

*(Legend → 🟩 Buy  |  🟦 Build  |  🟨 Extend / Configure)*

---

## 🔹 **Quadrant 4 – Implementation Approach (Tech-Agnostic Execution)**

| **Phase**                                      | **Major Activities**                                                                                       | **Key Deliverable**                                         |
| ---------------------------------------------- | ---------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| **P1 – Foundation Setup**                      | Establish data fabric, identity integration, and baseline security controls.                               | Platform foundation with governance hooks.                  |
| **P2 – Data Preparation & Model Abstraction**  | Build semantic chunking and metadata pipelines; enable model and embedding access via abstraction layer.   | Operational data and model plane.                           |
| **P3 – RAG Pipeline & Configuration Registry** | Implement retrieval and generation workflows; develop central configuration and version registry.          | Unified RAG execution framework.                            |
| **P4 – User Experience Enablement**            | Deliver dual-mode builder UI, template library, and testing interface for citizen developers.              | Self-Service RAG Studio (MVP).                              |
| **P5 – Evaluation & Governance Integration**   | Integrate evaluation feedback loop with policy and governance planes; roll out user training and adoption. | Production-ready RAG platform with governed feedback cycle. |

⏱ **Timeline:** ≈ 22 weeks aligned to RFP deliverables (5.4.7.1 – 5.4.7.5)

---

### ✅ **Key Takeaway**

> **VS-3** builds PromProm’s **self-service RAG ecosystem** — combining data preparation, retrieval, model abstraction and evaluation within a single governed studio.
> AWS is leveraged strategically for managed infrastructure and compliance, while PromProm retains ownership of the UX, configuration logic, and RAG orchestration that differentiate its platform.

---

This version now:

* Keeps **Quadrants 1, 2 and 4** platform-neutral.
* Concentrates **AWS alignment only in Quadrant 3 (Build vs Buy)** for a realistic enterprise delivery posture.
* Maintains exact visual and semantic parity with your VS-2 slide format.

