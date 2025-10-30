# 🧩 **F3 – Model Lifecycle Loop (Discovery → Evaluation → Deploy → Reuse)**

*(Strictly reusing component names from your logical view — VS4 + cross-VS5, VS6, VS7 integrations.)*

---

### 🎯 **Purpose**

Show how models flow through the lifecycle — discovery → evaluation → deployment → reuse — using the **same component blocks** as the logical view, only showing data/control flow and inter-VS interactions.

---

## 🔹 **Canvas Specification**

* **Layout:** Landscape 16×9
* **Primary Flow:** Left → Right (Discovery → Evaluation → Deployment → Reuse)
* **Feedback Flow:** Bottom → Top (Monitoring → Governance → Registry updates)
* **Connector Types:**

  * **Blue arrows:** Forward data/control flow
  * **Orange dashed:** Feedback (governance/compliance/telemetry)
  * **Grey solid:** Cross-VS integration
* **Included VSs:**

  * VS4 (core loop)
  * VS5 (observability & CI/CD)
  * VS6 (data tributary)
  * VS7 (governance & feedback)

---

## 🟩 **Functional Blueprint**

| **Zone / Box Title**                                        | **Exact Component (from Logical View)**                                                                   | **What to Write Inside (Function)**                                                                                                                                                                                                                      | **Arrows (→)**                                                                                                                                        |
| ----------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1️⃣ Discovery Stage (Leftmost)**                          | **AI Discovery & Catalog System**                                                                         | • Auto-registers internal, vendor, and agentic models from VS2 & VS3.<br>• Pulls metadata, lineage, & risk class from **Knowledge Graph & Lineage (VS5)** and **Metadata & Lineage Graph (VS6)**.<br>• Exposes search APIs for AskRegn-AI & RAG Builder. | → **Evaluation & Benchmark Lab** *(Label: “Candidate Models & Metadata”)*                                                                             |
| **2️⃣ Evaluation Stage (Next box right)**                   | **Evaluation & Benchmark Lab**                                                                            | • Runs accuracy, latency, cost benchmarks.<br>• Logs metrics to **Telemetry & Observability Hub (VS5)**.<br>• Integrates with **Prompt Engineering Studio** for design/testing.                                                                          | → **Prompt Engineering Studio** *(“Prompt Variants / Eval Scripts”)*<br>→ **Training & Fine-Tuning Infrastructure** *(“Needs improvement → retrain”)* |
| **3️⃣ Prompt Design & Testing (Parallel below Evaluation)** | **Prompt Engineering Studio**                                                                             | • Designs prompt templates, evaluates response quality.<br>• Logs reusable prompt assets into **Model Lifecycle Manager**.<br>• Sends best variants to **Deployment & Serving Framework** for versioned rollouts.                                        | ↔ **Evaluation & Benchmark Lab** *(bi-directional arrow: “Testing Loop”)*                                                                             |
| **4️⃣ Training & Fine-Tuning (Center)**                     | **Training & Fine-Tuning Infrastructure**                                                                 | • Uses datasets from **API Access & Catalog Services (VS6)**.<br>• Runs distributed fine-tune jobs; updates **Model Lifecycle Manager**.<br>• Captures lineage & performance metrics.                                                                    | → **Deployment & Serving Framework** *(“Approved Model Package”)*                                                                                     |
| **5️⃣ Deployment & Serving (Right of center)**              | **Deployment & Serving Framework**                                                                        | • Publishes models to runtime environments (Bedrock, K8s, SageMaker).<br>• Applies **RBAC** and **policy filters** from **Policy Registry & Compliance Hub (VS7)**.<br>• Registers endpoint in **Model Lifecycle Manager**.                              | → **Telemetry & Observability Hub (VS5)** *(“Runtime metrics”)*                                                                                       |
| **6️⃣ Monitoring & Ops Feedback (Below Deployment)**        | **Telemetry & Observability Hub** + **FinOps Module** + **Knowledge Graph & Lineage**                     | • Tracks latency, drift, utilization, and cost.<br>• Sends telemetry to **Audit & Report Automation (VS7)**.<br>• Updates lineage graph for model→data→endpoint links.                                                                                   | → **Governance & Compliance Hub (VS7)** *(Orange arrow: “Policy / Risk Feedback”)*                                                                    |
| **7️⃣ Governance Feedback (Rightmost / Bottom-Right)**      | **Policy Registry & Compliance Hub** + **Audit & Report Automation** + **Ethical Risk Assessment Engine** | • Monitors model risk & compliance status.<br>• Issues policy updates (allow/deny, retrain flags).<br>• Feeds reports to VS1 (Gateway) & VS4 (Registry).                                                                                                 | → **AI Discovery & Catalog System** *(“Update Status / Policy Tags”)*                                                                                 |
| **8️⃣ Reuse & Literacy (Top-Right)**                        | **AI Literacy & Training Portal**                                                                         | • Publishes reusable prompts, tested models, and policies.<br>• Enables users to select pre-approved models via AskRegn-AI.<br>• Closes loop between Registry and end-users.                                                                             | — (Loop back to Discovery for continuous improvement.)                                                                                                |

---

## 🟧 **Cross-Plane (VS) Integrations**

| **From / To**       | **Label on Arrow**                                             |
| ------------------- | -------------------------------------------------------------- |
| **VS6 → VS4**       | “Training & evaluation datasets (via Dremio, Milvus, Purview)” |
| **VS4 → VS5**       | “Telemetry & deployment metrics”                               |
| **VS5 → VS7**       | “Drift alerts, cost anomalies, lineage updates”                |
| **VS7 → VS4**       | “Policy & risk feedback”                                       |
| **VS4 → VS1 / VS3** | “Reusable models & prompt templates”                           |

---

## 🔁 **Flow Summary**

```
[VS6 Data] → AI Discovery & Catalog → Eval & Benchmark ↔ Prompt Engg
       ↓                               ↓
 Training & Fine-Tuning → Deployment & Serving → Telemetry/FinOps
                                          ↓
                                Governance & Compliance
                                          ↓
                              Registry & Literacy (Reuse)
```

---

## ✅ **Traceability Check (RFP → Diagram)**

| **RFP Requirement (5.5.x)**         | **Mapped Component**                             |
| ----------------------------------- | ------------------------------------------------ |
| Discovery of internal/vendor models | AI Discovery & Catalog System                    |
| Model lifecycle management          | Model Lifecycle Manager                          |
| Evaluation & benchmarking           | Evaluation & Benchmark Lab                       |
| Prompt testing & optimization       | Prompt Engineering Studio                        |
| Deployment pipelines                | Deployment & Serving Framework                   |
| Fine-tuning with data sources       | Training & Fine-Tuning Infrastructure (VS6 link) |
| Monitoring & cost governance        | Telemetry Hub, FinOps Module                     |
| Risk & audit compliance             | Policy Registry, Audit & Report Automation       |
| AI reuse & literacy enablement      | AI Literacy & Training Portal                    |

---

Would you like me to now build the **label hierarchy for this blueprint** (like we did for F1 — “Box → Sub-Box → Arrow Label → Integration Note”), so you can directly use it while designing your PowerPoint flow?
