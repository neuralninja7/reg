# VS1 – AI Gateway & Control Plane

**Needs:** API routing, authN/Z, policy, token/cost metering, audit, dev portal.

* **Unified API Gateway / Router**
  Options: Azure API Management (APIM); Kong Konnect Cloud; Gravitee Cloud
  **Selected: APIM** — native Azure, enterprise policies (masking, rewrite, quotas), SSO, analytics, dev portal.

* **Identity & Access Manager**
  Options: Azure Entra ID (AAD) + Conditional Access; Okta (federated); Ping
  **Selected: Entra ID (federate with Okta if present)** — least-friction SSO, MFA, RBAC; uses tenant policies automatically.

* **Token & Cost Metering (LLM usage)**
  Options: APIM analytics + Azure Monitor; **Helicone Enterprise (SaaS)**; OpenMeter (managed)
  **Selected: APIM + Azure Monitor now; Helicone Enterprise for per-prompt/token granularity** — keeps control-plane native, adds COTS metering where needed.

* **Security & Policy Filters**
  Options: APIM policies + DLP; OPA (Open Policy Agent) with Styra DAS; Azure AI Safety filters (for Azure OpenAI)
  **Selected: APIM policies + OPA (managed by Styra DAS) + Azure AI Safety** — defense-in-depth, all managed.

* **Audit & Event Logging**
  Options: Splunk Cloud; Azure Monitor/Log Analytics; ServiceNow Event Mgmt
  **Selected: Splunk Cloud (system of record) with Azure Monitor forwarders** — reuses existing SOC tooling.

* **Developer Portal & Self-Service**
  Options: APIM Dev Portal; Kong Dev Portal
  **Selected: APIM Dev Portal** — auto-updated, no custom code.

---

# VS2 – Agentic Runtime & Digital Workers

**Needs:** agent lifecycle/orchestration, MCP hub, memory/context, messaging, security.

* **Agent Orchestration & Runtime**
  Options: **Microsoft Agent Framework (Agents & Workflows)**; LangGraph Cloud; CrewAI Cloud
  **Selected: Microsoft Agent Framework** — Azure-native, managed evolution, clean tie-in with Azure AI/Events.

* **MCP Server & Client Hub**
  Options: Open-source MCP servers (containerized); Anthropic MCP toolchain (managed soon in ecosystem)
  **Selected: Containerized OSS MCP servers on **Azure Container Apps** — COTS protocol, no custom infra; auto-scale managed.

* **Agent Lifecycle Manager**
  Options: Azure AI Foundry (projects, deployments); Databricks (Unity Catalog model/func registry)
  **Selected: Azure AI Foundry projects + DevCenter** — versioning, environments, approvals, minimal ops.

* **Memory & Context Store**
  Options: Azure Cache for Redis Enterprise; Redis Cloud (managed); PostgreSQL for long-term session; Vector in VS6
  **Selected: Azure Cache for Redis Enterprise (short-term) + vector in VS6** — managed, highly available.

* **Message Bus / Service Mesh**
  Options: Azure Event Hubs (Kafka-compatible); Azure Service Bus; Dapr sidecars
  **Selected: Azure Event Hubs (Kafka endpoint)** — managed, high-throughput, easy tool integration.

* **Security & Compliance (agent side)**
  Options: Entra ID workload identities; Key Vault; OPA sidecar
  **Selected: Workload identities + Key Vault + OPA** — managed secrets + policy enforcement.

---

# VS3 – Self-Service RAG Builder

**Needs:** ingestion/connectors, vector integration, pipeline orchestration, app config, test/eval, governance.

* **Data Ingestion & Connectors**
  Options: Microsoft Graph/SharePoint connectors; ServiceNow/Confluence/Veeva vendor connectors; Azure Data Factory
  **Selected: Native vendor connectors + **Azure Data Factory** for scheduled pulls** — COTS first, minimal glue.

* **Vector Store Integration Layer**
  Options: **Zilliz Cloud (managed Milvus)**; Azure AI Search (vector); Pinecone
  **Selected: Zilliz Cloud** — preserves Milvus semantics, fully managed; switchable to Azure AI Search if policy mandates all-Azure.

* **Model Orchestration / Prompt Flow**
  Options: Azure AI Studio Prompt Flow; LangChain servers (LangServe Cloud)
  **Selected: Azure AI Prompt Flow** — managed, rapidly evolving, telemetry baked-in.

* **Application Configuration Manager**
  Options: Azure App Config + Key Vault; Feature flags (LaunchDarkly)
  **Selected: Azure App Configuration + Key Vault** — managed, zero custom code.

* **Dual-Mode UI (wizard + power)**
  Options: Power Apps + custom components; Low-code React shell on Static Web Apps
  **Selected: Power Apps for wizard + Static Web Apps for advanced** — quick COTS + controlled pro mode.

* **Interactive Testing & Evaluation**
  Options: Azure AI Studio evals; LangSmith Cloud
  **Selected: Azure AI evals (first-party) + optional LangSmith** — enterprise logging + richer traces if needed.

* **Governance & Security Controls**
  Options: Entra RBAC; APIM scopes; OPA policies; Content Safety
  **Selected: Entra + APIM + OPA + Azure AI Content Safety** — policy managed, no bespoke code.

---

# VS4 – Model Engineering & Registry (vertical pillar)

**Needs:** discovery/catalog, lifecycle, evaluation, prompt studio, serving, fine-tuning, cost/risk.

* **AI Discovery & Catalog**
  Options: Azure AI Model Catalog; Databricks Unity Catalog (models)
  **Selected: Azure AI Model Catalog + Unity Catalog linkage** — covers OSS & vendor models; governance via Purview.

* **Model Lifecycle / Registry**
  Options: Azure ML Registry; Databricks Model Registry (Unity Catalog)
  **Selected: Databricks Model Registry (primary) + Azure ML Registry (interop)** — fits existing Databricks, both managed.

* **Evaluation & Benchmark Lab**
  Options: Azure AI Studio evals; Databricks MLflow evals; LangSmith
  **Selected: Azure AI evals + MLflow metrics on Databricks** — native + standards.

* **Prompt Engineering Studio**
  Options: Azure AI Prompt Flow Studio; Humanloop (SaaS)
  **Selected: Prompt Flow Studio** — no-code tuning, auto-updated by MSFT.

* **Deployment & Serving**
  Options: Azure ML Managed Online Endpoints; Databricks Model Serving; Azure Functions for lightweight tools
  **Selected: Azure ML Endpoints (primary) + Databricks Serving for Spark-adjacent models** — fully managed.

* **Training & Fine-Tuning**
  Options: Azure ML Compute clusters; Databricks Jobs/Delta; Mosaic AI on Databricks
  **Selected: Azure ML Compute (pay-as-you-go) + Databricks Jobs** — vendor-maintained infra.

* **Cost & Risk Profiler**
  Options: Azure Policy + Purview sensitivity + custom dashboards; Calypso/CloudZero (SaaS)
  **Selected: Purview classifications + Azure Cost Mgmt + Splunk dashboard** — COTS + existing SOC view.

---

# VS5 – Enterprise AIOps / MLOps (vertical pillar)

**Needs:** telemetry/observability, CI/CD, FinOps, self-healing, DR/chaos, lineage.

* **Telemetry & Observability Hub**
  Options: Azure Monitor/Log Analytics + Managed Grafana; Splunk ITSI
  **Selected: Azure Monitor + Managed Grafana for SRE; Splunk ITSI as central SIEM/SOAR** — leverages both worlds.

* **CI/CD & Release Pipelines**
  Options: Azure DevOps Pipelines; GitHub Actions; Jenkins (existing)
  **Selected: Azure DevOps Pipelines (primary) with MLflow integration; keep Jenkins where already used** — managed, policy-gated.

* **FinOps Module**
  Options: Azure Cost Management + Anomaly detection; Kubecost (if AKS); Apptio Cloudability
  **Selected: Azure Cost Management (native) + optional Kubecost (if AKS introduced)** — low-ops, vendor-maintained.

* **Self-Healing Ops Agents**
  Options: ServiceNow AIOps; Azure Automation Runbooks; Dynatrace Davis (SaaS)
  **Selected: ServiceNow AIOps + Azure Automation** — COTS remediation tied to ITSM.

* **DR & Resilience**
  Options: Azure paired regions; Azure Chaos Studio
  **Selected: Paired-region failover patterns + Chaos Studio** — managed drills.

* **Knowledge Graph & Operational Lineage**
  Options: Purview + Databricks Unity lineage; Neo4j Aura (for ops runbook graph)
  **Selected: Purview/Unity lineage (primary)** — keeps governance centralized; Neo4j Aura optional if you need ops graph patterns.

---

# VS6 – Data & AI Capabilities (horizontal)

**Needs:** virtualization, vector store, metadata/lineage, pipelines, API access.

* **Data Virtualization**
  Options: **Dremio Cloud**; Denodo Cloud
  **Selected: Dremio Cloud** — your existing choice; cloud-managed.

* **Vector Semantic Store**
  Options: **Zilliz Cloud (Milvus managed)**; Azure AI Search (vector)
  **Selected: Zilliz Cloud** — zero ops, Milvus-native; fall back to Azure AI Search if procurement prefers all-Azure.

* **Metadata & Lineage Graph**
  Options: **Microsoft Purview**; Neo4j Aura
  **Selected: Purview (primary)** — auto lineage from ADF/Databricks/APIM; Neo4j Aura optional for advanced KG.

* **ETL / Feature Pipelines**
  Options: **Databricks on Azure**; Azure Data Factory; Dataiku Cloud
  **Selected: Databricks (Delta Live Tables + Jobs) + ADF for orchestration** — managed and proven.

* **API Access & Catalog Services**
  Options: Dremio reflections + APIM; DataHub OSS (managed)
  **Selected: Dremio + APIM** — consistent gateway experience.

---

# VS7 – Governance, Compliance & AI Literacy (vertical pillar)

**Needs:** policy registry, risk/ethics, audit/reporting, literacy, feedback loop.

* **Policy Registry & Compliance Hub**
  Options: **Microsoft Purview + Azure Policy**; OPA/Styra DAS
  **Selected: Purview + Azure Policy + Styra DAS (OPA)** — data + app + runtime policy centrally managed.

* **Ethical Risk Assessment**
  Options: Azure AI Safety/Evals; Responsible AI Dashboard (RAI)
  **Selected: Azure AI Safety & RAI Dashboard** — first-party, continually upgraded.

* **Audit & Report Automation**
  Options: **Splunk Cloud** + ServiceNow GRC; Purview reports
  **Selected: Splunk + ServiceNow GRC** — enterprise audit trail with existing tools.

* **AI Literacy & Training Portal**
  Options: Microsoft Viva Learning + SharePoint LMS; Seismic/Docebo (SaaS)
  **Selected: Viva Learning + SharePoint portal** — zero code, always current.

* **Policy Feedback & Enforcement Loop**
  Mechanism: APIM policies; OPA bundles; Azure AI content safety configs pushed via pipelines.
  **Selected: Policy bundles in Git (OPA/Purview) → Azure DevOps release gates → APIM/Agent runtime** — audited updates, no bespoke services.

---

## Cross-cutting standards & patterns (apply everywhere)

* **Secrets & Keys:** Azure Key Vault (Managed HSM for high-assurance).
* **Networking:** Azure Private Link + VNets; Front Door / WAF for public edges.
* **Packaging:** Containerize custom glue only; run on Azure Container Apps (managed) rather than AKS unless absolutely needed.
* **Tracing:** OpenTelemetry → Azure Monitor → Splunk forwarder.
* **Evidence:** All pipelines gated in Azure DevOps with **policy checks** (OPA), **RAI evals**, **security scans** before promote.

---

## Why this stack

* **Integrates with existing:** Dremio, Splunk, ServiceNow, Databricks, Purview are first-class here.
* **Buy > Build:** All critical functions are **managed** (APIM, Entra, Prompt Flow, Azure ML/AI, Event Hubs, Zilliz Cloud, Purview, Splunk, ServiceNow).
* **Future-agile:** Vendors (Microsoft, Databricks, Zilliz, Splunk, ServiceNow) push upgrades automatically; you don’t own patch cycles.
* **Switchable:** Vector (Zilliz ↔ Azure AI Search), serving (Azure ML ↔ Databricks), evals (Azure ↔ LangSmith) are **pluggable**—no lock-in beyond standards.

---

If you want, I can drop this **directly into your slide** by rewriting each box’s subtitle with the selected product names (super terse, presentation-ready).
