
# VS1 – AI Gateway & Control Plane

**Needs:** API routing, authN/Z, policy, token/cost metering, audit, dev portal.

* **Unified API Gateway / Router**
  Options: **Amazon API Gateway** (+ CloudFront/WAF), Kong Konnect Cloud, Tyk Cloud
  **Selected: Amazon API Gateway + CloudFront + AWS WAF** — fully managed, global scale, built-in auth & rate limiting, auto-evolving.

* **Identity & Access Manager**
  Options: **AWS IAM Identity Center (SSO)** (federate with Okta/AD), Amazon Cognito (app users), Ping/Okta
  **Selected: IAM Identity Center (federated to Okta/AD) + Cognito for external app users** — enterprise SSO/MFA, managed.

* **Token & Cost Metering (LLM usage)**
  Options: CloudWatch metrics + AWS CUR/Athena; **Helicone Enterprise** (SaaS); OpenMeter Cloud
  **Selected: CloudWatch + AWS CUR (Cost & Usage Report) + Athena dashboards; add Helicone if fine-grained prompt/token analytics needed** — native cost truth + optional COTS.

* **Security & Policy Filters**
  Options: API Gateway/Lambda authorizers; **AWS WAF** (DLP patterns), **Amazon Bedrock Guardrails**; OPA (Styra DAS)
  **Selected: WAF + Bedrock Guardrails + OPA (Styra) for runtime policy** — layered enforcement, all managed.

* **Audit & Event Logging**
  Options: **AWS CloudTrail & CloudWatch Logs → Kinesis Firehose → Splunk Cloud**; ServiceNow Event Mgmt
  **Selected: CloudTrail/CloudWatch with Firehose sink to Splunk** — retains Splunk as SOC system of record.

* **Developer Portal & Self-Service**
  Options: API Gateway Dev Portal (serverless reference), **Kong Konnect Cloud portal**
  **Selected: Kong Konnect Cloud Portal (COTS) fronting API Gateway** — richer, turnkey portal without owning code.

---

# VS2 – Agentic Runtime & Digital Workers

**Needs:** orchestration, MCP hub, memory/context, messaging, security.

* **Agent Orchestration & Runtime**
  Options: **Amazon Bedrock Agents** / **AWS Agent Core**; LangGraph Cloud; CrewAI Cloud
  **Selected: Amazon Bedrock Agents (augment with AWS Agent Core patterns)** — native tool-use, grounding, and RAG; AWS keeps it current.

* **MCP Server & Client Hub**
  Options: OSS MCP servers on **AWS App Runner** / **AWS Fargate (ECS)**; Anthropic MCP tooling
  **Selected: App Runner–hosted MCP servers** — zero-ops containers, autoscale, easy rollouts.

* **Agent Lifecycle Manager**
  Options: Bedrock Agents versions; **SageMaker Projects/Model Registry** for artifacts; AWS CodeCatalyst/CodePipeline
  **Selected: Bedrock Agents versioning + SageMaker Model Registry for shared artifacts** — governed rollout, minimal glue.

* **Memory & Context Store**
  Options: **Amazon ElastiCache for Redis**, DynamoDB for long-term session; vector lives in VS6
  **Selected: ElastiCache (session/short-term) + DynamoDB (long-term state)** — HA, managed.

* **Message Bus / Service Mesh**
  Options: **Amazon EventBridge**, **Amazon MSK (Managed Kafka)**, SQS/SNS
  **Selected: EventBridge (default); MSK only where Kafka protocol is mandatory** — serverless vs. managed Kafka.

* **Security for Agents**
  **Selected:** IAM roles for service accounts, AWS Secrets Manager + KMS, OPA sidecar where policy logic is needed.

---

# VS3 – Self-Service RAG Builder

**Needs:** ingestion/connectors, vector integration, pipeline orchestration, app config, test/eval, governance.

* **Data Ingestion & Connectors**
  Options: **AWS AppFlow** (SaaS→S3 connectors: Salesforce, Slack, ServiceNow, etc.), AWS Glue (ETL), native vendor connectors
  **Selected: AppFlow for SaaS connectors + Glue for transforms** — COTS, scheduled, secure.

* **Vector Store Integration Layer**
  Options: **Amazon OpenSearch Serverless (Vector Engine)**, **Zilliz Cloud (Milvus on AWS)**, Pinecone
  **Selected: OpenSearch Serverless (primary); Zilliz Cloud if Milvus semantics/perf are required** — AWS-native first, managed alternative ready.

* **Model Orchestration / Prompt Flow**
  Options: **Bedrock Prompt management & flows** (prompt templates, knowledge bases), LangSmith/Humanloop
  **Selected: Bedrock prompt templates & knowledge bases** — first-party, evolving rapidly.

* **Application Configuration Manager**
  Options: **AWS AppConfig + AWS Secrets Manager**; LaunchDarkly
  **Selected: AppConfig + Secrets Manager** — managed flags/config + secrets.

* **Dual-Mode UI**
  Options: **AWS Amplify Studio** (low-code) + AWS Amplify Hosting / AppRunner for advanced React
  **Selected: Amplify Studio (wizard) + Amplify Hosting for pro UI** — fast and serverless.

* **Interactive Testing & Evaluation**
  Options: **Bedrock Model Evaluation**, **SageMaker Clarify**; LangSmith (optional)
  **Selected: Bedrock evals + Clarify for bias/explainability** — managed evals with compliance posture.

* **Governance & Security Controls**
  **Selected:** IAM, APIGW scopes/authorizers, Bedrock Guardrails, OPA bundles via AppConfig.

---

# VS4 – Model Engineering & Registry (vertical)

**Needs:** discovery/catalog, lifecycle, evaluation, prompt studio, serving, fine-tuning, cost/risk.

* **AI Discovery & Catalog**
  Options: **Amazon Bedrock Model Catalog**, SageMaker JumpStart
  **Selected: Bedrock Model Catalog (primary)** — vendor/OSS models curated and updated by AWS.

* **Model Lifecycle / Registry**
  Options: **SageMaker Model Registry**, Databricks Model Registry (on AWS)
  **Selected: SageMaker Model Registry (primary) + Databricks Model Registry for Spark/Delta-adjacent work** — both managed.

* **Evaluation & Benchmark Lab**
  **Selected:** Bedrock Model Evaluation + SageMaker Model Monitor metrics + MLflow tracking on Databricks (where used).

* **Prompt Engineering Studio**
  **Selected:** Bedrock prompt templates & knowledge bases; Humanloop (optional) for advanced prompt ops.

* **Deployment & Serving**
  Options: **SageMaker Real-Time Endpoints**, Bedrock Invocations, SageMaker Serverless Inference
  **Selected: SageMaker Endpoints (for custom), Bedrock Invocations (managed vendor models)** — no servers to manage.

* **Training & Fine-Tuning**
  Options: **SageMaker Training Jobs**, Bedrock fine-tuning where supported, Databricks Jobs
  **Selected: SageMaker Training + Bedrock Fine-Tuning** — managed compute, auto-scaling.

* **Cost & Risk Profiler**
  **Selected:** AWS Macie (PII discovery), AWS Security Hub findings, Cost Explorer/CUR + QuickSight dashboard, surfaced in Splunk.

---

# VS5 – Enterprise AIOps / MLOps (vertical)

**Needs:** telemetry/observability, CI/CD, FinOps, self-healing, DR/chaos, lineage.

* **Telemetry & Observability Hub**
  Options: **Amazon CloudWatch**, AWS Distro for OpenTelemetry (ADOT), Amazon Managed Grafana; Splunk ITSI
  **Selected: ADOT → CloudWatch metrics/logs/traces + Managed Grafana (SRE) + Firehose sink to Splunk (SOC)** — unified view, no agents to manage.

* **CI/CD & Release Pipelines**
  Options: **AWS CodePipeline/CodeBuild/CodeDeploy**, GitHub Actions, Jenkins
  **Selected: CodePipeline/CodeBuild (primary) with approvals & OPA checks; keep Jenkins where it already exists**.

* **FinOps Module**
  Options: **AWS Cost Explorer/CUR + Athena/QuickSight**, Apptio Cloudability, CloudZero
  **Selected: CUR + QuickSight (native) + Cloudability if enterprise wants richer showback/optimization**.

* **Self-Healing Ops Agents**
  Options: **ServiceNow AIOps** (keep), Amazon DevOps Guru (ML anomalies), AWS Systems Manager Automation
  **Selected: DevOps Guru + SSM Automation integrated with ServiceNow AIOps** — COTS remediation with ITSM loop.

* **DR & Resilience**
  **Selected:** Multi-AZ + Multi-Region patterns, AWS Route 53 health checks, AWS Fault Injection Service (chaos).

* **Operational Lineage / Runbook Graph**
  Options: **AWS Glue Data Catalog lineage + OpenLineage on MWAA (Airflow)**, Amazon Neptune (optional)
  **Selected: Glue lineage (data) + OpenLineage; Neptune only if explicit KG for ops is requested**.

---

# VS6 – Data & AI Capabilities (horizontal)

**Needs:** virtualization, vector store, metadata/lineage, pipelines, API access.

* **Data Virtualization**
  Options: **Dremio Cloud on AWS**, Denodo Cloud
  **Selected: Dremio Cloud** — existing choice, fully managed.

* **Vector Semantic Store**
  Options: **Amazon OpenSearch Serverless (Vector Engine)**, **Zilliz Cloud (Milvus)**, Aurora PostgreSQL pgvector, Pinecone
  **Selected: OpenSearch Serverless (primary); Zilliz Cloud if Milvus features/perf required** — both managed.

* **Metadata & Lineage Graph**
  Options: **AWS Glue Data Catalog**, **AWS DataZone** (business glossary/data products), Amazon Neptune (KG)
  **Selected: Glue + DataZone (primary)** — native catalog/governance at scale.

* **ETL / Feature Pipelines**
  Options: **AWS Glue**, **AWS Step Functions**, **Databricks on AWS (Delta Live Tables)**, AWS Lambda for mini-jobs
  **Selected: Databricks (where already in use) + Glue for broad ETL; Step Functions for orchestration** — low ops, resilient.

* **API Access & Catalog Services**
  **Selected:** Dremio reflections/APIs fronted by API Gateway; DataZone catalog exposed to builders.

---

# VS7 – Governance, Compliance & AI Literacy (vertical)

**Needs:** policy registry, risk/ethics, audit/reporting, literacy, feedback loop.

* **Policy Registry & Compliance Hub**
  Options: **AWS Lake Formation & DataZone policies**, **AWS Config & Conformance Packs**, **AWS Organizations/Control Tower**, OPA/Styra
  **Selected: DataZone/Lake Formation for data policy + AWS Config/Control Tower for guardrails + Styra DAS (OPA) for app/runtime** — centralized, managed.

* **Ethical Risk Assessment**
  **Selected:** **Amazon Bedrock Guardrails** + **SageMaker Clarify** + **Bedrock Model Evaluation** — safety, bias, red-team style evals.

* **Audit & Report Automation**
  **Selected:** CloudTrail/Config snapshots → **AWS Audit Manager** controls; export to **Splunk Cloud** and **ServiceNow GRC**.

* **AI Literacy & Training Portal**
  Options: Keep **Microsoft Viva Learning + SharePoint** (most enterprises already use); AWS Skill Builder links
  **Selected: Viva/SharePoint (retain)** — zero build, org-standard LMS, with links to AWS modules.

* **Policy Feedback & Enforcement Loop**
  **Selected:** OPA policy bundles in Git → **CodePipeline** gates → API Gateway/WAF/Bedrock Guardrails/Agent configs; evidence stored in Audit Manager.

---

## Cross-cutting standards & patterns (AWS-first)

* **Secrets & Keys:** **AWS Secrets Manager + AWS KMS** (HSM where needed).
* **Networking:** **VPC + PrivateLink**, CloudFront/WAF at edges, ALB/NLB internally.
* **Packaging:** Prefer **AWS App Runner** or **Fargate** for any custom glue; avoid self-managed clusters unless unavoidable.
* **Tracing:** **OpenTelemetry → CloudWatch/X-Ray → Firehose → Splunk**.
* **Compliance evidence:** **AWS Audit Manager** + signed artifacts in S3/Glacier; pipeline gates in **CodePipeline** (OPA checks, security scans, eval results).

---

## Why this stack (with AWS as primary)

* **Integrates with existing:** Dremio, Splunk, ServiceNow, Databricks continue unchanged; native feeds from AWS services are standard.
* **Buy > Build:** Bedrock Agents, API Gateway, AppFlow, OpenSearch Serverless, Glue, SageMaker, DataZone, Audit Manager are **managed** and auto-updated.
* **Future-agile:** AWS evolves Bedrock, Guardrails, Agents, and OpenSearch Serverless; you avoid bespoke maintenance.
* **Switchable where it matters:** Vector (**OpenSearch ↔ Zilliz**), Registry/Serving (**SageMaker ↔ Databricks**), Prompt Ops (**Bedrock ↔ Humanloop**) — minimizes lock-in.

---

If you want, I’ll **condense each box subtitle** on your slide to “Selected: <service>” so you can paste directly into the component view (super terse, exec-ready).
