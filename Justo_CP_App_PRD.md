# Product Requirements Document: Justo CP App

Draft version: v0.3
Date: 2026-05-31  
Prepared for: Justo Realfintech  
PRD owner: Product, Justo CP App initiative  
Primary input: `Justo_CP_App_BRD_Draft.md` v0.2  
Artifact sequence: BRD -> PRD -> Persona-wise Journey Maps -> Google Stitch UI Screen Specs/Prototype

## Table Of Contents

- [0. Version And Ownership](#0-version-and-ownership)
- [1. Executive One-Pager](#1-executive-one-pager)
- [Scope Gatekeeper Addendum: MVP Scope Gate](#scope-gatekeeper-addendum-mvp-scope-gate)
- [2. Overview And Context](#2-overview-and-context)
- [3. Customer Insights And Evidence](#3-customer-insights-and-evidence)
- [4. Goals And Non-Goals](#4-goals-and-non-goals)
- [5. Alternatives Considered](#5-alternatives-considered)
- [6. User Personas And Use Cases](#6-user-personas-and-use-cases)
- [7. Requirements](#7-requirements)
- [8. UX And Design Considerations](#8-ux-and-design-considerations)
- [9. Technical Notes](#9-technical-notes)
- [10. Metrics And Success Criteria](#10-metrics-and-success-criteria)
- [11. Risks And Mitigations](#11-risks-and-mitigations)
- [12. Rollout Plan](#12-rollout-plan)
- [13. Decision Log](#13-decision-log)
- [14. Success Story Narrative](#14-success-story-narrative)
- [15. Open Questions And Assumptions](#15-open-questions-and-assumptions)
- [16. Glossary](#16-glossary)
- [Quality Check Report](#quality-check-report)
- [AI Gap Report](#ai-gap-report)

## 0. Version And Ownership

| Field | Value |
|---|---|
| Document | Justo CP App PRD |
| Version | v0.3 scope-gated draft |
| Date | 2026-05-31 |
| Mode | Full Mode |
| Owner | Product, Justo CP App initiative |
| Business sponsor | Justo leadership, CP business |
| Reviewers | CP sourcing, RM leadership, sales/admin ops, finance, compliance/legal, Manthan product/technology, vendor management |
| Source artifacts | `Justo_CP_App_BRD_Draft.md`, `Justo_CP_App_Business_Brief.md`, `.planning/REQUIREMENTS.md`, vendor proposals from Auum, TSPL/Triazine, I9/Indexnine, Manthan proposal and SoWs |
| Status | Scope-gated draft for stakeholder review |

### Evidence Confidence Tags

- `[high]` means supported by local project documents or explicit user instruction.
- `[moderate]` means a reasonable product inference from the BRD or vendor proposal comparison.
- `[low]` means a directional hypothesis needing field validation.
- `[unknown]` means a required business or technical decision is not yet available.

## 1. Executive One-Pager

### TL;DR

- [high] Justo needs the CP app to become a trusted CP operating layer for Maharashtra first, not merely a mobile lead-entry surface.
- [high] The app must use one credential per user, resolve assigned role(s), and drive the first screen, permissions, workflows, notifications, and data visibility through admin-configured role-based access control.
- [high] The product must prioritize CP trust workflows: onboarding, compliance, project discovery, approved collateral, lead ownership, site-visit proof, booking visibility, payout transparency, disputes, and audit.
- [high] The app must be offline-first where safe, with local draft/queue behavior and automatic sync when connectivity returns.
- [moderate] Success should be measured by CP activation, accepted leads, verified visits, bookings, payout SLA adherence, dispute reduction, and CP/RM adoption.

### Plain-Language Summary

Justo wants to scale into a large regional channel partner business in Maharashtra and then across India. [high] CPs will not adopt an app just because Justo launches one. They will adopt it if the app makes selling projects easier, protects their lead ownership, gives them current project information, proves site visits, shows what happened after a lead was submitted, and makes commission and payout status visible.

This PRD defines the first complete product requirement draft for the Justo CP App. [high] It now prepares directly for persona-wise journey maps and Google Stitch-ready UI screen specifications. It defines users, journeys, functional requirements, non-functional requirements, acceptance criteria, metrics, risks, open decisions, and design/technical constraints so that each persona journey can be converted into screen-level UI specs without additional product-scoping work.

## Scope Gatekeeper Addendum: MVP Scope Gate

### Core Launch Objective

[high] The launch MVP must prove one narrow business outcome: a controlled Maharashtra CP pilot can complete the trust loop from verified CP onboarding to assigned project access, lead ownership decision, site-visit proof, booking milestone visibility, and payout status visibility. Requirements outside this trust loop are valid product context, but they are not launch scope unless Manthan already supports them with near-zero incremental build.

### Launch Core

| Launch Core | Included Behavior |
|---|---|
| Identity and RBAC | Single credential, assigned role home, permission enforcement, suspended/deactivated access handling |
| CP onboarding | CP firm registration, required docs, approval/rejection, compliance status, RM visibility |
| CP employee control | Invite/import, role assignment, deactivation, historical attribution, active work reassignment |
| Project enablement | Assigned project catalog, freshness indicator, approved collateral share |
| Lead ownership | Quick lead submit, duplicate check, accepted/conflict/rejected/pending-sync state, reason, audit |
| Site visit proof | Scheduling plus launch-approved proof: QR, OTP, geofence, site-desk confirmation, or admin verification |
| Booking visibility | CP-safe booking milestone and next action, not full buyer/finance detail |
| Payout processing | Eligibility/status/reason visibility plus finance approval, rejection, scheduling, payment reference, reconciliation, clawback, dispute, and audit |
| Notifications | Native push plus in-app notification center for critical role-specific events |
| Offline reliability | Safe drafts, queued document uploads, and sync queue for launch-approved offline actions |
| Admin/support/audit | Lightweight evidence-backed tickets and audit logs for core trust workflows |
| Geofenced visit proof | Location-backed proof for scheduled site visits with consent, fallback, accuracy, and retention controls |

### Not Launch Scope

| Excluded From Launch | Reason |
|---|---|
| AI voice calling, AI assistant, KHOJ/Gemini, AI summaries, AI scoring | Does not unlock the core trust loop; adds integration and operating risk. |
| CP microsites and CP-branded public pages | Marketing/distribution feature, not required to prove CP trust. |
| Advanced telecaller queue, call intelligence, sentiment, automated scoring | Follow-up can launch through basic timeline, tasks, and notes. |
| Advanced analytics, gamification, loyalty, CP health scoring | Requires reliable event data first. |
| Workforce tracking outside scheduled visit proof | High legal/privacy risk and not required for launch trust loop. |
| Full buyer portal expansion | Reuse existing buyer flows; launch only safe project links and visit confirmation where needed. |
| Multi-tenant/white-label architecture | Not needed for Justo's first Maharashtra CP operating model. |

### Core Differentiator Guardrails

| Differentiator | Product Rule | Engineering Guardrail |
|---|---|---|
| Geofencing | Required for differentiated site-visit proof, with QR/OTP/site-desk/admin fallback | Capture only during scheduled/active visit windows; require OS location permission and role permission; store timestamp, coordinates if approved, accuracy, proof method, and fallback reason; avoid continuous tracking. |
| Queued document uploads | Required for CP/RM onboarding in poor-network field conditions | Encrypt files locally, restrict file type/size, show queue state, support retry/resume/cancel/delete, never mark compliance complete until server validation succeeds. |
| Full payout processing | Required because payout trust is a CP loyalty differentiator | Use finance-controlled state machine, maker-checker approval, GST/TDS fields, invoice validation, payment reference, reconciliation state, clawback/dispute states, and immutable audit log. |

### Journey Map Readiness Gate

When persona-wise journey maps are created, every journey step must map to one of these outcomes: CP onboarding, project enablement, lead ownership, site-visit proof, booking visibility, payout transparency, notification/offline reliability, or operational control. If a step does not map, keep it as deferred context and do not convert it into a Google Stitch screen.

## 2. Overview And Context

### Problem Statement

[high] Justo's business goal is to become a major CP player, starting in Maharashtra. The current operating reality for many CP-led real estate transactions is fragmented across calls, WhatsApp, spreadsheets, PDFs, CRM entries, site-desk confirmations, and finance follow-ups. [moderate] This fragmentation creates trust gaps around lead ownership, inventory accuracy, site-visit attribution, booking visibility, and commission payouts.

The CP app must solve these trust and operating-friction problems. A generic CRM wrapper will fail because it asks CPs to enter data without giving them enough practical value. A successful product will make each CP's working day simpler: find current projects, share approved material, register a protected lead, coordinate the visit, track booking progress, understand payout status, and escalate disputes with evidence.

### Why Now

- [high] Project Manthan already provides a CRM foundation that can be reused or extended.
- [high] Justo has received vendor proposals from Auum, TSPL/Triazine, and I9/Indexnine, creating a decision point for scope and implementation direction.
- [high] The BRD has identified the CP network lifecycle as the core business requirement.
- [moderate] CPs are likely to prefer partners that reduce payout anxiety, lead disputes, and information uncertainty.

### Strategic Alignment

| Strategy | Product Translation |
|---|---|
| Build a Maharashtra CP network first | Support CP firm onboarding, compliance, activation, and RM-led sourcing workflows |
| Increase qualified CP-led demand | Make project discovery, lead registration, and follow-up fast on mobile |
| Improve CP trust | Make lead status, booking status, payout status, and disputes transparent by permission |
| Control operational and compliance risk | Use RBAC, audit logs, compliance lifecycle, claim-safe collateral, and source-of-truth rules |
| Preserve Manthan investment | Reuse Manthan where it is source of truth; extend only where CP lifecycle gaps exist |

### Competitive / Landscape Snapshot

[moderate] India-focused broker and CP tools commonly market lead management, inventory, WhatsApp automation, site visits, team performance, commission tracking, and CP portals as core capabilities. [moderate] These categories indicate market expectations, but they do not by themselves solve Justo's deeper problem: becoming the trusted operating layer between developers, CP firms, CP employees, RMs, finance, and buyers.

## 3. Customer Insights And Evidence

### Evidence Available

| Evidence Type | Status | PRD Use |
|---|---|---|
| BRD synthesis | Available | Primary product scope source |
| Vendor proposals | Available | Capability benchmark and gap source |
| Manthan proposal and SoWs | Available | Baseline platform/source-of-truth input |
| Primary CP/RM interviews | Not available | Must be collected before final signoff |
| Quantitative app/CRM analytics | Not available | Instrumentation requirements included |
| Direct customer quotes | Not available | Do not fabricate; collect in validation sprint |

### Direct Quotes

| Required Quote Type | Quote | Status |
|---|---|---|
| Primary source quote | Not available | No direct CP, RM, finance, or buyer interview quote has been provided. |
| Secondary source quote | Not available | No directly quoted external research excerpt has been provided for this PRD draft. |

### Product Anecdotes Derived From The BRD

- [high] CPs need current project information and approved collateral because stale PDFs and forwarded messages can create claim risk and wasted effort.
- [high] CPs need lead ownership clarity because accepted/conflict/rejected status changes trust and sales behavior.
- [high] CP owners need employee controls because a CP firm is an organization, not a single login.
- [high] Finance needs approval discipline while CPs need visibility into eligibility, invoice status, deductions, expected payout date, and paid status.
- [high] RMs need a CP sourcing and activation dashboard because network growth is a managed lifecycle, not only a CP master record.

### Evidence Gaps To Close

- Interview 8-12 CP owners, CP employees, RMs, finance users, and ops users in Maharashtra.
- Measure current time-to-onboard CP, time-to-first-lead, lead conflict rate, visit proof leakage, booking visibility gaps, payout SLA performance, and CP support volume.
- Validate whether CPs prefer mobile-only workflows or hybrid mobile plus web access for owners.
- Validate which payout and booking details can be legally and operationally exposed.

## 4. Goals And Non-Goals

### Primary Goals

| Goal ID | Goal | Success Signal |
|---|---|---|
| G1 | Make CP onboarding, compliance, activation, and lifecycle management explicit and trackable | Higher CP onboarding completion and activation rate |
| G2 | Give CPs a fast, trusted mobile workflow for project discovery, approved sharing, lead registration, follow-up, and site visits | Higher accepted lead volume and verified visit conversion |
| G3 | Protect lead ownership through dedupe, lock, conflict, dispute, and audit workflows | Lower unresolved lead dispute rate |
| G4 | Improve booking and payout transparency without weakening finance controls | Higher payout SLA adherence and lower payout support volume |
| G5 | Give Justo RMs and sourcing leaders operational control over CP acquisition, activation, performance, and escalations | Better RM productivity and CP health visibility |
| G6 | Preserve Manthan as the CRM foundation and avoid duplicate systems of record | Clear source-of-truth ownership for CP, lead, visit, booking, payout, and audit entities |
| G7 | Make the app reliable in Indian field conditions through offline-first behavior and native notifications | Lower abandoned actions due to connectivity and higher timely follow-up completion |

### Non-Goals

| Non-Goal | Reason |
|---|---|
| Select a final vendor | Vendor selection requires procurement and stakeholder decision. |
| Build detailed API specifications | API design depends on Manthan technical discovery and vendor path. |
| Launch full AI voice calling in the first requirement set | AI should not crowd out core trust workflows unless tied to measurable business outcomes. |
| Build CP microsites as a core requirement | Microsites are deferred unless leadership explicitly makes them a launch requirement. |
| Build a multi-tenant SaaS platform | The immediate goal is Justo's CP network, not a white-label SaaS product. |
| Replace Manthan | Manthan is assumed to remain the CRM foundation unless leadership decides otherwise. |

## 5. Alternatives Considered

| Alternative | Why It Was Considered | Decision | Reason |
|---|---|---|---|
| Generic mobile CRM wrapper | Fastest way to expose lead entry and status on mobile | Rejected | [high] It does not solve CP trust, payout, employee, sourcing, and site-visit proof problems. |
| AI-first CP platform | Vendor proposals emphasize AI calling and automation | Deferred | [moderate] AI can help later, but the trust workflows must work manually first. |
| Vendor product adoption without Manthan continuity | Could speed up delivery if vendor has mature CP product | Deferred | [high] Duplicate sources of truth would create high operational risk. |
| WhatsApp-only operating model | CPs already use WhatsApp heavily | Rejected as primary product | [moderate] WhatsApp is useful as a channel, but it cannot provide complete RBAC, audit, payout ledger, and compliance lifecycle alone. |
| Web portal only | Easier for admin-heavy workflows | Rejected for CP field users | [high] CP employees and RMs need mobile-first workflows; owner/admin web views can be added if needed. |
| Full launch with all modules | Attractive for business completeness | Rejected for UI readiness | [high] Requirements should be complete, but persona journey maps and Google Stitch screens should focus on the core trust loop first. |

## 6. User Personas And Use Cases

### Persona Summary

| Persona | Role In Ecosystem | Primary Jobs-To-Be-Done | Key Pain Points Addressed |
|---|---|---|---|
| Justo leadership | Owns business growth and risk | Monitor CP growth, conversion, payout exposure, disputes, and vendor progress | Fragmented visibility, weak operating control |
| CP sourcing head | Owns CP network acquisition and activation | Build CP pipeline, assign RMs, monitor activation, intervene on escalations | No unified sourcing funnel, weak CP health view |
| RM / sourcing employee | Field relationship owner | Recruit CPs, onboard them, activate them, support lead/visit/booking flows | Manual follow-ups, unclear CP activation status |
| Sales/admin ops | Operational control center | Manage master data, project access, exceptions, lead conflicts, collateral | Manual exception handling and inconsistent data |
| Finance | Controls commission and payout | Validate eligibility, invoice, deductions, approval, payment, reconciliation | Payout queries, unclear eligibility evidence |
| Developer/project team | Provides project inventory, offers, approvals | Keep project facts, inventory, collateral, and visit outcomes current | Stale material and inconsistent claims |
| CP owner | Runs CP firm | Manage firm profile, employees, leads, visits, bookings, payout, disputes | Low team control, payout anxiety, lead disputes |
| CP employee / agent | Sells to buyers | Search projects, share collateral, register leads, follow up, schedule visits | Stale info, slow lead capture, follow-up leakage |
| CP telecaller | Qualifies and nurtures leads | Work call queue, record disposition, schedule follow-up/visit | Spreadsheet queues, missed follow-ups |
| Buyer / customer | Receives project information and attends visits | Confirm interest, receive accurate info, complete KYC/payment where needed | Inconsistent claims, fragmented confirmation |
| Compliance/support | Controls risk and issue resolution | Validate documents, monitor expiry, handle disputes, export evidence | Scattered evidence and non-repeatable decisions |

### Launch Role Classification

| Classification | Personas | Scope Rule |
|---|---|---|
| Launch core | CP owner, CP employee/agent, RM/sourcing employee, sales/admin ops, finance, compliance/support | Must be represented in the first journey-map set because they operate the trust loop. |
| Launch control | CP sourcing head, Justo leadership, developer/project team | Need lightweight dashboards, approvals, or inputs only; avoid advanced analytics buildout. |
| App-linked, not core app user | Buyer/customer | Use safe project links and existing buyer flows; do not expand buyer portal in launch scope. |
| Deferred specialist | CP telecaller | Preserve persona context, but do not build advanced queues, call intelligence, or AI scoring in launch. |

### Role-Based Entry Principle

[high] Every in-app journey starts after a user signs in with a single credential. The system resolves the assigned role or roles and then routes the user to the correct role home.

| Case | Required Behavior |
|---|---|
| One user, one role | User lands directly on that role's home screen. |
| One user, multiple roles | User selects active role/context or lands on admin-configured default role. |
| Role changed by admin | User's next session and available actions reflect the updated permissions. |
| Suspended/deactivated role | User cannot access restricted data or actions and sees the correct support/escalation path. |
| Offline session | User can access cached safe data and queued actions according to last known permissions until sync validates access. |

### Detailed Persona Journeys

#### 6.1 Justo Leadership Journey

| Journey Step | In-App Experience | Outside-App Activity | System Event/Data | Pain Point Simplified | Success Measure |
|---|---|---|---|---|---|
| Review CP network health | Executive dashboard by city, cluster, RM, CP segment, project | Business review meeting | Aggregated CP, lead, visit, booking, payout, dispute metrics | No single view of CP business | Weekly operating review uses app data |
| Identify bottleneck | Drill into onboarding, activation, conflicts, payout delays | Ask CP sourcing/finance to intervene | Bottleneck flags and trend comparisons | Problems discovered late | Escalations are triggered earlier |
| Evaluate vendor/product progress | Review adoption and conversion metrics | Steering committee | PRD metric dashboard | Product success unclear | Go/no-go decisions use measured outcomes |
| Control risk | View compliance, collateral, dispute, payout exceptions | Approve policy decisions | Audit-ready exception reports | Hidden regulatory/financial risk | High-severity exceptions have owner and SLA |

#### 6.2 CP Sourcing Head Journey

| Journey Step | In-App Experience | Outside-App Activity | System Event/Data | Pain Point Simplified | Success Measure |
|---|---|---|---|---|---|
| Build CP prospect funnel | Create/import prospect, source, geography, segment, RM assignment | Attend networking/channel meetings | Prospect record and RM task | Prospecting scattered across people | All target CPs have owner/status |
| Review onboarding queue | Pending docs, rejected docs, activation blockers | Follow up with RM/CP | Compliance status events | Hard to know why CP is stuck | Time-to-approval decreases |
| Activate CP | Assign projects, training tasks, first lead target | Conduct CP enablement | Activation checklist completion | CP approved but inactive | Time-to-first-lead and first-visit improves |
| Manage performance | CP health score, inactive CPs, conflict-heavy CPs, payout escalations | Coaching or suspension decision | Health score and escalation log | No early-warning system | More CPs remain active |

#### 6.3 RM / Sourcing Employee Journey

| Journey Step | In-App Experience | Outside-App Activity | System Event/Data | Pain Point Simplified | Success Measure |
|---|---|---|---|---|---|
| Start day | RM home with assigned CP prospects, pending tasks, escalations | Field visits/calls | Task queue and location-independent activity log | Manual task tracking | More CP touchpoints completed |
| Onboard CP | Assisted registration, document checklist, missing-item prompts | Meet CP owner and collect docs | CP profile, documents, consent | Back-and-forth document chasing | Higher complete first submission rate |
| Activate CP | Assign projects, share approved onboarding kit, schedule training | Conduct training | Activation status and collateral share | CP not sure how to start | First lead submitted faster |
| Support lead/visit | See CP escalations, help resolve conflict, schedule visit | Coordinate with site team | Lead/visit timeline event | RM is blind to CP issue history | Fewer unresolved escalations |
| Review performance | View assigned CP health, inactive CPs, conversion | Plan next visits | CP activity and conversion metrics | No prioritization | RM focuses on high-impact CPs |

#### 6.4 Sales/Admin Ops Journey

| Journey Step | In-App Experience | Outside-App Activity | System Event/Data | Pain Point Simplified | Success Measure |
|---|---|---|---|---|---|
| Manage master setup | Configure projects, CP access, role policies, lead rules | Coordinate with product/tech | Admin configuration records | Manual hidden setup | Fewer setup errors |
| Publish collateral | Approve/share project facts, offers, PDFs, videos, RERA facts | Get project/developer approval | Versioned collateral event | Stale forwarded material | Only approved collateral is shared |
| Resolve lead conflict | Review duplicate evidence, timestamps, channel source, policy | Escalate if policy ambiguity | Conflict decision/audit event | Ad hoc disputes | Faster and consistent decisions |
| Handle exceptions | Override, suspend, reactivate, reassign with reason | Coordinate with RM/finance/legal | Exception log | No audit trail | All exceptions are traceable |

#### 6.5 Finance Journey

| Journey Step | In-App Experience | Outside-App Activity | System Event/Data | Pain Point Simplified | Success Measure |
|---|---|---|---|---|---|
| Review eligible payouts | Queue by booking, milestone, CP, project, invoice readiness | Validate booking/finance records | Eligibility event | Manual eligibility checks | Fewer payout errors |
| Process invoice | View GST/TDS/bank details, invoice status | Use accounting/bank system if separate | Invoice and deduction state | Repeated CP payout queries | CP can see status without calling |
| Approve/reject payout | Approve, reject with reason, request correction | Finance approval workflow | Payout approval audit | Opaque decision process | SLA adherence improves |
| Reconcile payment | Mark paid/failed/retry with reference | Bank/accounting reconciliation | Payment status and reference | Paid status not visible | Lower payout support volume |

#### 6.6 Developer / Project Team Journey

| Journey Step | In-App Experience | Outside-App Activity | System Event/Data | Pain Point Simplified | Success Measure |
|---|---|---|---|---|---|
| Maintain project facts | Project inventory, price bands, offers, possession, RERA fields | Confirm changes internally | Project update event | CPs use stale info | Reduced stale-collateral incidents |
| Approve collateral | Review material before CP distribution | Coordinate approvals | Collateral version and approval | Risky claims | Claim-safe sharing |
| Support visits | Confirm visit slots, site instructions, site outcomes | Site desk operations | Visit schedule/proof/outcome | Visit attribution gaps | Higher verified visit rate |
| Review project performance | CP-led leads, visits, bookings, conversion | Sales planning | Project performance dashboard | No project-specific CP insight | Better CP-project matching |

#### 6.7 CP Owner Journey

| Journey Step | In-App Experience | Outside-App Activity | System Event/Data | Pain Point Simplified | Success Measure |
|---|---|---|---|---|---|
| Register firm | Single credential, firm profile, RERA/GST/PAN/bank/KYC checklist | Submit legal/finance documents | CP firm profile and document records | Unclear onboarding status | CP knows next required action |
| Manage team | Invite employees, assign roles/projects, deactivate exits | Hire/manage agents | Employee records, permissions, attribution | No team access control | Owner controls team safely |
| Monitor business | Dashboard for leads, visits, bookings, payout, disputes | Team review | Firm-level pipeline and payout ledger | Owner must call RM for status | Fewer status calls |
| Register/monitor leads | Submit or review team leads, conflicts, lock expiry | Buyer follow-ups | Lead ownership events | Ownership anxiety | More accepted leads |
| Track payout | Eligibility, invoice, deductions, approval, expected/paid date | Submit invoice/supporting docs | Payout ledger | Payout opacity | Payout queries reduce |
| Raise dispute | Evidence-backed lead/site/payout dispute | Provide evidence if needed | Ticket and evidence bundle | WhatsApp escalations | Disputes have status and SLA |

#### 6.8 CP Employee / Agent Journey

| Journey Step | In-App Experience | Outside-App Activity | System Event/Data | Pain Point Simplified | Success Measure |
|---|---|---|---|---|---|
| Open role home | Assigned projects, due follow-ups, pending sync, notifications | Begin field day | Session role and task state | No clear next action | Agent starts with priority work |
| Search project | Filters by location, budget, configuration, possession, offer | Discuss with buyer | Project view event | Manual PDF hunting | Faster buyer-project match |
| Share approved collateral | WhatsApp/share link with tracked approved material | Buyer conversation | Share event and attribution | Stale or risky claims | Approved share usage increases |
| Register lead | Phone-first lead capture, duplicate check, accepted/conflict/rejected result | Confirm buyer details | Lead record and lock event | Ownership uncertainty | Lead registration completes quickly |
| Follow up | Reminders, notes, call/WhatsApp timeline, next action | Calls/messages | Activity timeline | Follow-up leakage | Follow-up completion improves |
| Schedule visit | Slot, confirmation, QR/OTP/site proof | Coordinate buyer/site | Visit event and proof | Manual visit proof | Verified visits increase |
| Update outcome | Interested, dropped, reschedule, booked, reason | Talk to buyer/site | Outcome event | Pipeline stale | Current pipeline status |

#### 6.9 CP Telecaller Journey

| Journey Step | In-App Experience | Outside-App Activity | System Event/Data | Pain Point Simplified | Success Measure |
|---|---|---|---|---|---|
| Open queue | Prioritized leads by due follow-up, temperature, project | Make calls | Queue assignment | Spreadsheet follow-ups | Calls completed on time |
| Capture disposition | Budget, location, urgency, objection, visit intent | Buyer qualification | Structured disposition | Unstructured call notes | Better lead quality |
| Schedule next action | Follow-up or site visit from disposition | Confirm buyer availability | Task/visit event | Missed next steps | Follow-up leakage reduces |
| Escalate hot lead | Notify CP owner/agent/RM | Handover call | Notification and timeline | Hot leads delayed | Faster hot-lead response |

#### 6.10 Buyer / Customer App-Linked Journey

| Journey Step | Buyer Experience | App/System Event | Pain Point Simplified | Success Measure |
|---|---|---|---|---|
| Receive project link | Approved project page/link from CP | Share tracking and attribution | Inconsistent claims | Buyer sees current approved facts |
| Express interest | Callback/site visit CTA where enabled | Lead activity event | Back-and-forth coordination | More confirmed interest |
| Confirm visit | OTP/QR/site confirmation where enabled | Visit proof event | Weak visit attribution | Verified visit proof |
| Complete KYC/payment | Existing buyer portal/payment flow where applicable | Buyer portal/payment event | Fragmented transaction path | Cleaner booking path |

#### 6.11 Compliance / Support Journey

| Journey Step | In-App Experience | Outside-App Activity | System Event/Data | Pain Point Simplified | Success Measure |
|---|---|---|---|---|---|
| Review compliance queue | Pending docs, expiries, exceptions, high-risk CPs | Legal/compliance review | Compliance status | Hidden non-compliance | Fewer expired/invalid records |
| Approve/reject | Reasoned decision, checklist, audit | Contact CP/RM if needed | Decision log | Unclear rejection reasons | Faster resubmission |
| Handle disputes | Evidence bundle with lead, site, booking, payout timeline | Escalation committee if needed | Ticket and resolution | Scattered evidence | SLA-based resolution |
| Export audit | Download audit trail for CP/project/time range | Legal/regulatory response | Audit export | Manual evidence compilation | Faster audit readiness |

## 7. Requirements

### Requirement Traceability

| Requirement Group | Goals Supported |
|---|---|
| Identity, RBAC, role home | G1, G5, G6, G7 |
| CP onboarding and compliance | G1, G5, G6 |
| CP employee management | G1, G2, G3 |
| CP sourcing/RM operations | G1, G5 |
| Project catalog and collateral | G2, G6 |
| Lead ownership | G2, G3, G6, G7 |
| Communication and notifications | G2, G7 |
| Site visit | G2, G3, G6 |
| Booking visibility | G2, G4, G6 |
| Payout ledger | G4, G6 |
| Support, disputes, audit | G3, G4, G5, G6 |
| Analytics | G1, G5 |
| Offline-first sync | G2, G7 |

### Functional Requirements

#### 7.1 Identity, Role Home, And RBAC

| ID | Requirement | Priority | Goals |
|---|---|---|---|
| PRD-FR-001 | The app shall allow each user to sign in using a single credential and resolve assigned role(s) from the backend identity/RBAC system. | Must | G5, G6, G7 |
| PRD-FR-002 | The app shall route a user to a role-specific home screen after login. | Must | G5, G7 |
| PRD-FR-003 | If a user has multiple roles, the app shall let the user choose an active role/context or use an admin-configured default. | Must | G5, G6 |
| PRD-FR-004 | The app shall enforce admin-configured permissions for every screen, field, action, notification, and data object. | Must | G5, G6 |
| PRD-FR-005 | The app shall prevent suspended, deactivated, or expired roles from accessing restricted actions and data. | Must | G6 |
| PRD-FR-006 | The app shall show a clear access-denied state with support/escalation path where appropriate. | Should | G7 |

#### 7.2 CP Firm Onboarding And Compliance

| ID | Requirement | Priority | Goals |
|---|---|---|---|
| PRD-FR-007 | The app shall support CP firm registration with required profile fields, contact details, business geography, and source/RM attribution. | Must | G1, G5 |
| PRD-FR-008 | The app shall support document collection for RERA, GST, PAN, bank details, KYC, and any Justo-defined compliance documents. | Must | G1, G6 |
| PRD-FR-009 | The app shall show onboarding status, missing items, rejection reasons, resubmission actions, and approval state to CP owner and assigned RM. | Must | G1, G7 |
| PRD-FR-010 | Admin/compliance users shall be able to approve, reject, request clarification, suspend, reactivate, or offboard a CP firm with reason codes and audit logs. | Must | G1, G6 |
| PRD-FR-011 | The app shall support document expiry/renewal reminders for compliance documents where expiry applies. | Should | G1, G6, G7 |
| PRD-FR-012 | The app shall block or flag restricted CP actions according to compliance state and admin policy. | Must | G1, G6 |

#### 7.3 CP Employee And Team Management

| ID | Requirement | Priority | Goals |
|---|---|---|---|
| PRD-FR-013 | CP owners shall be able to invite, import, activate, and deactivate CP employees, subject to admin policy. | Must | G1, G2 |
| PRD-FR-014 | CP owners/admins shall assign employee roles, project access, and visibility rules. | Must | G1, G6 |
| PRD-FR-015 | The app shall preserve historical attribution when a CP employee is deactivated. | Must | G3, G6 |
| PRD-FR-016 | The app shall support reassignment of active leads/tasks from a deactivated employee to another permitted user. | Must | G2, G3 |
| PRD-FR-017 | CP owners shall view firm-level team performance by lead, visit, booking, and follow-up activity, subject to permissions. | Should | G1, G5 |

#### 7.4 CP Sourcing And RM Operations

| ID | Requirement | Priority | Goals |
|---|---|---|---|
| PRD-FR-018 | RMs and sourcing heads shall create or import CP prospects before formal approval. | Must | G1, G5 |
| PRD-FR-019 | CP prospects shall move through configurable statuses such as identified, contacted, documents pending, under review, approved, activated, inactive, suspended, and offboarded. | Must | G1, G5 |
| PRD-FR-020 | RMs shall see assigned CP prospects, activation tasks, pending documents, inactive CPs, and escalations on an RM home screen. | Must | G1, G5 |
| PRD-FR-021 | Sourcing heads shall monitor CP acquisition, onboarding conversion, activation, RM productivity, and CP health. | Must | G1, G5 |
| PRD-FR-022 | The app shall support RM notes, meeting logs, tasks, and next follow-up dates for CP prospects and active CPs. | Should | G1, G5 |

#### 7.5 Project Catalog, Inventory, And Approved Collateral

| ID | Requirement | Priority | Goals |
|---|---|---|---|
| PRD-FR-023 | CP users shall see only assigned/permitted projects based on role, geography, CP status, and admin configuration. | Must | G2, G6 |
| PRD-FR-024 | Each project shall show CP-relevant facts such as location, configurations, price band, inventory status, offers, possession, RERA details, site instructions, and commission policy summary where permitted. | Must | G2 |
| PRD-FR-025 | Project data shall show last-updated timestamp and source where available. | Must | G2, G6 |
| PRD-FR-026 | CP users shall only share approved collateral and approved project facts from the app. | Must | G2, G6 |
| PRD-FR-027 | Shared collateral shall create an auditable share event linked to CP firm, employee, project, channel, and buyer/lead where known. | Should | G2, G3, G6 |
| PRD-FR-028 | Admin/project users shall be able to publish, expire, replace, and version approved collateral. | Must | G2, G6 |

#### 7.6 Lead Registration, Dedupe, Lock, Conflict, And Dispute

| ID | Requirement | Priority | Goals |
|---|---|---|---|
| PRD-FR-029 | CP users shall register leads quickly using phone-first capture with minimum required fields and optional project/budget/location details. | Must | G2, G7 |
| PRD-FR-030 | The system shall perform duplicate detection before accepting a lead, using configured matching logic. | Must | G3, G6 |
| PRD-FR-031 | Lead submission shall return one of the following states: accepted, conflict, rejected, pending sync, or pending review. | Must | G3, G7 |
| PRD-FR-032 | Accepted leads shall show ownership, lock status, lock expiry where applicable, CP/employee attribution, and next action. | Must | G3 |
| PRD-FR-033 | Conflict leads shall show reason category, allowed next action, and dispute path without exposing unauthorized personal data. | Must | G3, G6 |
| PRD-FR-034 | Admin/ops users shall resolve conflicts with evidence, policy reason, decision, and audit trail. | Must | G3, G6 |
| PRD-FR-035 | CP users shall be able to raise lead ownership disputes with supporting evidence. | Must | G3 |
| PRD-FR-036 | The system shall preserve a lead ownership audit ledger for submission, dedupe, lock, override, expiry, conflict, and resolution events. | Must | G3, G6 |

#### 7.7 Communication, Follow-Up, And Notifications

| ID | Requirement | Priority | Goals |
|---|---|---|---|
| PRD-FR-037 | Each lead shall have a communication and activity timeline covering app notes, tasks, reminders, calls, WhatsApp/SMS/email events where integrated, visits, booking events, and payout-relevant milestones. | Must | G2, G6 |
| PRD-FR-038 | Users shall create follow-up tasks, reminders, notes, and dispositions from lead/project/CP contexts. | Must | G2, G7 |
| PRD-FR-039 | The app shall support native push notifications on Android and iOS. | Must | G7 |
| PRD-FR-040 | The app shall include an in-app notification center where users can review past notifications. | Must | G7 |
| PRD-FR-041 | Notifications shall deep-link to the relevant product state wherever possible, including lead conflict, pending sync, site visit, payout, document rejection, collateral update, task, or support ticket. | Must | G2, G7 |
| PRD-FR-042 | Users shall have notification permission handling and role-appropriate notification preferences where policy permits. | Should | G7 |
| PRD-FR-043 | Critical notifications shall remain visible in-app even if OS push permission is denied. | Must | G7 |

#### 7.8 Site Visit Scheduling, Proof, And Outcome

| ID | Requirement | Priority | Goals |
|---|---|---|---|
| PRD-FR-044 | CP users shall request or schedule site visits for accepted leads, subject to project/site rules. | Must | G2, G3 |
| PRD-FR-045 | Site visits shall support confirmation, reschedule, cancellation, no-show, and completion states. | Must | G2 |
| PRD-FR-046 | The system shall capture visit proof using launch-approved methods including QR, OTP, geofence, site-desk confirmation, or admin verification. | Must | G3, G6 |
| PRD-FR-047 | Site visit proof shall link to lead, CP firm, CP employee, buyer, project, timestamp, verification method, and outcome. | Must | G3, G6 |
| PRD-FR-048 | Site/project users shall record visit outcomes and next actions where permitted. | Should | G2 |
| PRD-FR-049 | Visit status changes shall trigger notifications to relevant CP, RM, site, and admin users. | Must | G2, G7 |
| PRD-FR-077 | Geofenced visit proof shall capture location only during a scheduled or active visit workflow, require device permission and role permission, store configured accuracy metadata, and offer QR/OTP/site-desk/admin fallback when location capture fails or is denied. | Must | G3, G6, G7 |

#### 7.9 Booking Visibility

| ID | Requirement | Priority | Goals |
|---|---|---|---|
| PRD-FR-050 | CP owners and permitted CP employees shall see booking status for their own eligible leads, with data exposure controlled by RBAC and policy. | Must | G2, G4, G6 |
| PRD-FR-051 | Booking status shall show understandable milestones such as booked, documentation pending, payment pending, cancelled, and commission eligibility pending, subject to source data. | Must | G4 |
| PRD-FR-052 | The app shall avoid exposing buyer-sensitive, finance-sensitive, or internal-only information to CP users unless explicitly permitted. | Must | G6 |
| PRD-FR-053 | Booking cancellation or eligibility-impacting events shall update payout state and notify permitted users. | Must | G4, G7 |

#### 7.10 Commission, Invoice, And Payout Ledger

| ID | Requirement | Priority | Goals |
|---|---|---|---|
| PRD-FR-054 | CP owners shall see a payout status ledger for eligible firm transactions, subject to finance policy. | Must | G4 |
| PRD-FR-055 | The payout ledger shall show status such as not eligible, eligible, invoice pending, invoice under review, approved, rejected, payment scheduled, paid, failed, disputed, or clawback. | Must | G4 |
| PRD-FR-056 | Payout records shall show commission basis, deductions, GST/TDS treatment, expected date, paid date, payment reference, and reason codes where available and permitted. | Must | G4, G6 |
| PRD-FR-057 | Finance users shall approve, reject, request correction, schedule, mark paid, mark failed, reconcile, claw back, and dispute payout records with reason and audit trail. | Must | G4, G6 |
| PRD-FR-058 | CP owners shall raise payout disputes linked to booking, invoice, payout status, and evidence. | Must | G4 |
| PRD-FR-059 | The app shall not promise payout dates unless finance has configured an approved payout SLA. | Must | G4 |
| PRD-FR-078 | Payout processing shall use a finance-controlled state machine with maker-checker controls for configured high-risk actions and immutable audit events for every status change. | Must | G4, G6 |

#### 7.11 Support, Dispute, And Audit

| ID | Requirement | Priority | Goals |
|---|---|---|---|
| PRD-FR-060 | Users shall raise support tickets from CP, lead, visit, booking, payout, document, or project contexts. | Must | G3, G4, G7 |
| PRD-FR-061 | Support tickets shall capture category, severity, linked entity, description, attachments, owner, status, SLA, and resolution. | Must | G5, G6 |
| PRD-FR-062 | Admin/support users shall view evidence bundles for lead, site visit, payout, compliance, and collateral disputes. | Must | G3, G4, G6 |
| PRD-FR-063 | The system shall maintain audit logs for login, role changes, CP approval, document decisions, lead lock/override, collateral publishing, visit proof, payout approval, and dispute resolution. | Must | G6 |
| PRD-FR-064 | Admin/compliance users shall export audit evidence for configured date/entity ranges. | Should | G6 |

#### 7.12 Analytics And Dashboards

| ID | Requirement | Priority | Goals |
|---|---|---|---|
| PRD-FR-065 | Leadership shall view aggregate CP network KPIs by geography, project, RM, CP segment, and time period. | Must | G1, G5 |
| PRD-FR-066 | CP sourcing heads shall view CP sourcing funnel, onboarding conversion, activation, inactivity, and escalations. Advanced CP health scoring is deferred. | Must | G1, G5 |
| PRD-FR-067 | RMs shall view assigned CP pipeline, tasks, inactive CPs, lead/visit/bookings, and escalations. | Must | G1, G5 |
| PRD-FR-068 | CP owners shall view firm-level leads, visits, bookings, team performance, payout, and disputes. | Must | G1, G4 |
| PRD-FR-069 | Finance shall view payout queue, SLA adherence, rejected payouts, failed payments, and dispute volume. | Must | G4 |
| PRD-FR-070 | Metrics shall be event-instrumented so adoption and funnel outcomes can be measured without manual reporting. | Must | G5, G6 |

#### 7.13 Offline-First Sync

| ID | Requirement | Priority | Goals |
|---|---|---|---|
| PRD-FR-071 | The app shall cache safe role-permitted data for offline use, including assigned project summaries, approved collateral metadata, previously opened assets where allowed, lead drafts, tasks, reminders, and notification history. | Must | G2, G7 |
| PRD-FR-072 | The app shall allow users to create offline drafts and queued submissions for launch-approved actions: leads, notes, tasks, visit updates, support ticket drafts, and onboarding/compliance document uploads. | Must | G2, G7 |
| PRD-FR-073 | Offline-created actions shall enter a visible sync queue with status: queued, syncing, synced, failed, blocked, or conflict. | Must | G7 |
| PRD-FR-074 | The app shall automatically sync queued actions when connectivity returns and the session/permissions remain valid. | Must | G7 |
| PRD-FR-075 | The app shall resolve sync conflicts with clear user/admin actions and shall not silently overwrite server-side authoritative data. | Must | G6, G7 |
| PRD-FR-076 | Lead lock and duplicate detection shall be confirmed by server sync before ownership is final; offline lead submissions shall show pending sync until confirmed. | Must | G3, G7 |
| PRD-FR-079 | Queued document uploads shall show file-level upload state, support retry/resume/cancel/delete before sync, preserve local encryption, enforce allowed file types and size limits, and require server-side validation before changing compliance status. | Must | G1, G6, G7 |

### Non-Functional Requirements

| ID | Category | Requirement | Target / Notes |
|---|---|---|---|
| PRD-NFR-001 | Simplicity | Core CP employee tasks should be possible with minimal steps: project search, share, lead submit, follow-up, visit schedule. | Target to validate: common actions within 3 taps after role home. |
| PRD-NFR-002 | Speed | App shell should become usable quickly on supported devices. | Target to validate: under 3 seconds on supported devices and good network. |
| PRD-NFR-003 | Speed | Critical screen loads should feel immediate with cached data where available. | Target to validate: under 2 seconds on good network for common screens. |
| PRD-NFR-004 | Offline reliability | Safe offline saves should complete locally without blocking on network. | Target to validate: under 1 second local save for draft actions. |
| PRD-NFR-005 | Reliability | Sync queue must be visible and recoverable after app restart, network loss, or backgrounding. | Must not lose queued user actions. |
| PRD-NFR-006 | Security | RBAC enforcement must occur server-side and client-side. | Client controls are UX aids, not authority. |
| PRD-NFR-007 | Security | Sensitive data at rest and in transit must be encrypted according to Justo/Manthan standards. | Exact standards pending tech review. |
| PRD-NFR-008 | Privacy | Buyer and CP personal data exposure must follow role, consent, and policy controls. | No unauthorized exposure in notifications or shared links. |
| PRD-NFR-009 | Compliance | RERA, GST, PAN, KYC, bank, invoice, audit, and consent workflows must be auditable. | Exact validation sources pending decision. |
| PRD-NFR-010 | Accessibility | Mobile app should meet WCAG 2.2 AA-equivalent practices where applicable. | Text contrast, touch targets, screen reader labels, focus order. |
| PRD-NFR-011 | Observability | Key events, errors, sync failures, notification delivery, and API failures must be logged for support. | Logs must avoid sensitive payload leakage. |
| PRD-NFR-012 | Availability | Product must degrade gracefully when Manthan or third-party services are unavailable. | Show cached data, queue safe actions, explain blocked actions. |
| PRD-NFR-013 | Maintainability | Source-of-truth ownership must be explicit for CP, lead, project, visit, booking, payout, audit, and notification objects. | Prevent duplicate domain logic across app and Manthan. |
| PRD-NFR-014 | Native capability | Android and iOS builds must support native push notifications and secure local storage. | Required for field reliability and reviewable notifications. |
| PRD-NFR-015 | Location privacy | Geofencing must be limited to scheduled/active site-visit proof and must not become continuous workforce tracking. | Requires consent, permission checks, retention policy, and fallback path. |
| PRD-NFR-016 | File security | Queued document uploads must use secure local storage, encrypted transport, retry-safe upload, and server-side validation before status changes. | Prevents false compliance completion and data leakage. |
| PRD-NFR-017 | Financial controls | Payout processing must support auditability, maker-checker controls where configured, immutable status history, and reconciliation against the authoritative finance/payment source. | Prevents payout errors and finance leakage. |

### Acceptance Criteria

#### Identity And Role Home

```gherkin
Scenario: User with one assigned role lands on role home
  Given a user has one active assigned role
  When the user signs in successfully
  Then the app routes the user to the home screen for that role
  And the visible actions match the user's permissions
```

```gherkin
Scenario: User with multiple roles selects active role
  Given a user has more than one active assigned role
  When the user signs in successfully
  Then the app shows the permitted role choices
  And the user can select one active role context
  And subsequent screens use that role context until changed or session ends
```

#### CP Onboarding

```gherkin
Scenario: CP owner submits onboarding documents
  Given a CP owner has an incomplete onboarding checklist
  When the CP owner uploads required documents and submits the profile
  Then the CP profile status changes to under review
  And the assigned RM and compliance reviewer receive a notification
  And the CP owner can see the submitted status and next expected step
```

```gherkin
Scenario: Compliance rejects a document
  Given a CP document is under review
  When compliance rejects the document with a reason
  Then the CP owner and assigned RM receive a notification
  And the document status shows the rejection reason
  And the CP owner can resubmit the document
```

#### CP Employee Exit

```gherkin
Scenario: CP owner deactivates an employee
  Given a CP employee has active leads and tasks
  When the CP owner deactivates the employee
  Then the employee loses access according to policy
  And historical attribution remains unchanged
  And active leads and tasks require reassignment or admin-approved handling
```

#### Project Catalog And Collateral

```gherkin
Scenario: CP agent shares approved collateral
  Given a CP agent has access to an active project
  And approved collateral is available
  When the CP agent shares the collateral from the app
  Then the app creates a share event
  And the buyer receives only the approved version
  And expired collateral cannot be shared
```

#### Lead Ownership

```gherkin
Scenario: CP agent submits a new non-duplicate lead online
  Given a CP agent has permission to submit leads
  And the buyer phone number does not match an active duplicate rule
  When the CP agent submits the lead
  Then the system returns accepted status
  And the lead shows owner, attribution, lock state, and next action
```

```gherkin
Scenario: CP agent submits a possible duplicate lead
  Given a CP agent has permission to submit leads
  And the buyer phone number matches a configured duplicate rule
  When the CP agent submits the lead
  Then the system returns conflict or rejected status according to policy
  And the app shows the reason category and allowed next action
  And unauthorized owner or buyer details are not exposed
```

```gherkin
Scenario: CP agent submits a lead while offline
  Given a CP agent is offline
  When the CP agent saves a lead submission
  Then the lead is stored in the local sync queue as pending sync
  And the app does not show final lead ownership until server sync completes
```

#### Notifications

```gherkin
Scenario: Notification deep-links to lead conflict
  Given a submitted lead enters conflict status
  When the system sends a notification to the CP owner
  Then the notification appears in the native OS notification channel where permission exists
  And the notification appears in the in-app notification center
  And tapping the notification opens the lead conflict detail screen
```

#### Site Visit

```gherkin
Scenario: Visit proof is captured
  Given a site visit is scheduled for an accepted lead
  When the visit is verified using the configured proof method
  Then the visit status changes to verified
  And the proof event is linked to lead, CP firm, CP employee, buyer, project, timestamp, and method
  And permitted users receive visit status updates
```

```gherkin
Scenario: Geofenced visit proof succeeds during visit window
  Given a site visit is scheduled for an accepted lead
  And the user has role permission to capture visit proof
  And device location permission is granted
  When the user checks in within the configured geofence and visit window
  Then the visit proof is captured with timestamp, proof method, and configured accuracy metadata
  And the proof event is linked to the lead, CP firm, CP employee, buyer, project, and visit
  And the system does not continue tracking location after the visit proof event is complete
```

```gherkin
Scenario: Geofenced visit proof falls back when location is unavailable
  Given a site visit is scheduled for an accepted lead
  When location permission is denied or geofence accuracy is insufficient
  Then the app shows the configured fallback options
  And the visit can be verified using QR, OTP, site-desk confirmation, or admin verification
  And the fallback reason is recorded in the audit trail
```

#### Payout Ledger

```gherkin
Scenario: CP owner reviews payout status
  Given a booking has reached a payout-relevant milestone
  When the CP owner opens the payout ledger
  Then the CP owner can see the payout status allowed by policy
  And the ledger shows missing actions or expected date only if finance has configured them
```

```gherkin
Scenario: Finance rejects payout
  Given a payout request is under finance review
  When finance rejects the payout with a reason
  Then the payout status changes to rejected
  And the reason is visible to permitted CP and Justo users
  And the action is recorded in the audit log
```

```gherkin
Scenario: Finance processes payout through controlled state machine
  Given a payout record is eligible for finance review
  When finance approves, schedules, marks paid, or reconciles the payout
  Then each status change follows the configured payout state machine
  And maker-checker approval is required for configured high-risk actions
  And the payout record stores reason, actor, timestamp, payment reference where applicable, and audit trail
```

#### Offline Sync

```gherkin
Scenario: Queued actions sync after reconnection
  Given a user has queued offline actions
  When connectivity returns
  And the user's session and permissions are valid
  Then the app automatically syncs queued actions
  And each action shows synced, failed, blocked, or conflict status
```

```gherkin
Scenario: CP uploads onboarding document while offline
  Given a CP owner or RM is completing onboarding with poor or no connectivity
  When the user adds an allowed document file
  Then the app stores the file securely in the upload queue
  And the file shows queued status with retry, cancel, and delete options
  And compliance status remains pending until server upload and validation succeed
```

## 8. UX And Design Considerations

### Product Design Principles

- [high] Role-first: the first screen must match the user's assigned role and daily job.
- [high] Status-first: every workflow must show current status, next action, owner, and reason where applicable.
- [high] Field-fast: CP employee and RM flows must prioritize speed, low typing, resilient drafts, and clear offline states.
- [high] Trust-visible: lead ownership, visit proof, booking state, payout state, and disputes must be visible enough to reduce calls and WhatsApp escalations.
- [moderate] Explain without training: screens should use plain-language labels, reason codes, and next-action buttons instead of internal CRM jargon.

### Wireframe Placeholders For Future UI Specs

The following are placeholders only. Detailed screen specs will be produced after persona-wise journey maps.

| Screen Placeholder | Primary Users | Core Purpose |
|---|---|---|
| Role selector / role home | Multi-role users | Choose or land in active role context |
| CP owner dashboard | CP owner | Firm status, team, leads, visits, bookings, payout, disputes |
| CP employee home | CP employee | Assigned projects, due follow-ups, lead quick action, sync state |
| RM dashboard | RM | CP prospects, activation tasks, escalations, performance |
| Sourcing head dashboard | CP sourcing head | CP funnel, RM productivity, activation, health |
| Project catalog | CP users, RM | Search/filter projects and view current facts |
| Project detail/share kit | CP users | View facts, inventory, offers, approved collateral, share |
| Lead quick submit | CP employee, CP owner | Phone-first lead registration and dedupe result |
| Lead detail/timeline | CP/RM/admin users | Status, ownership, follow-up, communication, visit, booking |
| Conflict/dispute detail | CP owner, admin/support | Evidence, status, decision, next action |
| Site visit schedule/proof | CP/RM/site users | Schedule, confirm, verify, outcome |
| Payout ledger | CP owner, finance | Eligibility, invoice, approval, deductions, paid/disputed state |
| Notification center | All users | Review prior notifications and deep-link to product state |
| Sync queue | Mobile users | See queued, failed, blocked, conflict actions |
| Admin/compliance queues | Admin/support/compliance | Review docs, conflicts, payouts, collateral, audit |

### Edge Case Handling

| Edge Case | Expected UX |
|---|---|
| User has no active role | Show no-access state and support contact. |
| User has multiple roles | Show role selector or admin default; allow role switch where permitted. |
| Push permission denied | Keep in-app notification center active and prompt only at appropriate moments. |
| Offline lead submission | Save as pending sync; do not show final ownership until server confirms. |
| Sync conflict | Show conflict state, reason, and next action; do not silently overwrite. |
| Expired collateral | Block share and point user to current approved collateral. |
| Suspended CP | Restrict configured actions and show suspension reason where policy permits. |
| Employee exits | Preserve attribution and force reassignment of active work. |
| Payout SLA unavailable | Show current status; do not invent expected date. |
| Unauthorized deep link | Open safe access-denied state, not a blank or leaking screen. |

### Accessibility Checklist

- Use readable text sizes and support OS font scaling where feasible.
- Maintain sufficient color contrast for statuses and warnings.
- Do not rely on color alone for lead, payout, visit, or sync states.
- Ensure touch targets are large enough for field use.
- Provide accessible labels for icons, status chips, inputs, and action buttons.
- Support logical focus order and screen reader navigation for critical flows.
- Make errors specific and actionable.
- Avoid time-limited actions without clear recovery.

## 9. Technical Notes

### Architecture Impact

[high] Manthan is assumed to remain the core CRM foundation. The CP app should be a mobile and service layer that reuses Manthan entities where Manthan is source of truth, and extends Manthan where the CP lifecycle is not currently modeled.

### Source-Of-Truth Rules

| Entity | Expected Source Of Truth | PRD Requirement |
|---|---|---|
| CP firm | Manthan CP master extended for lifecycle | Avoid duplicate CP masters. |
| CP employee | Manthan user/CP employee model | Preserve attribution and access state. |
| Role/permission | Manthan/common RBAC or agreed identity service | Enforce server-side. |
| Project/inventory | Manthan project/inventory modules | Show freshness timestamp/source. |
| Collateral | Manthan/project document repository or agreed CMS | Version and expiry required. |
| Lead | Manthan lead module | Add CP lock/conflict/dispute ledger. |
| Site visit | Manthan site-visit/walk-in modules extended | Add proof and outcome evidence. |
| Booking | Manthan booking/deal module | Expose CP-safe status. |
| Commission rule | Manthan finance/incentive config or finance system | Must be policy-controlled. |
| Invoice/payout | Finance/accounting system or Manthan finance module | Exposure depends on integration. |
| Notification | App notification service integrated to domain events | Must persist in-app history. |
| Audit log | Manthan/common audit layer | Mandatory for trust workflows. |

### Dependencies

| Dependency | Status | Risk |
|---|---|---|
| Manthan APIs for CP, lead, project, visit, booking, payout | [unknown] readiness not confirmed | High |
| Identity/RBAC service | [unknown] role model details pending | High |
| Push notification infrastructure | [unknown] provider pending | Medium |
| WhatsApp/SMS/email/call integrations | [unknown] integration scope pending | Medium |
| RERA validation source | [unknown] business/legal decision pending | High |
| Accounting/payment reconciliation | [unknown] integration path pending; core to launch payout processing | High |
| Offline storage and sync engine | [moderate] required by PRD | Medium |
| Analytics/event instrumentation | [moderate] required by PRD | Medium |
| Location/geofencing capability | [unknown] native implementation and consent model pending | High |
| Secure queued file upload | [unknown] file limits, malware scanning, and retry model pending | High |

### Data Schema Implications

The implementation will likely need or extend the following data concepts:

- CP firm lifecycle status and compliance status.
- CP prospect record before approved CP master, if Manthan does not already support this.
- CP employee role, project access, attribution, deactivation, and reassignment.
- Lead ownership ledger with duplicate check, lock, expiry, conflict, override, dispute.
- Project collateral version, status, expiry, share audit.
- Visit proof entity linked to lead, buyer, CP, project, and verification method.
- Geofence proof metadata: visit window, permission state, accuracy, fallback reason, retention rule, and audit event.
- Payout ledger state machine linked to booking, invoice, deductions, approvals, and payment.
- Payout processing state machine: maker/checker, approval, rejection, correction, scheduled payment, failed payment, paid, reconciliation, clawback, dispute.
- Notification entity with deep-link target, role visibility, read/unread state, and delivery status.
- Offline sync queue entity on device and server reconciliation events.
- Queued document upload entity: file metadata, local encrypted state, retry count, upload status, validation status, rejection reason, and linked compliance checklist item.

### Future-Proofing Considerations

- Keep AI calling, AI summaries, campaign automation, microsites, and advanced CP scoring behind clear domain events and feature flags.
- Do not embed business policy such as lock duration, payout SLA, or commission eligibility only in mobile clients.
- Do not implement geofencing as open-ended location tracking; keep it bound to site-visit proof events.
- Do not treat uploaded compliance documents as accepted until server-side validation and reviewer/system decision completes.
- Do not bypass finance controls for payout speed; payout transparency must be paired with approval and reconciliation discipline.
- Maintain an exportable audit trail for lead, visit, payout, compliance, and collateral events.
- Design role homes so additional roles can be added without changing identity assumptions.

## 10. Metrics And Success Criteria

### KPI Targets

Exact baseline values are not yet available. Targets below are directional and must be calibrated after baseline measurement.

| KPI | Definition | Target Direction | Owner | Instrumentation |
|---|---|---|---|---|
| CP onboarding completion rate | Approved CPs completing required onboarding steps | Increase | CP sourcing | CP profile/document events |
| Time to CP approval | Time from CP registration to approval/rejection | Decrease | CP sourcing/compliance | Status timestamps |
| CP activation rate | Approved CPs completing first lead/site visit/booking milestone | Increase | CP sourcing | Lead/visit/booking events |
| Time to first lead | Approval to first accepted lead | Decrease | CP sourcing/RM | CP and lead timestamps |
| Lead acceptance rate | Submitted leads accepted without conflict/rejection | Increase | Sales ops | Lead submission outcomes |
| Lead conflict rate | Submitted leads entering conflict | Decrease or stabilize with better detection | Sales ops | Conflict outcomes |
| Verified visit rate | Scheduled visits with proof captured | Increase | Sales ops/site team | Visit proof events |
| Visit-to-booking conversion | Verified visits converting to bookings | Increase | Sales leadership | Visit/booking linkage |
| Payout SLA adherence | Eligible payouts paid within configured SLA | Increase | Finance | Payout ledger timestamps |
| Payout support volume | Payout-related support tickets per active CP | Decrease | Finance/support | Ticket categories |
| Notification action rate | Notifications opened and acted on | Increase | Product | Notification delivery/open/deep-link events |
| Offline sync success rate | Queued actions that sync without user/admin correction | Increase | Product/tech | Sync queue events |
| RM productivity | CPs activated and maintained per RM | Increase | CP sourcing | RM assignments and CP activity |
| CP satisfaction | CP-reported score on trust and usability | Increase | Product/business | Surveys/interviews |

### Launch Readiness Criteria

- All must-have requirements have a tested happy path and at least one tested exception path.
- RBAC enforcement is verified for each role and unauthorized deep link.
- Offline queue survives app restart and network transition.
- Push and in-app notifications work for critical events.
- Lead conflict and payout states show correct reason and next action.
- Source-of-truth ownership is signed off for CP, lead, project, visit, booking, payout, notification, and audit.
- Support team has an escalation process for lead, payout, compliance, and sync failures.

## 11. Risks And Mitigations

| Risk | Severity | Why It Matters | Mitigation |
|---|---|---|---|
| CPs do not adopt the app | High | Product fails if CPs continue on WhatsApp/manual flows | Optimize first-session value: project catalog, share kit, lead lock, payout visibility |
| Manthan source-of-truth ambiguity | High | Duplicate data creates operational disputes | Sign off source-of-truth matrix before build |
| Lead disputes continue | High | CP trust breaks if ownership remains opaque | Implement dedupe, lock, conflict, dispute, and audit ledger |
| Payout visibility overpromises | High | CPs may lose trust if expected dates are wrong | Show expected dates only after finance SLA configuration |
| Offline lead ownership confusion | High | CP may believe a lead is protected before server check | Mark offline leads as pending sync until server confirms |
| Queued document upload false completion | High | CP may assume compliance is complete before server validation | Show uploaded as pending validation until server and reviewer/system checks pass |
| Geofence privacy overreach | High | Visit proof can become workforce tracking if poorly bounded | Capture only during visit workflow with consent, fallback, retention, and audit rules |
| Payout processing control failure | High | Incorrect approval/payment states can create financial leakage | Use state machine, maker-checker, reconciliation, reason codes, and immutable audit |
| Compliance gaps | High | RERA/KYC/GST/bank issues can create legal and payout risk | Add compliance lifecycle, expiry, blocking, and audit |
| Push notifications fail or are disabled | Medium | Follow-ups and escalations may be missed | Use in-app notification center and critical banners |
| Role complexity delays delivery | Medium | Many personas and permissions increase scope | Build from shared RBAC model and role homes; sequence delivery later |
| AI distracts from core workflows | Medium | Cost and complexity can rise before trust is solved | Keep AI deferred unless tied to measurable outcomes |
| Vendor lock-in | Medium | Future changes become costly | Require API, source, export, and IP clarity in SoW |
| Data privacy leakage in notifications/shared links | High | Buyer/CP data can leak outside permitted context | Use minimal notification payloads and permission checks on open |

## 12. Rollout Plan

### Important Scope Boundary

[high] The next artifact is persona-wise journey maps, followed by Google Stitch-ready UI screen specs. This section defines readiness gates and rollout controls only.

### Release Gates

| Gate | Required Evidence |
|---|---|
| Business policy gate | Decisions on lead lock, direct-vs-CP priority, payout SLA, compliance blocking, CP employee exit, and buyer data exposure |
| Technical source-of-truth gate | Signed matrix for Manthan/API ownership and external system dependencies |
| Security/RBAC gate | Role matrix tested across app, API, notifications, offline cache, and deep links |
| Field workflow gate | CP owner, CP employee, RM, finance, and ops users validate critical journeys |
| Offline reliability gate | Queued actions, reconnection, conflict handling, and failed sync recovery tested |
| Notification gate | Native push, in-app history, and deep links tested for critical events |
| Support readiness gate | Support categories, SLAs, owners, and escalation workflows configured |
| Analytics gate | KPI events implemented and dashboards validated |

### Feature Flag Strategy

- Use feature flags for role homes, lead conflict workflow, site visit proof methods, payout ledger exposure, notification categories, offline submission types, and AI/deferred features.
- Keep business policy values server-configured, not hardcoded in the app.
- Allow internal pilot users before broad CP exposure.

### Communication Plan

| Audience | Message |
|---|---|
| Justo leadership | Business goals, KPI dashboard, risk controls, rollout gates |
| CP sourcing/RMs | CP acquisition workflow, activation tasks, escalation handling |
| CP owners | How app protects leads, simplifies team management, and improves payout visibility |
| CP employees | How to find projects, share approved material, register leads, schedule visits, and track follow-ups |
| Finance | Payout ledger controls, visibility rules, approval/rejection flows |
| Ops/support/compliance | Queues, evidence bundles, audit logs, SLAs |
| Vendor/implementation team | Requirements, acceptance criteria, source-of-truth matrix, open decisions |

## 13. Decision Log

| Date | Decision | Owner | Status | Notes |
|---|---|---|---|---|
| 2026-05-31 | PRD will feed persona-wise journey maps directly. | Product | Decided | Product sequencing will be revisited only when explicitly requested. |
| 2026-05-31 | Product model uses single credential plus assigned role(s). | Product/business | Decided | Admin-based RBAC is mandatory. |
| 2026-05-31 | Offline-first behavior is preferred for safe mobile workflows. | Product | Decided | Server confirmation remains authoritative for lead ownership. |
| 2026-05-31 | Native push plus in-app notification center is required. | Product | Decided | Notifications should deep-link where possible. |
| 2026-05-31 | Core trust workflows take priority over AI-first scope. | Product/business | Draft decision | Needs stakeholder confirmation. |
| 2026-05-31 | Manthan remains assumed CRM foundation. | Product/technology | Draft decision | Needs technical source-of-truth validation. |

## 14. Success Story Narrative

Six months after launch, a CP owner in Pune no longer calls the RM each morning to ask which projects are current, whether a lead is protected, or when commission will be paid. The owner opens the Justo CP App with one credential, lands on the CP owner dashboard, sees team activity, pending follow-ups, accepted leads, scheduled visits, bookings, payout status, and two issues needing action.

An agent in the same firm meets a buyer, searches by budget and location, shares an approved project kit on WhatsApp, and registers the buyer's phone number in under a minute. The app immediately shows that the lead is accepted and protected. The buyer confirms a site visit, site proof is captured, and the visit outcome is visible to the CP owner, RM, and Justo ops team. When the booking reaches the finance milestone, the CP owner sees invoice status, deduction details, expected payout date where configured, and final paid status.

For Justo, the weekly business review changes from anecdotal status updates to measurable operating loops: CP onboarding, activation, lead acceptance, verified visits, bookings, payout SLA, and disputes. RMs focus on CPs that need activation or intervention. Finance reduces repetitive payout calls because CPs can see status. Compliance can export evidence instead of reconstructing events from chat messages.

The product succeeds because it does not ask CPs to work for the CRM. It makes the CRM work for CPs, RMs, finance, and leadership.

## 15. Open Questions And Assumptions

### Open Questions

| Question | Owner Needed | Impact |
|---|---|---|
| What is the exact lead-lock expiry duration? | Sales/CP leadership | Lead trust and conflict volume |
| What is the direct-vs-CP lead priority rule? | Sales leadership/legal | Conflict resolution |
| Who can override lead ownership and under what evidence? | Sales ops/compliance | Audit and dispute fairness |
| What booking milestone creates commission eligibility? | Finance/sales | Payout ledger accuracy |
| What payout SLA can Justo credibly show CPs? | Finance/leadership | CP trust |
| What GST/TDS rules must be shown in CP payout ledger? | Finance | Legal/financial correctness |
| What is the authoritative RERA validation source and renewal policy? | Legal/compliance | Compliance controls |
| What happens to leads when a CP employee exits? | CP sourcing/ops/legal | Attribution and data protection |
| What CP suspension policy should block app actions? | CP sourcing/legal | Risk controls |
| What buyer-facing data can CP-shared links expose? | Product/legal | Privacy and claim safety |
| Which Manthan APIs are production-ready for CP mobile integration? | Product/technology/I9 | Delivery feasibility |
| Is I9 default implementation partner, or are all vendors still active options? | Leadership/procurement | Delivery architecture |
| Which notification categories are legally/operationally sensitive? | Product/legal/compliance | Privacy and UX |
| Which offline actions are allowed for each role? | Product/technology | Sync complexity and risk |
| What geofence radius, accuracy threshold, consent copy, fallback path, and retention rule should apply? | Product/legal/technology | Visit proof reliability and privacy |
| What document file types, size limits, retry limits, malware scanning, and local retention rules should apply? | Product/technology/compliance | Queued upload reliability and data safety |
| Which payout actions happen in Manthan versus the finance/accounting system, and which reconciliation event is authoritative? | Finance/product/technology | Payout processing correctness |

### Assumptions

- [high] Android and iOS mobile apps are required.
- [high] Maharashtra is the first market.
- [high] Manthan remains the CRM foundation unless leadership changes direction.
- [high] The app must support CP owners and CP employees as distinct actors.
- [high] Admin-configured RBAC is mandatory.
- [high] Notifications must be native and reviewable in-app.
- [moderate] Payout ledger visibility is essential for CP loyalty.
- [moderate] CP telecaller workflows may be important but can be sequenced after core CP owner/agent journeys if needed.
- [moderate] Buyer-facing links should be limited to approved project facts and safe next actions.
- [unknown] Manthan's existing APIs fully support the required mobile/offline/deep-link workflows.

## 16. Glossary

| Term | Definition |
|---|---|
| BRD | Business Requirements Document. Defines business context, outcomes, personas, risks, and scope direction. |
| PRD | Product Requirements Document. Defines product behavior, requirements, acceptance criteria, metrics, and constraints. |
| CP | Channel Partner, typically a real estate broker/partner who sources buyers. |
| CP owner | The owner or administrator of a CP firm. |
| CP employee / agent | A user working under a CP firm who sells, registers leads, follows up, and schedules visits. |
| RM | Relationship Manager or sourcing employee responsible for CP acquisition, activation, and support. |
| Manthan | Justo's CRM foundation delivered by Indexnine/I9. |
| RBAC | Role-Based Access Control. Permissions are assigned by role and enforced in app and backend. |
| RERA | Real Estate Regulatory Authority. Relevant for real estate agent/project compliance. |
| Lead lock | A policy-controlled ownership period or state that protects a CP's submitted lead where applicable. |
| Duplicate detection | System logic to identify whether a submitted lead may already exist. |
| Conflict | A state where lead ownership or eligibility needs review under policy. |
| Site visit proof | Evidence that a buyer attended a site visit, such as QR, OTP, geofence, site-desk confirmation, or admin verification. |
| Geofencing | Location-based validation that a permitted user/device is within an approved project/site boundary during a scheduled or active visit workflow. |
| Payout ledger | CP-visible finance status view for commission eligibility, invoice, approval, deductions, payment, and disputes. |
| Payout processing | Finance-controlled workflow for approving, rejecting, scheduling, marking paid/failed, reconciling, clawing back, and disputing payouts. |
| Queued document upload | Offline-first upload flow where selected documents are stored locally, queued, synced later, and validated server-side before compliance status changes. |
| Sync queue | Local app queue holding offline actions until server sync succeeds, fails, or conflicts. |
| Deep link | A link or notification target that opens a specific app screen or product state. |
| Claim-safe collateral | Approved project material and facts that CPs are allowed to share. |
| SLA | Service Level Agreement, such as target time for payout or support resolution. |
| Gherkin | Acceptance criteria format using Given/When/Then scenarios. |

## Quality Check Report

| # | Verification Category | Status | Notes |
|---|---|---|---|
| 1 | Completeness | ✅ | All required Karo PRD sections are present, including PRD, quality report, AI gap report, and scope-gate addendum. |
| 2 | Clarity | ✅ | Acronyms are defined and major workflows use explicit actors, states, and next actions. |
| 3 | Actionability | ✅ | Requirements are numbered and paired with Gherkin acceptance criteria for critical flows. |
| 4 | Feasibility | ⚠️ | Feasibility depends on Manthan API readiness, RBAC model, finance integration, and offline sync architecture. |
| 5 | Risk & Edge Cases | ✅ | Major edge cases are listed, including offline lead ownership, unauthorized deep links, expired collateral, and employee exits. |
| 6 | Alignment | ✅ | Requirement groups map to product goals G1-G7. |
| 7 | Assumption Audit | ✅ | Open questions and assumptions are explicitly captured instead of being invented. |
| 8 | Accessibility Compliance | ⚠️ | Accessibility checklist is included; detailed screen-level validation must happen during UI spec/prototype work. |
| 9 | Evidence Rigor | ⚠️ | Local BRD/vendor evidence is used, but primary and secondary direct quotes are not available. |
| 10 | No Contradictions | ✅ | PRD is aligned to persona-wise journey map creation, marks launch exclusions, and keeps Manthan as assumed CRM foundation pending validation. |

## AI Gap Report

Overall Risk Level: Medium

### Detected Gaps

- Primary CP/RM/customer interview quotes are missing; the PRD should not be treated as field-validated yet.
- Quantitative baselines are missing for onboarding time, lead conflict rate, verified visit rate, payout SLA, and support volume.
- Manthan API readiness and source-of-truth ownership are not technically confirmed.
- Lead lock, direct-vs-CP priority, override authority, and conflict policy are open decisions.
- Payout SLA, GST/TDS display, invoice process, and accounting integration are open decisions.
- RERA validation source and compliance blocking policy are open decisions.
- Offline-first behavior is required, but exact allowed offline actions by role need technical and risk review.
- Geofencing is core scope, but radius, accuracy, consent, retention, and fallback policy are still open.
- Queued document upload is core scope, but file limits, scanning, retry limits, and local retention are still open.
- Full payout processing is core scope, but Manthan-vs-finance-system ownership and reconciliation authority are still open.
- Buyer-facing data exposure needs legal/product approval before shared links are specified in detail.
- Launch scope is now gated, but journey-map work must enforce the gate requirement-by-requirement.

### Recommended Clarifications

- Run stakeholder review to lock lead ownership policy, payout policy, compliance policy, and CP employee exit policy.
- Conduct 8-12 field interviews across CP owners, CP employees, RMs, finance, and support/compliance.
- Ask Manthan/I9 for an API/source-of-truth readiness matrix covering every PRD entity.
- Ask Manthan/I9 for explicit feasibility on geofence proof, queued document upload, and payout processing state machine.
- Define notification taxonomy, sensitivity rules, payload rules, and deep-link targets.
- Create persona-wise journey maps directly from this PRD.
- Convert those journey maps into Google Stitch-ready UI screen specs.
- Create a launch/deferred mapping for every journey step during journey-map creation.

---
*Draft status: v0.3, scope-gated and ready for persona-wise journey map creation, with geofencing, queued document uploads, and full payout processing restored as core differentiators pending stakeholder validation and open-question resolution.*
