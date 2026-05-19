Image 8 — REGENERATE-ADAS-PLAN-PART1.md (lines ~239–288)
## Section F. File 5 - dot github slash skills slash generate-project-system.md

268    [partial line] ...This project (real code with file paths); rules (numbered list); Anti-Patterns (what NOT to do). Mark Step 4 completed.

269    Step 5 – Generate Memory Structure at memoryRoot. Create directory and seed files. context.md – empty with header structure tailored to detected domains: frontend gets
       Components, Hooks, Pages, API Endpoints, Design System Usage sections; backend gets Routes, Services, Models, Middleware, Auth; database gets Tables, Migrations, Seeds,
       Relationships; infrastructure gets Services, Configs, Pipelines, Environments. patterns.md – empty with sections Discovered Patterns, Code Patterns, Anti-Patterns.
       lessons.md – empty with Lessons Learned section and rule "promote to skill at >=3 occurrences". decisions.md – empty with Architecture Decision Records section.
       component-usage.md – if frontend detected, empty inventory. Memory protection rule: NEVER overwritten on regenerate; agents append never truncate; exception is context.
       md refreshed by scan-repo-context. Mark Step 5 completed.

271    Step 6 – Generate Documentation at outputRoot. GETTING_STARTED.md – overview, project config table (framework, design system, API client, test framework), how to use
       (start the orchestrator, available agents table with invoke commands, memory system, wave execution). quickReference.md – quick commands for each generated agent.
       AGENT-SKILL-SYSTEM-GUIDE.md – explains how agents, skills, instructions, and memory interact. Mark Step 6 completed.

273    Step 7 – Run Repo Scan. Invoke the repo-context agent (or skill scan-repo-context) to populate memoryRoot slash context.md with the initial inventory. Mark Step 7
       completed.

275    Step 8 – Write Lock File at outputRoot slash adas-lock.md. For every file written in Steps 1–6, record path, size, first 100 characters, SHA-256 hash if available,
       generation timestamp. Format as Markdown table. After Step 8 completes successfully, DELETE the checkpoint file (clean finish).

277    Final Report to user: list of files created, agent count by tier, skill count, instruction count, memory location, suggested next commands (at-orchestrator to start,
       at-NAME for specific agent).

279    ---

281    ## Section G. File 6 - dot github slash skills slash manage-system.md

283    Standard skill disclaimer paragraph. Purpose: Handle all ADAS system management operations after initial generation. Owner: ADAS. Model: Claude Sonnet 4.5.

285    Operations (9 total):

287    Operation 1 – regenerate (full re-generation). Trigger at-adas regenerate. Steps: (1) read adas-config.md and parse YAML frontmatter; (2) version check – if config
       version less than 2.1, offer upgrade-config first, regenerate as-is, or cancel; (3) drift detection – read adas-lock.md, for each file check existence and compare size/
       preview, collect drift list; (4) report drift to user; (5) re-generate by executing generate-project-system.md with existing config (no questions); (6) update lock file;
       and refresh scan.

288    Operation 2 – [partial, cut off]
Image 9 — REGENERATE-ADAS-PLAN-PART1.md (lines ~317–356)
## Section H. File 7 - dot github slash skills slash validate-system.md

337    - V-13: adas-lock.md exists.
338    - V-14: Lock file count matches disk file count (within tolerance of plus or minus 2 for docs).

340    Step 8 – Version and Orchestrator Checks (V-15 to V-17):
341    - V-15: Config version matches current ADAS 2.1; warn if older.
342    - V-16: Orchestrator agent frontmatter lists ALL non-orchestrator agents from roster.
343    - V-17: Each agent file Skills Available section lists exactly the skills config assigns to it.

345    Step 9 – Generate Report. Output structured Markdown: project summary, total checks 17, passed count, failed count, warnings count. Per check show V-NN, status (pass/
       fail/warn), description, failure details if any. Return overall pass/fail.

347    ---

349    ## Section I. Files 8 to 13 – Documentation files under dot github slash

351    dot github slash README.md – Overview of ADAS. Sections: What is ADAS (discovery-driven generator for any project type); Works With Any Project (table mapping Domain to
       Examples: Frontend React Vue Angular Svelte Next Nuxt; Backend API Express FastAPI Spring Boot Django Rails Go Rust; Database PostgreSQL MySQL MongoDB plus Prisma
       SQLAlchemy TypeORM Alembic Flyway; Infrastructure Docker Kubernetes Terraform Ansible GitHub Actions Gitlab CI; CLI Tools Node Click Cobra; Libraries npm PyPI crates;
       Data Pipelines dbt Airflow Spark; Mobile React Native Flutter iOS Android; Monorepos Nx Turborepo Lerna pnpm; Legacy migration JSF AngularJS ASP.NET MVC Django 1 jQuery
       Rails 3 4). Supported Project Intents (Migration, New Development, Enhancement, Infrastructure DevOps). Quick Start (1 add ADAS folder to workspace, 2 run at-adas
       setup, 3 walk through 4 phases, 4 start using agents). How It Works (ASCII diagram showing adas.agent.md → Phase A Discovery → Phase B Roster → Phase C Skills → Phase D
       Generation, with arrows into the target repo github folder). Key Difference from v1 (v1 was template substitution with 65 base files and VARIABLE placeholders for
       frontend only; v2 is AI-composed and discovery-driven supporting any project). Sub-Agent Model (table of domain to sub-agents – same as Section D Step B1). Invocation
       Modes (Setup, Regenerate, Status). Reference Library tree.

352    dot github slash ADAS-MANUAL.md – Quick-Start Manual. Sections: TL;DR in 5 steps (clone or copy ADAS repo into a folder, add ADAS folder and project folder to same VS
       Code workspace, open Copilot Chat pick adas agent and type setup, walk through 4 phases, start using agents). Prerequisites table (VS Code latest, GitHub Copilot Chat
       extension, recommended Claude Sonnet 4.5, workspace with both ADAS folder and project folder). Clone/Workspace Setup. Workspace Structure diagram. Setup
       section with mermaid flow Phase A to D. Phase Details table. First Use (list of generated files: adas-config.md, adas-lock.md, agents/, skills/, instructions/, memory/,
       GETTING_STARTED.md, quickReference.md). Day-to-day workflow examples.

354    dot github slash ADAS-vs-alternatives.md – Short comparison doc. Compare ADAS vs (a) hand-crafting agent files, (b) generic Cursor or Continue rules, (c) v1
       template-substitution approach. Highlight: discovery-driven, focused sub-agents, model tier system, reference library as optional accelerator, supports [cut off]

356    dot github slash Confluence.md – Internal publishing notes placeholder. Sections: Where to publish announcements. Internal SharePoint URLs. Slack channels. Office hours
Create REGENERATE-ADAS-PLAN-PART1.md from all extracted text
Create REGENERATE-ADAS-PLAN-PART1.md from all extracted text

Create REGENERATE-ADAS-PLAN-PART1.md from all extracted text
REGENERATE-ADAS-PLAN-PART1.md
Done


You are out of free messages until 10:50 PM
Upgrade



Claude is AI and can make mistakes. Please double-check responses.



4:43 PM
Here are all 20 images with accurate line numbers extracted from the screen:

Image 9 — REGENERATE-ADAS-PLAN-PART1.md
1    # Regenerate ADAS - Part 1 of 3 – Core Files (OCR-Friendly Spec)
2
3    Goal: Recreate the tsp-adas project anywhere using only this plan plus GitHub Copilot. This file is written as plain English prose so it survives photo-to-text OCR. No
     backticks-heavy code blocks. Read all three parts in order, then hand them to Copilot.
4
5    ADAS (Agentic Developer Assistant System v2.1) is a meta-generator. It does not contain application code. It contains a single bootstrapper agent, six skill files,
     reference templates for known stacks, and documentation. When the user runs at-adas-setup in a target repo, ADAS scans that repo and writes a tailored agent system into
     the target repo dot github folder.
6
7    ---
8
9    ## Section A. Folder Layout to Create
10
11   Create a new empty folder, for example my-adas. Inside it create the following tree.
12
13   Top level files:
14   - dot-vscode slash tasks.json (a minimal stub, see Section J)
15   - generate_docx.py (optional Python script, see Section K)
16
17   Under dot-github slash:
18   - README.md
19   - ADAS-MANUAL.md
20   - ADAS-vs-alternatives.md
21   - Confluence.md
22   - todo.md
23   - agents slash adas.agent.md
24   - skills slash setup-full-team.md
25   - skills slash setup-custom-agent.md
26   - skills slash generate-project-system.md
27   - skills slash manage-system.md
28   - skills slash validate-system.md
29   - skills slash model-tier-rules.md
30   - templates slash generation slash README.md
31   - templates slash generation slash universal slash ...
32   - templates slash generation slash frontend slash ...
33   - templates slash generation slash backend slash agents slash ...
Image 10 — REGENERATE-ADAS-PLAN-PART1.md
1    # Regenerate ADAS - Part 1 of 3 – Core Files (OCR-Friendly Spec)
9    ## Section A. Folder Layout to Create
30   - templates slash generation slash README.md
31   - templates slash generation slash universal slash ...
32   - templates slash generation slash frontend slash ...
33   - templates slash generation slash backend slash agents slash ...
34   - templates slash generation slash database slash agents slash ...
35   - templates slash generation slash infrastructure slash agents slash ...
36
37   The full list of reference template filenames is in Parts 2 and 3.
38
39   ---
40
41   ## Section B. File 1 - dot github slash agents slash adas dot agent dot md
42
43   YAML frontmatter at top:
44   - name: adas
45   - description: Bootstraps a complete Agentic Developer Assistant System in any repository. Scans your project, detects tech stacks across all domains (frontend,
     backend, database, infrastructure, CLI, library, data pipeline, mobile, monorepo), proposes a tailored agent team or creates a single custom agent, with user approval
     at every stage.
46   - model: Claude Sonnet 4.5 (copilot)
47   - target: vscode
48   - user-invokable: true
49   - argument-hint: setup or regenerate or status or resume or validate
50
51   Body sections in order:
52
53   1. Heading: ADAS v2.1 - Agentic Developer Assistant System
54   2. Role: You are the ADAS bootstrapper agent. You analyze any repository, detect its tech stack, and either generate a complete multi-agent development assistant system
     OR create a single purpose-built agent. You do NOT write application code yourself. You generate the agent infrastructure that does.
55   3. Best Used For: First-time setup; re-generating; adding or removing agents, skills, instructions; resuming failed generation; validating consistency; checking status.
56   4. Model Guidance: Recommended Model is Claude Sonnet 4.5 (copilot). Analytical tier. This agent plans, coordinates, and generates; it does not write application code.
57   5. Key References: Schema definitions at adas slash dot github slash templates slash generation slash universal slash docs slash schema-definitions.base.md. Model tier
     rules at adas slash dot github slash skills slash model-tier-rules.md. Generation procedure at adas slash dot github slash skills slash generate-project-system.md.
58   6. Commands table - one row per command:
     - at-adas setup - interactive, branches to setup-full-team.md or setup-custom-agent.md
     - at-adas regenerate - manage-system.md Operation 1
Image 11 — REGENERATE-ADAS-PLAN-PART1.md
1    # Regenerate ADAS - Part 1 of 3 – Core Files (OCR-Friendly Spec)
41   ## Section B. File 1 - dot github slash agents slash adas dot agent dot md
59   - at-adas setup - interactive, branches to setup-full-team.md or setup-custom-agent.md
60   - at-adas regenerate - manage-system.md Operation 1
61   - at-adas regenerate agent NAME - manage-system.md Operation 2
62   - at-adas status - manage-system.md Operation 3
63   - at-adas add skill NAME - manage-system.md Operation 4
64   - at-adas add instruction NAME - manage-system.md Operation 5
65   - at-adas remove agent or skill or instruction NAME - manage-system.md Operation 6
66   - at-adas upgrade-config - manage-system.md Operation 7
67   - at-adas resume - manage-system.md Operation 8
68   - at-adas validate - manage-system.md Operation 9
69   7. Setup Flow: When user says at-adas setup, ask: "What would you like to create? Option 1 Full Agent Team or Option 2 Custom Agent." If Full Team, read and execute
     setup-full-team.md (Step A0 workspace validation, Phase A discovery, Phase B agent roster, Phase C skills and model confirmation, Phase D generation). If Custom Agent,
     read and execute setup-custom-agent.md (CA-0 workspace validation, CA-1 discover context, CA-2 define agent, CA-3 propose and confirm, CA-4 generate).
70
71   ---
72
73   ## Section C. File 2 - dot github slash skills slash model-tier-rules.md
74
75   Top block: standard "What is a Skill" disclaimer paragraph - Skills are step-by-step procedural documentation that agents read and follow. They are NOT callable
     functions.
76
77   Purpose: Define the model tier system and provide deterministic rules for auto-assigning the correct model to each agent based on its role. This is the single source of
     truth for model assignment, referenced by setup-full-team, setup-custom-agent, and generate-project-system.
78
79   Owner: ADAS agent. Model: Claude Sonnet 4.5.
80
82   Schema Reference: See universal slash docs slash schema-definitions.base.md - TierType section.
83
     Tier definitions table:
84   - Tier analytical, model string Claude Sonnet 4.5, frontmatter value "Claude Sonnet 4.5 (copilot)", role: Reads, reasons, plans, coordinates, reviews. Does NOT write
     application code.
85   - Tier coding, model string GPT-5.3-Codex, frontmatter value "GPT-5.3-Codex (copilot)", role: Creates and modifies source code files. Writes components, routes, tests,
     schemas, configs.
86   - Tier hybrid, model string Claude Sonnet 4.5 default, frontmatter value "Claude Sonnet 4.5 (copilot)", role: Mixed responsibilities. User can override
     during Phase C.
Image 12 — REGENERATE-ADAS-PLAN-PART1.md
1    # Regenerate ADAS - Part 1 of 3 – Core Files (OCR-Friendly Spec)
73   ## Section C. File 2 - dot github slash skills slash model-tier-rules.md
86   - Tier hybrid, model string Claude Sonnet 4.5 default, frontmatter value "Claude Sonnet 4.5 (copilot)", role: Mixed responsibilities. User can override to GPT-5.3-Codex
     during Phase C.
87
88   Rule 1 – Match by Agent Name (Exact):
89
90   Analytical agents (by name): orchestrator, batch-manager, review, repo-context, task-planner, upgrade-planner, legacy-analyzer, figma, initiator. Reason in each case:
     planning, coordination, review, scanning, extraction - never writes source code.
91
92   Coding agents (by name): code, api, ui, test-frontend, test, routes, services, middleware, schema, migration, seed, ci-cd, containerization, iac, cli-commands,
     cli-test, screens, navigation, native-bridge, library-core, library-docs, etl, scheduling, data-validation. Reason: creates or modifies source files.
93
     Rule 2 – Match by Role Keywords (Fuzzy): For custom or user-defined agents not in the lists above, scan the agent role description for keywords.
94
95
96   Analytical keywords: coordinate, orchestrate, plan, schedule, manage, review, audit, inspect, validate, verify, analyze, assess, evaluate, scan, detect, extract,
     gather, collect, summarize, propose, recommend, advise.
97
     Coding keywords: implement, create, generate, build, write, modify, edit, update, refactor, transform, code, component, file, module, function, test, spec, fixture,
98   mock, configure, scaffold, template.
99
100  Resolution order: (1) Check Rule 1 exact name match. (2) Check Rule 2 keyword counts. (3) If more analytical keywords assign analytical. (4) If more coding keywords
     assign coding. (5) If tied or no matches assign hybrid and ask user during Phase C.
101
     Rule 3 – User Override: During Phase C present model assignments and accept overrides like "make review coding" or "make custom-docs-agent analytical".
102
103
104  Applying tiers in generated files: In agent frontmatter use model field as "Claude Sonnet 4.5 (copilot)" or "GPT-5.3-Codex (copilot)". In handoffs, the model field MUST
     reference the TARGET agent model, not the caller model. Example: when an analytical agent hands off to a coding agent, the handoff entry uses "GPT-5.3-Codex (copilot)".
105
     Validation Checklist: Every agent has modelTier and model populated. Every handoff model equals target agent model. Analytical agents never write source files. Coding
106  agents never act as orchestrators.
107
108  ---
109
110  ## Section D. File 3 - dot github slash skills slash setup-full-team.md
Image 13 — REGENERATE-ADAS-PLAN-PART1.md
1    # Regenerate ADAS - Part 1 of 3 – Core Files (OCR-Friendly Spec)
349  ## Section I. Files 8 to 13 – Documentation files under dot github slash
356
357  dot github slash Confluence.md – Internal publishing notes placeholder. Sections: Where to publish announcements, Internal SharePoint URLs, Slack channels, Office hours
     schedule. (Generic content, no sensitive info; user customizes.)
358
359  dot github slash todo.md – Roadmap. Sections: Pending (Mobile sub-agent reference templates priority Low, CLI sub-agent reference templates priority Low, Library
     sub-agent reference templates priority Low, Data Pipeline sub-agent reference templates priority Low). Completed (Step A0 workspace validation, Backend sub-agent
     references, Database sub-agent references, Infrastructure sub-agent references, Default sub-agent roster per domain, Dynamic orchestrator wave dispatch).
360
361  dot github slash templates slash generation slash README.md – Reference Library overview. Explains references are NOT requirements (the system works for any stack
     without them); they are structural guidance, quality benchmarks, and accelerators. NOT fill-in-the-blank with VARIABLE substitution (v1 approach is deprecated). When
     references are used (Step 2 of generate-project-system checks for matching reference; if found use as guide; if not compose from scratch). Directory structure tree of
     universal, frontend, backend, database, infrastructure subdirectories. Current Coverage section listing checkmarks for each domain.
362
363  ---
364
365  ## Section J. File 14 - dot vscode slash tasks.json
366
367  Minimal stub. JSON content: version 2.0.0, tasks empty array, or one optional task "Generate ADAS docx" that runs python generate_docx.py. Not critical to ADAS function.
368
369  ---
370
371  ## Section K. File 15 - generate_docx.py (optional)
372
373  Standalone Python script using python-docx library. Purpose: convert dot github slash ADAS-Blog.md to docx for distribution. Implementation: read markdown file, parse
     headers and paragraphs and tables, write a docx document via python-docx Document class with styled headings, tables, and code blocks. Not required for ADAS to function.
374
375  ---
376
377  ## Section L. Authoring Rules for All Files
378
379  Rule 1: NO use of double-curly-brace VARIABLE substitution placeholders in the output. ADAS v2 is AI-composed; reference templates use illustrative content not
380  placeholders.
381
     Rule 2: Every dot agent dot md file MUST have valid YAML frontmatter between two lines of three dashes. Required fields: name, description, model, target (vscode), and
Image 19 — REGENERATE-ADAS-PLAN-PART1.md
1    # Regenerate ADAS - Part 1 of 3 – Core Files (OCR-Friendly Spec)
110  ## Section D. File 3 - dot github slash skills slash setup-full-team.md
156  - Data Pipeline: etl (coding), scheduling (coding), data-validation (coding).
157  - Legacy migration: legacy-analyzer (analytical).
158
159  Conditional agents: repo-context (when multiple domains, analytical), task-planner (when more than 5 work items, analytical), batch-manager (migration projects,
     analytical), upgrade-planner (Enhancement or Version Upgrade intent, analytical).
160
161  Auto-assign tier for each via model-tier-rules.md.
162
163  Step B2 - Present Agent Roster. Group by domain, show tier and resolved model for each agent. Offer options: remove agents not needed, add custom agents, override model
     assignments, rename, proceed.
164
165  Step B3 - Handle User Edits. Remove, add, override model, or rename agents per user request. Re-present until user confirms.
166
167  PHASE C - Skills, Instructions and Model Confirmation.
168
169  Step C1 - Build Skills Proposal. Skills are distributed across sub-agents by concern. Each skill has exactly one owner.
170
171  Universal skills (always proposed): scan-repo-context (owner repo-context, used by orchestrator), read-memory (built-in, all agents), write-memory (built-in, all
172  agents).
173
     Frontend sub-agent skills:
174  - code owns create-component, create-hook or create-composable or create-service depending on framework, add-ui-pattern, component-reuse-check.
175  - api owns add-api-endpoint.
176  - test-frontend owns create-test-file, create-mock.
177  - figma owns fetch-figma-design, fetch-figma-comments.
178  - ui is a CONSUMER of create-component, add-ui-pattern, component-reuse-check; it invokes them by handing off to code.
179
180  Backend API sub-agent skills:
181  - routes owns create-route, add-api-endpoint.
182  - services owns create-service.
183  - middleware owns create-middleware.
184
185  Database sub-agent skills:
186  - schema owns create-model.
187  - migration owns create-migration.
Image 20 — REGENERATE-ADAS-PLAN-PART1.md
1    # Regenerate ADAS - Part 1 of 3 – Core Files (OCR-Friendly Spec)
209  ## Section E. File 4 - dot github slash skills slash setup-custom-agent.md
216  Phase CA-0 - Validate Workspace (Prerequisites): Same as Setup Full Team Step A0.
217
218  Phase CA-1 - Discover Context.
219  - Step 1: Look for outputRoot slash adas-config.md. If found, parse YAML frontmatter to extract project profile, existing agents, skills, model tiers, memory paths. Set
     hasExistingSystem true. Version check: if config version less than 2.1, warn user and offer (1) upgrade config to 2.1 first via at-adas upgrade-config, (2) proceed
     anyway, (3) cancel. If not found, set hasExistingSystem false and perform lightweight repo scan.
220  - Step 2: Inventory existing agents. Scan outputRoot slash agents for all dot agent dot md files. Parse frontmatter of each to extract name, description, model,
     handoffs, agents. Build a map. Scan skills and instructions similarly.
221  - Step 3: Report findings to user. If existing system: show project name, intent, domains, output root, list of agents with tier and role, count of skills, memory
     active status. If no existing system: show detected languages and frameworks, note no ADAS system found, will create standalone.
222
223  Phase CA-2 - Define the Agent.
224  - Step 1: Ask user in a single conversational prompt to describe the agent freely. Give examples like "documentation agent that generates JSDoc and README files" or
     "security scanner that checks for common vulnerabilities" or "performance agent that analyzes bundle size".
225  - Step 2: Derive agent specification - name (kebab-case from role), role (detailed from user input), domain (match existing or assign universal), modelTier via Rule 1
     then Rule 2, model resolved from tier, conditional if context-triggered.
226  - Step 3: Derive 1 to 5 required skills. Check existing skills first (mark as reuse). For new skills define name, purpose, owner (the new agent by default), usedBy.
     Heuristics: "create/generate/build X" yields create-X; "analyze/scan/check X" yields analyze-X or scan-X; "validate/verify X" yields validate-X; fetching external data
     yields fetch-SOURCE.
227  - Step 4: Derive 0 to 3 instructions. Check existing first. Only propose new if introducing a genuine new pattern.
228  - Step 5: Derive handoff relationships. Rules: new agent always hands off to review if review exists. Same-domain peers get bidirectional handoffs. Orchestrator
     dispatches to new agent (add to appropriate wave). Cross-domain dependencies as needed.
229
230  Phase CA-3 - Propose and Confirm. Present full proposal: agent name, role, model, domain, activation; table of skills with New or Reuse status; table of instructions;
     list of files to create (new agent md, new skill md files, new instruction md files); files to update (orchestrator agent md, adas-config.md, adas-lock.md,
     GETTING_STARTED md, quickReference md). Wait for confirmation. Handle edits.
231
232  Phase CA-4 - Generate.
233  - Step 1: Generate the agent file using same approach as generate-project-system Step 2. Check for matching reference template, use as structural guide if exists, else
     compose from scratch. Include Model section explaining tier. Include Skills Available table with Owner or Consumer designation.
234  - Step 2: Generate new skills using same approach as generate-project-system Step 3. Include Owner and Consumers. Scan repo for real examples to inform the procedure.
235  - Step 3: Generate new instructions using generate-project-system Step 4 approach. Scan repo for real examples of the pattern.
236  - Step 4: Update existing files atomically: orchestrator agent md (add new agent to agents frontmatter list and to appropriate wave based on domain), adas-config.md
     (add to roster and skills tables), adas-lock.md (add new entries), GETTING_STARTED.md (add agent docs), quickReference.md (add commands).
IMG20260519145121.jpg
IMG20260519145110.jpg
IMG20260519145046.jpg
IMG20260519145027.jpg
IMG20260519145010.jpg
IMG20260519145000.jpg
IMG20260519144950.jpg
IMG20260519144834.jpg
IMG20260519144803.jpg
IMG20260519144753.jpg
IMG20260519144732.jpg
IMG20260519144722.jpg
IMG20260519144700.jpg
IMG20260519144636.jpg
IMG20260519144625.jpg
similarly for the attached images

4:49 PM
Here are all 15 images with accurate line numbers:

Image 8 — REGENERATE-ADAS-PLAN-PART1.md
1    # Regenerate ADAS - Part 1 of 3 – Core Files (OCR-Friendly Spec)
371  ## Section K. File 15 - generate_docx.py (optional)
375  ---
376
377  ## Section L. Authoring Rules for All Files
378
379  Rule 1: NO use of double-curly-brace VARIABLE substitution placeholders in the output. ADAS v2 is AI-composed; reference templates use illustrative content not
380  placeholders.
381
     Rule 2: Every dot agent dot md file MUST have valid YAML frontmatter between two lines of three dashes. Required fields: name, description, model, target (vscode), and
382  at minimum one of user-invokable or agents.
383
     Rule 3: Every skill file MUST start with the disclaimer paragraph: "What is a Skill? Skills are step-by-step procedural documentation that agents read and follow. They
384  are NOT callable functions."
385
     Rule 4: Schemas live in ONE place only: universal slash docs slash schema-definitions.base.md (see Part 2 Section M). All other files reference it by relative path,
386  never duplicate.
387
     Rule 5: Every file generated INTO a target repo (config, lock, agent, skill, instruction, memory seeds) is created by ADAS - none of those go into the ADAS source repo
388  itself. The ADAS source repo has only the bootstrapper, six skills, reference templates, and documentation.
389
     Rule 6: Generation order matters. Authoring order in this plan: (1) tasks.json stub, (2) schema-definitions.base.md FIRST because everything references it, (3)
     model-tier-rules.md, (4) generate-project-system.md, (5) manage-system, validate-system, setup-full-team, setup-custom-agent, (6) adas.agent.md, (7) templates slash
     generation slash README.md, (8) all universal reference templates, (9) all frontend reference templates, (10) backend, database, infrastructure agent references, (11)
390  the five top-level docs (README, MANUAL, vs-alternatives, Confluence, todo), (12) generate_docx.py optional.
391
392  ---
393
394  End of Part 1. Continue with Part 2 for universal reference templates and Part 3 for domain reference templates.
Image 9 — REGENERATE-ADAS-PLAN-PART1.md
1    # Regenerate ADAS - Part 1 of 3 – Core Files (OCR-Friendly Spec)
281  ## Section G. File 6 - dot github slash skills slash manage-system.md
307  ## Section H. File 7 - dot github slash skills slash validate-system.md
308
309  Standard skill disclaimer paragraph. Purpose: Validate the internal consistency of a generated ADAS agent system. Checks that config, agent files, skill files,
     instruction files, model tiers, skill ownership, handoffs, memory, and lock file are all in sync. Owner: ADAS. Model: Claude Sonnet 4.5.
310
311  Inputs: outputRoot and memoryRoot from adas-config.md.
312
313  Procedure: Step 1 - Read system state. Parse adas-config.md YAML to extract agents, skills, instructions, modelTiers, memoryRoot, version. Read adas-lock.md if exists.
314  List actual files in agents, skills, instructions directories.
315
     Step 2 - Run Config to Files Checks (V-01 to V-04):
316  - V-01: For each agent in config.agents verify outputRoot slash agents slash NAME.agent.md exists.
317  - V-02: For each skill in config.skills verify outputRoot slash skills slash NAME.md exists.
318  - V-03: For each instruction in config.instructions verify outputRoot slash instructions slash NAME.instructions.md exists.
319  - V-04: For each file on disk in those three directories verify it is referenced in config; warn on orphans.
320
321  Step 3 - Skill Ownership Checks (V-05 to V-07):
322  - V-05: Every skill has exactly one owner (non-empty, single agent).
323  - V-06: Each owner agent exists in config.agents.
324  - V-07: Every consumer agent in usedBy exists in config.agents.
325
326  Step 4 - Model Tier Checks (V-08 to V-09):
327  - V-08: Every agent tier is analytical, coding, or hybrid.
328  - V-09: Every model matches tier per model-tier-rules.md (analytical equals Claude Sonnet 4.5, coding equals GPT-5.3-Codex, hybrid equals Claude Sonnet 4.5 default).
329
330  Step 5 - Handoff Checks (V-10 to V-11): Read each agent file YAML frontmatter handoffs array.
331  - V-10: Every handoff target agent exists in roster.
332  - V-11: Every handoff agent model field matches the TARGET agent model from config (not the caller).
333
334  Step 6 - Memory Check (V-12): Verify memoryRoot directory exists and contains seed files context.md, patterns.md, lessons.md, decisions.md.
335
336  Step 7 - Lock File Checks (V-13 to V-14):
337  - V-13: adas-lock.md exists.
338  - V-14: Lock file count matches disk file count (within tolerance of plus or minus 2 for docs).
Image 10 — REGENERATE-ADAS-PLAN-PART1.md
1    # Regenerate ADAS - Part 1 of 3 – Core Files (OCR-Friendly Spec)
281  ## Section G. File 6 - dot github slash skills slash manage-system.md
287  Operation 1 - regenerate (full re-generation). Trigger at-adas regenerate. Steps: (1) read adas-config.md and parse YAML frontmatter; (2) version check - if config
     version less than 2.1, offer upgrade-config first, regenerate as-is, or cancel; (3) drift detection - read adas-lock.md, for each file check existence and compare size/
     preview, collect drift list; (4) report drift to user; (5) re-generate by executing generate-project-system.md with existing config (no questions); (6) update lock file
     and refresh scan.
288
289  Operation 2 - regenerate agent NAME. Steps: (1) validate - read config, find agent in roster, report if missing; (2) re-generate just that agent file following
     generate-project-system Step 2; (3) update its lock entry; (4) report.
290
291  Operation 3 - status. Steps: (1) check adas-config.md exists else suggest at-adas setup; (2) parse config to extract project summary, domains, agent count, version; (3)
     parse lock for generation timestamp and file list; (4) categorize files as unchanged, modified, deleted, new (untracked); (5) report with file counts and modified file
     list.
292
293  Operation 4 - add skill NAME. Steps: (1) read config, check skill does not exist; (2) ask user "what should this skill do and which agents should use it" to derive
     purpose, owner, usedBy; (3) generate skill file per generate-project-system Step 3, scan repo for examples; (4) update references: add to owner agent Skills Available
     with Owner role, add to consumer agents with Consumer role, update adas-config.md (YAML and body), update adas-lock.md; (5) report.
294
295  Operation 5 - add instruction NAME. Steps: (1) read config, check instruction does not exist; (2) ask user "what pattern should this document"; (3) scan repo for real
296  examples, generate instruction file per Step 4; (4) update adas-config.md and adas-lock.md; (5) report.
297
     Operation 6 - remove agent or skill or instruction NAME. Steps: (1) validate exists in config; (2) impact analysis - for agent removal list owned skills (offer to
     reassign or delete), list peer handoffs (will be updated), orchestrator wave entries (will be updated); for skill removal list referencing agents; for instruction
     removal no agent files will be removed; (3) confirm with user showing all files to delete and update; (4) execute - delete file, update affected agent files (remove
     handoffs, skill refs, wave entries), update adas-config.md, update adas-lock.md; (5) report.
298
299  Operation 7 - upgrade-config. Trigger at-adas upgrade-config (or auto from regenerate on version mismatch). Steps: (1) read current config and extract version; (2)
     determine upgrades needed (e.g., from 2.0 to 2.1 add modelTiers section, add skill owner field, add YAML frontmatter); (3) preview changes to user; (4) on confirmation
     update adas-config.md (preserve all existing data, add new structure); (5) optionally run at-adas regenerate to apply.
300
301  Operation 8 - resume. Trigger at-adas resume. Steps: (1) read outputRoot slash adas-generation-progress.md; (2) if not found report no resumable state; (3) check
     configHash vs current adas-config.md hash; if different warn and offer restart from scratch, resume anyway, or cancel; (4) skip completed steps; (5) re-run failed step
     from beginning; (6) continue sequentially; (7) on success delete checkpoint.
302
303  Operation 9 - validate. Hand off to validate-system.md skill. Returns pass/fail report with 17 checks.
304  ---
Image 11 — REGENERATE-ADAS-PLAN-PART1.md
1    # Regenerate ADAS - Part 1 of 3 – Core Files (OCR-Friendly Spec)
239  ## Section F. File 5 - dot github slash skills slash generate-project-system.md
256
257  Step 2 - Generate Agent Files at outputRoot slash agents slash NAME.agent.md for each approved agent. Approach: check for matching reference template in adas slash dot
     github slash templates slash generation slash universal slash agents or domain subdirectory; if found use as structural guide and adapt content; if not found compose
     from scratch using project profile. Standard sub-agent structure: YAML frontmatter (name, description, model from tier as "X (copilot)", agents empty array, target
     vscode, handoffs to peer sub-agents and review with target model in each handoff). Body sections: Heading "NAME Agent - projectName" (Role tailored to project tech
     stack, focused on this sub-agent concern), Model (resolved model with tier justification), Best Used For (3-5 bullets, narrow scope), Skills Available (table of only
     assigned skills with Owner or Consumer designation), Project Context (frameworks, paths relevant to this concern; include Additional Context subsection distilling 3-7
     bullets from contextSources and contextNotes relevant to this agent), Memory Integration (read paths and write paths under memoryRoot), Core Rules (5-10
258  sub-agent-specific rules; append rules from codingStandards if present).
259
     Orchestrator generation - dynamic wave dispatch: YAML frontmatter has agents field listing ALL sub-agent names from approved roster (flat), model Claude Sonnet 4.5
     (copilot), user-invokable true. Wave dispatch generated dynamically; only include waves with at least one sub-agent in the roster. Waves: Wave 1 Scaffold (code, schema,
     cli-commands, library-core, screens), Wave 2 API plus Data (api, routes, services, migration, middleware, etl), Wave 3 UI plus Routing (ui, code, navigation, screens),
260  Wave 4 Tests (test-frontend, test, cli-test, seed, data-validation), Wave 5 Infra (ci-cd, containerization, iac), Wave 6 Docs (library-docs), Wave 7 Review (always
     present). Figma is on-demand and not assigned to any wave.
261
     Batch-manager generation (migration projects only): YAML agents includes orchestrator, repo-context, legacy-analyzer or upgrade-planner, task-planner. user-invokable
262  true. argument-hint mentions workUnit and module count parallel. Sits above orchestrator.
263
     Key principles: every framework, library, path reference must match what is actually in the project. Skills listed match ONLY skills assigned to this specific
     sub-agent. Skills table shows Owner or Consumer. Sub-agents declare empty agents (they are leaf). Handoff model field matches TARGET agent model. Memory paths match
264  memoryRoot. Mark Step 2 completed.
265
     Step 3 - Generate Skill Files at outputRoot slash skills slash NAME.md. Same generation approach: check references in templates slash generation slash universal slash
     skills or domain subdirectory; use as guide or compose from scratch. Standard structure: heading "Skill: NAME", disclaimer paragraph, Purpose, Owner (agent name and
     model), Consumers (other agents that invoke via handoff), Inputs, Procedure (numbered steps tailored to project stack), Output, Validation. For universal skills
     (scan-repo-context, read-memory, write-memory) adapt scan targets to detected domains. For domain skills include real paths and patterns from the project profile. Mark
266  Step 3 completed.
267
     Step 4 - Generate Instruction Files at outputRoot slash instructions slash NAME.instructions.md. Critical: instructions are generated FROM the actual codebase, not from
     generic templates. For each instruction: scan target repo for real examples (e.g., grep for error handling patterns), extract the project actual conventions, document
     as the project living style guide. If no existing examples, generate a recommended approach based on tech stack. Structure: Convention (one paragraph), Examples from
268  This Project (real code with file paths), Rules (numbered list), Anti-Patterns (what NOT to do). Mark Step 4 completed.
Image 12 — REGENERATE-ADAS-PLAN-PART1.md
1    # Regenerate ADAS - Part 1 of 3 – Core Files (OCR-Friendly Spec)
209  ## Section E. File 4 - dot github slash skills slash setup-custom-agent.md
236  (add to roster and skills tables), adas-lock.md (add new entries), GETTING_STARTED.md (add agent docs), quickReference.md (add commands).
237
238  ---
239
240  ## Section F. File 5 - dot github slash skills slash generate-project-system.md
241
     Standard skill disclaimer paragraph. Purpose: Generate a complete multi-agent development assistant system in any repository based on the confirmed project profile,
242  approved agent roster, approved skills, and approved instructions. Owner: ADAS. Model: Claude Sonnet 4.5. Schema reference and model tier reference as in Section C.
243
     Inputs: Core config (projectName, projectIntent, domains array, languages array, outputRoot, memoryRoot, targetRoot). Optional context sources and notes from Phase A6.
244  Per-domain detail sections (frontend, backend, database, infrastructure, cli, library, testing, legacy) - see schema-definitions Section M. Approved agents, skills,
     instructions arrays.
245
     Model Tier System: See model-tier-rules.md. Every agent MUST have modelTier and model fields populated before generation begins.
246
247  Checkpoint System: Generation writes a checkpoint at outputRoot slash adas-generation-progress.md after each step. Format per Section M Checkpoint File Contract. On
     successful Step 8 completion, delete the checkpoint. On failure, preserve so user can run at-adas resume. On resume, always re-run Steps 0 and 0.5 (cheap validation),
248  check configHash; if different, warn user. Skip completed steps, re-run failed step from its beginning, continue sequentially.
249
250  Procedure:
251
     Step 0 - Validate Configuration. Create checkpoint with all steps pending and configHash. Verify outputRoot writable, targetRoot exists, domain marker files still
252  exist, every agent has tier and model. Mark Step 0 completed.
253
     Step 0.5 - Resolve Skill Ownership Conflicts. For each skill verify exactly one owner. If multiple, ask user to pick one (other becomes consumer). If no explicit owner,
     auto-assign first agent in usedBy. Validate consumer handoffs are feasible. Invariant: every skill has exactly one owner and zero or more consumers. Mark Step 0.5
254  completed.
255
     Step 1 - Write Config File at outputRoot slash adas-config.md. Format is YAML frontmatter plus Markdown body, both kept in sync. YAML must include: version 2.1,
     generatedAt ISO timestamp, intent, domains, languages, outputRoot, memoryRoot, targetRoot), modelTiers (analytical Claude Sonnet 4.5, coding GPT-5.
     3-Codex, hybrid Claude Sonnet 4.5), agents array (each with name, domain, role, tier, model, activation, skills), skills array (each with name, purpose, owner, usedBy),
     instructions array (any description). contextSources array if any, contextNotes object if any. Markdown body has matching tables: Project, Context Sources,
     Additional Context, Domain sections only for detected domains, Model Tiers, Agent Roster, Skills, Instructions. Mark file as auto-generated and rule: never
256  during regenerate, source of truth is YAML frontmatter. Mark Step 1 completed.
Image 13 — REGENERATE-ADAS-PLAN-PART1.md
1    # Regenerate ADAS - Part 1 of 3 – Core Files (OCR-Friendly Spec)
110  ## Section D. File 3 - dot github slash skills slash setup-full-team.md
186  - schema owns create-model.
187  - migration owns create-migration.
188  - seed owns create-seed.
189
190  Infrastructure sub-agent skills:
191  - ci-cd owns create-pipeline.
192  - containerization owns create-dockerfile (and create-compose if compose detected).
193  - iac owns create-iac-module.
194
195  Mobile sub-agent skills:
196  - screens owns create-screen, create-component.
197  - navigation owns create-navigator.
198
199  Step C2 - Propose Instructions. Based on actual repo scan, propose pattern guides found in the codebase (error handling, API mock pattern, form validation, etc.). Each
200  instruction is generated from real examples in the repo, not from generic templates.
201
202  Step C3 - Confirm Model Assignments. Present full table of agent to tier to resolved model. Accept overrides per Rule 3.
203
204  Step C4 - Get Output Location. Default outputRoot is targetRoot slash dot github. Default memoryRoot is outputRoot slash memory. Confirm with user.
205
206  PHASE D - Generation. Hand off to skill generate-project-system.md with the assembled profile, agents, skills, instructions, and context.
207
208  ---
209
210  ## Section E. File 4 - dot github slash skills slash setup-custom-agent.md
211
     Standard skill disclaimer paragraph. Purpose: Create a single purpose-built agent along with its required skills and instructions in an autonomous guided flow.
212  Context-aware: reads the repo and any existing ADAS system to ensure the new agent integrates properly. Owner: ADAS. Model: Claude Sonnet 4.5.
213
     Prerequisite: Can run with or without existing ADAS system. With existing system reads adas-config.md and integrates. Without existing system creates standalone agent.
214
215  Phase CA-0 - Validate Workspace Prerequisites: same as setup-full-team Step A0.
216
217  Phase CA-1 - Discover Context.
218  - Step 1: Look for outputRoot slash adas-config.md. If found, parse YAML frontmatter to extract project profile, existing agents, skills, model tiers, memory paths. Set
Image 14 — REGENERATE-ADAS-PLAN-PART1.md
1    # Regenerate ADAS - Part 1 of 3 – Core Files (OCR-Friendly Spec)
110  ## Section D. File 3 - dot github slash skills slash setup-full-team.md
132  index as sole entry.
133  - Data Pipeline: dbt_project.yml; airflow or dags; spark in deps; ipynb notebooks; etl directory; pipeline in folder names.
134  - Mobile: react-native in deps; flutter; ios; android; xcodeproj; build.gradle with Android; expo in deps.
135  - Monorepo: nx.json; turbo.json; lerna.json; pnpm-workspace.yaml; workspaces in package.json.
136  - Legacy (migration source): faces-config.xml (JSF); old at angular slash core (Angular 1); xhtml or jsp files; pom.xml without Spring Boot; jQuery; aspx files; Web.
     config.
137
138  For each detected domain, extract languages, frameworks, build tools, test frameworks, linters, package manager, key paths.
139
140  Step A5 - Present Findings and Confirm. Show a structured summary listing each detected domain with framework, build tool, router, design system, test framework, ORM,
141  auth, etc. Let user confirm or correct.
142
     Step A6 - Gather Additional Context. (A6.1) Check if context-for-adas.md already exists in target root and has content; if so parse and confirm. (A6.2) Otherwise ask
     user "Do you have additional context?" then store as options: Paste in chat / Generate a context-for-adas.md template file / Skip. (A6.3) Handle each option. For Paste in
     chat: collect URLs and text; fetch each public URL with fetch_webpage and extract key conventions; categorize into documentationUrls, architecture, codingStandards,
     apiSpecs, componentPatterns, auth, other. For Generate Template: write a context-for-adas.md file with sections for Documentation URLs (table with Label, URL, Notes),
     Architecture, Coding Standards, API Specifications, Component Patterns, Authentication, Testing, Other Notes. Tell user to fill it in and return when ready by typing
     continue. Then resume parsing the file. For Skip: leave context fields empty. (A6.4) Store all collected context in the project profile as contextSources array and
143  contextNotes object.
144
145  PHASE B - Agent Roster Proposal.
146
     Step B1 - Build Agent Proposal. Universal agents always proposed: orchestrator (analytical, coordinates all sub-agents via dynamic waves), review (analytical, code
147  review and quality enforcement).
148
149  Per-domain sub-agents (separation of concerns by default):
150  - Frontend: code (coding), api (coding), ui (coding), test-frontend (coding), figma (analytical, on-demand).
151  - Backend API: routes (coding), services (coding), middleware (coding).
152  - Database: schema (coding), migration (coding), seed (coding).
153  - Infrastructure: ci-cd (coding), containerization (coding), iac (coding).
154  - Mobile: screens (coding), navigation (coding), native-bridge (coding).
155  - CLI: cli-commands (coding), cli-test (coding).
156  - Library: library-core (coding), library-docs (coding).
157  - Data Pipeline: etl (coding), scheduling (coding), data-validation (coding).
Image 15 — REGENERATE-ADAS-PLAN-PART1.md
1    # Regenerate ADAS - Part 1 of 3 – Core Files (OCR-Friendly Spec)
73   ## Section C. File 2 - dot github slash skills slash model-tier-rules.md
108  ---
109
110  ## Section D. File 3 - dot github slash skills slash setup-full-team.md
111
112  Standard skill disclaimer paragraph. Purpose: Execute the full 4-phase interactive setup flow to create a complete multi-agent development assistant system for any
     repository. Owner: ADAS. Model: Claude Sonnet 4.5. Schema reference and model tier reference as in Section C.
113
114  Procedure:
115
116  PHASE A - Project Discovery.
117
118  Step A0 - Validate Workspace Prerequisites. Use list_dir on workspace root. (1) Verify ADAS folder is in the workspace by looking for a folder containing dot github
     slash agents slash adas.agent.md. If not found, report "ADAS system folder is not in your VS Code workspace. Add it via File - Add Folder to Workspace" and stop. (2)
     Verify at least one other folder (target project) is present. If not, report "No target project found" and stop. (3) If both present, list available project folders
119  excluding the ADAS folder, proceed to Step A1.
120
121  Step A1 - Ask Project Intent. Present six options to user: Migration, New Development, Enhancement, Version Upgrade, Infrastructure or DevOps, Other.
122
     Step A2 - Collect Project Information. For Migration: ask legacy app name and target app name and confirm both repos are in workspace. For others: ask project name and
123  confirm repo is in workspace.
124
125  Step A3 - Detect and Validate Workspace Folders. Use list_dir on workspace root, match user-provided names case-insensitively, store resolved paths.
126
127  Step A4 - Universal Project Scan. Detect domains by scanning for markers:
128  - Frontend: package.json with react, vue, at angular slash core, svelte, next, nuxt; index.html; src slash App; src slash pages; vite.config; webpack.config.
129  - Backend API: package.json with express, fastify, koa, hapi, nest; requirements.txt or pyproject.toml with fastapi, flask, django; pom.xml with spring-boot; go.mod;
130  Cargo.toml with actix, axum, rocket; csproj for ASP.NET; Gemfile with rails or sinatra.
131  - Database: migrations directory; prisma slash schema.prisma; alembic; flyway; liquibase; SQL files; knexfile; typeorm in deps; sequelize in deps; drizzle.config.
132  - Infrastructure: Dockerfile; docker-compose.yml; terraform or tf files; ansible; kubernetes or k8s; helm; dot github slash workflows; Jenkinsfile; gitlab-ci.yml;
     cloudformation; pulumi.
133  - CLI Tool: bin directory; commander, yargs, inquirer, click, typer, cobra, clap in deps; shebangs in entry files.
134  - Library: main or module or exports in package.json without a start script; setup.py or pyproject.toml with project; gemspec; Cargo.toml with lib section: src slash
135  index as sole entry.
can u collect text from all the files...using the line number can u genetrate 3 md files?

4:56 PM

You are out of free messages until 9:30 PM
Get more
can u collect text from all the files...using the line number can u genetrate 3 md files?

Claude is AI and can make mistakes. Please double-check responses.
You’ve hit your limit for Claude messages. Limits will reset at 9:30 PM. For higher limits, explore our Pro plan.
