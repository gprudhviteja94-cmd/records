Image 10 — REGENERATE-ADAS-PLAN-PART2.md (lines ~82–104)
# Regenerate ADAS – Part 2 of 3 – Universal Reference Templates (OCR-Friendly Spec)

## Section N. universal slash agents slash (8 reference templates)

84     ### N1. orchestrator.base.md

86     Frontmatter: name orchestrator; description "End-to-end WORK_UNIT implementation orchestrator that drives a single WORK_UNIT through the full lifecycle using all
       available agents"; model "Claude Sonnet 4.5 (copilot)"; agents array listing all sub-agents (repo-context, analysis-agent, upgrade-planner, task-planner, code, api, ui,
       test, figma, review); target vscode; user-invokable true; argument-hint "WORK_UNIT=UserManagement"; handoffs to review and to next WORK_UNIT.

88     Body: Role – implementation orchestrator driving a single WORK_UNIT through context building, implementation, testing, review by coordinating with specialized agents.
       Best Used For – executing full implementation, coordinating multi-agent workflows, tracking phased progress, capturing lessons. Model Guidance – Claude Sonnet 4.5
       analytical tier. Agents Available table (RepoContext, LegacyAnalyzer for migration, Initiator for new-dev, UpgradePlanner for upgrade, TaskPlanner, Code, API, UI, Test,
       Review). Skills Available (scan-repo-context, analyze-legacy-page/analyze-requirements/analyze-upgrades per intent, generate-micro-tasks, create-component,
       add-api-endpoint, create-hook, add-ui-pattern, component-reuse-check, create-test-file, merge-staged-fragments, read-memory, write-memory).

90     Wave-Based Execution Model: Wave 1 Scaffold (Code), Wave 2 API+Data (API then Code), Wave 3 UI+Routing (UI, Code), Wave 4 Tests (Test), Wave 5 Review (Review), Wave 6
       Finalize (Orchestrator).

92     Pre-Flight Validation: read code-snippets.md and patterns.md; after Scaffold run validate-page.js (HALT if fails); before UI wave verify component reuse done.

94     Memory Integration: Pre-flight read of context.md sections (componentInventory, hooks, rbac). On retry: lessons.md and patterns.md. Writes: lessons.md (issues),
       patterns.md (new patterns), component-usage.md.

97     Terminal Execution Guidelines: validation scripts 20000 ms timeout; lint 30000 ms; tests 60000 ms; build 60000 ms.

98     ### N2. batch-manager.base.md

100    Frontmatter: name batch-manager; description "Batch coordinator that manages parallel WORK_UNIT implementations through the orchestrator, handling queue management,
       concurrent execution with conflict-aware merge queuing, context optimization, and progress tracking"; model "Claude Sonnet 4.5 (copilot)"; agents [orchestrator,
       repo-context, analysis-agent, upgrade-planner, task-planner]; target vscode; user-invokable true; argument-hint with three modes; handoffs to orchestrator (Implement
       WORK_UNIT), batch-manager (Continue Batch), repo-context (Scan).

102    Body: Role – batch coordinator managing multiple WORK_UNITs through orchestrator; handles queue, parallel execution, conflict-aware merge queuing, batch chunking,
       context optimization, progress tracking, session resume; delegates implementation to orchestrator.

104    Input Modes: Mode A Single (WORK_UNIT=Name, parallel=1). Mode B Module Slice (module=X count=N parallel=P; auto-discovers legacy view files or spec docs). Mode C Named
       [cut off]
4:43 PM Here are all 20 images with accurate line numbers extracted from the screen: Image 1 — REGENERATE-ADAS-PLAN-PART2.md 1 # Regenerate ADAS - Part 2 of 3 – Universal Reference Templates (OCR-Friendly Spec) 225 ## Section O. universal slash skills slash (10 reference templates) 328

pasted

Using the already generated text and this text I just pasted....using the line numbers and file names....can u create the 3 md files...

6:01 PM

Check skills directory for relevant skills
Check skills directory for relevant skills
Now I'll assemble all three MD files from the collected text, sorted by line numbers.


Image 1 — REGENERATE-ADAS-PLAN-PART2.md
1    # Regenerate ADAS - Part 2 of 3 – Universal Reference Templates (OCR-Friendly Spec)
225  ## Section O. universal slash skills slash (10 reference templates)
328  ### O10. generate-micro-tasks.base.md
336  Procedure: Step 1 read memory (context.md available components/APIs/hooks, component-usage.md); Step 2 parse spec doc (component hierarchy, form fields + validation,
337  grid columns, API endpoints CRUD, auth/RBAC, navigation, acceptance criteria); Step 3 generate 5 task files using templates from dot github slash templates slash tasks.
338  ---
339
340  ## Section P. universal slash prompts slash (5 reference templates)
341
342  Prompts are not callable; they are reference workflows the user (or another agent) can paste into chat as starting points.
343
344  ### P1. scan-repo-context.base.md
345  Wraps the scan-repo-context skill. Use when user wants to refresh context.md.
346
347  ### P2. generate-tasks.base.md
348  Wraps the generate-micro-tasks skill. Use after a spec doc exists.
349
350  ### P3. implement-feature.base.md
351  Pre-work (read context, patterns, component-usage). Implementation Order: Types (if TS), API functions, mock handlers, data hooks, filter panel, grid/table, form, page,
     route. Post-work (update component-usage.md with new shared components, update context.md with completed page, update patterns.md if new patterns discovered).
352
353  ### P4. document-legacy-module.base.md
354  Wraps analyze-legacy-page for a whole module at once.
355
356  ### P5. migrate-page.base.md
     Phase 1 Analysis (read memory, analyze legacy source for UI/API/RBAC/business-logic). Phase 2 Component Mapping (table mapping legacy components to design-system
     equivalents). Phase 3 Implementation order (API service → mock handlers → data hooks → custom hooks → page scaffold → UI implementation → route registration → tests).
     Phase 4 Validation checklist (all legacy functionality preserved, RBAC mapped, API contracts match, error/loading states handled, design-system used correctly, route
     accessible and guarded). Post-migration update component-usage.md.
357
358  ---
359
360  ## Section Q. universal slash docs slash (5 files; schema-definitions covered in Section M)
361
362
363  ### Q1. adas-config.base.md
364  A reference example of a populated config file with YAML frontmatter + Markdown body. Body sections: Project table, Context Sources, Domain blocks per detected domain,
Image 2 — REGENERATE-ADAS-PLAN-PART2.md
1    # Regenerate ADAS - Part 2 of 3 – Universal Reference Templates (OCR-Friendly Spec)
361  ## Section Q. universal slash docs slash (5 files; schema-definitions covered in Section M)
363  ### Q1. adas-config.base.md
364  A reference example of a populated config file with YAML frontmatter + Markdown body. Body sections: Project table, Context Sources, Domain blocks per detected domain,
     Model Tiers (Tier-Model-Agents), Agent Roster, Skills, Instructions.
365
366  ### Q2. GETTING_STARTED.base.md
367  Overview of generated agent system. Sections: Project Configuration (framework, design system, API client, test framework, mock framework, legacy info if migration);
     How to Use (start the orchestrator example "at-orchestrator What should I work on next?"); Available Agents table (Orchestrator, Code, API, UI, Test, Review,
     RepoContext, TaskPlanner, BatchManager, plus LegacyAnalyzer for migration or Initiator for new-dev) with invoke commands; Memory System overview (context, patterns,
     lessons, decisions, component-usage); Wave Execution (Scaffold → API → UI → Integration → Testing).
368
369  ### Q3. quickReference.base.md
370  Quick code patterns for the project stack. Sections: Component Patterns (Page example, API Hook example, Mutation example); File Structure tree; Key Imports for the
371  detected design system.
372
373  ### Q4. AGENT-SKILL-SYSTEM-GUIDE.base.md
     Architectural overview. Sections: Architecture (multi-agent collaboration via shared memory and tasks); Core Concepts (Agents in agents folder are VS Code chat
     participants with role+tools+instructions+agents handoffs; Skills in skills folder are procedural documentation NOT callable functions; Instructions in instructions
     folder are project-wide conventions; Memory in memory folder persists context; Tasks in templates/tasks define work by wave); Workflow (1 user invokes agent, 2
     orchestrator reads manifest and delegates, 3 specialized agent reads memory + skills + instructions, does work, updates memory).
374
375  ---
376
377  ## Section R. universal slash templates slash memory slash (8 files - seed templates for memory)
378
379  These are seed files that ADAS copies into the target repo at Step 5 of generation. All start with project name header.
380
381  ### R1. context.base.md
382  Headings: Project Overview (Application name, Framework + version, Design System, API Client, Test Framework; if migration also Legacy Application + Legacy Framework);
     Source Structure (tree showing api/, components/, features/, hooks/, routes/, types/, utils/); Completed Pages (table - populated as work proceeds).
383
384  ### R2. patterns.base.md
385  Headings: Discovered Patterns; Code Patterns; Anti-Patterns. Empty placeholders.
386
387  ### R3. lessons.base.md
     Headings: Lessons Learned (empty list). Note: lessons are appended; auto-promotion rule fires at 3 or more occurrences.
Image 3 — REGENERATE-ADAS-PLAN-PART2.md
1    # Regenerate ADAS - Part 2 of 3 – Universal Reference Templates (OCR-Friendly Spec)
377  ## Section R. universal slash templates slash memory slash (8 files - seed templates for memory)
387  ### R3. lessons.base.md
     Headings: Lessons Learned (empty list). Note: lessons are appended; auto-promotion rule fires at 3 or more occurrences.
388
389
390  ### R4. decisions.base.md
391
392  Headings: Architecture Decision Records (empty list). Each ADR will follow standard ADR format (Context, Decision, Status, Consequences).
393
394  ### R5. component-usage.base.md
     Headings: Shared Component Usage Registry (empty table - Component name, Usage count, Used by features).
395
396  ### R6. page-template.base.md
397  Per-page memory file template - populated when each page completes.
398
399  ### R7. batch-state.base.md
400  Headings: Current Batch (Batch ID, Status idle, Wave, Started); Batch History (empty); Pending Tasks (empty).
401
402  ### R8. batch-context-brief.base.md
     Headings: Active Context (compressed context for agents joining batch mid-execution); Project Stack (Framework, Design System, API Client, Test Framework; Legacy if
     migration); Current Focus (Batch, Wave, Target Pages); Key Files (Config path, Context Memory path).
403
404
405  ---
406
407  ## Section S. universal slash templates slash tasks slash (6 files - task structure templates)
408
409  ### S1. manifest.base.md
     Heading: Task Manifest. Sections: Overview (master task list tracking all pages/features); Status Legend (red circle Not Started, yellow circle In Progress, green
     circle Completed, skip icon Skipped); Pages/Features table (for migration: # | Page | Legacy Source | Wave | Status | Assigned To; for new-dev: # | Page | Priority |
410  Wave | Status | Assigned To); Wave Summary table (Wave 1 Scaffold & Shared Components, Wave 2 API Layer & Data Hooks, Wave 3 UI Components & Pages, Wave 4 Integration &
     Routing, Wave 5 Testing, Wave 6 Review & Polish - each with page count and status).
411
412  ### S2. scaffold-tasks.base.md
413  Wave 1 task checklist: create folder structure; create main component with auth guard; create styles + barrel export; create sub-component stubs. Agent: Code.
414
415  ### S3. api-hooks-tasks.base.md
     Wave 2 task checklist: add endpoint constants; create API service functions using detected API client; create mock framework handlers and register them; create
     state-management data-fetching hooks; create mutation hooks; create filter/form hooks. Agents: API, Code.
Image 4 — REGENERATE-ADAS-PLAN-PART2.md
1    # Regenerate ADAS - Part 2 of 3 – Universal Reference Templates (OCR-Friendly Spec)
407  ## Section S. universal slash templates slash tasks slash (6 files - task structure templates)
412  ### S2. scaffold-tasks.base.md
413  Wave 1 task checklist: create folder structure; create main component with auth guard; create styles + barrel export; create sub-component stubs. Agent: Code.
414
415  ### S3. api-hooks-tasks.base.md
416  Wave 2 task checklist: add endpoint constants; create API service functions using detected API client; create mock framework handlers and register them; create
     state-management data-fetching hooks; create mutation hooks; create filter/form hooks. Agents: API, Code.
417
418  ### S4. ui-routing-tasks.base.md
419  Wave 3 task checklist: component-reuse-check for new UI components; implement search/filter panel using design system; implement data grid/table; implement create/edit
     form (dialog or drawer); register route in router; add navigation link; wire auth guards. Agents: UI, Code.
420
421  ### S5. tests-tasks.base.md
422  Wave 4 task checklist: write component smoke tests; write component interaction tests; write hook unit tests; write API function tests. Agent: Test.
423
424  ### S6. upgrade-spec.base.md
425  Template for upgrade-planner output. Sections: Overview (What/Why/Scope/Risk Level); Dependency Impact Matrix (Package | Current | Target | Impact | Action); Breaking
     Changes (BC-1, BC-2, ... each with Description, Affected Files, Remediation, Risk, Effort); Migration Steps Ordered (10-step checklist - manifest update, install, fix
     breaking changes one by one, update configs, update tests, run tests, run build, smoke test, update docs); External References table; Risk Assessment table.
426
427  ---
428
429  End of Part 2. Continue with Part 3 for frontend, backend, database, infrastructure reference templates.
430
Image 8 — REGENERATE-ADAS-PLAN-PART2.md (Explorer + Chat panel visible)
1    # Regenerate ADAS - Part 2 of 3 – Universal Reference Templates (OCR-Friendly Spec)
2
3    Read Part 1 first. This part covers all files under dot github slash templates slash generation slash universal slash.
4
5    The universal subtree:
6    - agents slash : orchestrator, batch-manager, initiator, legacy-analyzer,
       repo-context, review, task-planner, upgrade-planner (8 files)
7    - skills slash : scan-repo-context, read-memory, write-memory,
       manage-batch, merge-staged-fragments, analyze-requirements,
       analyze-legacy-page, analyze-upgrade, component-reuse-check,
       generate-micro-tasks (10 files)
8    - prompts slash : scan-repo-context, generate-tasks, implement-feature,
       document-legacy-module, migrate-page (5 files)
9    - docs slash : adas-config, GETTING_STARTED, quickReference,
       AGENT-SKILL-SYSTEM-GUIDE, schema-definitions (5 files)
10   - templates slash memory slash : context, patterns, lessons, decisions,
       component-usage, page-template, batch-state, batch-context-brief (8 files)
11   - templates slash tasks slash : manifest, scaffold-tasks, api-hooks-tasks,
       ui-routing-tasks, tests-tasks, upgrade-spec (6 files)
12
13   All files end with dot base dot md (the suffix marks them as reference
     templates). Curly-brace placeholders like double-curly WORK_UNIT
     double-curly are legacy artifacts; in v2 they are illustrative only - the
     LLM composes real content at generation time.
14
15   ---
16
17   ## Section M. universal slash docs slash schema-definitions.base.md
     (SINGLE SOURCE OF TRUTH)
18
19   Heading: ADAS Schema Definitions. Subheading: Single source of truth for
     all data structures shared between ADAS components. Version 2.1.
20
     Sub-section Agent Definition Schema. Used by adas.agent.md,
     setup-full-team.md, setup-custom-agent.md, generate-project-system.md.
Image 14 — REGENERATE-ADAS-PLAN-PART2.md
1    # Regenerate ADAS - Part 2 of 3 – Universal Reference Templates (OCR-Friendly Spec)
82   ## Section N. universal slash agents slash (8 reference templates)
119  ### N3. initiator.base.md
128
129  Detection keywords for upgrade: upgrade, bump, update version, migrate to v, update dependency, upgrade package, version bump, update to latest, upgrade runtime.
130
131  Analysis Procedure:
132  - Step 0 read memory (context, patterns, decisions)
133  - Step 1 parse requirements (1a check for upgrade keywords → handoff to upgrade-planner; 1b standard requirements analysis - extract core WORK_UNIT, sub-features, data
     entities, user interactions, ask clarifying questions if needed)
134  - Step 2 design component hierarchy (decide reuse-existing vs create-new-shared vs create-WORK_UNIT-specific for each)
135  - Step 3 design API contracts (Search GET, Create POST, Update PUT, Delete DELETE, Get One GET)
136  - Step 4 define auth/RBAC (allowView, allowEdit, allowDelete, allowAdmin keys)
137  - Step 5 define form fields (field, type, required, validation, default)
138  - Step 6 define data grid columns (column, header, field, sortable, filterable, width)
139  - Step 7 produce spec document at mdfiles slash module slash NN-Name-Implementation-Plan.md
140
141  ### N4. repo-context.base.md
142
143  Frontmatter: name repo-context; description "Repository context scanner that builds comprehensive context.md for the TARGET_APP project"; model "Claude Sonnet 4.5
     (copilot)"; agents empty; user-invokable true; handoffs to legacy-analyzer (migration) or initiator (other) based on project intent.
144
145  Body: Role - scan target repo and build comprehensive context document used as foundation by all other agents; creates shared memory that prevents hallucination. Best
     Used For - initial scan before WORK_UNIT batch, building/refreshing context.md, extracting components/hooks/APIs/patterns/conventions, documenting auth privilege
     mappings, establishing baseline for component reuse.
146
147  Skills Available: scan-repo-context.
148
149  Key Locations to Scan table: Shared Components (componentPath), Custom Hooks (hookPath), API Endpoints (apiPath), Existing Pages (pagePath), Auth Module (authModule),
     Mock Handlers (mockPath), Config Files (configPath), Design System Usage (scan imports).
150
151  Output: context.md sections - Repository Overview, Components Inventory, Hooks Inventory, API Endpoints, Design System Usage, RBAC/Auth Mapping, Common Patterns,
     Routing Conventions.
152
153  ### N5. review.base.md
154
155  Frontmatter: name review; description "Code review agent for quality checks, standards compliance, and actionable feedback"; model "Claude Sonnet 4.5 (copilot)"; agents
     empty; user-invokable true; handoffs to code (fix issues), model GPT-5.3-Codex (copilot) and orchestrator (Next WORK_UNIT).
Image 15 — REGENERATE-ADAS-PLAN-PART2.md
1    # Regenerate ADAS - Part 2 of 3 – Universal Reference Templates (OCR-Friendly Spec)
82   ## Section N. universal slash agents slash (8 reference templates)
171  ### N6. task-planner.base.md
178
179  Task Generation Output: 5 micro-task files per WORK_UNIT in mdfiles slash module slash tasks slash Name slash:
180  1. manifest.md - master overview with execution graph + validation gates + progress tracking
181  2. scaffold-tasks.md - Wave 1 create full scaffold (folder, main component, styles, barrel, sub-component stubs) - Agent Code
182  3. api-hooks-tasks.md - Wave 2 endpoints + state-management hooks + mocks - Agents API and Code
183  4. ui-routing-tasks.md - Wave 3 UI + routing + auth guards - Agents UI and Code
184  5. tests-tasks.md - Wave 4 test suites - Agent Test
185
186  ### N7. upgrade-planner.base.md
187
188  Frontmatter: name upgrade-planner; description "Version upgrade specialist that analyzes dependency/framework upgrade requests, gathers migration context from users and
     external sources, identifies breaking changes and dependency conflicts, and produces structured Upgrade Spec documents for the implementation pipeline"; model "Claude
     Sonnet 4.5 (copilot)"; agents empty; user-invokable true; argument-hint "Upgrade React from 18 to 19 | Bump Terraform to 1.6"; handoffs to task-planner (Generate Tasks)
189  and orchestrator (Start Full Implementation).
190
     Body: Role - senior dependency and upgrade specialist; gathers context from user and external sources; identifies breaking changes and conflicts; produces structured
     Upgrade Spec; bridges "upgrade X to Y" to "here is exactly what needs to change in what order with what risks".
191
     Skills Available: analyze-upgrade, read-memory, write-memory.
192
193
194  Input Formats: Format 1 simple upgrade request; Format 2 multi-dependency; Format 3 with context (URL + known issues); Format 4 tool/runtime upgrade.
195
196  Analysis Procedure (Steps 0-6 detailed in skill file Section O3):
197  - Step 0 read memory
198  - Step 1 parse upgrade request - extract target dependency, current version (from manifest), target version, scope
199  - Step 2 scan dependency manifest (npm, pip, maven, go, cargo, terraform, ruby, runtimes)
200  - Step 3 gather user context (MANDATORY; ask 4 question sets via ask_questions: changelog URL, known breaking changes, internal docs, constraints/blockers)
201  - Step 4 fetch and analyze external resources (use fetch_webpage for each URL, extract breaking changes, deprecated APIs, peer dep requirements, config changes,
     migration steps, caveats)
202  - Step 5 build impact analysis (Dependency Impact Matrix, Breaking Changes Inventory with affected files in THIS project, Affected Files list)
203  - Step 6 produce Upgrade Spec at mdfiles slash module slash NN-Name-Upgrade-Spec.md (Overview, Impact Matrix, Breaking Changes, Migration Steps ordered checklist,
     External References, Risk Assessment)
204
205  ### N8. legacy-analyzer.base.md
Image 16 — REGENERATE-ADAS-PLAN-PART2.md
1    # Regenerate ADAS - Part 2 of 3 – Universal Reference Templates (OCR-Friendly Spec)
82   ## Section N. universal slash agents slash (8 reference templates)
205  ### N8. legacy-analyzer.base.md
206
207  Frontmatter: name legacy-analyzer; description "Legacy LEGACY_FRAMEWORK code analysis agent for extracting WORK_UNIT structure, business logic, auth rules, and API
     contracts from the LEGACY_APP codebase"; model "Claude Sonnet 4.5 (copilot)"; agents empty; user-invokable true; argument-hint "WORK_UNIT=UserSearch module=admin";
     handoffs to task-planner (Generate Tasks) and orchestrator (Start Full Migration).
208
209  Body: Role - senior analyst reading/understanding/documenting the legacy application to produce structured migration specifications. Best Used For - analyzing legacy
     view files for UI/forms/tables/actions; reading backend controllers/beans for business logic/validation/service calls; extracting RBAC rules; mapping legacy navigation
210  to target router routes; producing structured Markdown analysis docs.
211
212  Skills Available: analyze-legacy-page, read-memory, write-memory.
213
     File Locations vary by legacy framework:
214  - JSF: WebContent/web/controller/**/*.xhtml, faces-config.xml, src/main/java/**/controller/**/*.java, WebPrivilege.java
215  - Angular old: src/app/**/*.component.ts, src/app/**/*.component.html, src/app/**/*.service.ts, src/app/**/*-routing.module.ts, src/app/**/*.guard.ts
216  - ASP.NET MVC: Views/**/*.cshtml, Controllers/**/*.cs, Models/**/*.cs, Services/**/*.cs
217  - Generic fallback: any view extension, any controller in legacy source root
218
219  Legacy Framework Patterns: JSF uses faces-config.xml outcome routing + managed beans + WebPrivilege session bean + RichFaces; Angular uses Router + Injectable services
     + HttpClient + route guards; ASP.NET MVC uses convention-based or attribute routing + MVC controllers + Authorize attributes + Razor templates.
220
221  Analysis Procedure: Step 0 read memory; Step 1 locate source files (view, controller, navigation); Step 2 extract UI structure (template, forms, data tables with EVERY
     column, action buttons; conditional rendering); Step 3 extract business logic (controller method to CRUD mapping, validation rules, service calls to API candidates,
222  data transformations); Step 4 extract auth/RBAC (authorization checks, map to target auth pattern).
223
224  ---
225
226  ## Section O. universal slash skills slash (10 reference templates)
227
228  Each skill file starts with the "What is a Skill?" disclaimer paragraph.
229
230  ### O1. scan-repo-context.base.md
231  Purpose: Scan the target repository and produce comprehensive context.md as shared memory for all agents. Owner: RepoContext. Inputs: mode (default "full", or
Image 17 — REGENERATE-ADAS-PLAN-PART2.md
1    # Regenerate ADAS - Part 2 of 3 – Universal Reference Templates (OCR-Friendly Spec)
225  ## Section O. universal slash skills slash (10 reference templates)
277  ### O5. merge-staged-fragments.base.md
278
279  Purpose: Consolidate staged file fragments after a wave completes. Parallel tasks write to underscore staged to prevent race conditions on shared files; this skill
280  merges them. Owner: Orchestrator.
281
282  Inputs: stagedDir (path to staged fragments), waveNumber.
283
284  Procedure: Step 1 inventory fragments (list files matching pattern *.fragment.*); Step 2 group by target (encoded in filename); Step 3 merge each group - read target
285  file if exists, read all fragments for this target, apply changes to target, delete fragment files after success; report any conflicts to user.
286
287  ### O6. analyze-requirements.base.md
288  Purpose: Convert user requirements (free-form or structured) into structured implementation specification document. Owner: Initiator. Inputs: requirements (text/
289  markdown), module (optional auto-determined). Output: mdfiles slash module slash NN-Name-Implementation-Plan.md.
290
     Procedure:
291  - Step 1 parse requirements (extract core WORK_UNIT purpose, sub-features, data entities, user interactions; ask clarifying questions if ambiguous)
292  - Step 2 check existing context (read context.md for components/APIs/hooks; identify reuse vs create-new; check for conflicting patterns)
293  - Step 3 design solution (component hierarchy tree, API contracts, auth requirements, form fields, grid columns)
294  - Step 4 write spec document
295
296  ### O7. analyze-legacy-page.base.md
297
298  Purpose: Analyze single legacy WORK_UNIT and produce structured implementation specification for the target project. Owner: LegacyAnalyzer. Inputs: name (legacy
     WORK_UNIT name), module, viewPath (optional override). Output: mdfiles slash module slash NN-Name-Implementation-Plan.md.
299
     Procedure:
300  - Step 0 read memory (legacyMapping, rbac)
301  - Step 1 locate source files (varies per legacy framework - JSF view + faces-config + Java controller; Angular component + template + service + routing; ASP.NET view +
     controller + models)
302  - Step 2 extract UI structure (template, forms, data tables with EVERY column - header, field binding, sort/filter capability, interactive elements; action buttons;
303  conditional rendering)
304  - Step 3 extract business logic (controller methods to CRUD, validation rules, service calls to API candidates, data transformations)
305  - Step 4 extract auth/RBAC (all authorization checks, map to target auth pattern)
306
307  ### O8. analyze-upgrade.base.md
Image 18 — REGENERATE-ADAS-PLAN-PART2.md
1    # Regenerate ADAS - Part 2 of 3 – Universal Reference Templates (OCR-Friendly Spec)
225  ## Section O. universal slash skills slash (10 reference templates)
295  ### O7. analyze-legacy-page.base.md
305
306  ### O8. analyze-upgrade.base.md
307
308  Purpose: Analyze a version upgrade request, gather migration context, identify breaking changes and dependency conflicts, produce structured Upgrade Spec. Owner:
     upgrade-planner. Inputs: upgrade_request, module optional, urls optional.
309
310  Procedure: Steps 1-7 same as upgrade-planner agent body (see N7).
311
312  ### O9. component-reuse-check.base.md
313
314  Purpose: Verify component reuse opportunities before creating new shared components. Owners: Code, UI.
315
316  Inputs: componentName, purpose (what it should do e.g. "data table with sorting and pagination").
317
318  Procedure:
319  - Step 1 read component inventory (context.md componentInventory section + component-usage.md)
320  - Step 2 check in order, stop at first match (the order varies by design system):
321    - Salt DS: project shared → UIPax/Pepper → Salt DS Core → Salt DS Lab → create new
322    - MUI: project shared → MUI Core → MUI X → MUI Lab → create new
323    - Chakra UI: project shared → Chakra UI → create new
324    - Ant Design: project shared → Ant Design → Ant Design Pro → create new
325    - Generic fallback: project shared → third-party dependencies → create new
326  - Step 3 if creating new, document reuse-check result in memory before proceeding
327
328  ### O10. generate-micro-tasks.base.md
329
330  Purpose: Generate 5-phase micro-task files from analysis/spec document to guide implementation agents. Owner: TaskPlanner.
331
332  Inputs: specDocPath, name (PascalCase), module.
333
334  Output: 5 files in mdfiles slash module slash tasks slash Name slash - manifest.md, scaffold-tasks.md, api-hooks-tasks.md, ui-routing-tasks.md, tests-tasks.md.
335
336  Procedure: Step 1 read memory (context.md available components/APIs/hooks, component-usage.md); Step 2 parse spec doc (component hierarchy, form fields
337  grid columns, API endpoints CRUD, auth/RBAC, navigation, acceptance criteria); Step 3 generate 5 task files using templates from dot github slash templates slash tasks.
Image 1 — REGENERATE-ADAS-PLAN-PART2.md
1    # Regenerate ADAS - Part 2 of 3 – Universal Reference Templates (OCR-Friendly Spec)
225  ## Section O. universal slash skills slash (10 reference templates)
252  ### O3. write-memory.base.md
253
254  Purpose: Write to shared memory files to capture patterns, lessons, decisions, and component usage. Owner: All agents.
255
256  Memory Files table: patterns.md (new reusable patterns + anti-patterns; written after discovering pattern worth reusing), lessons.md (bugs/mistakes/solutions; written
     after encountering and solving an issue), decisions.md (architecture decisions with rationale; written after making non-obvious design choice), component-usage.md
     (component usage tracking; written after using or creating shared component), context.md (repo inventory updates; written after adding new components/APIs/hooks).
257
258  Writing a Pattern format: heading PatternName, Category (componentPatterns/hookPatterns/apiPatterns/testPatterns/designSystemPatterns), Added date, Source (which
     WORK_UNIT discovered in), Pattern (code or description), Anti-Pattern if applicable.
259
260  Writing a Lesson format: heading LessonTitle, Category (structure/import/naming/api/mock/test/ui/a11y), Severity (error/warn/info), Occurrences count, First Seen date,
     File path, Problem, Solution, Prevention.
261
262  Lesson Promotion Rule: when a lesson reaches 3 or more occurrences, consider promotion to a skill file or instruction file.
263
264  ### O4. manage-batch.base.md
265
266  Purpose: Coordinate batch execution of multiple WORK_UNITs through Orchestrator with parallel execution and conflict-aware merge queuing. Owner: BatchManager.
267
268  Inputs: mode (single/module-slice/named-list), names (CSV), module, count, parallel (default 2 migration, 1 others, max 3).
269
270  Procedure:
271  - Step 1 build queue per mode
272  - Step 2 validate prerequisites (analysis/spec doc exists, task files exist, no blocking dependencies)
273  - Step 3 build context brief (compress 2000+ line memory to ~250 lines)
274  - Step 4 create batch-state.md with all WORK_UNITs queued (columns: #, WORK_UNIT, Module, Status, Chunk, Slot, Started, Completed)
275  - Step 5 execute parallel-aware: chunk queue into groups of parallel size, create memoryRoot dot staged directory, for each chunk launch parallel orchestrator sessions
     (each writes WORK_UNIT-scoped files directly; shared-file changes go to dot staged fragment files), wait for all sessions, run merge-staged-fragments skill, update
     batch state, inter-chunk context refresh
276
277  ### O5. merge-staged-fragments.base.md
278
279  Purpose: Consolidate staged file fragments after a wave completes. Parallel tasks write to underscore staged to prevent race conditions on shared files; this skill
     merges them. Owner: Orchestrator.
Image 2 — REGENERATE-ADAS-PLAN-PART2.md
1    # Regenerate ADAS - Part 2 of 3 – Universal Reference Templates (OCR-Friendly Spec)
225  ## Section O. universal slash skills slash (10 reference templates)
230  ### O1. scan-repo-context.base.md
231  Purpose: Scan the target repository and produce comprehensive context.md as shared memory for all agents. Owner: RepoContext. Inputs: mode (default "full", or
     "incremental").
232
233  Memory Writes: memoryRoot slash context.md (all sections), component-usage.md (baseline counts), patterns.md (detected patterns).
234
235  Procedure:
236  - Step 1 Scan Shared Components: list folders in componentPath, for each component read main file, extract JSDoc/TSDoc, extract exports (named preferred), check styles,
     note design-system categories as Form Controls/Data Display/Layout/Feedback/Navigation/Actions; output to context.md Components Inventory section.
237  - Step 2 Scan Custom Hooks: list files in hookPath, extract hook names, read comments for descriptions, categorize as Data (query/mutation)/State/Effect/Context; output
     to Hooks Inventory.
238  - Step 3 Scan API Endpoints: read apiPath files, extract exported functions, identify HTTP method/path/resource, cross-reference with mockPath (mock only → Mock Only
     status, both exist → Backend+Mock Only); output to API Endpoints.
239  - Step 4 Scan Existing Pages: list folders in pagePath, note name + route registration + auth guard; output to Repository Overview Existing Pages.
240  - Step 5 Extract Auth/RBAC Keys: read authModule, find auth state/type definition, extract all privilege keys; output to RBAC/Auth Mapping.
241  - Step 6 Extract Design System Usage: search all source files for imports from design-system packages, count usage frequency per component; output to Design System
     Usage.
242  - Step 7 Detect Common Patterns: scan 3-5 existing pages for recurring patterns (forms, grids, dialogs); output to Common Patterns.
243
244  ### O2. read-memory.base.md
245
246  Purpose: Read shared memory files to inform agent decisions; implements lazy loading - minimal sections first, expand on retry/failure. Owner: All agents.
247
248  Memory Files table: Context (context.md - repo inventory), Patterns (patterns.md - proven + anti-patterns), Lessons (lessons.md - bug log with auto-promotion),
     Decisions (decisions.md - ADRs), Component Usage (component-usage.md - reuse tracking).
249
250  Lazy Loading Pattern: First read minimal sections (save context window) - Code agent reads componentInventory + hooks lists; API agent reads apiEndpoints list; UI agent
     reads componentInventory + uiPatterns lists; Test agent reads testing setup info; Review agent reads componentInventory + apiEndpoints + rbac. On retry/failure expand
     by reading lessons.md filtered by relevant category and patterns.md filtered by relevant pattern type.
251
252  ### O3. write-memory.base.md
253
254  Purpose: Write to shared memory files to capture patterns, lessons, decisions, and component usage. Owner: All agents.
255
Image 3 — REGENERATE-ADAS-PLAN-PART2.md
1    # Regenerate ADAS - Part 2 of 3 – Universal Reference Templates (OCR-Friendly Spec)
82   ## Section N. universal slash agents slash (8 reference templates)
153  ### N5. review.base.md
154
155  Frontmatter: name review; description "Code review agent for quality checks, standards compliance, and actionable feedback"; model "Claude Sonnet 4.5 (copilot)"; agents
     empty; user-invokable true; handoffs to code (Fix Issues, model GPT-5.3-Codex copilot) and orchestrator (Next WORK_UNIT).
156
157  Body: Role - meticulous code reviewer, final quality gate before PR-ready. Best Used For - reviewing completed WORK_UNIT implementations for scope/standards/
     architectural consistency; verifying skill compliance; checking accessibility and design-system adherence; producing blocker/warning/suggestion feedback; capturing
     lessons.
158
159  Skills Available: component-reuse-check, read-memory, write-memory.
160
161  Memory Integration: required reads - context.md (componentInventory, apiEndpoints, rbac), lessons.md ALL lessons, decisions.md ALL decisions. On retry: patterns.md,
     component-usage.md. Writes: lessons.md automatic for blockers/warnings, patterns.md if non-standard approved, decisions.md if new architectural decisions made.
162
163  Review Checklist sections:
164  - Structure & Imports: folder structure correct, named exports, import paths follow conventions, barrel file present, no circular dependencies
165  - Design System Compliance: design-system components used, reuse-check order followed, consistent styling approach
166  - API Integration: API functions use the project API client wrappers, mock handlers created for all endpoints, mocks registered, error handling present
167  - Data Layer: state management used for fetching, loading states handled, error states handled, transformations clean
168  - Auth/RBAC: guards present where required, provider wiring verified
169  - Testing: tests exist for new components, behavior-driven queries, deterministic and independent tests, mock framework used properly
170
171  ### N6. task-planner.base.md
172
173  Frontmatter: name task-planner; description "Task planning agent for generating structured per-WORK_UNIT micro-task files from analysis documentation"; model "Claude
     Sonnet 4.5 (copilot)"; agents empty; user-invokable true; argument-hint "WORK_UNIT=UserManagement"; handoffs to orchestrator.
174
175  Body: Role - convert analysis/spec documents into structured actionable per-WORK_UNIT micro-task files guiding implementation agents through the full lifecycle. Best
     Used For - converting analysis to task checklists, breaking complex work into phased dependency-ordered micro-tasks, assigning agents and skills per task, ensuring
     complete coverage, generating task manifests.
176
177  Skills Available: generate-micro-tasks, read-memory, write-memory.
178
179  Task Generation Output: 5 micro-task files per WORK_UNIT in mdfiles slash module slash tasks slash Name slash:
180  1. manifest.md - master overview with execution graph + validation gates + progress tracking
Image 4 — REGENERATE-ADAS-PLAN-PART2.md
1    # Regenerate ADAS - Part 2 of 3 – Universal Reference Templates (OCR-Friendly Spec)
82   ## Section N. universal slash agents slash (8 reference templates)
98   ### N2. batch-manager.base.md
104  Input Modes: Mode A Single (WORK_UNIT=Name, parallel=1). Mode B Module Slice (module=X count=N parallel=P; auto-discovers legacy view files or spec docs). Mode C Named
     List (module=X WORK_UNITs=Name1,Name2,Name3 parallel=P).
105
106  Parallel Execution Model: parallel=1 sequential; parallel=2 default for migration; parallel=3 max.
107
108  Conflict-Aware File Classification table:
109  - WORK_UNIT-scoped (page folder, tests, hooks) - None - Parallel safe write directly
110  - Router config (src/router) - High - Staged fragment merge after chunk
111  - Mock handlers barrel - High - Staged fragment
112  - Barrel exports - High - Staged fragment
113  - Memory/context files - Medium - Append lock one writer per chunk
114
115  Staged Fragment Approach: each parallel WORK_UNIT writes shared-file changes to memoryRoot slash dot staged slash route-Name.fragment.md etc; after chunk completes
     batch-manager runs merge-staged-fragments skill; fragments deleted on success.
116
117  Batch Execution Flow: parse input, build queue, validate prerequisites, build batch-context-brief (compress 2000+ line memory to ~250 lines), create batch-state.md,
     chunk queue, for each chunk launch parallel orchestrator sessions, wait for completion, merge fragments, update batch state, inter-chunk context refresh, final batch
     checkpoint and report.
118
119  ### N3. initiator.base.md
120
121  Frontmatter: name initiator; description "Requirements analysis agent that converts user requirements into structured spec documents"; model "Claude Sonnet 4.5 (copilot)
     "; agents empty; user-invokable true; argument-hint example "Build a user management page with search, CRUD, and role-based access"; handoffs to task-planner (Generate
     Tasks), orchestrator (Start Full Implementation), upgrade-planner (Gather Upgrade Context).
122
123  Body: Role - senior requirements analyst and solution architect; bridges "what user wants" to "what agents need to build it". Best Used For - converting requirements to
     spec docs, designing component hierarchy, determining API contracts from CRUD, identifying auth/RBAC, producing implementation-ready specs.
124
125  Skills Available: analyze-requirements, read-memory, write-memory.
126
127  Input Formats: Format 1 free-form text. Format 2 structured markdown (Feature/Pages/API/Auth/Fields). Format 3 mixed. Format 4 version upgrade request (handed off to
128  upgrade-planner).
129  Detection keywords for upgrade: upgrade, bump, update version, migrate to v, update dependency, upgrade package, version bump, update to latest, upgrade runtime.
Image 5 — REGENERATE-ADAS-PLAN-PART2.md
1    # Regenerate ADAS - Part 2 of 3 – Universal Reference Templates (OCR-Friendly Spec)
17   ## Section M. universal slash docs slash schema-definitions.base.md (SINGLE SOURCE OF TRUTH)
58   Sub-section Memory File Contract. Table of file - path - created by - written by - read by:
59   - context.md - memoryRoot/context.md - generate-project-system Step 5 - scan-repo-context skill - All agents
60   - patterns.md - memoryRoot/patterns.md - generate-project-system Step 5 - All agents (append) - All agents
61   - lessons.md - memoryRoot/lessons.md - generate-project-system Step 5 - All agents (append) - All agents
62   - decisions.md - memoryRoot/decisions.md - generate-project-system Step 5 - orchestrator, initiator - All agents
63
64   Memory Protection Rules: NEVER overwritten during re-generation; context.md exception is refreshed by scan-repo-context; agents APPEND to patterns/lessons/decisions,
     never truncate.
65
66   Sub-section Config File Contract (adas-config.md). Format: YAML frontmatter (machine-parseable) + Markdown body (human-readable). YAML must include version "2.1",
     generatedAt ISO, project block (name, intent, domains, languages, outputRoot, memoryRoot, targetRoot), modelTiers block (analytical "Claude Sonnet 4.5", coding "GPT-5.
     3-Codex", hybrid "Claude Sonnet 4.5"), agents array, skills array, instructions array, optional contextSources and contextNotes.
67
68   Markdown body has matching tables: Project table, Context Sources (Documentation URLs + Additional Context), one Domain table per detected domain, Model Tiers (Tier -
     Model - Agents), Agent Roster table (Agent - Domain - Role - Skills - Tier - Model - Activation), Skills table (Skill - Purpose - Owner - Used By), Instructions table.
69
70   Config Protection Rules: NEVER overwrite during regenerate (source of truth input); CAN be updated by manage-system operations; version bumped on structural updates.
71
72   Sub-section Checkpoint File Contract (adas-generation-progress.md). YAML format with: status (in-progress/completed/failed), startedAt, lastUpdatedAt, configHash (hash
     of adas-config at start), adasVersion "2.1", lastCompletedStep (0-8 or -1), failedStep (or null), failureReason (or null), steps array. Each step entry: step number,
     name, status (pending/completed/skipped/failed), completedAt, filesWritten array.
73
74   Step definitions (0 through 8 per Part 1 Section F).
75
76   Checkpoint Rules: Created at Step 0; updated after each step; deleted after Step 8 success; preserved on failure for at-adas resume; Steps 0 and 0.5 always re-run on
     resume.
77
78   Sub-section Validation Report Contract. 17 checks V-01 through V-17. Report format: project summary, total checks, passed count, failed count, warnings count, per-check
     rows (ID, status pass/fail/warn, description, failure details).
79
80   ---
81
82   ## Section N. universal slash agents slash (8 reference templates)
83
84   ### N1. orchestrator.base.md
Image 6 — REGENERATE-ADAS-PLAN-PART2.md
1    # Regenerate ADAS - Part 2 of 3 – Universal Reference Templates (OCR-Friendly Spec)
17   ## Section M. universal slash docs slash schema-definitions.base.md (SINGLE SOURCE OF TRUTH)
32   DomainType enum values: frontend, backend-api, database, infrastructure, cli, library, data-pipeline, mobile, universal, migration, conditional.
33
34   TierType enum values: analytical (Claude Sonnet 4.5; planning/coord/review), coding (GPT-5.3-Codex; file creation/modification), hybrid (Claude Sonnet 4.5 default,
35   user-overridable).
36
37   ActivationType enum values: always, on-demand, conditional.
38
39   Sub-section Skill Definition Schema. Fields: name (string, kebab-case), purpose (string, one-line), owner (string, single agent responsible for execution, added in 2.
     1), usedBy (string array, all agents that can invoke - owner plus consumers).
40
     Ownership rules: Every skill has exactly one owner; other agents in usedBy are consumers that invoke by handing off to owner; if no clear single owner, the agent whose
     domain most closely matches the skill purpose becomes owner.
41
42   Sub-section Instruction Definition Schema. Fields: name (string, kebab-case e.g. error-handling-pattern), description (string), basedOn (optional, reference template
     name).
43
44   Sub-section Project Profile Schema. Core config: projectName, projectIntent (IntentType: migration, new-development, enhancement, version-upgrade, infrastructure,
     other), domains (array), languages (array), outputRoot, memoryRoot, targetRoot.
45
     Optional Context Sources block: contextSources is an array of ContextSource objects (label, url, notes, type one of documentation/style-guide/api-spec/architecture/
     example-repo/other, fetched boolean, keyPoints array). contextNotes is an object with string fields: architecture, codingStandards, apiSpecs, componentPatterns, auth,
46   testing, other.
47
48   Sub-section Domain Detail Schemas (only included if domain detected):
49   - Frontend: framework, language, buildTool, router, designSystem, stateManagement, stylingApproach, componentPath, pagePath, hookPath.
50   - Backend API: framework, language, apiStyle (REST/GraphQL/gRPC), orm, authStrategy, srcRoot, routesPath, servicesPath.
51   - Database: engine, migrationTool, schemaPath, seedPath.
52   - Infrastructure: containerRuntime, orchestrator, iac, cicd, configPaths.
53   - CLI: entryPoint, argParser.
54   - Library: packageManager, entryPoint, publishTarget.
55   - Testing (cross-domain): frameworks array, libraries array, mockFramework, coverageTool.
56   - Legacy (migration only): appName, root, framework, language, viewExtension.
57
58   Sub-section Memory File Contract. Table of file - path - created by - written by - read by:
59   - context.md - memoryRoot/context.md - generate-project-system Step 5 - scan-repo-context skill - All agents
Image 7 — REGENERATE-ADAS-PLAN-PART2.md
1    # Regenerate ADAS - Part 2 of 3 – Universal Reference Templates (OCR-Friendly Spec)
2
3    Read Part 1 first. This part covers all files under dot github slash templates slash generation slash universal slash.
4
5    The universal subtree:
6    - agents slash : orchestrator, batch-manager, initiator, legacy-analyzer, repo-context, review, task-planner, upgrade-planner (8 files)
7    - skills slash : scan-repo-context, read-memory, write-memory, manage-batch, merge-staged-fragments, analyze-requirements, analyze-legacy-page, analyze-upgrade,
       component-reuse-check, generate-micro-tasks (10 files)
8    - prompts slash : scan-repo-context, generate-tasks, implement-feature, document-legacy-module, migrate-page (5 files)
9    - docs slash : adas-config, GETTING_STARTED, quickReference, AGENT-SKILL-SYSTEM-GUIDE, schema-definitions (5 files)
10   - templates slash memory slash : context, patterns, lessons, decisions, component-usage, page-template, batch-state, batch-context-brief (8 files)
11   - templates slash tasks slash : manifest, scaffold-tasks, api-hooks-tasks, ui-routing-tasks, tests-tasks, upgrade-spec (6 files)
12
13   All files end with dot base dot md (the suffix marks them as reference templates). Curly-brace placeholders like double-curly WORK_UNIT double-curly are legacy
     artifacts; in v2 they are illustrative only - the LLM composes real content at generation time.
14
15   ---
16
17   ## Section M. universal slash docs slash schema-definitions.base.md (SINGLE SOURCE OF TRUTH)
18
19   Heading: ADAS Schema Definitions. Subheading: Single source of truth for all data structures shared between ADAS components. Version 2.1.
20
21   Sub-section Agent Definition Schema. Used by adas.agent.md, setup-full-team.md, setup-custom-agent.md, generate-project-system.md.
22
23   Field list:
24   - name - string - required - kebab-case (e.g., code, test-frontend, legacy-analyzer)
25   - role - string - required - one-line description
26   - domain - DomainType - required
27   - skills - string array - required - default empty
28   - modelTier - TierType - required - auto-assigned (added in 2.1)
29   - model - string - required - resolved string (added in 2.1)
30   - activation - ActivationType - required - default always (added in 2.1)
31
32   DomainType enum values: frontend, backend-api, database, infrastructure, cli, library, data-pipeline, mobile, universal, migration, conditional.
33
     TierType enum values: analytical (Claude Sonnet 4.5; planning/coord/review), coding (GPT-5.3-Codex; file creation/modification), hybrid (Claude Sonnet 4.5
34   user-overridable).