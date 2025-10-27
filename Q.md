**what we buy vs build**, **how we architect**, and **where we put risk**. I’ve also called out what would change in our logical/component blueprint if the answer goes one way or the other. 

---

### High-impact technical questions (with RFP context → concrete impact → affected components)

| RFP clause & exact context                                                                                                                                          | Clarification question (not business)                                                                                                   | Impact on buy-vs-build & architecture                                                                                                                                      | What changes in our blueprint (logical/component)                                                                                                                        |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **5.1.3 Existing App Infra**: NextJS MFE, FastAPI microservices, OKTA/AD SSO; internal multi-LLM layer (30+ models).                                                | **Should the RAG Builder run as a NextJS micro-frontend inside AskRegn-AI (shared session) or as a standalone SPA behind the Gateway?** | **MFE (embed)** → reuse identity/session; less to build in auth & nav. **Standalone** → more gateway auth flows, CSRF, reverse proxy rules; higher latency risk.           | **User & Experience Plane / RAG Builder**: either *MFE with shared SSO* or *separate app + OAuth/OIDC flow*. **Gateway** adds session propagation/callback routes.       |
| **5.2 (VS-1 Gateway)**: “centralized unified access,” policy, cost, SIEM, real-time PII; 10k+ conc, ≤50 ms overhead; multi-protocol (REST/WS/GraphQL/**MCP**).      | **Do we extend the *existing* enterprise AI Gateway or stand up a dedicated GenAI sub-gateway for RAG/agents?**                         | **Extend** → Hybrid (buy gateway, build policy/metering plugins); minimizes sprawl. **Sub-gateway** → more build but gives tighter latency/caching control for RAG.        | **AI Gateway & Control Plane**: one control plane vs tiered ingress; affects **Token Metering**, **PII Filter**, **Edge cache**, **Splunk/ServiceNow exporters**.        |
| **5.2.1–5.2.3**: Requires **MCP** alongside REST/WS/GraphQL; message normalization; failover, circuit breakers.                                                     | **Is MCP a first-class protocol at ingress (Gateway speaks MCP) or only inside Runtime (Gateway passes through)?**                      | **Ingress MCP** → build/extend gateway adapters & schema validation; bigger surface but cleaner interop. **Runtime-only** → simpler gateway; more work in Agentic Runtime. | **Gateway “Protocol Adapters”** vs **Agentic Runtime MCP Server/Client** placement; moves where we implement **schema validation** and **tool discovery**.               |
| **5.2.4 Security**: Zero-trust, SSO, OAuth/OIDC, immutable audit, Splunk SIEM; encryption at rest/in transit.                                                       | **KMS/HSM location**: PromProm enterprise KMS only, or cloud-managed KMS allowed for embeddings, caches, vector indices?                | **Enterprise KMS** → more build (key routing, envelope encryption) but simpler compliance. **Cloud KMS** → faster, but needs data-residency guardrails.                    | **Security & Compliance Filters**, **Memory & Context Store (Redis/Milvus)**: key-handling code paths; at-rest encryption settings; audit scope in **Governance Plane**. |
| **5.2.4 Security**: PII detection/redaction and masking; immutable audit logs.                                                                                      | **PII masking point**: pipeline **pre-ingest** (before vectorizing) vs **retrieval-time** masking?                                      | **Pre-ingest** → heavier ETL build, safer vectors. **Retrieval-time** → smaller pipeline, more runtime cost & latency controls.                                            | **Data Fabric / Ingestion & Chunking** vs **RAG Orchestration**: moves masking middleware; affects **Prompt/Context Assembler** and **cache reuse**.                     |
| **5.2.1 / 5.2.3**: Caching, edge deployment, 10k+ conc, ≤50 ms gateway overhead, p95 ≤3 s end-to-end.                                                               | **Real-time streaming telemetry (Kafka/NATS) to Splunk, or batch exports acceptable?**                                                  | **Real-time** → build event bus + OTel collectors; better SLOs. **Batch** → simpler, but weaker live ops.                                                                  | **AIOps Telemetry Bus**, **Gateway Meter Service**: add streaming pipeline and cardinality controls if real-time.                                                        |
| **5.4 (VS-3 RAG Builder)**: Dual-mode UX (regular/advanced), vector DB integration, model/embedding abstraction, templates, evaluation, cost tracking.              | **Should we *buy/white-label* a no-code builder if ≥80% fit, or is *custom builder* preferred?**                                        | **Buy** → integration effort, faster time-to-value; limited deep policy hooks. **Build** → full control over guardrails & UX; higher cost/schedule.                        | **RAG Builder UI + Workflow Engine**: either **white-label + governance adapters** or **custom React flow engine + template repo**.                                      |
| **5.4.3 + 5.1.4**: Vector DB abstraction + **Milvus as corporate standard**.                                                                                        | **Treat Milvus as the mandated primary (optimize for it) or build a provider-agnostic vector layer now?**                               | **Milvus-first** → simpler build, better performance tuning. **Abstraction** → more build now, enables Pinecone/FAISS later.                                               | **Data Fabric / Vector Store Adapters**: add **Vector Interface Layer** + driver registry if multi-store.                                                                |
| **5.4.6 Integration**: Deep integration into AskRegn-AI (UX/SSO/patterns); “all model interactions flow through Gateway”; Splunk integration; API-first, versioned. | **API versioning & deprecation** required from MVP-1, or post-MVP?**                                                                    | **From MVP-1** → build version routing, compat shims, deprecation policy; stronger SDLC. **Later** → faster MVP, higher tech debt.                                         | **Gateway / Unified API**, **Registry APIs**: add **semver routing**, **contract tests**, **changelog**.                                                                 |
| **5.5 (VS-4 Model Eng.)**: Central discovery, reuse before build; vendor agents (Oracle/Snowflake/ServiceNow) with their MCPs; registry integration.                | **Registry sync**: read-only discovery or **bi-directional** (publish newly built apps/agents)?                                         | **Read-only** → light adapter. **Bi-dir** → build **publisher**, approvals, lifecycle.                                                                                     | **Model Catalog & Registry Plane**: add **publish flows**, **governance approvals**, **Deprecation handling**.                                                           |
| **5.5.6 Integration**: “All AI service interactions flow through AI Gateway”; conversational discovery in AskRegn-AI.                                               | **Do vendor MCPs get *native bridging* (true protocol) or *wrappers* around vendor APIs?**                                              | **Native bridging** → deeper build in MCP layer; best future-proofing. **Wrappers** → faster now, possible lock-in quirks.                                                 | **Agentic Runtime – Tool Adapters/MCP**: scope of **protocol handlers**, **schema validators**, **tool registry**.                                                       |
| **5.6 (VS-5 AIOps)**: DR, chaos tests, error budgets; ChatOps; auto-remediation agents.                                                                             | **Are chaos tests & DR drills *must-pass gates* pre-go-live?**                                                                          | **Yes** → build chaos tooling, DR runbooks, simulated region failovers; longer Foundations phase. **No** → defer to post-go-live.                                          | **AIOps / DR & Resilience**: adds **ChaosMesh**, **multi-region runbooks**, **SLA attestations**.                                                                        |
| **5.4.7.2 / 5.5.7.8**: Evaluation framework integration; quality metrics; prompt studio; comparison & benchmarking.                                                 | **Reuse existing eval stack (internal) or procure commercial eval suite now?**                                                          | **Reuse** → Hybrid (plugins); **Procure** → Buy subscription, integrate APIs; impacts cost & speed of quality gates.                                                       | **Model Evaluation Lab / Prompt Optimization Studio**: choose framework & build adapters accordingly.                                                                    |
| **5.4.4 Security**: Prompt-injection/content filtering; exfiltration prevention; masking in non-prod; retention.                                                    | **Where to enforce content-safety: Gateway pre-invoke, Runtime post-invoke, or both (layered)?**                                        | **Gateway-only** → simpler, consistent; **Runtime-only** → more context-aware but complex; **Both** → strongest defense, more build.                                       | **Security & Compliance Filters** (+ **Runtime Evaluator Agent**): placement of **policy middlewares** and **reflexion loops**.                                          |

> These answers directly change cost, timeline, performance, and compliance posture. That’s why they’re essential—not “for the sake of asking.”

---

## Gaps & risks we’d miss if we **don’t** ask (requirement & scope check)

1. **Tenancy & isolation model (multi-tenant vs per-project runtimes)**
   *Why it matters:* affects memory persistence boundaries, data leakage risk, cost envelopes.
   *Where in RFP:* implied by platform-wide reuse and governance (§5.2, §5.4, §5.5).
   *Blueprint impact:* **Agentic Runtime Memory**, **RAG Builder namespaces**, **Gateway RBAC**.

2. **Data residency & geo strategy (edge vs region)**
   *Why:* RFP targets edge caching and multi-region DR; residency determines KMS choice and cache policy (§5.2.3, §5.2.4).
   *Impact:* **Gateway Edge Caches**, **Vector store placement**, **KMS routing**.

3. **Throughput SLOs for ingestion/indexing/retrieval**
   *Why:* RFP says “enterprise-scale within acceptable timeframes” (§5.4.7.2); without targets we may under- or over-build.
   *Impact:* **Data Ingestion Workers**, **Milvus sizing**, **cache tiers**.

4. **SDK/extensibility mandate from MVP-1**
   *Why:* RFP stresses API-first and future extensibility (§5.4.6, §5.5); without a decision, we risk rework.
   *Impact:* **Connector SDK**, **MCP Tool SDK**, **Template Library APIs**.

5. **Bi-modal UX governance** (Regular vs Advanced)
   *Why:* RFP requires both modes (§5.4.5). Advanced may allow custom tools—governance differs.
   *Impact:* **RAG Builder Advanced Mode**, **Plugin review workflow**, **policy scopes**.

6. **Immutable audit (WORM) requirement**
   *Why:* §5.2.4 references tamper-proof; if WORM is mandatory, Splunk alone may be insufficient.
   *Impact:* Add **immutable log store** beneath **Governance/Audit**.

7. **Cost attribution granularity**
   *Why:* §5.2 requires per-user/group/project/BU allocation; confirms metering tag schema.
   *Impact:* **Gateway Metering**, **FinOps Module**, **chargeback reports**.

8. **Vendor agent governance path**
   *Why:* §5.5 centers on reuse of vendor agents; need approval and change-control path.
   *Impact:* **Model Catalog/Registry**, **Governance Policy Push**, **Access workflows**.

---

### How to use this, concretely

* Add the table to your **Discovery/Clarifications** annex; these are **decision gates**.
* For each row, record PromProm’s answer → immediately switch the affected component in the slide(s) (I can provide a quick toggle version if you want).

