# Architecture

## Pattern Overview

**Overall:** Artifact-chain document planning project with a Goal-Structured Delivery (GSD) framework

**Key Characteristics:**
- Artifact sequence produces BRD -> PRD -> journey maps -> Google Stitch UI screen prompts in lockstep
- GSD framework provides state tracking, requirements definition, roadmap sequencing, and research artifact management
- All planning artifacts anchor to source evidence in `Justo_CP_App_Business_Brief.md` and the `docs/` vendor proposals
- Confidence-tagged claims (`[high]`, `[moderate]`, `[low]`) separate document facts, market inference, and open assumptions
- No application source code lives in this repo — it is a planning-only project

## Layers

**Source Evidence Layer:**
- Purpose: Grounds all planning claims in vendor proposals, SOWs, and business analysis
- Location: `docs/` and `Justo_CP_App_Business_Brief.md`
- Contains: PDF vendor proposals from Auum, TSPL/Triazine, I9/Indexnine; Manthan project SOWs; business brief with market research and external references
- Depends on: Nothing within the repo (externally sourced documents)
- Used by: BRD draft, PRD draft, research artifacts

**Extraction Layer:**
- Purpose: Makes PDF/Word proposal content machine-readable for reference and search
- Location: `.tmp_doc_extract/`
- Contains: Plain-text extracts (`.txt`), flow analyses (`.flow.txt`), and normalized versions (`.norm.txt`) of each source document; a `manifest.json` tracks processed files
- Depends on: `docs/` source documents
- Used by: Planning agents (not exposed as final deliverables)

**Planning Framework Layer (GSD):**
- Purpose: Tracks project state, requirements, roadmap, and research artifacts for the artifact-generation workflow
- Location: `.planning/`
- Contains: `PROJECT.md` (scope, constraints, decisions), `STATE.md` (current focus, artifact status, next action), `REQUIREMENTS.md` (active requirements), `ROADMAP.md` (phase sequencing), `config.json` (workflow settings)
- Depends on: Nothing — defines how the project operates
- Used by: All artifact generation sessions

**Research Layer:**
- Purpose: Captures domain analysis, architectural patterns, technology stack assumptions, feature mapping, and risk analysis
- Location: `.planning/research/`
- Contains: `ARCHITECTURE.md` (BRD structure pattern and business architecture layers), `STACK.md` (target tech ecosystem and evidence standards), `FEATURES.md` (capability mapping), `PITFALLS.md` (risk patterns), `SUMMARY.md` (research synthesis)
- Depends on: Source Evidence Layer and external market research
- Used by: BRD and PRD drafts

**Artifact Chain Layer:**
- Purpose: Produces the four sequential planning deliverables that form the project output
- Location: Project root
- Contains: `Justo_CP_App_BRD_Draft.md` (business requirements), `Justo_CP_App_PRD.md` (product requirements), `Justo_CP_App_Journey_Maps.md` (persona-wise journey maps), `Justo_CP_App_UI_Stitch_Prompts.md` (Google Stitch-ready UI screen prompts)
- Depends on: Each artifact depends on the prior one in the sequence; all depend on Source Evidence and Research layers
- Used by: Stakeholder review; Stitch MCP tool for screen generation

**Tooling Layer:**
- Purpose: Configures the OpenCode agent toolchain used for artifact generation
- Location: `.opencode/`
- Contains: `package.json` (tooling dependencies), `package-lock.json` (resolved versions), `magic-context/` (Magic Context plugin historian state)
- Depends on: OpenCode runtime
- Used by: All planning sessions

## Data Flow

**Artifact Generation Chain:**

1. Source evidence is collected into `docs/` from external vendor proposals and SOWs — external input
2. Business analysis written into `Justo_CP_App_Business_Brief.md` — `Justo_CP_App_Business_Brief.md`
3. Research artifacts synthesized from source evidence and business brief — `.planning/research/*`
4. BRD drafted from business brief, research artifacts, and GSD requirements — `Justo_CP_App_BRD_Draft.md`
5. PRD derived from BRD requirements and decisions — `Justo_CP_App_PRD.md`
6. Persona-wise journey maps traced from PRD personas and functional requirements — `Justo_CP_App_Journey_Maps.md`
7. Google Stitch UI screen prompts generated from journey map rows marked `Build Screen: Yes` — `Justo_CP_App_UI_Stitch_Prompts.md`
8. Stitch screens generated via Stitch MCP tool from prompt files — external (Stitch project `16963605453633474186`)

**Document Extraction Flow:**

1. Source PDF/Word document placed in `docs/`
2. Machine-readable extract written to `.tmp_doc_extract/{filename}.txt`
3. Flow analysis written as `.flow.txt`
4. Normalized version written as `.norm.txt`
5. Manifest updated at `.tmp_doc_extract/manifest.json`

## Key Abstractions

**Three Operating Loops (Business Domain):**
- Purpose: Defines the interconnected business cycles the CP app must support
- Location: `Justo_CP_App_Business_Brief.md`, `Justo_CP_App_BRD_Draft.md`
- Loops: CP Acquisition & Enablement Loop (source -> verify -> onboard -> train -> activate -> retain), Transaction Loop (project discovery -> lead capture -> lead lock -> site visit -> booking -> documents -> payout), Trust Loop (inventory transparency -> auditable lead ownership -> compliance -> payout ledger -> dispute resolution -> performance scoring)

**Launch MVP Trust Loop:**
- Purpose: Defines the v1 scope boundary for the CP app
- Location: `Justo_CP_App_BRD_Draft.md` (Scope Gatekeeper Addendum)
- Flow: Verified CP onboarding -> Project access -> Lead protection -> Site-visit proof -> Booking visibility -> Payout status visibility

**Eleven Personas:**
- Purpose: Defines user archetypes for requirements, journey maps, and screen generation
- Location: `Justo_CP_App_PRD.md` (section 6), `Justo_CP_App_Journey_Maps.md`
- Personas: Justo Leadership, CP Sourcing Head, RM/Sourcing Employee, Sales/Admin Ops, Finance, Developer/Project Team, CP Owner/Org Leader, CP Employee/Agent, CP Telecaller, Buyer/Customer, Compliance/Support

**GSD State Machine:**
- Purpose: Tracks which artifact is current, what is next, and what decisions are pending
- Location: `.planning/STATE.md`
- States: Artifact status per step (Not Started -> Drafted -> Drafted pending stakeholder review -> Complete); workflow state tracked in `STATE.md` under Current Focus

**Scope Gatekeeper:**
- Purpose: Enforces the Launch MVP boundary — every feature and journey map step must pass the trust-loop test
- Location: `Justo_CP_App_BRD_Draft.md` (Scope Gatekeeper Addendum), `Justo_CP_App_PRD.md` (Scope Gatekeeper Addendum)
- Rules: Features not directly improving CP onboarding, project enablement, lead ownership, site-visit proof, booking visibility, payout transparency, or operational control are deferred

**Universal Screen State Contract:**
- Purpose: Every Stitch-generated screen must handle these states
- Location: `Justo_CP_App_Journey_Maps.md` (Universal Screen State Contract section)
- States: Loading, Empty, Error, Access Denied, Offline Cached, Pending Sync, Conflict/Blocked, Audit Visible

**Evidence Confidence Tagging:**
- Purpose: Separates verified facts from inference to support stakeholder review
- Location: All planning artifacts
- Tags: `[high]` (local document fact), `[moderate]` (reasonable inference), `[low]` (directional hypothesis), `[unknown]` (decision not yet available)

## Entry Points

**New reader:**
- Location: `Justo_CP_App_Business_Brief.md`
- Triggers: Anyone needing to understand the CP app strategy and evidence base
- Responsibilities: Provides the strategic foundation, persona map, Manthan baseline, lifecycle analysis, and vendor comparison that all downstream artifacts reference

**Active contributor:**
- Location: `.planning/STATE.md`
- Triggers: Start of every planning session
- Responsibilities: Shows current focus, artifact status, last completed action, and next action

**Stakeholder reviewer:**
- Location: `Justo_CP_App_BRD_Draft.md` and `Justo_CP_App_PRD.md`
- Triggers: Milestone review
- Responsibilities: Contain the business case, requirements, scope gates, and acceptance criteria for stakeholder sign-off

## Error Handling

**Strategy:** Artifact validation is manual via GSD verifier checks. The planning framework uses `"verifier": true` in `.planning/config.json` to enable automated plan-check after each artifact update. Stitch MCP tool failures are captured as known issues (see CONOPS-identified gaps tracked in existing memories and `Justo_CP_App_UI_Stitch_Prompts.md`).

## Cross-Cutting Concerns

**Evidence sourcing:** All claims trace to `Justo_CP_App_Business_Brief.md` or `docs/` source documents. No unsourced assertions in planning artifacts.
**Confidence tagging:** Every non-trivial claim carries a `[high/moderate/low/unknown]` confidence tag per `Justo_CP_App_PRD.md` section 0.
**Formatting:** All artifacts use Markdown. Artifacts are versioned with `Draft version: vX.Y` headers. Indian locale formatting (Rs, lakh/crore, dd/mm/yyyy, +91 phone) throughout.
**Internationalization readiness:** UI prompts in `Justo_CP_App_UI_Stitch_Prompts.md` specify RTL-safe alignment, locale-safe date/currency labels, and text expansion safety for Middle East and ASEAN localization.
**Artifact version correlation:** BRD, PRD, journey maps, and Stitch prompts are kept at the same minor version and reference each other by version number.