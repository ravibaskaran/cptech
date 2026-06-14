# Codebase Structure

## Directory Layout

```
cptech/
├── .githooks/                  # Git hooks for local automation
├── .opencode/                  # OpenCode agent toolchain
│   └── magic-context/          # Magic Context plugin historian state
├── .planning/                  # GSD planning framework (state, requirements, roadmap)
│   └── research/               # Domain and technology research artifacts
├── .tmp_doc_extract/           # Machine-readable extracts from vendor proposals
├── docs/                       # Source vendor proposals and Manthan SOWs
├── AGENTS.md                   # Agent runtime instructions
├── ARCHITECTURE.md             # System architecture documentation
├── Justo_CP_App_BRD_Draft.md   # Business Requirements Document (artifact 1)
├── Justo_CP_App_Business_Brief.md  # Strategic business analysis and evidence base
├── Justo_CP_App_Journey_Maps.md    # Persona-wise journey maps (artifact 3)
├── Justo_CP_App_PRD.md            # Product Requirements Document (artifact 2)
├── Justo_CP_App_UI_Stitch_Prompts.md  # Google Stitch UI screen prompts (artifact 4)
└── STRUCTURE.md                 # Codebase structure documentation
```

## Directory Purposes

**.githooks:**
- Purpose: Local git hook scripts for workflow automation
- Contains: `post-commit` hook that attempts to push the current branch to origin after each successful commit
- Key files: `.githooks/post-commit`

**.opencode:**
- Purpose: Configuration and tooling state for the OpenCode agent environment
- Contains: Tooling dependency manifest (`package.json`, `package-lock.json`), Magic Context historian database and compartment storage
- Key files: `.opencode/package.json`, `.opencode/package-lock.json`, `.opencode/magic-context/`

**.planning:**
- Purpose: Goal-Structured Delivery (GSD) planning framework that tracks project state, active requirements, roadmap, and configuration
- Contains: Project definition (`PROJECT.md`), session state (`STATE.md`), active requirements (`REQUIREMENTS.md`), phase roadmap (`ROADMAP.md`), workflow configuration (`config.json`)
- Key files: `.planning/PROJECT.md`, `.planning/STATE.md`, `.planning/REQUIREMENTS.md`, `.planning/config.json`

**.planning/research:**
- Purpose: Captures structured research outputs used to inform the BRD and PRD
- Contains: Domain architecture analysis (`ARCHITECTURE.md`), target technology stack (`STACK.md`), capability feature mapping (`FEATURES.md`), risk/pitfall analysis (`PITFALLS.md`), research synthesis (`SUMMARY.md`)
- Key files: `.planning/research/STACK.md`, `.planning/research/ARCHITECTURE.md`, `.planning/research/PITFALLS.md`

**.tmp_doc_extract:**
- Purpose: Intermediate processing output from converting PDF/Word vendor proposals into machine-readable text
- Contains: For each source document: plain-text extract (`.txt`), flow analysis (`.flow.txt`), normalized text (`.norm.txt`), and a `manifest.json` tracking all processed documents
- Key files: `.tmp_doc_extract/manifest.json`

**docs/:**
- Purpose: Source evidence documents — the authoritative vendor proposals and Manthan SOWs that ground all planning artifact claims
- Contains: PDF proposals from Auum, TSPL/Triazine, I9/Indexnine; Manthan SOWs for Phases 1, 2, 2.4, 3
- Key files: `docs/Manthan Proposal IndexNine.docx`, `docs/Auum Justo Proposal CP App.pdf`, `docs/TSPL_Business_Proposal_Justo_AI_CP_Platform.pdf`, `docs/CP tech proposal from I9.pdf`

## Key File Locations

**Entry Points:**
- `Justo_CP_App_Business_Brief.md`: Strategic foundation — the starting point for anyone new to the project
- `.planning/STATE.md`: Session state — the starting point for active contributors

**Artifact chain (in generation order):**
- `Justo_CP_App_BRD_Draft.md`: Business Requirements Document — scope, objectives, personas, lifecycle, vendor gaps, MVP boundary
- `Justo_CP_App_PRD.md`: Product Requirements Document — functional requirements, roles, permissions, UX rules, technical notes, metrics
- `Justo_CP_App_Journey_Maps.md`: Persona-wise journey maps covering 11 personas with universal screen state contracts, cross-persona handoffs, and PRD traceability
- `Justo_CP_App_UI_Stitch_Prompts.md`: Google Stitch-ready screen generation prompts with design system rules, screen specifications, and persona flows

**Configuration:**
- `.planning/config.json`: GSD workflow settings (model profile, research/verifier toggles, branching strategy, PR body templates)
- `.opencode/package.json`: OpenCode tooling dependency manifest
- `.gitattributes`: Git attribute overrides (line endings, diff drivers)
- `.gitignore`: Git ignore patterns

**Agent instructions:**
- `AGENTS.md`: Agent runtime instructions for OpenCode sessions — commit policy, push behavior, hook configuration

**Documentation:**
- `ARCHITECTURE.md`: Architecture overview (layers, data flows, key abstractions, entry points, cross-cutting concerns)
- `STRUCTURE.md`: Codebase structure (directory layout, naming conventions, where to add new content)

## Naming Conventions

**Files (root-level artifacts):** `Justo_CP_App_{Content}_{Type}.md` — Example: `Justo_CP_App_BRD_Draft.md`
**Files (research):** UPPER_SNAKE_CASE with descriptive suffix — Example: `ARCHITECTURE.md`, `FEATURES.md`, `STACK.md`
**Files (planning):** UPPER_SNAKE_CASE — Example: `PROJECT.md`, `STATE.md`, `REQUIREMENTS.md`, `ROADMAP.md`
**Files (extracts):** `{SourceFileName}.{suffix}` — Example: `Auum_Justo_Proposal_CP_App.pdf.txt`, `...flow.txt`, `...norm.txt`
**Directories:** Dot-prefixed for framework/tooling directories (`.planning/`, `.opencode/`, `.githooks/`, `.tmp_doc_extract/`); plain name for evidence directory (`docs/`)

## Where to Add New Content

**This is a planning-only project — no application code lives here. To extend planning artifacts:**

**New planning artifact in the chain:** Create at project root following the naming pattern `Justo_CP_App_{Content}_{Type}.md`. Update `.planning/STATE.md` artifact status table and `.planning/PROJECT.md` requirements/decisions accordingly.

**New research artifact:** Add to `.planning/research/{Topic}.md` — follow the existing format with confidence-tagged claims and source references.

**New source evidence document:** Place in `docs/` as PDF or DOCX. The extraction pipeline in `.tmp_doc_extract/` processes new documents automatically on the next planning session.

**New GSD planning configuration:** Edit `.planning/config.json` for workflow settings, `.planning/PROJECT.md` for scope/constraints, `.planning/REQUIREMENTS.md` for new requirements.

**New Stitch screen prompt:** Add as a new prompt section in `Justo_CP_App_UI_Stitch_Prompts.md` following the existing format: screen list with Vibe, Design System, Connections, Dev-Ready Inputs, and Constraints.

**New integration or architecture decision:** Document in `.planning/research/ARCHITECTURE.md` for domain architecture patterns or `Justo_CP_App_BRD_Draft.md` for business/integration scope.