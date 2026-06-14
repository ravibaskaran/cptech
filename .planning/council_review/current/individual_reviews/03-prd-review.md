# PRD Document Quality Review — Product Architecture Council

## Review Summary

The Justo CP App PRD (v0.5) is a **well-structured, unusually thorough draft** for a product at this stage. It contains 94 functional requirements (PRD-FR-001 through PRD-FR-094), 20 non-functional requirements, 16 Gherkin acceptance scenarios, a detailed scope gatekeeper addendum, edge case handling, an RBAC permission matrix, a source-of-truth matrix, and explicit open-question/assumption registers. The document demonstrates strong alignment with its parent BRD and a disciplined approach to scope control.

However, the review identifies several critical and major gaps: **incomplete BRD-to-PRD traceability mapping**, **NFRs lacking numeric targets for several categories**, **acceptance criteria missing for ~60% of requirement groups**, **inconsistency between BRD Phase 1/2/3 persona simplification and PRD persona treatment**, **RBAC matrix covering all 10 personas rather than the stated 3-persona MVP**, and **several duplicate/overlapping requirement areas**. These must be addressed before the PRD can be considered implementation-ready.

---

## Strengths

### 1. Exceptional Scope Gatekeeper Discipline [high]
- **Source:** PRD §Scope Gatekeeper Addendum (lines 70–116), BRD §Scope Gatekeeper Addendum (lines 24–63)
- The PRD has one of the clearest MVP scope gates seen in a draft PRD. The "Launch Core" table explicitly names 12 included behavior categories. The "Not Launch Scope" table provides explicit cut justifications. The "Journey Map Readiness Gate" at line 113–115 creates a requirement-level enforcement rule for downstream artifacts.
- The Core Differentiator Guardrails table (lines 106–111) is excellent — it keeps geofencing, queued uploads, and full payout processing in scope while defining strict engineering boundaries.

### 2. Strong Functional Requirements Coverage [high]
- **Source:** PRD §7 Requirements (lines 354–539)
- 94 functional requirements organized into 14 logical groups covering identity/RBAC, onboarding, employee management, sourcing, project catalog, lead ownership, communication, site visits, booking, payout, support/audit, analytics, offline sync, and gamification.
- Every FR has an ID, priority classification (Must/Should), and goal mapping (G1–G7).
- The requirement traceability table at lines 356–373 links requirement groups to goals.

### 3. Well-Defined Acceptance Criteria for Core Flows [high]
- **Source:** PRD §7 Acceptance Criteria (lines 566–747)
- 16 Gherkin scenarios covering identity/role, CP onboarding, employee exit, collateral sharing, lead ownership (3 scenarios), notifications, site visits (3 scenarios), payout (3 scenarios), and offline sync (2 scenarios).
- Scenarios properly use Given/When/Then format and cover both happy path and exception paths (e.g., offline lead, geofence fallback, finance rejection).

### 4. Transparent Evidence and Confidence Tagging [high]
- **Source:** PRD §0, §3 (lines 47–52, 146–179)
- The PRD uses consistent [high], [moderate], [low], [unknown] confidence tags throughout.
- Evidence gaps are honestly declared (no CP interviews, no quantitative baselines, no direct quotes).
- The AI Gap Report (lines 1061–1089) is a genuinely useful self-assessment tool.

### 5. Comprehensive Risk and Edge Case Treatment [high]
- **Source:** PRD §8 Edge Case Handling (lines 781–794), §11 Risks (lines 905–922)
- 10 explicit edge cases with expected UX behavior.
- 13 risks with severity, impact rationale, and mitigation strategy.
- Specific edge cases like "Payout SLA unavailable" and "Unauthorized deep link" show mature product thinking.

### 6. Source-of-Truth Matrix [high]
- **Source:** PRD §9 (lines 813–828)
- Every major entity (CP firm, employee, lead, project, visit, booking, payout, notification, audit) has explicit source-of-truth ownership and PRD requirement linkage.

---

## Critical Issues (Must Fix)

### C1. Incomplete BRD-to-PRD Requirement Traceability [high]

**Source:** PRD §7 Requirement Traceability (lines 356–373) vs. BRD §13 PRD-Ready Functional Themes (lines 754–770) and BRD §10 Capability Requirements (lines 674–719)

The PRD's traceability table maps requirement *groups* to *PRD goals* (G1–G7), but there is **no explicit mapping from individual PRD-FR-xxx requirements to BRD business requirements, BRD capability requirements (§10), or BRD persona journey mechanics**. This means:

- It is impossible to verify that every BRD business outcome (§3.2, lines 96–104) has at least one PRD-FR implementing it.
- It is impossible to verify that every PRD-FR has a BRD parent (orphan check).
- The BRD's 13 PRD-Ready Functional Themes (§13) are not referenced in the PRD at all.

**Recommendation:** Add a traceability matrix mapping each PRD-FR to its parent BRD requirement(s) (e.g., BRD §10.1 capability, BRD §3.2 business outcome, BRD persona journey). This should be a table or appendix.

### C2. Acceptance Criteria Missing for ~60% of Requirement Groups [high]

**Source:** PRD §7 Acceptance Criteria (lines 566–747) vs. PRD §7 Functional Requirements (lines 375–539)

Acceptance criteria (Gherkin scenarios) are provided for 8 of 14 requirement groups. The following groups have **zero acceptance criteria**:

| Missing Group | PRD-FR Range | Risk |
|---|---|---|
| CP Employee Management (§7.3) | PRD-FR-013 to 017 | Employee deactivation edge cases untested |
| CP Sourcing/RM Ops (§7.4) | PRD-FR-018 to 022 | RM home screen behavior unspecified |
| Communication/Follow-up (§7.7) | PRD-FR-037 to 043 | Timeline rendering, notification preferences untested |
| Analytics/Dashboards (§7.12) | PRD-FR-065 to 070 | Dashboard data freshness, drill-down untested |
| Gamification/Leaderboards (§7.14) | PRD-FR-080 to 094 | Leaderboard ranking, privacy, refresh untested |
| Booking Visibility (§7.9) | PRD-FR-050 to 053 | Partial — only payout-adjacent scenarios exist |

**Recommendation:** Add at least one happy-path and one exception-path Gherkin scenario per requirement group. For "Must" priority requirements, acceptance criteria should be mandatory.

### C3. Phase 1/2/3 Boundaries Inconsistent Between BRD and PRD [high]

**Source:** BRD §15 Project Phases (lines 807–827) vs. PRD §Scope Gatekeeper (lines 70–116) and PRD §6 Persona Summary (lines 219–233)

The BRD §15 defines a clear 3-phase model:
- **Phase 1:** UI/UX & Architecture Definition (No Code) — 3 core flows: RM, CP, Customer Doc Upload
- **Phase 2:** Core MVP Technical Implementation — RM flow, CP flow, Customer flow
- **Phase 3+:** Expansion to Finance, Admin Ops, Leadership, Telecallers, advanced features

The PRD does **not reference this Phase 1/2/3 model anywhere**. Instead, it uses a "Launch Core vs. Not Launch Scope" binary. This creates several problems:

1. The PRD's Launch Core table (lines 76–91) includes "Admin/support/audit" and analytics dashboards, but BRD Phase 2 only covers RM, CP, and Customer flows — the admin/support/audit personas are explicitly Phase 3+ in the BRD.
2. The PRD includes full gamification (PRD-FR-080–094, priority "Should") in its main requirement list without clearly marking these as Phase 3+.
3. The PRD's persona summary (lines 219–233) correctly identifies "RM, CP, Buyer" as Launch MVP personas and defers others to Phase 3+, but then **defines full journey maps and functional requirements for all deferred personas** (Finance: §6.5, Leadership: §6.1, Sourcing Head: §6.2, Sales/Admin Ops: §6.4, Telecaller: §6.9, Compliance/Support: §6.11).

**Recommendation:** 
- Add a Phase column to every PRD-FR requirement row (Phase 1, Phase 2, Phase 3+).
- Align the PRD's phase boundaries with BRD §15 explicitly.
- Clearly mark journey maps for deferred personas as "Phase 3+ Context — Not for Journey Map or Screen Generation."

---

## Major Issues (Should Fix)

### M1. NFRs Lack Measurable Targets for Several Categories [moderate]

**Source:** PRD §7 Non-Functional Requirements (lines 541–564)

Several NFRs use "according to standards" or "where applicable" language without defining measurable acceptance criteria:

| NFR | Issue |
|---|---|
| PRD-NFR-007 (Encryption) | "according to Justo/Manthan standards" — standards are undefined |
| PRD-NFR-009 (Compliance) | "exact validation sources pending decision" — no interim target |
| PRD-NFR-010 (Accessibility) | "WCAG 2.2 AA-equivalent practices where applicable" — "where applicable" is escape clause |
| PRD-NFR-011 (Observability) | No target for log retention, query latency, or alert thresholds |
| PRD-NFR-012 (Availability) | No uptime target (e.g., 99.5%, 99.9%) |
| PRD-NFR-013 (Maintainability) | No measurable criteria |

NFRs with clear targets: PRD-NFR-001 (3 taps), PRD-NFR-002 (3 seconds), PRD-NFR-003 (2 seconds), PRD-NFR-004 (1 second), PRD-NFR-018 (5 min refresh), PRD-NFR-019 (30s export) — these are well-done.

**Recommendation:** For each NFR, define either a numeric target or a testable condition. Use "[unknown] — pending tech review" explicitly where targets cannot be set yet, rather than vague qualifiers.

### M2. RBAC Matrix Covers All Personas, Not Simplified MVP Set [moderate]

**Source:** PRD §6 Persona Summary (lines 219–233), PRD BRD §9 Role and Permission Matrix (BRD lines 656–672)

The PRD correctly identifies the simplified MVP persona set as {RM, CP Owner/Employee, Buyer/Customer (Doc Upload)} at lines 219–233. However:

1. The PRD **does not include its own RBAC matrix** — it relies on the BRD's RBAC matrix (BRD §9, lines 656–672), which covers all 10 personas.
2. There is no PRD-specific RBAC matrix that shows **only the MVP-scope permissions**.
3. The BRD RBAC matrix uses informal permission descriptions ("View," "Create," "Admin support") rather than formal permission names that can be directly implemented.

**Recommendation:**
- Add a PRD-specific RBAC matrix for Phase 1/2 MVP personas only (RM, CP Owner, CP Employee, Buyer).
- Define formal permission identifiers (e.g., `lead.create`, `payout.view.own_firm`, `cp.employee.manage`).
- Add a separate "Phase 3+ RBAC Extensions" section for deferred personas.

### M3. Customer/Buyer Persona Requirements Are Thin [moderate]

**Source:** PRD §6.10 Buyer Journey (lines 336–343), BRD §15 Phase 2 (lines 817–822)

The Buyer/Customer persona is listed as an MVP persona (lines 230–233), but:

1. The PRD has **no dedicated functional requirements section** for the Buyer/Customer persona. There is no "§7.x Buyer/Customer Document Upload" section.
2. The buyer journey at §6.10 (lines 336–343) has only 4 journey steps with minimal detail.
3. BRD §15 Phase 2 defines "Customer Flow: Queued document uploads for underwriting with secure local storage and server-side validation" — but the PRD's queued document upload requirements (PRD-FR-079) are written from the CP/RM onboarding perspective, not the buyer/customer underwriting perspective.
4. No acceptance criteria exist for the buyer/customer document upload flow.

**Recommendation:** Add a dedicated §7.x section for Buyer/Customer requirements covering: document submission for underwriting, document status visibility, underwriting progress visibility, and secure upload. Add Gherkin scenarios for this flow.

### M4. Duplicate and Overlapping Requirements [moderate]

**Source:** Multiple PRD sections

Several requirements overlap or could be consolidated:

| Overlap | Involved Requirements |
|---|---|
| Offline sync queue visibility | PRD-FR-073 ("visible sync queue with status") and PRD-FR-079 ("show file-level upload state") both define queue visibility with different scopes but no clear relationship |
| Payout audit requirements | PRD-FR-057 ("reason and audit trail"), PRD-FR-078 ("immutable audit events"), and PRD-FR-063 ("audit logs for... payout approval") all require payout audit but from different angles |
| Notification requirements | PRD-FR-039 (push), PRD-FR-040 (in-app center), PRD-FR-041 (deep links), PRD-FR-043 (critical persistence) could be one composite requirement with sub-requirements |
| Dashboard requirements | PRD-FR-065 through PRD-FR-069 (analytics per persona) and PRD-FR-085 through PRD-FR-094 (gamification dashboards per persona) create a large surface of "Should" requirements that blur the line between MVP and Phase 3 |

**Recommendation:** Add a "Related Requirements" column or cross-reference notes to make overlapping requirements explicit. Consider consolidating notification and dashboard requirements into fewer composite requirements with sub-items.

### M5. Open Questions Blocking Critical Requirements [moderate]

**Source:** PRD §15 Open Questions (lines 985–1004)

17 open questions are listed, but **7 of them directly block "Must" priority requirements**:

| Open Question | Blocked Must Requirement(s) |
|---|---|
| Lead-lock expiry duration | PRD-FR-032 (lock status/expiry) |
| Direct-vs-CP lead priority | PRD-FR-030 (duplicate detection logic) |
| Booking milestone for commission | PRD-FR-053 (eligibility-impacting events) |
| Payout SLA | PRD-FR-059 (payout date promise) |
| GST/TDS rules | PRD-FR-056 (deduction display) |
| RERA validation source | PRD-FR-008 (document collection) |
| Which Manthan APIs are ready | All requirements depending on Manthan |

There is no tracking of **which open questions block which requirements**, and no escalation owner or deadline for resolution.

**Recommendation:** Add a "Blocked Requirements" column to the Open Questions table and assign resolution deadlines. Mark blocked requirements as "Must — Pending Decision" rather than plain "Must."

---

## Minor Issues (Nice to Fix)

### N1. Requirement Numbering Gap [low]
- **Source:** PRD §7 (lines 375–539)
- PRD-FR-076 is followed by PRD-FR-077 (Geofenced visit proof) in §7.8 instead of §7.13, then PRD-FR-078 (Payout processing) in §7.10, and PRD-FR-079 (Queued uploads) in §7.13. Requirements 077–079 appear to have been inserted after initial numbering. PRD-FR-080–094 (Gamification) follow sequentially.
- This out-of-sequence numbering creates confusion about which section a requirement belongs to.
- **Recommendation:** Re-number requirements sequentially within each section, or add a "Section" column.

### N2. Glossary Could Include More Domain Terms [low]
- **Source:** PRD §16 Glossary (lines 1019–1044)
- Missing terms: "Activation" (referenced 15+ times), "CP health score" (referenced in analytics), "Maker-checker" (used in payout), "Feature flag" (used in rollout), "Freshness indicator" (used in project catalog).
- **Recommendation:** Add 5–10 additional domain-specific terms.

### N3. Decision Log Is Sparse [low]
- **Source:** PRD §13 Decision Log (lines 961–970)
- Only 6 decisions logged, 2 of which are "Draft decision." For a PRD of this complexity, more architectural and product decisions should be captured (e.g., "Why geofencing over GPS-only", "Why Gherkin for acceptance criteria", "Why offline-first vs. offline-capable").
- **Recommendation:** Expand the decision log to capture key product and architectural choices.

### N4. Quality Check Report Self-Assessment Is Overly Generous [low]
- **Source:** PRD §Quality Check Report (lines 1046–1059)
- The self-assessment marks "Actionability" as ✅ with the note "Requirements are numbered and paired with Gherkin acceptance criteria for critical flows." As identified in C2 above, ~60% of requirement groups lack acceptance criteria. This should be ⚠️.
- **Recommendation:** Update the Quality Check Report to reflect the acceptance criteria coverage gap.

---

## Missing Items

| Missing Item | Why It Matters | Evidence |
|---|---|---|
| BRD-to-PRD traceability matrix | Cannot verify requirement lineage or find orphans | No mapping from PRD-FR to BRD section exists |
| Phase column on each PRD-FR | Cannot determine which requirements are in MVP vs. Phase 3+ | BRD §15 defines 3 phases; PRD does not reference them |
| Buyer/Customer functional requirements section | MVP persona has no dedicated FR section | BRD §15 Phase 2 includes "Customer Flow" |
| PRD-specific RBAC matrix for MVP personas | Cannot implement permission enforcement without formal permissions | BRD RBAC matrix covers all 10 personas |
| Data retention and deletion policies | GDPR/privacy compliance requirement | No mention of data retention periods or right-to-delete |
| Scalability NFR | No concurrent user targets or data volume estimates | [Missing evidence] |
| Internationalization/Localization NFR | Maharashtra launch may need Marathi/Hindi support | [Missing evidence] |
| API versioning requirements | Manthan integration needs version strategy | [Missing evidence] |
| Rate limiting / abuse prevention requirements | Lead submission could be abused without rate limits | [Missing evidence] |
| Acceptance criteria for deferred-persona requirements | Requirements exist for 7 deferred personas but have no testable criteria | PRD §7 covers deferred persona FRs without acceptance criteria |

---

## Recommendations

### Immediate (Pre-Signoff)
1. **Add a BRD-to-PRD traceability matrix** mapping each PRD-FR to its parent BRD requirement(s). Flag any orphan PRD-FRs and any BRD requirements without PRD coverage.
2. **Add a Phase column to every PRD-FR** aligned with BRD §15's Phase 1/2/3+ model. Clearly mark which requirements are Phase 2 MVP and which are Phase 3+ deferred.
3. **Add acceptance criteria for missing requirement groups** — at minimum for CP Employee Management, CP Sourcing/RM Ops, Communication/Follow-up, and Booking Visibility.
4. **Add a Buyer/Customer requirements section** (§7.x) with dedicated FRs for document upload for underwriting.
5. **Add blocked-requirement tracking** to the Open Questions table.

### Near-Term (Pre-Journey Maps)
6. **Create a PRD-specific MVP RBAC matrix** with formal permission identifiers for the 3 MVP personas (RM, CP Owner/Employee, Buyer).
7. **Define measurable targets for NFRs** PRD-NFR-007, 009, 010, 011, 012, and 013 — or explicitly mark them as "[unknown] — pending tech review" with a resolution deadline.
8. **Consolidate overlapping requirements** — especially notification (FR-039 through FR-043) and payout audit (FR-057, FR-078, FR-063).
9. **Add missing NFRs** for scalability, data retention, localization, rate limiting, and API versioning.

### Process
10. **Align the PRD's Quality Check Report** with the findings from this review — the self-assessment should match external review findings.
11. **Expand the Decision Log** to capture major product and architecture decisions made during PRD drafting.

---

## Cross-Cutting Concerns

- **Architecture Review Dependency:** The source-of-truth matrix (PRD §9, lines 813–828) has 10 dependency rows marked `[unknown]`. The architecture review should verify whether the PRD's offline-first and sync requirements (PRD-FR-071–076) are feasible given Manthan's API readiness.
- **Security Review Dependency:** PRD-NFR-006 (RBAC enforcement server-side and client-side) and PRD-NFR-007 (encryption) need the security reviewer to validate the stated requirements against actual Manthan capabilities.
- **UX/Journey Map Dependency:** The PRD's edge case table (§8, lines 781–794) is excellent context for the UX review, but the acceptance criteria gap (C2) means several edge cases cannot be formally tested.

---

## Score (out of allocated points)

**Score: 10 / 15**

**Justification:**

| Criterion | Weight | Score | Notes |
|---|---|---|---|
| FR completeness, testability, unambiguity | 3 | 2.5 | 94 FRs, well-structured, but ~60% lack acceptance criteria |
| BRD traceability | 2 | 0.5 | Group-to-goal mapping exists; individual FR-to-BRD mapping missing |
| NFR specificity with measurable targets | 2 | 1.0 | 6 of 20 NFRs have numeric targets; rest are qualitative |
| Acceptance criteria coverage | 2 | 1.0 | 16 Gherkin scenarios cover ~40% of requirement groups |
| Edge cases and error states | 1 | 1.0 | Excellent — 10 edge cases plus risk table |
| Persona simplification correctness | 1 | 0.5 | Correctly identified but inconsistently applied (full journeys for deferred personas) |
| Phase 1/2/3 boundary clarity | 1 | 0.5 | BRD phases not referenced; PRD uses binary scope model |
| Scope gatekeeper consistency | 1 | 1.0 | Excellent — clear Launch Core, Not Launch, and Differentiator Guardrails |
| RBAC model completeness | 1 | 0.5 | Relies on BRD's 10-persona matrix; no MVP-specific formal RBAC |
| No orphans/duplicates/contradictions | 1 | 0.5 | Some overlaps identified (notifications, dashboards, payout audit) |
| **Total** | **15** | **10.0** | |

The PRD is a strong draft with excellent scope discipline, risk awareness, and honest evidence tagging. The critical gaps are structural (traceability, phase alignment, acceptance criteria coverage) rather than content quality issues. Fixing C1–C3 would likely raise the score to 13+/15.

---

*Review completed: 2026-06-14*  
*Reviewer: PRD Quality Reviewer, Product Architecture Council*  
*Documents reviewed: Justo_CP_App_PRD.md (v0.5, 1093 lines), Justo_CP_App_BRD_Draft.md (v0.5, 850 lines), .planning/REQUIREMENTS.md (220 lines)*
