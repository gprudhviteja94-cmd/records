# 💡 Proposals for Manager Call — 17 Mar 2026

> Based on analysis of **81 call records** (Jan–Mar 2026) covering DSUs, automation demos, training sessions, and strategy discussions.

---

## 🤖 1. Gen AI–Powered SQL & Code Generation (High Impact)

**Problem identified:** The team is manually creating and maintaining hundreds of SQL files per table (e.g., CM11 has many duplicate SQL files). Template mapping is done manually by analyzing ~1,588 DQ rules across 5 check types (stagnant, threshold, valid value, missing, duplicate).

**Proposal:** Build a **Gen AI agent** that automatically generates DQ SQL scripts from rule definitions.

| Aspect | Details |
|---|---|
| **Input** | DQ Repository rule (check type, description, filter criteria, frequency) |
| **Output** | Production-ready SQL file following the team's template patterns |
| **Tech** | VS Code LLM extension (already POC'd by Prithvi using GitHub Copilot's Cloud Haiku) or a GCP-hosted Vertex AI endpoint |
| **Impact** | Reduce SQL generation from **hours → minutes**; eliminate duplicate SQL files; enforce the single-SQL-per-table pattern |

> **IMPORTANT:** A working POC already exists — Prithvi demo'd a VS Code extension that orchestrates multiple AI agents to generate SQL and JSON from rule inputs. Leadership approval (Raj) is pending — this is a ready-to-pitch initiative.

**Quick win:** Deploy the existing LLM extension on an approved GCP environment to unblock org-wide adoption.

---

## ⚙️ 2. Self-Serve Rule Onboarding Automation Pipeline (High Impact)

**Problem identified:** New rules from the UI go through a manual chain: ACE DB → manual SQL creation → manual tag modification → manual Git commit → manual deployment. This pipeline has been discussed since January and is partially built.

**Proposal:** Complete the **end-to-end automation utility** with these enhancements:

1. **Intelligent rule classifier** — Automatically identify check type + frequency + template from the DQ repository entry
2. **SQL consolidator** — Enforce single-SQL-per-table design; merge UNION DISTINCT blocks dynamically
3. **Automated Git commit** — Investigate ADS ID token-based Git automation; if infeasible, build a staging mechanism with one-click approval
4. **Email summary report** — Auto-generate HTML reports after each execution showing records processed, files created, success/failure counts

**Tech stack:** Apache Airflow DAGs + Python on Lumi/GCP Composer

---

## 📊 3. Proactive Data Ingestion Monitoring & Self-Healing (Medium-High Impact)

**Problem identified:** Recurring data ingestion failures (sequence gaps, E3 notification failures, pipeline failures going undetected). The team has been reacting to incidents rather than preventing them.

**Proposal:** Build an **intelligent monitoring & alerting framework:**

| Component | Description |
|---|---|
| **Real-time ingestion validator** | Hourly checks using `created_time` (not `start_time`) with `status = 'FAIL'` filter — fixing the current query logic issues discussed on 3/17 |
| **Sequence gap detector** | Proactively detect out-of-sequence file arrivals before they cause cascade failures (as seen in the Feb 26 incident) |
| **Smart alerting** | One email per failed table (not batch), with audit log error summaries auto-attached; suppress duplicate alerts for retried-and-succeeded jobs |
| **Self-healing hooks** | Auto-retry failed ingestions; auto-create incidents in the ticketing system when retries exhaust |

> **TIP:** Consider adding a Dynatrace integration for real-time pipeline observability.

---

## 🏗️ 4. GCP Cloud Optimization & Infra Improvements (Medium Impact)

**Problem identified:** Multiple DataProc jobs spinning up clusters repeatedly; manual GCS bucket uploads for E1 testing; no GitHub↔Composer sync; compression/SFTP issues with large files.

**Proposals:**

### 4a. Consolidate DataProc Jobs
- Club multiple DataProc jobs into **single jobs** to avoid repeated cluster creation (discussed 3/12)
- Use dictionary-based result storage for multi-sheet Excel generation within one job

### 4b. CI/CD Pipeline for Composer
- Enable **GitHub ↔ GCS Composer bucket sync** for all environments (E1→E3)
- Currently E1 uses manual upload; E2/E3 require pipeline but sync isn't enabled
- This would eliminate the manual upload workflow and prevent deployment errors

### 4c. Intelligent File Compression & Transfer
- Build a reusable **zip-and-SFTP utility** for large file exports (>1GB)
- Test and standardize Python-based compression that mirrors the Cornerstone approach

---

## 🔄 5. ACE Platform Workflow Automation Expansion (Medium Impact)

**Problem identified:** ACE platform capabilities (BPMN, CMMN, RPA, RuleAssist) are underutilized — currently used mainly for rule onboarding but not for broader operational workflows.

**Proposals:**

### 5a. Automated Reminder & Escalation Workflows
- Build BPMN-based **non-interrupting timer workflows** for human task reminders (1st, 2nd, 3rd reminder → auto-close) — already in progress, extend to all approval workflows

### 5b. RPA for Repetitive Portal Operations
- Use **Robot Framework RPA** to automate repetitive web portal tasks (payment processing, data validation on mainframes, SFTP profile management)
- ACE already supports web, mainframe, and desktop RPA

### 5c. Business Rules for Automated Decision-Making
- Leverage **RuleAssist (Drools)** for data validation, eligibility checks, and automated routing decisions without code changes
- Rules can be updated without redeploying processes

---

## 🧠 6. AI-Powered Meeting Intelligence & Knowledge Management (New Idea)

**Problem identified:** The team generates massive amounts of meeting context (81 recordings in 3 months) with action items, decisions, and technical details scattered across transcripts. Status updates to leadership (Raj/Sindhuja/Rajan) are manually consolidated.

**Proposal:** Build an **AI-powered meeting assistant:**

1. **Auto-extract action items** from call transcripts and push to Rally/project tracker
2. **Smart status report generator** — Auto-consolidate weekly team updates from DSU transcripts into leadership-ready reports
3. **Searchable knowledge base** — Index all meeting transcripts for quick retrieval of past decisions, technical details, and patterns

---

## 🔐 7. PR Review Process Optimization (Quick Win)

**Problem identified:** PR merges are blocked for weeks because only Bhagwan and Saurabh review/merge code. This is delaying deployments and impacting production (insurance records failing, dropdown data not persisting).

**Proposal:**
- **Designate merge authority** during IST hours (Syed/Athar with limited merge rights)
- Establish **SLA for PR reviews** (max 1 business day)
- Implement **automated PR checks** (linting, test gates) so human review focuses on logic only

---

## 📋 Summary: Recommended Priority Order

| # | Proposal | Effort | Impact | Quick Win? |
|---|---|---|---|---|
| 1 | Gen AI SQL Generation | Medium | 🟢 High | ✅ POC exists |
| 2 | Self-Serve Automation Pipeline | Medium-High | 🟢 High | Partial |
| 3 | Proactive Ingestion Monitoring | Medium | 🟡 Med-High | Partial |
| 7 | PR Review Process Fix | Low | 🟡 Med-High | ✅ Yes |
| 4 | GCP Cloud Optimization | Medium | 🟡 Medium | Partial |
| 5 | ACE Workflow Expansion | Medium | 🟡 Medium | Partial |
| 6 | AI Meeting Intelligence | Medium | 🟡 Medium | No |

> **Best leads for the call:** Start with **#1 (Gen AI)** and **#7 (PR Process)** — one shows innovation leadership, the other shows process maturity. Both have concrete evidence from team discussions.
