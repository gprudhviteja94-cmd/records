Image 1 — REGENERATE-ADAS-PLAN-PART3.md (lines ~47–71)
# Regenerate ADAS – Part 3 of 3 – Domain Reference Templates (OCR-Friendly Spec)
## Section U. frontend slash skills slash (7 reference templates)

48     ### U1. create-component.base.md
49     Purpose: Scaffold a new component file following project conventions. Owner: Code. Inputs: name (PascalCase), targetPath, props list, isPage boolean.

51     Procedure: Step 1 component-reuse-check; Step 2 determine file extension by framework+language (.tsx/.jsx/.vue/.component.ts/.svelte); Step 3 generate skeleton using
       framework-idiomatic pattern with named export, JSDoc/TSDoc header, props interface or defineProps, basic semantic HTML; Step 4 create barrel re-export if folder has
       index; Step 5 if isPage, register route via add-ui-pattern (router-export-pattern instruction). Mark Step 5 completed.

53     ### U2. create-hook.base.md
54     Purpose: Scaffold a custom hook/composable following project state-management conventions. Owner: Code. Inputs: name (use prefix or useResource), purpose (data/state/
       effect/context), dataShape optional.

56     Procedure: Step 1 detect state management; Step 2 generate hook by category – data uses query/mutation patterns of detected library (React Query useQuery/useMutation;
       SWR useSWR; Pinia store; RTK Query endpoint); Step 3 export from hookPath; Step 4 if exposing shared utility add to barrel; Step 5 update component-usage.md hook
       section.

58     ### U3. create-test-file.base.md
60     Purpose: Scaffold a test file colocated with the unit under test. Owner: Test. Inputs: target (component/hook/api), targetPath, testcases array.

62     Procedure: Step 1 detect test framework; Step 2 create __tests__ folder if absent; Step 3 generate test skeleton with describe/it/test, beforeEach setup, render helper,
       role/label queries, behavior-driven assertions; Step 4 mock network at boundary using detected mock framework; Step 5 ensure no testing-library-no-debug warnings.

63     ### U4. add-api-endpoint.base.md
64     [line 65 blank]
65     Purpose: Add a new endpoint to the project API client layer with mock handler and hook(s). Owner: API. Inputs: resource, method, path, requestType optional,
       responseType optional.

66     Procedure: Step 1 add path constant to API endpoints constants file; Step 2 create service function in apiPath/resource-service file (uses detected API client wrapper);
       Step 3 create mock handler in mockPath/resource-handlers; Step 4 register handler in mock barrel; Step 5 generate data hook (query for GET, mutation for POST/PUT/
       DELETE); Step 6 update context.md API endpoints section with method, path, status (Backend/Mock or Mock Only).

68     ### U5. add-ui-pattern.base.md
69     Purpose: Implement a documented UI pattern (filter panel, grid, dialog, form, search page). Owner: UI. Inputs: pattern (name from instructions), targetComponent, props.

71     Procedure: Step 1 read the corresponding instruction file (e.g., filter-panel-pattern); Step 2 component-reuse-check for sub-components needed; Step 3 c[cut off]
Image 2 — REGENERATE-ADAS-PLAN-PART3.md (lines ~68–95)
## Section U. frontend slash skills slash (7 reference templates)
### U5. add-ui-pattern.base.md

71     Procedure: Step 1 read the corresponding instruction file (e.g., filter-panel-pattern); Step 2 component-reuse-check for sub-components needed; Step 3 compose using
       design-system primitives following the pattern; Step 4 apply styling approach; Step 5 verify accessibility checklist for that pattern (focus trap for dialog, ARIA
       labels for grid, etc.).

73     ### U6. fetch-figma-design.base.md
74     [line 75 blank]
75     Purpose: Fetch a Figma file or node and extract design tokens + component specs. Owner: figma. Inputs: fileKey, nodeId optional.

77     Procedure: Step 1 validate FIGMA_TOKEN; Step 2 curl GET to api.figma.com/v1/files/fileKey or /nodes; Step 3 parse JSON for fills/strokes/typography/effects/auto-layout;
       Step 4 extract color tokens (de-duped hex), spacing tokens (4/8/12/16 etc grid), typography tokens (family, size, weight, line-height); Step 5 write design-extract.md.

78     ### U7. fetch-figma-comments.base.md
79     Purpose: Fetch comment threads on a Figma file for design review context. Owner: figma. Inputs: fileKey. Procedure: curl GET to api.figma.com/v1/files/fileKey/comments,
       group by node, format as Markdown thread list in design-extract.md.

81     ---

83     ## Section V. frontend slash instructions slash (19 reference templates)

85     Brief spec for each. All have description, applyTo glob, and pattern body with do/don't and code-style examples.

87     - api-mock-pattern: mock handlers live in mockPath, register in mock barrel, response shape matches backend, status codes match real API, simulate latency optional.
88     - authentication-pattern: auth state stored in detected auth module, expose useAuth or equivalent, protect routes with guard component, token refresh handled centrally.
89     - cascading-dropdown-pattern: parent dropdown value passed as filter to child query, child resets to empty when parent changes, disable child while parent loading.
90     - component-imports: prefer named exports, absolute imports for shared code (configured alias), relative imports within feature folder, no circular imports.
91     - data-fetching-pattern: use state-management library hooks (not raw fetch in components), pass query key array for cache, handle loading/error/empty states explicitly,
       invalidate queries on mutation success.
92     - dialog-pattern: use design-system Dialog primitive, manage open state in parent, focus first input on open, restore focus on close, esc closes, click outside optional
       behavior, form submit closes only on success.
93     - error-handling-pattern: catch network errors at hook layer, expose typed error object to component, display ErrorBanner with retry, log to monitoring if available,
       never silently swallow.
94     - export-pattern: each feature folder has barrel index file exporting public API only, internal components/utils not exported, pages re-exported from feature barrel.
95     - filter-panel-pattern: filters in left or top panel, debounce text inputs 300 ms, dropdown options come from data hook, reset button clears all filters, applied
       filters shown as chips.
Image 3 — REGENERATE-ADAS-PLAN-PART3.md (lines ~94–120)
## Section V. frontend slash instructions slash (19 reference templates)

94     - export-pattern: each feature folder has barrel index file exporting public API only, internal components/utils not exported, pages re-exported from features barrel.
95     - filter-panel-pattern: filters in left or top panel, debounce text inputs 300 ms, dropdown options come from data hook, reset button clears all filters, applied
       filters shown as chips.
96     - form-validation-pattern: use detected form library (react-hook-form / VeeValidate / Angular Reactive Forms / Felte), schema validation with Zod/Yup/Valibot, inline
       error messages below fields, submit disabled while invalid, server errors mapped to fields.
97     - grid-pattern: use design-system DataGrid, columns memoized, server-side pagination/sort when dataset > 100 rows, row selection optional, row click navigates to detail.
98     - loading-state-pattern: Spinner for short loads, Skeleton for content placeholders, full-page PageLoading for initial render, optimistic update for mutations when safe.
99     - page-structure-pattern: PageHeader at top with title and primary action, FilterPanel below header, main content (Grid/Form/Detail) in center, status bar at bottom
       optional.
100    - performance-pattern: lazy-load route components, memoize expensive computations, virtualize grids over 200 rows, debounce search input, avoid prop drilling (use
       context or state library).
101    - rbac-pattern: read privilege keys from auth module, wrap protected UI in AuthGuard component, hide vs disable based on key type, server still enforces (UI is
       convenience).
102    - router-export-pattern: route definitions live in routes folder, lazy import page components, register guard component per protected route, breadcrumb config optional.
103    - search-page-pattern: combines FilterPanel + Grid + CreateDialog; URL params reflect filters for shareable links; back button restores state.
104    - terminal-usage-pattern: use detected package manager commands (npm/pnpm/yarn/bun); never edit lock files by hand; respect node version in dot nvmrc.
105    - testing-patterns: tests colocated with code; describe block per component/hook; arrange-act-assert; mock at network boundary; deterministic data.

106    [blank]
107    ---

109    ## Section W. frontend slash scripts slash (2 reference templates – JavaScript)

111    ### W1. validate-page.base.js
112    Node.js script run after Scaffold wave. Walks pagePath/PageName folder, verifies: PageName main file exists with named export; barrel index file exists and re-exports
       the page; folder has components subfolder; styles file present (matching styling approach); auth guard wraps top-level render when RBAC keys exist. Exit code 0 pass; 1
       fail with list of missing items.

114    ### W2. validate-route.base.js
115    Node.js script run after UI+Routing wave. Reads router config file, verifies the new route path is registered, the page component is lazy-imported, guard component is
       wired when RBAC keys present, no duplicate routes. Exit code 0 pass; 1 fail with details.

117    ---

119    ## Section X. frontend slash templates slash code-snippets.base.md
120    [blank]
Image 4 — REGENERATE-ADAS-PLAN-PART3.md (lines ~119–148)
## Section X. frontend slash templates slash code-snippets.base.md

121    Reference snippet library used by Code/UI/API/Test agents. Sections per stack:
122    - Page Component skeleton (loading/error/data, with PageHeader + FilterPanel + Grid)
123    - API Hook skeleton (useQuery with queryKey array, params, error handling)
124    - Mutation Hook skeleton (useMutation with invalidate on success, optimistic update example)
125    - Mock Handler skeleton (MSW handler returning paged response)
126    - Dialog skeleton (controlled open state, form inside, submit closes on success)
127    - Filter Panel skeleton (debounced inputs, dropdown from data hook, reset button)
128    - Grid skeleton (memoized columns, server pagination, row click navigation)
129    - Test skeleton (component smoke, interaction with userEvent, hook with renderHook).

131    For each, include both TypeScript and JavaScript variants and adapt imports to the detected design system. The base file holds React+Salt DS as canonical example; the
       generator transforms imports for other stacks.

133    ---

135    ## Section Y. backend slash agents slash (3 reference templates)

137    ### Y1. routes.base.md
138    Frontmatter: name routes; description "Backend route/endpoint handler agent for Express/FastAPI/Spring Boot/Django/Rails"; model "GPT-5.3-Codex (copilot)";
       user-invokable true; handoffs to services, middleware, test.

140    Body: Role – own the HTTP boundary. Defines route handlers, request validation, response shape, status codes. Framework conditionals:
142    - Express/Node: routes in routesPath as functions per resource, use middleware chain, Joi/Zod for validation, async error middleware
143    - FastAPI/Python: APIRouter per resource, Pydantic models for request/response, status codes via fastapi.status, dependency injection for auth/db
144    - Spring Boot/Java: RestController per resource, DTO records for request/response, Bean Validation annotations, ResponseEntity for typed responses, ControllerAdvice for
       errors
144    - Django REST: ViewSets with serializers, URL routing via router register, permission classes
145    - Rails: controllers with strong params, before_action filters, jbuilder/serializer for response

147    Conventions: REST naming (GET /resources for list, /resources/id for one, POST /resources for create, PUT /resources for update, DELETE /resources/id, query params
       (backend variant), read-memory, write-memory.

148    ### Y2. [cut off]
Image 5 — REGENERATE-ADAS-PLAN-PART3.md (lines ~148–176)
## Section Y. backend slash agents slash (3 reference templates)

149    ### Y2. services.base.md
150    Frontmatter: name services; description "Backend business logic/service layer agent"; model "GPT-5.3-Codex (copilot)"; user-invokable true; handoffs to routes, schema,
       test.

152    Body: Role – own business logic separated from transport. Services receive validated DTOs from routes, call data layer (ORM/repository), enforce business rules, return
       at service method (not in route); no HTTP concerns leak in (no req/res objects). Skills: dependency injection (FastAPI Depends / Spring @Service / NestJS @Injectable /
       Express factory); transaction boundaries at service method. Skills: add-service, read-memory, write-memory.

154    ### Y3. middleware.base.md
155    Frontmatter: name middleware; description "Backend cross-cutting middleware agent for auth, CORS, error handling, logging, rate limiting"; model "GPT-5.3-Codex (copilot)
       "; user-invokable true; handoffs to routes.

157    Body: Role – own cross-cutting concerns. Auth strategies (JWT bearer / session cookie / API key / OAuth2); error handler that maps exceptions to status codes; request
       logger with correlation IDs; CORS allow-list; rate limiter; request size limits; PII redaction in logs.

       Framework conditionals:
160    - Express: app.use middleware chain
161    - FastAPI: middleware via add_middleware, dependencies via Depends
162    - Spring Boot: Filter or HandlerInterceptor + WebSecurityConfigurerAdapter; @ControllerAdvice for global exceptions
163    - Django: MIDDLEWARE setting + middleware classes
164    - Rails: Rack middleware + before_action chains

166    Skills: add-middleware, read-memory, write-memory.

168    ---

170    ## Section Z. database slash agents slash (3 reference templates)

172    ### Z1. schema.base.md
173    Frontmatter: name schema; description "Database schema definition agent for ORM models / DDL / migration definitions"; model "GPT-5.3-Codex (copilot)"; user-invokable
       true; handoffs to migration, services, test.

175    Body: Role – own schema definitions. ORM conditionals:
176    - Prisma: schema.prisma file, model blocks with field types, relations, indexes; run prisma generate after edit
Image 6 — REGENERATE-ADAS-PLAN-PART3.md (lines ~172–199)
## Section Z. database slash agents slash (3 reference templates)
### Z1. schema.base.md

176    - Prisma: schema.prisma file, model blocks with field types, relations, indexes; run prisma generate after edit
177    - SQLAlchemy: declarative_base models, Column types, relationship(); use Alembic for migrations
178    - TypeORM: @Entity classes with @Column decorators, relations; use TypeORM migrations
179    - JPA/Hibernate: @Entity classes with @Column/@JoinColumn/@OneToMany; Flyway/Liquibase for migrations
180    - Django ORM: models.Model with field classes; makemigrations
181    - ActiveRecord/Rails: migrations as Ruby DSL; schema.rb generated

183    Conventions: snake_case columns, plural table names, primary key id (uuid preferred over autoincrement), created_at/updated_at timestamps, soft delete via deleted_at
       when needed, foreign keys with ON DELETE CASCADE/RESTRICT explicit, unique constraints named, indexes for foreign keys and frequent WHERE columns. Skills:
       define-schema, read-memory, write-memory.

185    ### Z2. migration.base.md
186    Frontmatter: name migration; description "Database migration scripting agent ensuring safe forward/backward schema evolution"; model "GPT-5.3-Codex (copilot)";
       user-invokable true; handoffs to schema, seed.

188    Body: Role – own migration lifecycle. Tool conditionals (Prisma Migrate / Alembic / TypeORM / Flyway / Liquibase / Django / Rails). Safety rules: never edit applied
       migrations; new migration per change with descriptive name; reversible when possible (provide down); for renames use two-step (add new column, copy, drop old) on large
       tables; for not-null on existing table use default first then drop default; long-running migrations executed online (concurrent index where supported); always test on
       staging copy first. Skills: create-migration, read-memory, write-memory.

190    ### Z3. seed.base.md
191    Frontmatter: name seed; description "Database seed data agent for dev/test fixtures and reference data"; model "GPT-5.3-Codex (copilot)"; user-invokable true; handoffs
       to schema.

193    Body: Role – produce idempotent seed scripts. Seed types: reference data (always present countries/currencies), dev fixtures (deterministic, used by tests). Idempotency rules: upsert by natural key; safe to run multiple times; never delete user-created data. Tool conditionals match the ORM
       (Prisma seed.ts / Alembic data migration / Django fixtures or factory_boy / Rails seeds.rb + fixtures). Skills: create-seed, read-memory, write-memory.

195    ---

197    ## Section AA. infrastructure slash agents slash (3 reference templates)

199    ### AA1. ci-cd.base.md
       Frontmatter: name ci-cd; description "CI/CD pipeline agent for GitHub Actions / GitLab CI / Azure Pipelines / CircleCI workflows"; model "GPT-5.3-Codex (copilot)";
Image 7 — REGENERATE-ADAS-PLAN-PART3.md (lines ~197–236)
## Section AA. infrastructure slash agents slash (3 reference templates)

197    ### AA3. iac.base.md
222    Frontmatter: name iac; description "Infrastructure as Code agent for Terraform / CloudFormation / Pulumi / Bicep / CDK modules"; model "GPT-5.3-Codex (copilot)";
       user-invokable true; handoffs to ci-cd, containerization.

225    Body: Role – own cloud resource definitions. Tool conditionals:
226    - Terraform: HCL modules with inputs/outputs/locals, remote state backend (S3+DynamoDB / Azure Storage / GCS), provider version pinning, workspaces or directories per
       env, terraform fmt + validate + tflint in CI
227    - CloudFormation: YAML templates with Parameters/Resources/Outputs, nested stacks, change sets before apply
228    - Pulumi: TypeScript/Python programs, stack per env, secrets via pulumi config set --secret
229    - Bicep: modules with @description and @allowed decorators, what-if before deploy
230    - CDK: TypeScript/Python stacks, constructs by layer, cdk diff before deploy

231    Conventions: IAM least privilege (no wildcard Action plus wildcard Resource); encryption at rest enabled by default (KMS where supported); secrets in dedicated service
       (Secrets Manager / Key Vault / Secret Manager) referenced not embedded; tagging policy (env, owner, cost-center); network defaults private (no 0.0.0.0/0 ingress except
       documented); state file never committed; module versioning via git tag or registry. Skills: create-module, create-stack, read-memory, write-memory.

233    ---

235    End of Part 3 and end of regeneration plan. After Copilot reads all 3 parts, it has a complete blueprint to reconstruct the tsp-adas project. Reconstruction order: Part
       1 Sections A and B first (folder skeleton + main agent), then Part 1 Sections C through H (skills), then Part 1 Section I (root docs and tasks), then Part 2 Section M
       Part 1 Section H once complete.
       (schema definitions), then Part 2 Sections N through S (universal references), then Part 3 Sections T through AA (domain references). Validate with the 17 checks in

236    [end of file]
That's the complete transcription across all 10 images. The document is a 3-part ADAS (Agent-Driven Autonomous System) regeneration plan spec, covering frontend skills/instructions/scripts/templates (Parts 1 & 3) and universal + backend/database/infrastructure agent reference templates (Parts 2 & 3).


Image 5 — REGENERATE-ADAS-PLAN-PART3.md
1    # Regenerate ADAS - Part 3 of 3 – Domain Reference Templates (OCR-Friendly Spec)
2
3    Read Part 1 and Part 2 first. This part covers files under dot github slash templates slash generation slash for each detected domain. ADAS copies only the relevant
     subtrees based on detected domains; the LLM composes final agents at generation time using these references.
4
5    Domains covered: frontend, backend, database, infrastructure. Each is conditional (only included if detected in the target repo).
6
7    All files use the dot base dot md suffix (scripts use dot base dot js).
8
9    ---
10
11   ## Section T. frontend slash agents slash (5 reference templates)
12
13   ### T1. code.base.md
14   Frontmatter: name code; description "Frontend code implementation agent for React/Vue/Angular/Svelte components, hooks/composables, and page-level wiring"; model "GPT-5.
     3-Codex (copilot)" (coding tier); agents [ui]; user-invokable true; argument-hint "implement UserGrid component"; handoffs to ui, api, test.
15
16   Body: Role - frontend developer producing production-ready component code following project conventions. Reads context.md + patterns.md + component-usage.md before
     writing; runs component-reuse-check before creating new shared components; uses framework-idiomatic patterns (React hooks, Vue Composition API, Angular signals, Svelte
17   5 runes). Skills available: create-component, create-hook, component-reuse-check, read-memory, write-memory.
18
     Framework conditionals: when framework is React produce TSX with named exports; Vue produce SFC; Angular produce standalone components with signals when version 17+;
19   Svelte produce .svelte files with runes when version 5+.
20
21   ### T2. api.base.md
     Frontmatter: name api; description "Frontend API integration agent for fetch/axios endpoint wiring and state-management hook creation"; model "GPT-5.3-Codex (copilot)";
22   agents empty; user-invokable true; handoffs to code, test.
23
     Body: Role - own the data layer. Creates API service functions using the detected API client (axios/fetch/ky); creates mock handlers using detected mock framework (MSW/
     Mirage); registers mocks in mock barrel file. Skills: add-api-endpoint, create-hook, read-memory, write-memory.
24
25   ### T3. ui.base.md
     Frontmatter: name ui; description "UI specialist for design-system component composition, layout, accessibility, and visual consistency"; model "GPT-5.3-Codex (copilot)
26   "; agents empty; user-invokable true; handoffs to code.
27
28   Body: Role - design-system expert. Implements UI patterns using the detected design system; runs component-reuse-check in design-system-specific order (Salt DS: project
Image 6 — REGENERATE-ADAS-PLAN-PART3.md
1    # Regenerate ADAS - Part 3 of 3 – Domain Reference Templates (OCR-Friendly Spec)
11   ## Section T. frontend slash agents slash (5 reference templates)
25   ### T3. ui.base.md
27
28   Body: Role - design-system expert. Implements UI patterns using the detected design system; runs component-reuse-check in design-system-specific order (Salt DS: project
     shared then UIPax/Pepper then Salt DS Core then Salt DS Lab then create new; MUI: project shared then MUI Core then MUI X then MUI Lab then create new; Chakra: project
     needed, keyboard navigation, focus management); applies the detected styling approach (CSS Modules / Tailwind / styled-components / Emotion / vanilla-extract / Salt CSS
     tokens). Skills: add-ui-pattern, component-reuse-check, read-memory, write-memory.
29
30   ### T4. test.base.md
31   Frontmatter: name test; description "Frontend testing specialist for component, hook, and integration tests"; model "GPT-5.3-Codex (copilot)"; agents empty;
32   user-invokable true; handoffs to code (when bugs found).
33
     Body: Role - write deterministic behavior-driven tests using the detected test framework (Vitest/Jest) + Testing Library (React/Vue/Angular/Svelte adapter). Test types:
     component smoke (renders without crash), component interaction (user events), hook unit (renderHook), API function (mocked fetch). Conventions: queries by role/label/
     text first then by test-id; mock the network layer not the hook; avoid testing implementation details; one assert per behavior. Skills: create-test-file, read-memory,
34   write-memory.
35
     Framework adaptation: React uses Testing Library + Vitest/Jest; Vue uses Vue Test Utils + Vitest; Angular uses TestBed + Karma/Jest; Svelte uses Svelte Testing Library
36   + Vitest.
37
38   ### T5. figma.base.md
     Frontmatter: name figma; description "Figma design extraction specialist for fetching design specs, component metadata, and design tokens via Figma REST API"; model
38   "Claude Sonnet 4.5 (copilot)" (analytical - design interpretation); agents empty; user-invokable true; activation on-demand; handoffs to ui.
39
40   Body: Role - on-demand Figma fetcher. Uses curl (NOT npm packages) to call Figma REST API endpoints (files, nodes, images, comments). Requires FIGMA_TOKEN env var.
     Skills: fetch-figma-design, fetch-figma-comments, write-memory. Output: design-extract.md in memoryRoot with component specs, color tokens, spacing tokens, typography
41   tokens, comment threads.
42
43   ---
44
45   ## Section U. frontend slash skills slash (7 reference templates)
46
47   Each starts with the skill disclaimer paragraph.
48   ### U1. create-component.base.md
Image 7 — REGENERATE-ADAS-PLAN-PART3.md
1    # Regenerate ADAS - Part 3 of 3 – Domain Reference Templates (OCR-Friendly Spec)
197  ## Section AA. infrastructure slash agents slash (3 reference templates)
199  ### AA1. ci-cd.base.md
200  Frontmatter: name ci-cd; description "CI/CD pipeline agent for GitHub Actions / GitLab CI / Azure Pipelines / CircleCI workflows"; model "GPT-5.3-Codex (copilot)";
     user-invokable true; handoffs to containerization, iac.
201
202  Body: Role - own pipeline definitions. Pipeline conditionals:
203  - GitHub Actions: dot github slash workflows slash YAML files, jobs with matrix strategy, reusable workflows, OIDC for cloud auth, action pinning by SHA for security
204  - GitLab CI: dot gitlab-ci.yml stages and jobs, includes, rules with if conditions
205  - Azure Pipelines: azure-pipelines.yml with stages/jobs/steps, templates for reuse
206  - CircleCI: dot circleci slash config.yml with workflows and orbs
207
208  Standard stages: install (with cache), lint, test (with coverage), build (artifacts), security scan (SAST/dep scan), publish (registry/artifact), deploy (env-gated with
     approval). Conventions: caching by lock-file hash; secrets via OIDC or vault not raw secrets; fail fast on lint/test; artifact retention 30 days; deploy requires PR
     merged to main + manual approval for prod. Skills: create-workflow, read-memory, write-memory.
209
210  ### AA2. containerization.base.md
     Frontmatter: name containerization; description "Container build agent for Docker/Podman images and Compose/Kubernetes manifests"; model "GPT-5.3-Codex (copilot)";
211  user-invokable true; handoffs to ci-cd, iac.
212
213  Body: Role - own image builds and local orchestration. Multi-stage Dockerfile templates per language:
214  - Node: stage 1 deps with npm ci or pnpm install with lockfile; stage 2 build (compile TS / vite build / next build); stage 3 runtime on node:lts-slim or distroless
     with non-root user; copy only dist + node modules production
215  - Python: stage 1 wheels with pip install --target; stage 2 runtime on python slim with non-root user; uvicorn/gunicorn entrypoint
216  - Java: stage 1 maven/gradle build; stage 2 runtime on eclipse-temurin jre slim with non-root user; java -jar entrypoint
217  - Go: stage 1 build with CGO_ENABLED=0 static binary; stage 2 distroless or scratch
218
219  Conventions: pin base image by digest in prod, healthcheck instruction, non-root USER, COPY only what is needed, dot dockerignore to exclude node_modules/dist/secrets,
     layer ordering for cache hit (deps before code). Compose: services per process, named volumes for persistent data, env via env_file, depends_on with healthcheck
     condition. Kubernetes: Deployment + Service + ConfigMap + Secret (separate from manifest), resource requests/limits, probes (liveness/readiness/startup), HPA when
     applicable. Skills: create-dockerfile, create-compose, create-k8s-manifest, read-memory, write-memory.
220
221  ### AA3. iac.base.md
222  Frontmatter: name iac; description "Infrastructure as Code agent for Terraform / CloudFormation / Pulumi / Bicep / CDK modules"; model "GPT-5.3-Codex (copilot)";
     user-invokable true; handoffs to ci-cd, containerization.
223
224  Body: Role - own cloud resource definitions. Tool conditionals: