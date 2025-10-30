# VS-4 – Model Engineering, Catalog & Reuse Platform

---

## 🔹 Quadrant 1 – Our Understanding of the Value Stream

**What PromProm is asking for in VS-4**

* Create a **single, authoritative Model / AI Asset Catalog** that can register:

  * internal fine-tuned models,
  * vendor / foundation models (OpenAI, Anthropic, Bedrock),
  * RAG components (retrievers, re-rankers, embed models),
  * and **prompt assets**.
* Make **reuse-before-build** the default: every new VS (VS-2 agents, VS-3 RAG apps) should **discover** and **bind** to an existing registered model/prompt before anyone fine-tunes again.
* Provide a **Model Evaluation & Benchmark Lab** so teams can compare models on accuracy, latency, cost, safety — and store the results next to the model.
* Support a **governed deployment path** — only evaluated / approved models can be pushed to runtime targets (EKS, SageMaker, Bedrock endpoints).
* Link models to **risk & cost classification** (low / medium / high) so the gateway (VS-1) and runtime (VS-2) can enforce policy at call time.
* Everything must be **discoverable conversationally** (your AskRegn-AI / self-service layer can query the registry).

> In short: VS-4 is the **system of record for AI assets** — models, prompts, evals, and their deployment status — so the rest of the platform doesn’t become model-sprawl.

---

## 🔹 Quadrant 2 – Key Solution Tenets (conceptual, not components)

| Tenet / Principle                        | Essence                                                                                             |
| ---------------------------------------- | --------------------------------------------------------------------------------------------------- |
| **1. Centralized AI Asset Discovery**    | One registry for models, embeddings, prompt packs, and RAG building blocks; searchable by metadata. |
| **2. Evaluation-First Model Governance** | No model goes to runtime without eval scores (accuracy, latency, safety) stored in the registry.    |
| **3. Prompt Lifecycle Management**       | Prompts are first-class assets — versioned, ranked, and bound to models/use cases.                  |
| **4. Governed Multi-Target Deployment**  | Push only approved models to AWS targets (SageMaker, Bedrock, EKS) through policy-aware pipelines.  |
| **5. Reuse-Before-Build Policy**         | VS-2 and VS-3 must bind to an existing registered asset before proposing new training/fine-tuning.  |
| **6. Policy-Linked Registry**            | Risk/cost classification is stored with the model so VS-1 gateway can enforce access/cost caps.     |

**Edge labels to show interactions:**

* **Inbound:** “Model / Prompt registration from VS-2 (agents) and VS-3 (RAG builder)”
* **Outbound:** “Model/prompt bindings → VS-2, VS-3” and “Deployable packages → VS-5 (CI/CD)”
* **Feedback:** “Compliance / risk rules ← VS-7”

---

## 🔹 Quadrant 3 – Build vs Buy Strategy (AWS-first, 1 row per component, dense)

| **Component**                                      | **Options (Top COTS / Managed)**                                                                             | **Potential selection & rationale**                                                                                            |
| -------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------ |
| **Model / AI Asset Registry**                      | **Amazon SageMaker Model Registry**, AWS Service Catalog, MLflow Registry (self-managed)                     | **SageMaker Model Registry** — AWS-native, auto-evolving, integrates with pipelines; extend schema for prompts/RAG blocks.     |
| **Evaluation & Benchmark Lab**                     | **SageMaker Clarify**, **SageMaker Model Monitor**, open-source eval harness (EKS)                           | **SageMaker Clarify + custom eval jobs** — managed eval + bias/drift; add OSS harness only for domain metrics.                 |
| **Prompt Management / Prompt Store**               | No native AWS prompt store; **Bedrock Prompt flows** (limited), 3rd-party prompt hubs (PromptHub, Humanloop) | **Lightweight custom prompt store on DynamoDB/S3** — gap in COTS; small, schema-driven, auto-versioned.                        |
| **Governed Deployment (to Bedrock/SageMaker/EKS)** | **SageMaker Pipelines**, **AWS CodePipeline**, **AWS Step Functions**                                        | **SageMaker Pipelines** for MLOps-style deploys; **CodePipeline** to push containers to EKS; both auto-upgrade and AWS-native. |
| **Cost & Risk Profiler (per model)**               | **AWS Cost & Usage + CUR**, tagging via Service Catalog, custom policy service                               | **Custom policy service on Lambda + CUR data** — COTS doesn’t classify models by regulatory risk; small custom fills RFP gap.  |
| **Metadata & Lineage for models**                  | **SageMaker Lineage**, **AWS Glue Data Catalog**, OpenSearch for search                                      | **SageMaker Lineage** — ties artifacts, datasets, and training jobs to registered models; zero infra management.               |
| **Access / Policy over registry**                  | **AWS IAM / Lake Formation / Verified Permissions**                                                          | **Verified Permissions + IAM** — future-proof, auto-updated, policy-as-data; no software upgrades needed.                      |

**Logic applied:**

* AWS is primary → choose SageMaker-native where available.
* Where AWS has no first-class concept (prompts) → build *thin* custom, not a big platform.
* Buy/integrate whenever updates are better handled by provider (SageMaker, Verified Permissions).
* Build only where RFP wants **model-level risk/cost classification**.

---

## 🔹 Quadrant 4 – Implementation Approach

| **Phase**                                    | **What we do**                                                                                                           | **What PromProm gets**                                           |
| -------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------- |
| **P1 – Baseline Registry Enablement**        | Stand up SageMaker Model Registry; define extended schema for prompts, RAG components, eval results.                     | Central AI Catalog (models + prompts) online.                    |
| **P2 – Evaluation & Scoring Pipeline**       | Wire SageMaker Clarify / custom eval jobs; define standard eval templates per use case (summarization, Q&A, extraction). | “Evaluation-first” guard: no model to prod without scores.       |
| **P3 – Prompt Lifecycle & Reuse Hooks**      | Build DynamoDB/S3-based prompt store; link prompts to models and to VS-2/VS-3 consumers.                                 | Reuse-before-build possible for RAG/agents.                      |
| **P4 – Governed Deployments**                | Integrate with SageMaker Pipelines / CodePipeline; add policy checks (Verified Permissions/OPA) before deploy.           | Only approved/rated models can be deployed to AWS runtimes.      |
| **P5 – Integration with Other VS (2,3,5,7)** | Expose registry APIs to VS-2 (agent binding), VS-3 (RAG builder), VS-5 (observability), VS-7 (policy updates).           | Registry becomes the single source of truth across the platform. |

⏱ **Indicative duration:** 16–20 weeks (P1–P3 can be parallelized; P4–P5 gated on policy design from VS-7).

---

### 🧠 Presenter note (optional)

> “VS-4 is deliberately COTS-heavy because the hyperscaler is AWS. We use SageMaker Model Registry + Clarify + Pipelines for 70–80% of the capability and only build small pieces where the RFP asks for things AWS doesn’t yet productize — mainly prompt lifecycle and model-level risk/cost classification.”

This keeps your VS-4 slide consistent with VS-2 but obviously about **models & reuse**, not **runtime & agents**.
