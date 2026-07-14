# 🧠 Recommended AI Use Cases for the Optum Project

> **Source:** Synthesized from analysis of Optum call recordings and design specifications (Dec 2025 – May 2026). This document identifies specialized AI use cases tailored to **ADAS (Agentic Development Assistant System)**, **vulnerability patch orchestration (CPM)**, **RPT spreadsheet comparison workflows**, and **run duplication version management**.

---

## 1. Mapped Project Workstreams

Based on Optum workspace recordings, we have identified **5 core technical workstreams** forming the operational baseline:

1. **ADAS (Agentic Developer Assistant System):** An agentic meta-generator framework designed to scan repositories and dynamically spawn 13-16 specialized developer sub-agents (frontend, backend, testing, DevOps) to generate code in waves based on local memory markdown files (`context.md`, `lessons.md`, `patterns.md`).
2. **RPT (Rules Parameter Tool) Module UI & API Automation:** Multi-tab financial and statistical modules containing complex pages: **RA Output**, **Rates per Quantity**, **Exclusion Summary**, **Detail Stats/Experience Summary** (5-year projections), and **Rate Buildup** (complex grouped/merged layouts).
3. **Spreadsheet & API Data Comparison:** Automating the reconciliation of JSON API exports against Excel "gold standard" sheets on SharePoint. The comparison involves running multi-year macros and outputting mismatch HTML reports.
4. **Vulnerability Remediation / CPM (Critical Patch Management):** Orchestrating security CVE scanning, patching strategies, repository updating, and audit trail compilation.
5. **Run Duplication & Versioning Management:** UI-driven duplication of parameter runs that maps schema values and checks model version compatibility matrices in dropdown fields.

---

## 2. Recommended AI Use Cases

---

### UC-1: Figma-to-Code Autonomous UI Agent (ADAS Extension)
- **Workstream:** ADAS Frontend Agent & Figma Extractor
- **Current Pain:** The team has a script (`figma_extractor.js`) to extract Figma nodes as raw design metadata, but translating that structural JSON into styled React/Vue pages and mapping them to corresponding backend APIs remains a manual coordination step.
- **AI Use Case:** Integrate the Figma Extractor parser into an ADAS Custom Agent. The agent consumes Figma layout coordinates, geometries, and typography metadata, references the repository’s style memory (`context.md`), and automatically codes responsive UI pages. It maps UI inputs to REST clients and database schemas using custom templates.
- **Tech Stack:** Node.js, Model Context Protocol (MCP), Gemini API / Claude Sonnet, Figma Web API.
- **Impact:** Accelerates UI screen and API contract generation from Figma designs, decreasing manual styling and integration effort.
- **Feasibility:** **High** — Parser logic and ADAS wave orchestrator are already active in non-prod.
- **Priority:** 🔴 **Critical**

---

### UC-2: Intelligent Spreadsheet Structure Normalizer
- **Workstream:** RPT Data Comparison & QA Automation
- **Current Pain:** Spreadsheet comparison scripts fail on sheets with complex, non-tabular layouts. The **Rate Buildup** tab features merged cells and grouped columns ("Group" + "Detail" headers), while **Detail Stats** requires running Excel macros for five separate years. Manually formatting these into flat CSVs/Pandas dataframes is a major testing bottleneck.
- **AI Use Case:** An LLM-assisted data prep utility that sits in front of the Pandas comparison script. It reads the Excel structure, automatically resolves grouped headers, unmerges cells while preserving hierarchical indices, normalizes five-year tabs, and outputs clean canonical dataframes for comparison.
- **Tech Stack:** Python (Pandas, OpenPyXL), Vertex AI (structured JSON schema parsing).
- **Impact:** Eliminates the manual spreadsheet cleanup step, enabling instant comparison of complex tabs like Rate Buildup and Detail Stats.
- **Feasibility:** **Medium-High** — Leverages existing Python comparison scripts.
- **Priority:** 🔴 **Critical**

---

### UC-3: Auto-Regression Test Oracle and Diff Analyzer
- **Workstream:** RPT Data Comparison & QA Automation
- **Current Pain:** When data mismatches are found (e.g. 35 mismatches in 20 seconds), QA engineers manually investigate whether the delta is an application regression, a database indexing variance, a minor rounding difference, or an outdated SharePoint Excel template.
- **AI Use Case:** An intelligent test oracle that categorizes mismatches. It analyzes the HTML comparison report and classifies each mismatch (e.g. "Rounding issue: within 0.01% tolerance", "Configuration drift: SharePoint template outdated by 3 days", or "Application Bug: API output null"). It automatically generates a JIRA ticket with root cause details for high-priority failures.
- **Tech Stack:** Python, Pandas, Vertex AI Classifier, JIRA/Rally APIs.
- **Impact:** Speeds up bug identification during regression runs, preventing manual sorting of false positives.
- **Feasibility:** **Medium** — Requires historical classification labels from manual test results.
- **Priority:** 🟡 **High**

---

### UC-4: Cloud-Orchestrated Vulnerability Patch Agent (CPM Consolidation)
- **Workstream:** Vulnerability Remediation / CPM Orchestrator
- **Current Pain:** The local ADAS system lacks the cloud connectivity needed to authenticate, scan Azure databases, run security queries, and patch repositories in production.
- **AI Use Case:** A hybrid orchestrator where the local ADAS client triggers a secure, cloud-hosted CPM agent. The cloud agent queries vulnerabilities (e.g., outdated library dependencies or exposed keys), devises a patching plan, edits the repository, runs verification pipelines, and creates a merge request with a compliance audit log.
- **Tech Stack:** Javascript, Model Context Protocol (MCP), Codex CLI, Azure DevOps APIs, GitHub Actions.
- **Impact:** Automates vulnerability patch management for critical repositories while maintaining compliance rails.
- **Feasibility:** **Medium** — Requires secure cloud integration endpoints and AARB clearance for automated code generation.
- **Priority:** 🟡 **High**

---

### UC-5: Run Schema Mapper & Version Compatibility Classifier
- **Workstream:** Run Duplication & Versioning Management
- **Current Pain:** When duplicating an old run, version upgrades introduce schema changes. Determining whether parameters from a previous run are compatible with the latest model versions is governed by complex, hard-coded backend compatibility matrices.
- **AI Use Case:** An AI classifier that analyzes schema delta structures between different model versions. When duplicating a run, the agent maps old parameter values to new fields, flags data loss risks, suggests defaults for new mandatory fields, and recommends whether to enable or disable specific versions in the UI selection dropdown.
- **Tech Stack:** Python, FastAPI, Vertex AI.
- **Impact:** Eases the run duplication experience when migrating old data to new model versions, reducing run-time execution errors.
- **Feasibility:** **Medium-Low** — Schema mapping is highly deterministic; AI is useful for handling unstructured parameters or complex dependency hierarchies.
- **Priority:** 🟢 **Medium**

---

### UC-6: User Story-to-ADAS Prompt Generator (Product Coach)
- **Workstream:** Product Management & ADAS Requirements Intake
- **Current Pain:** POs write requirements in plain text. If stories lack technical context, database schemas, or validation boundaries, the ADAS developer agents produce hallucinations or incomplete code components.
- **AI Use Case:** An interactive agent integrated with Rally/Jira. It analyzes newly created user stories, compares them to the repository memory files (`context.md`, `patterns.md`), identifies missing technical details, and asks the PO or developer clarifying questions. It then generates the structured prompt needed for the ADAS orchestrator.
- **Tech Stack:** Rally/Jira Webhooks, Gemini API, ADAS config parser.
- **Impact:** Decreases code generation errors by standardizing the technical requirements fed to developer agents.
- **Feasibility:** **High** — Requires no code access; analyzes text requirements and metadata files.
- **Priority:** 🟢 **Medium**

---

## 3. Priority & Feasibility Matrix

| Priority | Use Case | Effort | Impact | Status / Feasibility |
|---|---|---|---|---|
| 🔴 **Critical** | **UC-1**: Figma UI-to-Code Agent | Medium | 🟢 Very High | Uses existing Figma extractor scripts and ADAS framework. |
| 🔴 **Critical** | **UC-2**: Spreadsheet Normalizer | Low-Medium | 🟢 Very High | Plugs into current Pandas scripts; solves the Rate Buildup blocker. |
| 🟡 **High** | **UC-3**: Auto-Regression Test Oracle | Medium | 🟢 High | Speeds up daily QA triage loops. |
| 🟡 **High** | **UC-4**: Cloud CPM Patch Agent | Medium-High | 🟢 High | Crucial for security automation; needs Azure connectivity. |
| 🟢 **Medium** | **UC-5**: Version Compatibility Mapper | Medium | 🟡 Medium | Prevents run duplication runtime errors. |
| 🟢 **Medium** | **UC-6**: Story-to-Prompt Generator | Low-Medium | 🟡 High | Helps coach POs and avoids agent hallucinations. |

---

## 4. Proposed Implementation Roadmap

### Phase 1: Local Automation & Extractor Enhancements (1 - 4 Weeks)
1. **UC-2 (Spreadsheet Normalizer):** Integrate a header-unmerging script into the Pandas comparison tool to automate Rate Buildup testing.
2. **UC-1 (Figma-to-Code):** Plug the figma JSON parsing utility into the ADAS UI developer agent wave.
3. **UC-6 (Story-to-Prompt):** Create a basic markdown template tool to help POs structure acceptance criteria for ADAS.

### Phase 2: QA & Security Triage (1 - 3 Months)
1. **UC-3 (Regression Test Oracle):** Classify mismatches automatically during UAT runs and output RCA reports.
2. **UC-4 (Cloud CPM Patch Agent):** Secure AARB approval for non-prod CPM testing, establishing the Azure connection.
3. **UC-5 (Version Schema Mapper):** Build the compatibility classifier for RPT run duplication version dropdowns.
