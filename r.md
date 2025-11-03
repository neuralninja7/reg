

# 1) How to think about RL for this RFP (the model)

### Core drivers you’ll size against

* **Use-case load:** initial pilots (2–3) → scale (6–10).
* **Integration count:** data sources (8–15), enterprise apps (4–6), model providers (3–4).
* **Compliance depth:** HITL gates, policy bundles, audit automation (continuous).
* **Environments:** Dev/Test/UAT/Prod with GitOps.
* **Sprints:** 2-week cadence.

### Capacity quick math (for live adjustments)

* **One mature feature pod** ≈ **20–24 story points/sprint**.
* **One dev FTE** contributes ≈ **6–8 points/sprint** (after ceremonies/overhead).
* **FTE needed** ≈ `Total backlog points / (points per sprint * #sprints)`.
* **Backlog proxy** (no time to estimate everything):

  * New service/module = **13–21 pts**;
  * Integration/connector = **8–13 pts**;
  * Compliance gate/report = **5–8 pts**;
  * RAG app template = **13–20 pts**.

---

# 2) Delivery structure (pods & shared “platform spine”)

### Pods (value-stream aligned)

* **Pod-0: Platform Enablement** (Gateway, IAM hooks, developer portal, landing zones).
* **Pod-1: Agentic Runtime** (planner/executor/evaluator, MCP tools, memory, bus).
* **Pod-2: Self-service RAG** (builder wizard/advanced, prompt kits, preview, eval UI).
* **Pod-3: Model Eng & Registry** (catalog, eval lab, deployment handlers).
* **Pod-4: AIOps/FinOps** (observability, SLOs, cost metering, runbooks).
* **Pod-5: Data & AI Fabric** (Dremio, Milvus, lineage graph, ETL hooks).
* **Pod-6: Governance & Literacy** (policies, HITL gates, audit reports, LMS hooks).

### Shared “spine” (cross-cutting)

* **SRE/SecOps crew** (perf, DR, secrets, pen-test fixes).
* **UX & Content** (AskRegn-AI shell, literacy content wiring).
* **QE & Evals** (test harnesses, eval datasets, non-prod data).
* **Program PMO** (RAID, vendor mgmt, finance, change).

---

# 3) Phases & waves (timeline with RL ramp)

> **28 weeks total** (can scale to 36) • 2-week sprints • 60/40 offshore:onshore blend

## Phase 0 – Mobilize (Weeks 1–2)

**Objective:** Foundations, environments, access, skeletons.
**Team (≈ 12 FTE):** PM (1), EA/Lead (1), Platform Eng (3), Sec/Identity (1), DevEx (1), Data Eng (2), SRE (2), QA (1).
**Outcomes:** Dev/Test up, IAM wired, repo & CI/CD, baseline Gateway, VS7 policy draft v0.1.

## Wave 1 – Platform Core MVP (Weeks 3–10, 4 sprints)

**Scope:** VS1 (Gateway), VS2 (Runtime baseline), VS5 (AIOps baseline), VS6 (Data read), VS7 (policies v1).
**Pods active:** Pod-0, Pod-1, Pod-4, Pod-5, Pod-6.
**FTE load (≈ 28–32 FTE):**

* Pod-0: 5 (Lead, 2 Platform, Sec, QA)
* Pod-1: 6 (Lead, 3 Eng, MCP/Tools, QA)
* Pod-4: 5 (Obs 2, FinOps 1, QE 1, SRE 1)
* Pod-5: 6 (Dremio 2, Vector 2, Metadata 1, Data QE 1)
* Pod-6: 4 (Gov lead, Policy Eng, Audit/Reports, LMS/Comms)
* PMO/UX/shared: 4–6

**Milestones:** Gateway live for internal callers; Runtime executes tool-backed tasks; AIOps dashboards v1; RAG can call data via Fabric (read-only); policy v1 in Gateway.

## Wave 2 – Builder + Registry + 2 pilots (Weeks 11–18, 4 sprints)

**Scope:** VS3 (RAG builder), VS4 (Registry/Eval/Deploy), expand VS2 tools, 2 pilot use cases.
**Pods active:** Pod-1, Pod-2, Pod-3, Pod-5, Pod-6 (lighter), Pod-4.
**FTE load (≈ 38–44 FTE):**

* Pod-2: 8 (UX 2, Frontend 2, Orchestration 2, QE 1, Lead 1)
* Pod-3: 7 (Registry 2, Eval 2, Deploy 2, Lead 1)
* Pod-1: 7 (planner/executor upgrades, HITL wiring)
* Pod-5: 6 (more sources, lineage, embeddings pipelines)
* Pod-4: 6 (SLOs, FinOps budgets/alerts, runbooks)
* Pod-6: 3 (policy v2, literacy launch)
* PMO/shared: 3–7

**Milestones:** Builder GA (wizard/advanced), Registry live with eval gates, 2 pilots in UAT, cost guardrails active.

## Wave 3 – Scale-out + Hardening + Handover (Weeks 19–28, 5 sprints)

**Scope:** +4–6 use cases, performance & DR, governance automation, handover.
**Pods active:** All, but **taper** Pod-0 and **boost** Pod-1/2/5/4.
**FTE load (≈ 42–48 FTE peak → taper to 26–30 in last sprint):**

* Pod-1: 9 (multi-agent plans, advanced tools, perf)
* Pod-2: 8 (templates, app catalog, multi-tenant)
* Pod-3: 5 (MLOps tighten, prompt lab ops)
* Pod-4: 8 (self-healing, DR drills, SLO sign-off)
* Pod-5: 7 (source scale-out, feature stores)
* Pod-6: 3 (audit automation, literacy v2, attestation)
* PMO/Shared: 2–8

**Milestones:** 6–8 use cases live, DR validated, audit pack automated, operational handover complete.

---

# 4) Role pyramid per pod (copy to staffing sheet)

**Typical pod (7–9 FTE):**

* 1 Lead/Architect
* 3–4 Engineers (full-stack or platform specific)
* 1 Data/ML or Tooling Specialist
* 1 QA/QE (automation first)
* 1 SRE/DevOps (shared at 0.5–1.0 FTE)
* 0.5–1 UX/Content (RAG & literacy heavy pods)

**Onshore/offshore split:** 40/60 early; shift to 30/70 after Wave-1 once patterns stabilize.

---

# 5) Concrete RL table (weeks × FTE)

| Phase          | Weeks | FTE (range) | Notes                         |
| -------------- | ----: | ----------: | ----------------------------- |
| Mobilize       |   1–2 |          12 | Foundations, access, CI/CD    |
| Wave 1         |  3–10 |       28–32 | Core platform MVP             |
| Wave 2         | 11–18 |       38–44 | Builder + Registry + 2 pilots |
| Wave 3 (ramp)  | 19–24 |       42–48 | Scale-out + hardening         |
| Wave 3 (taper) | 25–28 |       26–30 | Handover, DR, audit close     |

> **Quarter view (FTE-months):** Q1 ≈ 60–64; Q2 ≈ 80–88; Q3 (partial) ≈ 60–70.

---

# 6) RACI (who does what at scale)

* **Architecture decisions:** Enterprise Architect (A), Stream Leads (R), Security & Data Gov (C), PMO (I).
* **Policy bundles & HITL levels:** Governance Lead (A), Compliance (R), Runtime Lead (C), Gateway Lead (C).
* **Model approvals & evals:** Registry Lead (A), Model Owners (R), Evals Team (R), AIOps (C).
* **Cost guardrails:** FinOps (A), Gateway Lead (R), PMO (C), Finance (C).
* **DR drills & SLO sign-off:** SRE Lead (A), AIOps (R), Runtime & Data Leads (C).

---

# 7) Risks that affect RL (translate to buffers—not prose)

* **Environment lag:** keep **2-week shadow sprint** of infra tasks.
* **Data readiness:** stage **synthetic data** and “no-provenance → HITL required” fallback.
* **Provider quotas:** pre-approve **multi-provider routing**; pool keys.
* **Compliance reviews:** book **standing review slots** every sprint-end.

---

# 8) What you’ll put in the staffing XLS (columns)

* Week start date, Phase/Wave, Pod, Role, FTE, Location (On/Off), Start/End, Bill rate band, Comments.
* Calculated fields: **FTE-weeks**, **FTE-months**, **On/Off split**, **Run rate**.
* Tabs: `Master Plan`, `By Pod`, `By Value Stream`, `By Quarter`, `Ramp & Taper`.

---

# 9) Three ready-to-defend scenarios

* **Conservative (cost-tight):** Cap peaks at **36–38 FTE**; reduce pilots to 2 + 3 scaled; push DR to last 2 sprints.
* **Base (recommended):** Plan above (peak **42–48 FTE**, 6–8 scaled use cases).
* **Aggressive (time-to-value):** Start **Pod-2 & Pod-3 in Wave-1**; peak **52–56 FTE**; aim for 10+ use cases by Week-28.

---

# 10) One-liners you can say in orals

* “We load the spine first (Gateway/Runtime/Data/AIOps), then light up RAG and Registry—so every use case rides a common highway.”
* “Peaks sit in the middle eight weeks; we taper into DR and audit automation.”
* “Every pod is replaceable and right-sized; we can shift 15–20% capacity between pods in a sprint without chaos.”
* “Governance is not a phase; it’s staffed from day-1 and closes every loop.”

---


