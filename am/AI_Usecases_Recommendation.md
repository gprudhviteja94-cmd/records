# 🧠 Recommended AI Use Cases for the Project

> **Based on analysis of 160+ meeting transcripts (Jan–Jul 2026)** covering all project workstreams. Each use case is mapped to **real work happening today** and shows how AI can improve it.

---

## Project Workstreams Identified

Before recommending AI use cases, here is a summary of the **10 major workstreams** happening across the project:

| # | Workstream | What It Involves |
|---|---|---|
| 1 | **DQ Rule Onboarding & SQL Generation** | Business partners submit rule requests → team manually maps to templates → generates SQL → deploys via Airflow DAGs |
| 2 | **Data Ingestion & Pipeline Management** | SFTP file intake → Cornerstone/Lumi ingestion → pipeline monitoring → incident handling for failures |
| 3 | **Alert & Case Management (Q-Track/ACE)** | DQ alerts raised → triaged as TP/FP → escalated or closed → BPMN workflows route tasks to humans |
| 4 | **Dynamic Thresholding (Quantra/Control)** | Statistical algorithms (Holt-Winters, EWMA, ARIMA) calculate DQ thresholds; 76% false alert suppression |
| 5 | **Self-Serve UI & Portal (Q-Track)** | Web portal for business users to create rules, view alerts, manage DQ checks, approve/reject rules |
| 6 | **Data Migration (Cornerstone → Lumi)** | 340+ tables migrating from on-prem to GCP; DT flow creation, validation, cut-over execution |
| 7 | **BPMN/RPA Workflow Automation (ACE)** | BPMN process design, human task routing, RPA scripts for repetitive portal operations (ACDV disputes, payments) |
| 8 | **Code Review & Deployment (CI/CD)** | PR reviews (bottlenecked to 2 reviewers), RFC approvals, environment promotion E1→E2→E3→Prod |
| 9 | **Reporting & Status Tracking** | Manual status consolidation for leadership, Rally/Jira updates, sprint metrics, PI planning |
| 10 | **Data Matching & Transformation** | Entity matching (RESI↔MX), DT flow transformations, downstream table production |

---

## 🎯 Recommended AI Use Cases

### UC-1: AI-Powered DQ Rule SQL Generator
**Workstream:** DQ Rule Onboarding & SQL Generation

| Aspect | Details |
|---|---|
| **Current Pain** | Team manually maps ~1,600 rules across 5 check types (duplicate, missing, stagnant, threshold, valid value) to 29+ templates. Small variations in SQL (e.g., `feed_key` filters, `CONCAT` usage for multi-variable checks) require manual judgment. Template selection for new rules is non-deterministic without business metadata. |
| **AI Use Case** | An LLM-based agent that takes rule metadata (table, column, check type, filter criteria, schedule) as input, analyzes existing SQL patterns in the repository, and generates production-ready SQL. It handles edge cases like single vs. multi-variable checks, optional `WHERE` clauses, and template selection automatically. |
| **How It Differs From Manual** | Instead of developers spending hours matching rules to templates and handling variations, the AI learns from all 1,600 existing rules and produces SQL in seconds. It also validates generated SQL against the table schema. |
| **Feasibility** | **High** — A POC already exists (VS Code extension by Prithvi using GitHub Copilot's Cloud Haiku, demonstrated Feb 17 and Apr 15). Needs GCP deployment for org-wide adoption. |
| **Priority** | 🔴 **Critical** |

---

### UC-2: Intelligent Alert Triage & Auto-Resolution
**Workstream:** Alert & Case Management (Q-Track/ACE)

| Aspect | Details |
|---|---|
| **Current Pain** | Hundreds of DQ alerts pile up (200+ ICMB alerts, 54+ USC alerts seen in single meeting). Analysts manually classify each as True Positive (TP) or False Positive (FP). Bulk closure is broken due to permission issues. Team closes alerts selectively by date, which is time-consuming. |
| **AI Use Case** | An ML classifier trained on historical alert resolution data that auto-classifies alerts as TP/FP based on: alert type, table, historical resolution patterns, data trends, and Quantra threshold outputs. For high-confidence FP predictions, alerts are auto-closed with audit trail. For uncertain cases, the AI provides a recommendation with confidence score to speed up human decision. |
| **How It Differs From Manual** | Instead of analysts opening each alert and deciding, the system pre-classifies the entire batch. Analysts only review low-confidence or TP items. |
| **Feasibility** | **Medium-High** — Historical resolution data exists in ACE/Q-Track. Quantra already produces threshold signals that can feed the classifier. |
| **Priority** | 🔴 **Critical** |

---

### UC-3: Predictive Pipeline Failure Detection
**Workstream:** Data Ingestion & Pipeline Management

| Aspect | Details |
|---|---|
| **Current Pain** | Pipelines fail due to sequence gaps, SFTP delays, schema mismatches, and file format issues (documented in the Feb 25 insurance E3 incident). Failures are discovered only *after* they happen. A single pipeline failure cascades to 7 other pipelines. Root cause investigation is manual — reading audit logs, tracing timestamps. Team discussed needing "piece of error ownership model" in SOPs. |
| **AI Use Case** | A time-series anomaly detection model monitoring pipeline health signals: ingestion latency, file arrival times, record counts, sequence numbers, and failure rates. The system detects drift patterns (e.g., "latency for table 065 increasing 3x over 48 hours") and sends pre-failure warnings before the pipeline actually breaks. Includes auto-generated root cause summaries when failures do occur. |
| **How It Differs From Manual** | Instead of reacting to incidents, the team receives warnings 30-60 minutes before failures. Root cause analysis that took hours is summarized in seconds. |
| **Feasibility** | **Medium** — Audit logs and task metadata exist in BigQuery. BigQuery ML supports time-series forecasting natively. |
| **Priority** | 🟡 **High** |

---

### UC-4: AI-Suggested DQ Checks from Business Context
**Workstream:** DQ Rule Onboarding + Self-Serve Portal

| Aspect | Details |
|---|---|
| **Current Pain** | When business partners submit a basic check (e.g., null check on column X), the Data Office team manually reviews and suggests additional relevant checks. This requires deep domain knowledge. The Apr 22 meeting explicitly discussed using LLMs to propose "3 nuanced checks" based on business context, metadata, existing checks, and data profiling. |
| **AI Use Case** | Given a new DQ rule request plus business context documents (PDFs, PPTs, Excel), metadata, existing checks on the table, and data profiling results, an LLM generates 3-5 additional recommended checks with: descriptions, expected pass/fail rates, SQL implementations, and rationale. Users can "add to cart" relevant suggestions for approval. |
| **How It Differs From Manual** | Analysts currently spend 30-60 min per request analyzing what other checks might be relevant. The AI does this in seconds and can surface patterns humans might miss across 900+ existing rules. |
| **Feasibility** | **Medium** — POC completed by Acharya/Antarsh using ChatGPT (chat, not API). Blocked by API access policy. Can proceed via Custom GPT or internal Vertex AI when approved. |
| **Priority** | 🟡 **High** |

---

### UC-5: Smart Template Consolidation & Deduplication
**Workstream:** DQ Rule Onboarding & SQL Generation

| Aspect | Details |
|---|---|
| **Current Pain** | Multiple developers over the years have created SQL scripts with slight variations for the same check type. The team found 29 distinct templates for DQ checks, with duplicates differing only in SQL logic (e.g., one uses negation, another uses `CONCAT`). The May 25 meeting focused entirely on trying to manually consolidate templates. CM11 table has many duplicate SQL files. |
| **AI Use Case** | An AI tool that analyzes all existing SQL scripts (1,600+ rules), performs semantic similarity analysis, clusters them into canonical templates, and identifies: (a) scripts that are functionally identical but syntactically different, (b) scripts that can be merged with parameterization, (c) dead/unused scripts. Produces a consolidation report with recommended canonical templates and migration plan. |
| **How It Differs From Manual** | Instead of developers manually reviewing 3-4 SQL files at a time (as assigned in the Jan 28 meeting), the AI scans the entire repository in minutes and produces a complete deduplication map. |
| **Feasibility** | **High** — This is a batch analysis task. Can use embedding models to compute similarity, no real-time API access needed. |
| **Priority** | 🟡 **High** |

---

### UC-6: Anomaly Detection at Record Level (Isolation Forest)
**Workstream:** Dynamic Thresholding (Quantra/Control)

| Aspect | Details |
|---|---|
| **Current Pain** | Current Quantra system only checks aggregate thresholds (mean, count, median). It doesn't detect record-level anomalies — e.g., individual customer records showing out-of-pattern behavior. The Apr 22 meeting discussed using Isolation Forest to identify correlated variables, segment customers into clusters, and surface anomalous clusters. |
| **AI Use Case** | An ML pipeline using Isolation Forest (or similar) that: (1) identifies correlated variables for a given table, (2) segments records into behavioral clusters, (3) surfaces clusters with divergent patterns (e.g., "balance decreasing when normally increasing"), (4) drills down to record-level examples. Business partners review anomalous clusters and can add corresponding checks to the system. |
| **How It Differs From Manual** | Currently, anomalies at the record level go completely undetected. This introduces a new capability that doesn't exist today. |
| **Feasibility** | **Medium** — POC by Charmi already in progress. Isolation Forest runs in BigQuery ML or Python. Data exists in Lumi. |
| **Priority** | 🟡 **High** |

---

### UC-7: Dynamic Algorithm Selection for Thresholding
**Workstream:** Dynamic Thresholding (Quantra/Control)

| Aspect | Details |
|---|---|
| **Current Pain** | Current algorithm selection uses sequential if-else logic to choose between Holt-Winters, EWMA, and ARIMA based on ACF values. This is rigid — the Jun 9 meeting discussed Samir's proposal to dynamically shortlist candidate methods based on data seasonality and characteristics instead of hard-coded rules. Current false alert suppression is at 76%, and true alerts are sometimes being suppressed. |
| **AI Use Case** | An AutoML-style meta-learner that, for each DQID, evaluates multiple statistical/ML methods (ARIMA, EWMA, Holt-Winters, Prophet, plus ML alternatives) on historical data, selects the best-performing method per rule based on backtesting accuracy, and automatically retrains monthly. Includes a feedback loop where analyst TP/FP classifications improve future selections. |
| **How It Differs From Manual** | Instead of a static if-else tree, the system continuously optimizes which algorithm works best for each specific rule, adapting to changing data patterns. |
| **Feasibility** | **Medium** — Existing Quantra infrastructure handles the statistical calculations. Adding a meta-learner on top is incremental. |
| **Priority** | 🟢 **Medium** |

---

### UC-8: AI-Assisted Code Review for PR Bottleneck
**Workstream:** Code Review & Deployment (CI/CD)

| Aspect | Details |
|---|---|
| **Current Pain** | Only 2-3 people (Bhagwan, Saurabh, Raj) can review and merge PRs. PRs are stuck for weeks, blocking deployments and impacting production. The Feb 17 meeting documented a secrets exposure incident. The Jul 10 meeting emphasized peer code reviews. |
| **AI Use Case** | An automated first-pass PR reviewer (GitHub Action or VS Code integration) that checks: SQL injection risks, exposed secrets/passwords, BigQuery cost estimation, coding standards compliance, and XCOM variable cleanup (a specific issue raised Jul 10). Tags PRs as "AI-Approved" or "Needs Human Review" with specific flagged lines. Human reviewers only focus on flagged items. |
| **How It Differs From Manual** | Cuts review time by 60-80%. The 2 authorized reviewers can focus on logic-only review instead of scanning for basic issues. |
| **Feasibility** | **High** — GitHub Copilot Code Review is available. Can augment with team-specific rules. |
| **Priority** | 🟢 **Medium** |

---

### UC-9: Natural Language to SQL for Business Self-Service
**Workstream:** Self-Serve UI & Portal (Q-Track)

| Aspect | Details |
|---|---|
| **Current Pain** | Business partners (Rachna, Tanisha, Anand) constantly ask engineers for data lookups, quarterly reports, fill rate checks, and feasibility assessments. Engineers write BigQuery queries, generate Excel, and email results. This back-and-forth consumes 20-30% of developer time. |
| **AI Use Case** | A "Ask Lumi" interface embedded in the Q-Track portal where business users type questions in natural language: *"How many insurance ingestions failed this week?"* or *"Show fill rate for CM11 table last 6 months."* The system converts the question to a BigQuery SQL query using an LLM with guardrails (no PII exposure, approved datasets only), executes it, and returns formatted tables or charts. |
| **How It Differs From Manual** | Eliminates the engineer-as-middleman pattern entirely. Business users get answers in seconds instead of days. |
| **Feasibility** | **Medium** — Requires LLM API access (currently restricted). Can start with a Custom GPT POC using metadata-only context. |
| **Priority** | 🟢 **Medium** |

---

### UC-10: Intelligent Data Migration Assistant
**Workstream:** Data Migration (Cornerstone → Lumi)

| Aspect | Details |
|---|---|
| **Current Pain** | 340+ tables migrating from Cornerstone to Lumi. Each requires: Hive-to-BigQuery SQL conversion, DT flow creation, DAG configuration, schema validation, metadata synchronization, and downstream dependency checking. Conversion is done manually or via the DT tool's import feature which requires cleanup. Schema mismatches (datatype incompatibilities, string length issues) cause flow failures that require manual debugging. |
| **AI Use Case** | An AI assistant that: (1) auto-converts Hive SQL to optimized BigQuery SQL with schema-aware transformations, (2) identifies potential failure points (datatype mismatches, column length issues) *before* execution, (3) auto-generates DAG config and DT config files from migration metadata, (4) maps downstream dependencies by scanning existing DAGs and ingestion pipelines. |
| **How It Differs From Manual** | Migration prep per table drops from hours to minutes. Schema issues are caught before DT flow execution instead of during debugging. |
| **Feasibility** | **High** — SQL conversion is a well-understood LLM capability. Schema analysis can be rule-based with LLM augmentation. |
| **Priority** | 🟢 **Medium** |

---

### UC-11: AI-Powered Meeting Intelligence & Action Tracker
**Workstream:** Reporting & Status Tracking

| Aspect | Details |
|---|---|
| **Current Pain** | The team generates massive amounts of meeting context (160+ recordings in 6 months). Action items, decisions, and technical details are scattered across transcripts. Status updates to leadership are manually consolidated. Sprint planning requires reviewing past meeting decisions. DSU updates are manually compiled. |
| **AI Use Case** | An AI system that: (1) auto-extracts action items from meeting transcripts and pushes to Rally/Jira, (2) tracks completion status by cross-referencing subsequent meetings, (3) generates weekly leadership status reports from DSU transcripts, (4) provides a searchable knowledge base of past decisions and technical discussions. |
| **How It Differs From Manual** | Eliminates the "who was supposed to do what?" problem. Leadership gets auto-generated reports. Past decisions are instantly searchable instead of lost in transcript files. |
| **Feasibility** | **High** — Meeting transcripts already exist as text files. LLMs excel at extraction and summarization. |
| **Priority** | 🟢 **Medium** |

---

### UC-12: ACDV Dispute Resolution AI Agent
**Workstream:** BPMN/RPA Workflow Automation (ACE)

| Aspect | Details |
|---|---|
| **Current Pain** | ACDV dispute handling involves complex multi-step validation: eligibility checks, account pattern verification, GCBR report construction, Triumph/GAR data retrieval, negative/deletion policy checks, bankruptcy lookups, consumer info verification, and response code computation. Currently automated via RPA but failures require manual intervention. Response code logic involves many conditional branches. |
| **AI Use Case** | An AI agent that augments the existing RPA workflow by: (1) predicting dispute resolution outcomes based on historical patterns (which disputes were TP/FP), (2) auto-generating CLiC notes and closure rationale, (3) handling edge cases (new SCC codes, ambiguous deletion policies) by analyzing similar past resolutions, (4) flagging disputes likely to fail downstream before they enter the pipeline. |
| **How It Differs From Manual** | RPA follows rigid rules. AI handles the ambiguous cases that currently require human judgment or cause business exceptions. |
| **Feasibility** | **Medium-Low** — Requires historical dispute resolution data and careful validation given financial compliance requirements. |
| **Priority** | 🔵 **Lower** |

---

### UC-13: Automated DQ Rule Description Standardization
**Workstream:** DQ Rule Onboarding & SQL Generation

| Aspect | Details |
|---|---|
| **Current Pain** | 1,000+ existing DQ rules have free-text descriptions with no standard format. The team spent multiple meetings (May 25, Jun 2, Jun 4, Jun 9) trying to manually standardize descriptions. Migration to the new template format requires reviewing each rule individually. Rachna estimated 29 templates but descriptions still don't match cleanly. |
| **AI Use Case** | An LLM that reads each existing free-text rule description, maps it to the closest standard template, fills in dynamic parameters (variable names, thresholds, percentages), and produces the standardized description. Outputs a batch migration file (Excel with: DQID, old description, new template description, confidence score) for human review before execution. |
| **How It Differs From Manual** | Instead of manually reviewing 1,000+ rules one-by-one, the AI produces a complete migration file in minutes. Humans only review low-confidence mappings. |
| **Feasibility** | **High** — Text classification + template filling is a straightforward LLM task. Can run as a batch offline job. |
| **Priority** | 🔵 **Lower** (but very quick win) |

---

## 📋 Summary: Priority Matrix

| Priority | Use Case | Effort | Impact | Status |
|---|---|---|---|---|
| 🔴 Critical | **UC-1**: AI SQL Generator | Medium | 🟢 Very High | POC exists |
| 🔴 Critical | **UC-2**: Intelligent Alert Triage | Medium | 🟢 Very High | Historical data available |
| 🟡 High | **UC-3**: Predictive Pipeline Failures | Medium | 🟢 High | Audit data in BigQuery |
| 🟡 High | **UC-4**: AI-Suggested DQ Checks | Medium | 🟢 High | POC exists (ChatGPT) |
| 🟡 High | **UC-5**: Template Consolidation | Low | 🟡 High | Batch analysis, no API needed |
| 🟡 High | **UC-6**: Record-Level Anomaly Detection | Medium | 🟢 High | POC by Charmi in progress |
| 🟢 Medium | **UC-7**: Dynamic Algorithm Selection | Medium | 🟡 Medium | Builds on Quantra |
| 🟢 Medium | **UC-8**: AI Code Review | Low | 🟡 Medium | GitHub Copilot available |
| 🟢 Medium | **UC-9**: NL-to-SQL Self-Service | Medium-High | 🟢 High | Needs API access approval |
| 🟢 Medium | **UC-10**: Migration Assistant | Medium | 🟡 Medium | 340 tables remaining |
| 🟢 Medium | **UC-11**: Meeting Intelligence | Low | 🟡 Medium | Transcripts ready |
| 🔵 Lower | **UC-12**: ACDV Dispute AI | High | 🟡 Medium | Compliance constraints |
| 🔵 Lower | **UC-13**: Description Standardization | Low | 🟡 Medium | Quick batch job |

---

## 🚀 Recommended Implementation Roadmap

### Phase 1: Quick Wins (0-4 weeks)
> Use cases that can be delivered with existing tools/POCs

- **UC-1** — Deploy existing VS Code LLM extension to GCP (POC already built)
- **UC-5** — Run batch SQL similarity analysis (no real-time API needed)
- **UC-13** — Batch description standardization (offline LLM job)
- **UC-8** — Enable GitHub Copilot Code Review on the repo

### Phase 2: Core AI Capabilities (1-3 months)
> Use cases that require model training or new infrastructure

- **UC-2** — Train alert triage classifier on historical TP/FP data
- **UC-3** — Build pipeline health scoring with BigQuery ML time-series
- **UC-6** — Productionize Charmi's Isolation Forest POC
- **UC-7** — Implement AutoML meta-learner for Quantra algorithm selection

### Phase 3: Transformational (3-6 months)
> Use cases requiring API access approval or cross-team coordination

- **UC-4** — AI-suggested checks (needs LLM API approval from Manju/Marcus)
- **UC-9** — Natural language data queries for business users
- **UC-10** — Migration assistant for remaining Cornerstone tables
- **UC-11** — Meeting intelligence platform
- **UC-12** — ACDV dispute resolution agent

---

> [!IMPORTANT]
> **Key Blocker:** Many AI use cases (UC-1, UC-4, UC-9) are blocked by the current restriction on LLM API access. Only ChatGPT chat and Custom GPTs are allowed — no programmatic/API access. Leadership alignment with Manju and Marcus (new VP) is the single most impactful unblock action. The Apr 22 and Jun 1 meetings confirm this is being discussed.

> [!TIP]
> **Biggest Impact with Least Effort:** UC-5 (Template Consolidation) and UC-13 (Description Standardization) can be done immediately as offline batch analysis without any API access — they just need embedding models or even regex-based similarity. These deliver immediate value and build confidence for larger AI initiatives.
