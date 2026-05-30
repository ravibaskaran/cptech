# Roadmap: Justo CP App Planning

**Created:** 2026-05-30  
**Mode:** Vertical MVP  
**Granularity:** Coarse  
**Project goal:** BRD -> PRD -> Product Roadmap/Phases -> Journey Maps -> UI Screen Specs/Prototype

## Overview

This roadmap produces stakeholder-reviewable artifacts in sequence. Each phase takes the approved output of the previous phase as input and moves the project closer to a vendor-alignment and product-design-ready state.

| # | Phase | Goal | Requirements |
|---|---|---|---|
| 1 | BRD Completion | Finish a decision-grade BRD for stakeholder review | DOC, BUS, MANT, PERS, LIFE, PAIN, CAP, VEND, REV |
| 2 | PRD Definition | Convert approved BRD into product requirements | PRD |
| 3 | Product Roadmap | Convert PRD into product delivery phases | ROAD |
| 4 | Journey Maps | Map personas and workflows across product phases | JOUR |
| 5 | UI Specs/Prototype | Define phase-aligned screen specs and prototype structure | UI |

## Phases

### Phase 1: BRD Completion

**Goal:** Complete the BRD so Justo stakeholders can align on business objectives, personas, lifecycles, pain points, Manthan baseline, vendor gaps, MVP scope, risks, and open decisions.  
**Mode:** mvp

**Requirements:** DOC-01, DOC-02, DOC-03, DOC-04, BUS-01, BUS-02, BUS-03, BUS-04, MANT-01, MANT-02, MANT-03, MANT-04, PERS-01, PERS-02, PERS-03, LIFE-01, LIFE-02, LIFE-03, LIFE-04, LIFE-05, LIFE-06, PAIN-01, PAIN-02, PAIN-03, PAIN-04, CAP-01, CAP-02, CAP-03, CAP-04, VEND-01, VEND-02, VEND-03, VEND-04, REV-01, REV-02, REV-03

**Success Criteria:**
1. BRD draft is complete enough for internal review without requiring every stakeholder to read all source proposals first.
2. BRD clearly separates confirmed source facts, market inferences, assumptions, open questions, and recommendations.
3. BRD includes persona responsibilities, lifecycle deep dives, pain-point mapping, capability map, vendor comparison, and decision checklist.
4. BRD identifies what Manthan already covers and what must be reused, configured, extended, or added.
5. Stakeholder review checklist is present.

**Primary output:** `Justo_CP_App_BRD_Draft.md`

### Phase 2: PRD Definition

**Goal:** Convert the approved BRD into a product requirements document for the CP app.  
**Mode:** mvp

**Requirements:** PRD-01, PRD-02, PRD-03, PRD-04, PRD-05

**Success Criteria:**
1. PRD defines product goals, user stories, roles, permissions, functional requirements, non-functional requirements, and acceptance criteria.
2. PRD maps product capabilities to the business objectives and lifecycle requirements established in the BRD.
3. PRD states source-of-truth ownership and integration expectations for Manthan and third-party systems.
4. PRD distinguishes MVP, v2, and deferred capabilities.

**Primary output:** `Justo_CP_App_PRD.md`

### Phase 3: Product Roadmap And Phases

**Goal:** Convert the PRD into product delivery phases that can guide implementation, vendor scoping, and later UI design.  
**Mode:** mvp

**Requirements:** ROAD-01, ROAD-02, ROAD-03, ROAD-04

**Success Criteria:**
1. Product phases are capability-based, not document-section-based.
2. Each product phase has scope, dependencies, risks, success criteria, and decision gates.
3. MVP, v2, and deferred capabilities are explicitly mapped.
4. Journey-map and UI-spec ownership by phase is clear.

**Primary output:** `Justo_CP_App_Product_Roadmap.md`

### Phase 4: Journey Maps

**Goal:** Create journey maps for the core CP app personas and workflows, aligned to product phases.  
**Mode:** mvp

**Requirements:** JOUR-01, JOUR-02, JOUR-03, JOUR-04

**Success Criteria:**
1. Journey maps cover CP firm onboarding, CP employee activation, lead ownership, site visit, booking, payout, CP sourcing/RM operations, and support/dispute handling.
2. Each journey includes app actions, outside-app actions, system events, pain points, decisions, and success measures.
3. Every journey maps to personas, PRD requirements, and product phases.
4. Gaps requiring BRD or PRD updates are explicitly listed.

**Primary output:** `Justo_CP_App_Journey_Maps.md`

### Phase 5: UI Screen Specs And Prototype

**Goal:** Produce phase-aligned UI screen specifications and prototype guidance for the CP app.  
**Mode:** mvp

**Requirements:** UI-01, UI-02, UI-03, UI-04

**Success Criteria:**
1. Screen inventory is grouped by product phase and persona.
2. Each screen spec includes purpose, user action, data shown, source system, validation, empty/error states, and acceptance criteria.
3. Critical flows have low-fidelity prototype structure or clickable prototype guidance.
4. Every screen traces back to a journey, PRD requirement, and product phase.

**Primary output:** `Justo_CP_App_UI_Screen_Specs.md`

## Coverage

- v1 requirements: 53
- Mapped to phases: 53
- Unmapped: 0

## Next Step

Run `$gsd-discuss-phase 1` to refine and complete the BRD phase.

---
*Roadmap created: 2026-05-30*
