# 🧠 Master Catalog: AI and Innovation Proposals

> **Source:** Synthesized from analysis of 160+ meeting transcripts (Jan–Jul 2026), strategic proposals for manager calls, and net-new architectural ideas. This document serves as a unified catalog for pitching and planning AI and automation initiatives.

---

## 1. Project Workstreams Map

Before diving into proposals, here is a summary of the **10 major workstreams** currently active in the project workspace. These form the operational baseline for all recommendations:

| # | Workstream | What It Involves |
|---|---|---|
| 1 | **DQ Rule Onboarding & SQL Generation** | Business partners submit rule requests → team manually maps to templates → generates SQL → deploys via Airflow DAGs. |
| 2 | **Data Ingestion & Pipeline Management** | SFTP file intake → Cornerstone/Lumi ingestion → pipeline monitoring → incident handling for failures. |
| 3 | **Alert & Case Management (Q-Track/ACE)** | DQ alerts raised → triaged as True/False Positives → escalated or closed → BPMN workflows route tasks. |
| 4 | **Dynamic Thresholding (Quantra/Control)** | Statistical algorithms (Holt-Winters, EWMA, ARIMA) calculate DQ thresholds; false alert suppression. |
| 5 | **Self-Serve UI & Portal (Q-Track)** | Web portal for business users to create rules, view alerts, manage DQ checks, and approve/reject rules. |
| 6 | **Data Migration (Cornerstone → Lumi)** | 340+ tables migrating from on-prem to GCP; DT flow creation, validation, and cut-over execution. |
| 7 | **BPMN/RPA Workflow Automation (ACE)** | BPMN process design, human task routing, and RPA scripts for repetitive portal operations (ACDV disputes, payments). |
| 8 | **Code Review & Deployment (CI/CD)** | PR reviews, RFC approvals, and environment promotion E1→E2→E3→Prod. |
| 9 | **Reporting & Status Tracking** | Manual status consolidation for leadership, Rally/Jira updates, sprint metrics, and PI planning. |
| 10 | **Data Matching & Transformation** | Entity matching (RESI↔MX), DT flow transformations, and downstream table production. |

---

## 2. Catalog of Proposals

---

### Category A: Gen AI & Business Enablement

#### Proposal 1: AI-Powered DQ Rule SQL Generator (UC-1 / Call Proposal 1)
- **Workstream:** DQ Rule Onboarding & SQL Generation
- **Problem:** Developers manually map ~1,600 rules across 5 check types to templates. Small SQL variations (filters, concat options) require manual coding. Duplicate SQL files often accumulate for a single table (e.g., CM11).
- **Proposal:** A Gen AI agent that analyzes rule metadata (table, column, check type, filters, schedule) and generates production-ready SQL following template conventions.
- **Tech Stack:** VS Code LLM extension (POC already built by Prithvi using GitHub Copilot's Cloud Haiku) or a GCP-hosted Vertex AI endpoint.
- **Impact:** Reduces SQL generation from hours to seconds, enforces a single-SQL-per-table design pattern, and eliminates duplicates.
- **Priority:** 🔴 **Critical**

#### Proposal 2: Natural Language Data Query Interface / "Ask Lumi" (UC-9 / Innovative Proposal 2)
- **Workstream:** Self-Serve UI & Portal (Q-Track)
- **Problem:** Business partners frequently request ad-hoc data lookups, quarterly reports, and fill-rate checks. Engineers must manually write queries and export files, consuming 20-30% of developer time.
- **Proposal:** An "Ask Lumi" chatbot in the Q-Track portal. Users ask questions in natural language (*"Show fill rate for CM11 table over the last 6 months"*), and an LLM converts the text to a secure BigQuery SQL query, executes it, and returns formatted charts or tables.
- **Tech Stack:** Vertex AI / Gemini API + BigQuery + Lumi governance layer.
- **Impact:** Empowers business users with self-service data retrieval and eliminates engineering bottlenecks.
- **Priority:** 🟢 **Medium**

#### Proposal 3: AI-Suggested DQ Checks from Business Context (UC-4)
- **Workstream:** DQ Rule Onboarding + Self-Serve Portal
- **Problem:** When business partners request basic checks, the Data Office manually reviews requirements to suggest nuanced additional checks. This requires deep domain knowledge and manual analysis.
- **Proposal:** An LLM that ingests business requirements (PDFs, Excel, PPTs) and data profiling statistics to recommend 3-5 additional DQ checks, complete with descriptions, expected pass rates, and draft SQL.
- **Tech Stack:** Vertex AI / ChatGPT API (POC completed by Acharya/Antarsh using ChatGPT UI).
- **Impact:** Automates business logic discovery, improving coverage of complex threshold and stagnant checks.
- **Priority:** 🟡 **High**

#### Proposal 4: Automated DQ Rule Description Standardization (UC-13)
- **Workstream:** DQ Rule Onboarding & SQL Generation
- **Problem:** Over 1,000 existing DQ rules have free-text descriptions with no standard format, complicating the migration to the new template format.
- **Proposal:** A batch LLM job to parse free-text descriptions, map them to standard templates, extract variables/percentages, and generate standardized descriptions.
- **Tech Stack:** Offline batch Python script utilizing Vertex AI or Gemini APIs.
- **Impact:** Standardizes 1,000+ rules in minutes instead of weeks of manual editing.
- **Priority:** 🔵 **Lower** (Quick Win)

#### Proposal 5: AI-Powered Meeting Intelligence & Action Tracker (UC-11 / Call Proposal 6)
- **Workstream:** Reporting & Status Tracking
- **Problem:** Team action items and technical decisions are scattered across hundreds of hours of meeting transcripts. Leadership status reports are manually compiled.
- **Proposal:** An AI assistant that extracts action items from DSU and planning transcripts, pushes them to Jira, and auto-generates weekly leadership status updates.
- **Tech Stack:** Whisper API / Gemini API + Python transcript parsing parser.
- **Impact:** Eliminates manual progress tracking and ensures zero lost actions from calls.
- **Priority:** 🟢 **Medium**

---

### Category B: Ingestion Intelligence & Observability

#### Proposal 6: Intelligent Alert Triage & Auto-Resolution (UC-2)
- **Workstream:** Alert & Case Management (Q-Track/ACE)
- **Problem:** Thousands of data quality alerts pile up. Analysts spend hours manually triaging alerts as True Positives (TP) or False Positives (FP). Bulk closure is frequently constrained by permissions.
- **Proposal:** An ML classifier that evaluates incoming alerts against historical triage logs, tables, and Quantra threshold outputs to auto-classify alerts. High-confidence FPs are closed automatically; TPs are flagged for analysts with a confidence score.
- **Tech Stack:** Python (Scikit-Learn/XGBoost) or BigQuery ML trained on historical ACE/Q-Track databases.
- **Impact:** Suppresses noise, auto-resolves false alerts, and lets analysts focus on real issues.
- **Priority:** 🔴 **Critical**

#### Proposal 7: Predictive Pipeline Health Scoring (UC-3 / Innovative Proposal 3)
- **Workstream:** Data Ingestion & Pipeline Management
- **Problem:** Pipeline failures (sequence gaps, schema drifts, file delays) are detected only after they crash, causing cascade failures downstream.
- **Proposal:** A live health scoring model (0-100) that monitors ingestion latency drifts, data volume anomalies, and upstream dependency status to alert teams *before* failures occur.
- **Tech Stack:** BigQuery ML (time-series forecasting) + Looker dashboard + Cloud Functions.
- **Impact:** Transition from reactive incident management to proactive prevention.
- **Priority:** 🟡 **High**

#### Proposal 8: AI-Powered Root Cause Analysis Engine (Innovative Proposal 1)
- **Workstream:** Data Ingestion & Pipeline Management
- **Problem:** Troubleshooting pipeline failures is a manual process. Engineers spend hours reviewing audit logs, comparing timestamps, and identifying which file caused a gap.
- **Proposal:** An LLM-powered engine that analyzes logs from BigQuery and Airflow on pipeline failure, correlates them with historical incidents, and produces a plain-English root cause summary with remediation steps.
- **Tech Stack:** Vertex AI + BigQuery ML + Log Analytics.
- **Impact:** Cuts Mean Time to Resolution (MTTR) by 50-70%.
- **Priority:** 🟡 **High**

#### Proposal 9: Self-Healing Data Pipelines with Circuit Breaker (Innovative Proposal 6 / Call Proposal 3)
- **Workstream:** Data Ingestion & Pipeline Management
- **Problem:** Intermittent SFTP connection issues, out-of-order files, and database lock failures block pipelines, requiring manual restarts.
- **Proposal:** A self-healing framework utilizing the circuit breaker pattern. Closed state runs normally; Half-Open auto-retries with exponential backoffs; Open isolates the table, generates alerts, quarantines bad files, and auto-replays sequences once healthy.
- **Tech Stack:** Airflow retry policies + Cloud Functions + Pub/Sub.
- **Impact:** Resolves 60-80% of transient network/database issues automatically.
- **Priority:** 🟡 **High**

#### Proposal 10: Dynamic Algorithm Selection for Thresholding (UC-7)
- **Workstream:** Dynamic Thresholding (Quantra/Control)
- **Problem:** Current thresholding selects EWMA, ARIMA, or Holt-Winters using rigid if-else branches based on static ACF values. False alert suppression is capped at 76%.
- **Proposal:** An AutoML meta-learner that backtests multiple models on historical data for each rule, auto-selects the best-performing model, and updates selection dynamically based on analyst feedback.
- **Tech Stack:** Python statistical libraries (Statsmodels, Prophet) + Quantra engine.
- **Impact:** Adapts dynamically to seasonality shifts and increases false alert suppression.
- **Priority:** 🟢 **Medium**

#### Proposal 11: Record-Level Anomaly Detection (UC-6)
- **Workstream:** Dynamic Thresholding (Quantra/Control)
- **Problem:** Quantra checks only aggregated metrics (counts, sums, averages). Individual anomalous records (e.g., specific customer transactions violating trends) bypass checks.
- **Proposal:** An unsupervised ML pipeline (Isolation Forest/clustering) that groups records, flags outliers, and provides drill-downs of anomalous records for analyst review.
- **Tech Stack:** BigQuery ML (Isolation Forest) or Python-based ML operators.
- **Impact:** Introduces new capability to catch record-level data issues before they load downstream.
- **Priority:** 🟡 **High**

#### Proposal 12: GCP Cloud Optimization & Ingestion Enhancements (Call Proposal 4)
- **Workstream:** Data Ingestion & Pipeline Management
- **Problem:** Repeated DataProc cluster creation for separate jobs increases latency and cloud costs. E1 testing relies on manual GCS uploads.
- **Proposal:**
  - **Club DataProc Jobs:** Group multiple PySpark tasks into single cluster runs using dictionary-based state tracking.
  - **Composer CI/CD:** Implement automatic GitHub-to-GCS bucket synchronization for E1 environments.
  - **Compression Utility:** Standardize a Python-based zip-and-SFTP utility to handle large (>1GB) file exports.
- **Tech Stack:** GCP Composer, DataProc, PySpark, GitHub Actions.
- **Impact:** Reduces cloud infrastructure cost, speeds up testing, and prevents deployment errors.
- **Priority:** 🟢 **Medium**

---

### Category C: Development Lifecycle & Governance

#### Proposal 13: AI Code Review Copilot & PR Optimization (UC-8 / Call Proposal 7)
- **Workstream:** Code Review & Deployment (CI/CD)
- **Problem:** Merges are bottlenecked because only 2-3 leads can approve PRs. Basic validation checks (missing variables, un-flushed XCOM variables, credentials) delay code review.
- **Proposal:** An automated PR reviewer checking for SQL injections, secrets exposure, BQ cost estimation, and XCOM cleanup guidelines, tagging issues directly in GitHub before human review.
- **Tech Stack:** GitHub Copilot Code Review / GitHub Actions.
- **Impact:** Clears the PR bottleneck, reduces review turnaround time, and enforces coding hygiene.
- **Priority:** 🔴 **Critical**

#### Proposal 14: Intelligent Change Impact Analyzer (Innovative Proposal 4)
- **Workstream:** Code Review & Deployment (CI/CD)
- **Problem:** Interconnected tables mean SQL changes, DAG configuration adjustments, or rule updates can cause cascade failures downstream.
- **Proposal:** A dependency graph mapping `Rule -> SQL -> DAG/Tag -> Table -> Downstream Consumer`. When code changes are proposed, the system outputs a change impact report to the PR.
- **Tech Stack:** Neo4j / BigQuery Graph + Python codebase parser.
- **Impact:** Minimizes risk of regression bugs and improves reviewer confidence.
- **Priority:** 🟡 **High**

#### Proposal 15: Intelligent Data Migration Assistant (UC-10)
- **Workstream:** Data Migration (Cornerstone → Lumi)
- **Problem:** Migrating 340+ tables requires manual conversion of Hive SQL to BigQuery, schema mapping, and DAG configuration updates. Datatype mismatches cause runtime failures.
- **Proposal:** An AI assistant that auto-translates Hive SQL to optimized BigQuery SQL, predicts datatype mapping issues, and auto-generates DAG and DT configuration files.
- **Tech Stack:** LLM translation models + BigQuery translation API.
- **Impact:** Drastically speeds up table migration and minimizes debugging effort.
- **Priority:** 🟢 **Medium**

#### Proposal 16: ACE Platform Workflow Automation Expansion (Call Proposal 5)
- **Workstream:** BPMN/RPA Workflow Automation (ACE)
- **Problem:** ACE capabilities are underutilized; human task operations are manual and lack automated reminders or escalations.
- **Proposal:**
  - **BPMN Reminders:** Deploy non-interrupting timer boundary events for 1st, 2nd, and 3rd reminders, with auto-escalation pathways.
  - **RPA Integrations:** Use Robot Framework RPA to automate repetitive portal tasks (mainframe logins, SFTP profile status tracking).
  - **RuleAssist Decisioning:** Embed Drools RuleAssist blocks in BPMN/CMMN models to automate business routing logic without code redeployment.
- **Tech Stack:** ACE Studio Composer (BPMN/CMMN), Drools (RuleAssist), Robot Framework.
- **Impact:** Increases automation depth and reduces manual operations workload.
- **Priority:** 🟢 **Medium**

#### Proposal 17: Automated Executive Intelligence Dashboard (Innovative Proposal 7)
- **Workstream:** Reporting & Status Tracking
- **Problem:** Weekly sprint status, pipeline metrics, and incident reports are manually compiled from various sources (Rally, GitHub, BigQuery, Airflow).
- **Proposal:** An automated dashboard pulling sprint velocity (Rally API), PR stats (GitHub API), ingestion failure rates (BigQuery logs), and ticketing details into Looker, sending weekly automated reports.
- **Tech Stack:** Looker Studio + Cloud Scheduler + API integrators.
- **Impact:** Reduces management overhead and provides real-time progress visibility.
- **Priority:** 🟡 **High**

---

## 3. Priority & Feasibility Matrix

| Priority | Proposal | Effort | Impact | Status / Feasibility |
|---|---|---|---|---|
| 🔴 **Critical** | **P-1**: AI SQL Generator | Medium | 🟢 Very High | Working POC exists (VS Code Extension). |
| 🔴 **Critical** | **P-6**: Intelligent Alert Triage | Medium | 🟢 Very High | Feasible; historical ACE/Q-Track data is ready. |
| 🔴 **Critical** | **P-13**: AI Code Review Copilot | Low | 🟡 High | High; GitHub Copilot / custom actions are ready. |
| 🟡 **High** | **P-3**: AI-Suggested DQ Checks | Medium | 🟢 High | Working POC exists (ChatGPT UI). |
| 🟡 **High** | **P-7**: Predictive Pipeline Health | Medium | 🟢 High | Audit data exists in BigQuery. |
| 🟡 **High** | **P-8**: AI Root Cause Analysis | Medium | 🟢 High | Feasible via Vertex AI log integration. |
| 🟡 **High** | **P-9**: Self-Healing Data Pipelines | Medium | 🟢 High | Uses native Airflow and GCP structures. |
| 🟡 **High** | **P-11**: Record-Level Anomalies | Medium | 🟢 High | POC in progress (Isolation Forest by Charmi). |
| 🟡 **High** | **P-14**: Change Impact Analyzer | Medium-High | 🟡 High | Medium; requires parsing of SQL/DAG dependencies. |
| 🟡 **High** | **P-17**: Auto Executive Dashboard | Low-Medium | 🟡 High | Feasible via Looker Studio. |
| 🟢 **Medium** | **P-2**: NL Data Query / Ask Lumi | Medium-High | 🟢 High | High impact, but blocked by LLM API approvals. |
| 🟢 **Medium** | **P-5**: Meeting Intelligence | Low | 🟡 Medium | Feasible; transcript text is readily available. |
| 🟢 **Medium** | **P-10**: Dynamic Algo Selection | Medium | 🟡 Medium | Integrates into Quantra engine. |
| 🟢 **Medium** | **P-12**: GCP Cloud Optimization | Medium | 🟡 Medium | High; refactoring existing Spark/Composer tasks. |
| 🟢 **Medium** | **P-15**: Migration Assistant | Medium | 🟡 Medium | Well-understood SQL translation capability. |
| 🟢 **Medium** | **P-16**: ACE Workflow Expansion | Medium | 🟡 Medium | Standard BPMN/RPA capabilities. |
| 🔵 **Lower** | **P-4**: Description Standardization | Low | 🟡 Medium | Highly feasible offline batch LLM task. |

---

## 4. Implementation Roadmap

### Phase 1: Quick Wins & Immediate Value (0 - 4 Weeks)
*Targeting items that can be deployed offline or with minimal infrastructure/policy changes.*
1. **P-1 (AI SQL Generator):** Deploy the existing VS Code extension to the GCP E1 environment.
2. **P-4 (Description Standardization):** Run the offline batch script to clean up the 1,000+ rules list.
3. **P-13 (AI Code Review Copilot):** Enable GitHub Action checks for SQL injections, secrets, and XCOM cleanup patterns.
4. **P-12 (GCP Cloud Optimization):** Merge parallel DataProc jobs into single-cluster execution steps.

### Phase 2: Core Ingestion Intelligence (1 - 3 Months)
*Targeting model development, monitoring setups, and self-healing configurations.*
1. **P-6 (Intelligent Alert Triage):** Train the classification model on historical Q-Track resolution logs.
2. **P-7 & P-8 (Predictive Ingestion & RCA):** Implement time-series health forecasting and hook Vertex AI to logs.
3. **P-9 (Self-Healing / Circuit Breaker):** Build Pub/Sub queueing and auto-replay Airflow retry logic.
4. **P-11 (Record Anomaly Detection):** Productionize Charmi's Isolation Forest model.

### Phase 3: Transformational Self-Service (3 - 6 Months)
*Targeting API-dependent, cross-team, or highly regulated deployments.*
1. **P-2 (Ask Lumi Interface):** Establish Gemini API gateways and implement Q-Track frontend chat integrations.
2. **P-3 (AI-Suggested Checks):** Deploy Vertex AI context processing to prompt checks from onboarding metadata.
3. **P-14 (Change Impact Analyzer):** Integrate code dependency graphing into PR flows.

---

## 5. Key Recommendations for Management Pitch

1. **Address the API Blocker:** Programs like *Ask Lumi* and *AI-Suggested Checks* require programmatic Gemini API gateway access. Presenting these to leadership (Manju/Marcus) as key business differentiators is the fastest way to get API access approved.
2. **Promote the Existing POCs:** Emphasize that **P-1 (AI SQL Generator)** and **P-11 (Record Anomaly)** are not conceptual—the team already has working prototypes ready for E1 integration.
3. **Focus on Developer Velocity:** Highlight how resolving the PR bottleneck (**P-13**) and automating data migration (**P-15**) directly addresses the team's capacity constraints.
