# 👥 Team Member Assignments — As of 17 Mar 2026

> Compiled from call records (Mar 10–17, 2026) — DSUs, sprint reviews, code reviews, and coordination calls.

---

## 🔵 Leadership & Managers

### Sachin (Tech Lead / Engineering Lead)
- **Role:** Overall technical oversight, code reviews, production incident coordination, architecture decisions
- **Current work:**
  - Production incident coordination (29 GB Composer bucket incident)
  - PR reviews and approvals
  - Audio metadata registration (in progress)
  - SME support for insurance, Razy, SFTP, and discovery
  - Working on control-on-metric code analysis and status history dataflows
  - Raising Lumi API engagement request for fetching table/attributes
  - Reviewing & guiding team on GCP best practices (no unnecessary file IO, temp tables instead of files)
- **Blockers:** Need to connect with Jason on alternate data source for large-file transfers; need Raj to confirm GCP storage quotas

### Sindhuja (Delivery / Scrum Lead)
- **Role:** Sprint planning, story creation, follow-ups, PR approvals, leave tracking
- **Current work:**
  - Following up on pending PR merges with Bhagwan/Saurabh
  - Creating user stories for new validation/use cases
  - Chasing table/data access with Tanisha's team for AFC validation
  - Leave plan management and board audit
  - Coordinating RESI Venue Status DT flow runs with Suman
  - Promoting loyalty status metadata to E3 via RFC
- **Blockers:** Partner availability (Tanisha team) for access calls; Bhagwan not approving PRs quickly

### Anand (Product / Program Manager)
- **Role:** Sprint oversight, story point management, use case prioritization
- **Current work:**
  - Reviewing and approving story point handling (partial completions)
  - Coordinating E2→E3 movements and approvals
  - Finalizing self-serve architecture with Raj
  - Reviewing new validation stories

---

## 🟢 Developers — Active Assignments

### Kundan
| Area | Details |
|---|---|
| **Data Migration** | Completed DQIM data migration (Mar 1–7) and validated in E3 |
| **Dashboard Migration** | PR raised for dashboard migration to E3; targeting deployment by Friday. Hit a missing index issue — reported to channel |
| **Non-interrupt Timer** | Backend build for self-serve (BPMN non-interrupting timer); one phase tested, further testing ongoing |
| **QTrack UI** | E3 dashboard is live; has download error — raised with platform team (Gaurav). CSV download workaround available |
| **Self-Serve Integration** | Started working on QTrack self-serve initiative |
| **Production Issue** | Investigating Airflow production issue; ticket raised and resolved |

### Samir / Sameer
| Area | Details |
|---|---|
| **Quantum Player V3** | Automatic detection of table name + auto-construction of weight/score for CSV model tables. Coding nearly done; fixing BigQuery result iteration issue |
| **DT Flow (RESI)** | Promoted DT flow changes to E3; testing data write to use case folder with full-refresh/overwrite behavior |
| **Connector Automation** | Connector demo done; automation job completed; alerting is live and team is receiving alerts |
| **Contro / Razy Support** | Created DT flow to extract platform project data → insert into loyalty history warehouse table (for Suman/Razy) |
| **Metadata** | Updating metadata after E3 deployment; cross-checking columns/data types |

### Prithvi
| Area | Details |
|---|---|
| **QTrack Automation** | Implementing missing value check (3rd validation type) for QTrack automation |
| **SQL Generation** | Working on single-file consolidation for different check types |
| **Code Refactoring** | Refactoring automation codebase: removing unnecessary credential code, renaming folders (daily_tag → scripts/DAX), aligning to team coding conventions (class-based structure). Due: Monday review with Sachin |
| **Feasibility Check** | Assessing implementation requested by Anand (append functionality) |
| **Blockers:** | Code style concerns raised by Sachin (not class-based); weekend refactoring committed. Office attendance concern flagged by Sindhuja (will regularize from April 1) |

### Anasik / NC / Ansi
| Area | Details |
|---|---|
| **AFC Build** | Completed Excel export with multiple tabs and email attachment functionality |
| **Code Refactoring** | Working on refactoring per Suchin/Sachin's review comments before finalizing PR |
| **YouTube Work** | Confirmed as responsible for YouTube-related tasks |
| **New Validation** | Potentially assigned new AFC/RPA validation use cases |

### Nirmal
| Area | Details |
|---|---|
| **Tag Status Updates** | Assigned to update a status table for tags per diagram |
| **Ingestion Monitor** | Working on injection monitor for RGCUS table (per Sachin's note) |
| **Manual Tag Monitoring** | Capturing manual tag monitoring details while waiting for hydration table |
| **Board Hours** | Must burn down hours on sprint board (shows zero — audit risk) |
| **Blockers:** | Blocked on hydration table details from SRE/platform team; has bandwidth for additional tasks |

### Ayyappa / Appa / IAPA
| Area | Details |
|---|---|
| **DL/Database Changes** | Implemented and tested DB changes for USCF top-10 use cases in E2; deploying to E3 |
| **Consolidated Report** | Built consolidated report running in E2; deploying to E3. Schedule adjusted to 4 PM (16:00) for data completeness |
| **GCS SPOC** | Designated single point of contact for moving files to E3 GCS buckets (post 29 GB incident). Must get approval before any file placement |
| **Production Fix** | Resolved one production issue this week |
| **RPA Review** | Reviewing RPA video/checklist; will note additional checks |
| **Ad-hoc Support** | Supporting Samir with ad-hoc DB change requests |

### Pai
| Area | Details |
|---|---|
| **Production Fix** | Resolved T-shirt Dealer 1 production issue; DAGs now running fine |
| **ICM Consolidated Report** | Working on ICM new day creation for consolidated report; tested in dev with exception scenarios; PR raised, addressing Sachin's review comments |

### Suman
| Area | Details |
|---|---|
| **RESI / Contro** | Working on Contro/Razy — DT flow for loyalty history; created resume/status history data flows in E1 |
| **Event Testing** | Needs to complete event testing for RESI and confirm to Sindhuja for certification |
| **Status History PR** | PR for history table change pending approval (blocked by slow reviewer response — 3–4 days and counting) |
| **Blockers:** | Reviewer taking too long; Sachin suggested creating incident if needed since E3 release is blocked |
| **Capacity:** | May be reassigned to Quantro or new use case depending on progress |

### Athar / Ather
| Area | Details |
|---|---|
| **Front-End Work** | E2 testing completed for assigned tasks; movement to E3 pending approval |
| **Story Points** | Partial story points remain (1 of 3 done); needs to create new story for remaining work or carry to next sprint |
| **Status:** | On personal leave (expecting first child — C-section). Returning Monday. Story point handling to be confirmed with PO |

---

## 🟡 Business / Product Partners

### Rachna
- RPA use case documentation and coordination
- Lead execution for new use cases with Tanisha as SME
- Routing ad-hoc requests from the team
- Coordinating RPA handoff and walkthrough with ANSI

### Tanisha
- Domain/business expertise for use cases (especially AFC access)
- Coordinating with partner manager (Manish) for data access
- **Blocker for team:** Tanisha's availability is blocking AFC table access calls

### Jason
- SFTP file transfer testing (Lumi PRD host connectivity)
- Uploading test files and validating connectivity with RESI team
- Expected to discuss alternate data source (to avoid large E3 file dumps)

### Raj (Platform / Leadership)
- GCP storage quota confirmation
- Evaluating segregating RISI initiative into separate bucket/project
- Self-serve architecture review with Sachin/Anand

---

## 🔴 Key Blockers Summary

| Blocker | Who's Affected | Owner to Resolve |
|---|---|---|
| AFC table/data access not granted | Anasik, validation team | Sindhuja → Tanisha |
| 2 PRs pending Bhagwan's approval | Deployment pipeline | Sindhuja → Bhagwan |
| Hydration table details from SRE | Nirmal (blocked) | SRE/Platform team |
| E3 dashboard download error | Kundan, users | Platform team / Gaurav |
| Slow PR reviewer (Suman's PR) | Suman, E3 release | Create incident if needed |
| GCP storage quota unknown | All (risk of repeat incident) | Raj / Platform team |
| Athar on leave | Front-end stories incomplete | Returns Monday |
