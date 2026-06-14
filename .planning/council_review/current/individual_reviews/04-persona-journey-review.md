# Personas & Journey Maps Review — Product Architecture Council

## Review Summary

The Journey Maps document (`Justo_CP_App_Journey_Maps.md` v0.5) and PRD Section 6 (`Justo_CP_App_PRD.md` v0.5) together define an ambitious, well-structured persona and journey framework covering 11 personas, 12 cross-persona handoffs, a universal screen state contract, and a consolidated Google Stitch screen inventory. The documents demonstrate strong product thinking, particularly in traceability (every journey step carries a PRD trace), screen state discipline, and clear build/reuse/no-screen guidance for the UI generation pipeline.

However, there is a **critical scope contradiction** between the PRD's MVP simplification (3 personas for Phase 1) and the Journey Maps document, which builds complete journeys and screens for all 11 personas without clearly gating which journeys are MVP vs. deferred. This contradiction is the single biggest issue in the review and must be resolved before development begins.

**Overall Assessment:** Strong foundational work with excellent structural scaffolding, undermined by a major scope alignment gap and several missing edge-case/detail items.

---

## Strengths

### 1. Excellent PRD Traceability [high]
Every journey step in the Journey Maps carries explicit PRD-FR references (e.g., `RM-003` → `PRD-FR-008, PRD-FR-072, PRD-FR-079`). This is exceptionally well-done and rare in early-stage product documents. It creates a direct audit trail from user action → system behavior → requirement.
- **Source:** Journey Maps, all persona tables (lines 96–261)

### 2. Comprehensive Universal Screen State Contract [high]
The 8-state screen contract (Loading, Empty, Error, Access Denied, Offline Cached, Pending Sync, Conflict/Blocked, Audit Visible) is thorough and well-defined with required behavior and applicability rules.
- **Source:** Journey Maps, lines 49–62

### 3. Mature Cross-Persona Handoff Map [high]
The 12 handoffs (HND-001 through HND-012) explicitly define triggering persona, trigger event, receiving persona, target screen, and required UI signal. This is a critical artifact that many product documents miss entirely.
- **Source:** Journey Maps, lines 64–81

### 4. Clear Build/Reuse/No-Screen Guidance [high]
Every journey step is tagged with `Build Screen: Yes`, `Build Screen: Reuse`, or `Build Screen: No`. This directly supports the Google Stitch pipeline and prevents screen proliferation.
- **Source:** Journey Maps, lines 37–47, all persona tables

### 5. Consolidated Screen Inventory with Data Contracts [high]
The Screen Data and State Contract table (lines 313–349) maps each screen to primary data objects, source authority, and must-have states. This is production-grade scaffolding for both UI and API design.

### 6. Persona Screen Bundle Map [high]
The Persona Screen Bundle Map (lines 351–367) explicitly prevents duplicate screen generation by mapping build-specific vs. reuse screens per persona. Well thought-out.

### 7. "Explicitly Not To Generate" Section [high]
Lines 369–378 clearly enumerate what Google Stitch must NOT build (AI calling, microsites, advanced gamification, workforce tracking, full buyer portal). This scope guardrail is essential.

### 8. Google Stitch Prompt Quality [high]
The Stitch prompts (UI_Stitch_Prompts.md) are exceptionally well-structured with vibe descriptions, exact screen lists, design system tokens, connections, dev-ready inputs, and constraints per prompt. These follow a repeatable pattern that should produce consistent outputs.
- **Source:** UI Stitch Prompts, lines 22–197

---

## Critical Issues (Must Fix)

### C1. Massive Scope Contradiction: MVP ≠ Journey Maps Coverage [high]

**The PRD defines 3 MVP personas** (RM/Sourcing Employee, CP Owner/Employee, Buyer/Customer Doc Upload) at PRD Section 6 Persona Summary (line 221–233). The Launch Role Classification (lines 230–233) explicitly states that Leadership, CP Sourcing Head, Sales/Admin Ops, Finance, Developer/Project Team, Telecaller, and Compliance/Support are **"Deferred (Phase 3+)"** and **"Excluded from Phase 1 MVP journey maps and screen generation."**

**However, the Journey Maps document builds full journeys and screens for ALL 11 personas**, including complete Build Screen instructions for deferred personas:
- Justo Leadership: 8 journey steps, all marked `Build Screen: Yes` (lines 102–115)
- CP Sourcing Head: 10 journey steps (lines 117–132)
- Sales/Admin Ops: 5 journey steps (lines 152–162)
- Finance: 5 journey steps (lines 164–174)
- Developer/Project Team: 4 journey steps (lines 176–185)
- CP Telecaller: 8 journey steps (lines 225–238)
- Compliance/Support: 5 journey steps (lines 251–261)

The Persona Coverage Matrix (lines 83–90) partially acknowledges this by stating "All Other Personas: Deferred (Phase 3+), Do not build screens for Phase 1" — but the full journey tables below it directly contradict this by marking everything as `Build Screen: Yes`.

**Impact:** If developers or Google Stitch follow the Journey Maps document literally, they will build 40+ screens for 8 deferred personas, massively exceeding MVP scope. If they follow the PRD classification, they will only build for 3 personas but have no clear guidance on which journey steps to implement first.

**Recommendation:** 
1. Add a `Phase` or `MVP` column to every journey table marking each step as `Phase 1 / Phase 3+`.
2. Alternatively, restructure the Journey Maps document into two clearly separated sections: "MVP Journeys (Build Now)" and "Deferred Journeys (Context Only — Do Not Build)".
3. The Persona Coverage Matrix (lines 83–90) is correct and should be the authoritative gating mechanism, but the journey tables must visually enforce it.

### C2. Buyer/Customer Persona Is Severely Under-Defined for MVP [high]

The PRD classifies the Buyer as an MVP persona with scope limited to "Doc Upload." Yet:

- **PRD Persona Summary (line 225):** Describes them as "Customer applying for underwriting" with JTBD "Submit documents for underwriting, receive accurate project info."
- **PRD Detailed Journey (lines 336–343):** Only 4 journey steps, none of which mention document upload for underwriting. The steps are: Receive project link, Express interest, Confirm visit, Complete KYC/payment.
- **Journey Maps BUY-001 to BUY-004 (lines 240–249):** 4 steps covering project link, interest, visit confirmation, and KYC handoff. Again, no explicit "document upload for underwriting" journey step.

The persona summary says "Submit documents for underwriting," but neither the PRD journey nor the Journey Map contains an actual document upload step for the buyer. The KYC/payment step (BUY-004) simply says "Continues into existing buyer portal."

**Impact:** The one unique MVP function for the Buyer persona (document upload for underwriting) has no journey mapping, no screen definition, and no Stitch prompt. This is a launch-blocking gap.

**Recommendation:**
1. Add a BUY-005 journey step: "Uploads documents for underwriting" with system checks (file type/size, upload queue state, validation), system response (queued/uploaded/validated/rejected), and UI requirement.
2. Add a corresponding Stitch prompt for the Buyer Document Upload screen.
3. Clarify whether this document upload uses the same upload infrastructure as CP onboarding docs (it should, for reuse).

---

## Major Issues (Should Fix)

### M1. Persona Definitions Lack Demographic/Psychographic Context [moderate]

The PRD Persona Summary (lines 221–226) provides Role, JTBD, and Pain Points — but personas lack:
- **Demographics:** Age range, tech savviness, device type (low-end Android?), typical network conditions
- **Psychographic context:** Motivation model, trust level with technology, willingness to adopt new tools
- **Usage context:** When/where they use the app (field, office, home), session frequency, typical session duration
- **Frustrations in current workflow:** More specific than one-line pain points

The Journey Maps do not add persona context either — they jump directly to journey tables.

**Impact:** Without context, design and prioritization decisions are made on assumptions. An RM in a rural Maharashtra field has very different needs from a CP Owner in a Mumbai office.

**Recommendation:** Add a 5–7 line persona card for each MVP persona (RM, CP Owner/Employee, Buyer) with demographics, device/network context, usage patterns, and a "day in the life" paragraph.

### M2. Journey Maps for MVP Personas Lack Emotional Journey Layer [moderate]

The journey tables capture User Action → System Check → System Response → UI Requirement, which is excellent for engineering. However, they completely omit:
- **User emotion/mindset at each step** (anxious, confident, frustrated, relieved)
- **Moments of truth** (where trust is won or lost)
- **Pain intensity** at each step

This is the difference between a "functional journey map" and a "design journey map."

**Source:** All persona journey tables in Journey Maps document.

**Recommendation:** Add an `Emotion / Moment of Truth` column to at least the 3 MVP persona journeys. Example: CPO-005 (Lead Submit) should note "High anxiety — this is the trust moment where CP decides if the app is worth using."

### M3. Offline/Sync Scenarios Are Documented at System Level but Missing from Individual Journeys [moderate]

GLOBAL-003 (line 100) establishes the offline contract. The screen data contract includes sync states. However, individual persona journey steps do not consistently document what happens when that specific step is performed offline:

- **RM-002** (CP Prospecting) mentions offline: "Prospect saved online or queued" ✓
- **CPE-004** (Lead Submit) mentions offline: "Lead returns accepted/conflict/rejected/pending sync/pending review" ✓
- **CPO-006** (Visit Visibility) does NOT mention what happens if the visit scheduling is done offline
- **CPO-003** (Team Control) does NOT mention offline behavior for employee management
- **BUY-001 through BUY-004** do NOT mention offline at all (buyer may have poor connectivity too)

**Impact:** Developers may not implement offline paths for steps where they're not explicitly mentioned but are practically needed (e.g., an RM scheduling a visit in a rural area with poor connectivity).

**Recommendation:** Add an `Offline Behavior` note (even if it's "Not applicable — requires server authority") to each MVP persona journey step.

### M4. Handoff Map Does Not Indicate MVP vs. Deferred Handoffs [moderate]

The Cross-Persona Handoff Map (lines 64–81) defines 12 handoffs. However, many handoffs involve deferred personas:
- HND-001: RM → **CP Sourcing Head**, Compliance (both deferred)
- HND-003: **Compliance** → CP Owner (Compliance deferred)
- HND-004: **Sales/Admin Ops** → CP Owner (Ops deferred)
- HND-006: **Sales/Admin Ops** → CP Owner (Ops deferred)
- HND-009: Booking event from **Manthan** → CP Owner, **Finance** (Finance deferred)
- HND-010: **Finance** → CP Owner (Finance deferred)

**Impact:** Without MVP gating, developers may try to implement handoffs to/from personas that don't exist yet, or worse, leave handoff endpoints dangling.

**Recommendation:** Add a `Phase` column to the handoff map. For deferred handoffs, document the MVP fallback (e.g., "In MVP, compliance review notifications go to RM instead of Compliance persona").

### M5. Journey Gaps — Steps That Don't Lead Anywhere (Dead Ends) [moderate]

Several journey steps reference screens or flows that are outside the persona's own journey and also outside the MVP:

1. **CPO-009** (Support/Audit): "Opens support ticket or audit timeline" → marked `Build Screen: Reuse` but reuses `PRD-FR-060 to PRD-FR-064` screens from the Compliance/Support persona, which is deferred.
2. **CPE-007** (Status Review): References booking/payout visibility but these are view-only. Who creates/updates these? The Finance persona is deferred.
3. **BUY-004** (KYC/Payment): "Continues into existing buyer portal" → `Build Screen: Reuse` with "Handoff screen with safe redirect and status return if available." What if the existing buyer portal doesn't exist or isn't integrated? This is a dead end.

**Recommendation:** For each reuse/handoff step, document what the MVP fallback looks like if the receiving system or persona isn't available yet. Even a "Coming Soon" state is better than a broken link.

---

## Minor Issues (Nice to Fix)

### N1. Inconsistent Journey Step Granularity Across Personas [low]

The Buyer persona has 4 journey steps (BUY-001 to BUY-004). The CP Owner has 13 steps (CPO-001 to CPO-013). The CP Employee has 11 steps. The RM has 11 steps. This imbalance is partly natural (the Buyer has limited in-app scope), but the Buyer steps are also much coarser-grained than other personas.

**Recommendation:** Ensure the Buyer journey steps, especially the MVP doc-upload flow, are broken down to comparable granularity.

### N2. CP Owner and CP Employee Are Bundled in Persona Summary but Split in Journeys [low]

PRD Persona Summary (line 224) groups them as "CP owner / employee" in one row. But the Journey Maps treat them as two separate personas with distinct journeys (CPO-001 to CPO-013 and CPE-001 to CPE-011), distinct home screens, and distinct dashboards. This is correct in the Journey Maps but the PRD summary table conflates them.

**Recommendation:** Split the PRD Persona Summary into two rows: "CP Owner / Org Leader" and "CP Employee / Agent" to match the Journey Maps.

### N3. Stitch Prompts Don't Reference MVP Scope Gate [low]

The UI Stitch Prompts document (lines 22–31) includes global generation rules but does not reference the MVP scope gate from the PRD. Prompts 02 (Leadership), 03 (Sourcing Head), 05 (Sales/Admin Ops), 06 (Finance), 07 (Developer/Project) are for deferred personas but are fully written and ready to generate screens.

**Source:** UI Stitch Prompts, lines 54–176

**Recommendation:** Add a prominent note at the top of the Stitch Prompts document: "For Phase 1 MVP, generate ONLY Prompts 01 (Shared Foundation), 04 (RM), 08 (CP Owner), 09 (CP Employee), and the Buyer prompts. All other prompts are context for Phase 3+."

### N4. Missing Error Recovery Paths in Some Journey Steps [low]

Some journey steps define the happy path and conflict/rejection states but don't describe what happens after an error:
- **RM-003** (Assisted Onboarding): What happens if a document upload permanently fails after max retries?
- **CPO-005** (Lead Submit): What happens if the server is unreachable for extended periods and lock expiry occurs?

**Recommendation:** Add error recovery guidance for the most critical MVP journey steps.

### N5. "Remaining Open Constraints" Section Is Good but Needs Owners and Deadlines [low]

Lines 380–388 list 5 open constraints (lead-lock duration, payout SLA, geofence radius, document file types, buyer data exposure) with "Owner Needed" but no assigned owners or target resolution dates.

**Recommendation:** Assign owners and set a deadline (e.g., "Must be resolved before Stitch prompt generation begins").

---

## Missing Items

### MI1. No Buyer Document Upload Journey or Screen [high]
As detailed in C2, the defining MVP function for the Buyer persona has no journey mapping whatsoever. [Missing evidence]

### MI2. No Persona Cards / Empathy Maps for MVP Personas [moderate]
Standard persona artifacts (empathy map, photo/illustration, quote, context of use) are missing for all personas. [Missing evidence]

### MI3. No Accessibility Journey Considerations [moderate]
Neither the persona definitions nor the journey maps mention accessibility needs (screen reader flows, high-contrast modes, large text). The PRD has PRD-NFR-010 requiring WCAG 2.2 AA, but no journey step accounts for this. [Missing evidence]

### MI4. No First-Time User Experience (FTUX) Journey [moderate]
There is no onboarding/FTUX journey for any MVP persona. What does a new RM see the first time they open the app? What does a CP Owner see before their firm is approved? GLOBAL-001 covers login, but not the guided first experience. [Missing evidence]

### MI5. No Session Timeout / Re-authentication Journey [low]
What happens when a session expires mid-action? No journey step covers this. [Missing evidence]

### MI6. No Multi-Device or Device-Switch Scenario [low]
The PRD mentions Android and iOS. No journey covers what happens when a user switches devices or uses the app on two devices simultaneously. [Missing evidence]

### MI7. No Journey for CP Owner Whose Firm Gets Suspended Mid-Operation [moderate]
CPO-002 covers onboarding, but there's no journey step for what happens when a CP Owner's firm is suspended after activation (during active lead/payout workflows). HND-003 partially covers document rejection but not firm-level suspension during active operations. [Missing evidence]

---

## Recommendations

### R1. Resolve the MVP Scope Contradiction (Priority: Immediate)
The Journey Maps must clearly separate Phase 1 MVP content from Phase 3+ context. The Persona Coverage Matrix is correct but is contradicted by the journey tables. Options:
- **(Preferred)** Add a `Phase` column to all journey tables and the handoff map.
- **(Alternative)** Split the document into two files: `Justo_CP_App_Journey_Maps_MVP.md` and `Justo_CP_App_Journey_Maps_Full.md`.

### R2. Create the Missing Buyer Document Upload Journey (Priority: Immediate)
This is the one unique MVP function for the Buyer persona and has zero documentation. Write BUY-005 with full system checks, response states, and a Stitch prompt.

### R3. Add Persona Context Cards (Priority: Before Design Finalization)
Create 1-page persona cards for the 3 MVP personas with demographics, device/network context, usage patterns, frustrations, and a representative quote (can be synthesized from BRD evidence, clearly tagged as `[low]` confidence).

### R4. Add Offline Behavior Notes to All MVP Journey Steps (Priority: Before Development)
Each MVP journey step should explicitly state its offline behavior, even if it's "Requires server — show error state."

### R5. Gate the Stitch Prompts to MVP Scope (Priority: Before UI Generation)
Add a clear MVP scope note at the top of the Stitch Prompts document indicating which prompts to generate for Phase 1.

### R6. Add FTUX Journeys for MVP Personas (Priority: Before Design)
Create first-time user experience journey steps for RM, CP Owner, and Buyer showing the guided onboarding flow from first app open to first productive action.

### R7. Document MVP Fallbacks for Deferred Handoffs (Priority: Before Development)
For each cross-persona handoff that involves a deferred persona, document the Phase 1 fallback behavior.

---

## Score (out of allocated points)

**Score: 6.0 / 10**

**Justification:**

| Area | Max | Awarded | Rationale |
|---|---|---|---|
| Persona definitions (goals, frustrations, context) | 2.0 | 1.0 | JTBD and pain points present; demographics, psychographics, and context missing. CP Owner/Employee conflated in PRD summary. Buyer persona under-defined. |
| Journey completeness (entry to completion) | 2.0 | 1.5 | Excellent structural coverage for all 11 personas with full action→check→response→UI chains. But Buyer doc upload journey is completely missing, and FTUX journeys don't exist. |
| Handoff documentation | 1.5 | 1.0 | 12 handoffs well-defined with triggering/receiving personas and UI signals. But no MVP gating, no fallback documentation for deferred persona handoffs. |
| Universal Screen State Contract | 1.5 | 1.5 | Complete and well-structured. All 8 states defined with behavior and applicability. No gaps found. |
| MVP scope alignment | 1.5 | 0.5 | Persona Coverage Matrix is correct. But journey tables, handoff map, Stitch prompts, and screen inventory all contradict it by building everything without MVP gating. This is the most critical issue. |
| Edge cases & offline/sync in journeys | 1.5 | 0.5 | Offline covered at system level (GLOBAL-003) and in some journey steps, but inconsistently applied. Error recovery paths, session timeout, device switch, and firm suspension mid-operation are all missing. |

**Total: 6.0 / 10**

The documents show excellent product architecture thinking and rare structural discipline (PRD tracing, screen state contracts, build/reuse tagging). The score is held back primarily by the critical MVP scope contradiction (which would cause massive waste if not resolved), the missing Buyer document upload journey (a launch-blocking gap), and insufficient persona context/edge-case coverage. Fixing C1 and C2 alone would raise the score to 7.5+.
