# Journey Maps: Justo CP App

Draft version: v0.3
Date: 2026-05-31
Prepared for: Justo Realfintech
Primary inputs: `Justo_CP_App_BRD_Draft.md` v0.4 and `Justo_CP_App_PRD.md` v0.3
Artifact sequence: BRD -> PRD -> Persona-wise Journey Maps -> Google Stitch UI Screen Specs/Prototype

## Scope Gatekeeper Review

### Critical Gaps Fixed

The first journey-map draft covered only the CP Owner / Org Leader. The second draft added actionable journey maps for every persona named in the PRD. This third draft adds the missing UI-generation contracts Google Stitch needs to create coherent screens without inventing product scope:

- Universal screen states.
- Cross-persona handoffs.
- Per-screen data and state contracts.
- Persona-to-screen bundle mapping.
- Clear build/reuse/no-screen boundaries.

Personas covered:

- Justo Leadership.
- CP Sourcing Head.
- RM / Sourcing Employee.
- Sales/Admin Ops.
- Finance.
- Developer / Project Team.
- CP Owner / Org Leader.
- CP Employee / Agent.
- CP Telecaller.
- Buyer / Customer.
- Compliance / Support.

Each journey is constrained to the PRD-defined trust loop: onboarding, compliance, employee control, project enablement, lead ownership, follow-up, site-visit proof, booking visibility, payout processing, notifications, offline recovery, support, and audit.

### Google Stitch Readiness Rules

Every journey row contains:

- User action.
- System check.
- System response.
- UI requirement.
- PRD trace.

Google Stitch should create screens only from rows marked `Build Screen: Yes` or `Build Screen: Reuse`. Rows marked `Build Screen: No` are contextual or external-system actions and should not become new app screens.

### Universal Screen State Contract

Every generated screen must account for these states unless explicitly irrelevant:

| State | Required Behavior | Applies To |
|---|---|---|
| Loading | Show skeleton/progress without implying data is final. | All data-backed screens |
| Empty | Explain why no data exists and show the next allowed action. | Dashboards, queues, lists |
| Error | Show recoverable error message and retry/support path. | All data-backed screens |
| Access denied | Show safe denial without leaking restricted data. | Deep links, role-protected screens |
| Offline cached | Show cached timestamp and disable actions that require server authority. | Mobile role homes, catalog, lead/detail, sync queue |
| Pending sync | Show local queued status and warn that server confirmation is pending. | Leads, notes, tasks, uploads, visit updates |
| Conflict/blocked | Show reason, owner, next action, and escalation path. | Leads, sync queue, payouts, support, documents |
| Audit visible | Show timestamp, actor type, reason/status change where permitted. | Lead, visit, payout, document, support |

### Cross-Persona Handoff Map

These handoffs define how screens connect across personas. Google Stitch should reflect the source screen and target screen relationship in navigation, deep links, and status labels.

| Handoff ID | Triggering Persona | Trigger | Receiving Persona | Target Screen | Required UI Signal |
|---|---|---|---|---|---|
| HND-001 | RM | Creates CP prospect / assisted onboarding | CP Sourcing Head, Compliance | Sourcing Dashboard, Compliance Queue | Prospect status, RM owner, pending docs |
| HND-002 | CP Owner / RM | Uploads document | Compliance / Support | Document Review | Queued/synced/validation status, rejection reason |
| HND-003 | Compliance | Rejects or approves document | CP Owner, RM | Onboarding Checklist, Notification Center | Decision, reason, next action |
| HND-004 | Sales/Admin Ops | Publishes or expires collateral | CP Owner, CP Employee, RM | Project Catalog / Share Kit | Current version, expired-share block |
| HND-005 | CP Owner / CP Employee | Submits lead | Sales/Admin Ops, RM | Lead Conflict Resolution, Firm Lead Dashboard | Accepted/conflict/rejected/pending state |
| HND-006 | Sales/Admin Ops | Resolves lead conflict | CP Owner, CP Employee, RM | Lead Detail, Notification Center | Decision, reason, next action |
| HND-007 | CP Owner / CP Employee / RM | Schedules visit | Developer/Project, Buyer | Site Visit Schedule / Proof, Buyer Visit Confirmation | Slot, proof method, visit status |
| HND-008 | Buyer / Site / CP Employee | Completes visit proof | CP Owner, RM, Developer/Project | Site Visit Detail, Visit Outcome | Proof method, timestamp, fallback reason |
| HND-009 | Booking event from Manthan | Booking milestone changes | CP Owner, CP Employee if permitted, Finance | Booking Status, Payout Queue | CP-safe milestone, payout impact |
| HND-010 | Finance | Changes payout state | CP Owner, Leadership, Support | Payout Ledger, Leadership Dashboard, Evidence Bundle | Status, reason, reference, SLA |
| HND-011 | CP Owner / RM / Support | Raises dispute/ticket | Support / Compliance | Evidence Bundle / Support Ticket | Linked entity, category, SLA, owner |
| HND-012 | Support / Compliance | Resolves ticket | Originating persona | Notification Center, Support Ticket | Resolution, reason, audit timeline |

## Persona Coverage Matrix

| Persona | PRD Classification | Journey Status | Google Stitch Action |
|---|---|---|---|
| Justo Leadership | Launch control | Complete | Build lightweight dashboard/risk views only |
| CP Sourcing Head | Launch control | Complete | Build sourcing and activation control views |
| RM / Sourcing Employee | Launch core | Complete | Build RM field and activation views |
| Sales/Admin Ops | Launch core | Complete | Build admin configuration and exception views |
| Finance | Launch core | Complete | Build payout processing views |
| Developer / Project Team | Launch control | Complete | Build project/collateral/visit input views |
| CP Owner / Org Leader | Launch core | Complete | Build full CP owner flow |
| CP Employee / Agent | Launch core | Complete | Build mobile selling flow |
| CP Telecaller | Deferred specialist | Complete | Preserve basic queue flow; avoid AI/call intelligence |
| Buyer / Customer | App-linked, not core app user | Complete | Build only safe link/confirmation views or reuse buyer portal |
| Compliance / Support | Launch core | Complete | Build compliance, dispute, evidence, and audit views |

## Common App Foundation

These shared steps apply to every authenticated app persona and should be reused in UI specs.

| Step ID | User Action | System Check | System Response | UI Requirement | Build Screen | PRD Trace |
|---|---|---|---|---|---|---|
| GLOBAL-001 | User signs in with one credential. | Validate credential, active account, assigned role(s), CP/Justo context, device/session state. | User lands on assigned role home or role selector. | Login, loading, role selector, role home routing, safe error states. | Yes | PRD-FR-001 to PRD-FR-004 |
| GLOBAL-002 | User opens a deep link from notification. | Validate role, permission, entity access, current account state. | User lands on the exact allowed screen or access-denied state. | Notification center, deep-link resolver, access-denied state. | Yes | PRD-FR-006, PRD-FR-039 to PRD-FR-043 |
| GLOBAL-003 | User works with weak/no network. | Check cached data, local queue, session validity, allowed offline action list. | App shows cached data and queues allowed actions. | Offline banner, sync queue, queued/syncing/synced/failed/blocked/conflict states. | Yes | PRD-FR-071 to PRD-FR-076 |

## Persona Journey: Justo Leadership

Goal: Monitor CP business health and risk without operational detail overload.

| Step ID | Phase | User Action | System Check | System Response | UI Requirement | Build Screen | PRD Trace |
|---|---|---|---|---|---|---|---|
| JL-001 | Executive Review | Opens leadership dashboard. | Check leadership role, metric permissions, geography/project filters. | Shows aggregate CP network KPIs. | Dashboard with CP count, activation, leads, visits, bookings, payout SLA, disputes, compliance exceptions. | Yes | PRD-FR-065 |
| JL-002 | Executive Review | Filters by city, cluster, RM, project, CP segment, or date. | Query permitted aggregate metrics; suppress restricted PII. | Dashboard refreshes with scoped metrics. | Filter bar, saved view, empty/stale data state. | Yes | PRD-FR-065, PRD-NFR-008 |
| JL-003 | Risk Control | Opens risk exceptions. | Fetch dispute, payout delay, compliance expiry, failed sync, and collateral exception counts. | Shows ranked exception list. | Risk queue with severity, owner team, SLA, linked entity count. | Yes | PRD-FR-060 to PRD-FR-064 |
| JL-004 | Risk Control | Opens a high-severity exception. | Check leadership detail permission and privacy rules. | Shows summary and accountable team, not restricted raw data. | Exception detail summary with owner, status, escalation note, allowed drill-down. | Yes | PRD-FR-052, PRD-FR-062 |

## Persona Journey: CP Sourcing Head

Goal: Build, activate, and govern the CP network through RM-owned execution.

| Step ID | Phase | User Action | System Check | System Response | UI Requirement | Build Screen | PRD Trace |
|---|---|---|---|---|---|---|---|
| CSH-001 | Sourcing Control | Opens sourcing dashboard. | Check sourcing-head role, geography/team permissions. | Shows CP prospect funnel, activation, inactivity, and escalations. | Sourcing dashboard with prospect statuses, RM workload, pending docs, activation blockers. | Yes | PRD-FR-021, PRD-FR-066 |
| CSH-002 | CP Prospecting | Creates/imports CP prospect or assigns RM. | Validate required fields, duplicate CP/prospect, RM availability, territory rules. | Prospect is created and assigned. | Prospect create/import form, duplicate warning, RM assignment selector, status. | Yes | PRD-FR-018, PRD-FR-019 |
| CSH-003 | Onboarding Governance | Reviews onboarding queue. | Fetch CPs pending docs, under review, rejected, blocked, approved. | Shows blockers by CP and RM. | Onboarding queue with CP, RM, missing docs, ageing, next action. | Yes | PRD-FR-009, PRD-FR-020 |
| CSH-004 | Activation Governance | Opens inactive or stalled CP. | Check activation signals: first login, employee, project access, first lead, first visit. | Shows activation gap and owner. | Activation detail with checklist, RM notes, escalation CTA. | Yes | PRD-FR-019, PRD-FR-021, PRD-FR-022 |
| CSH-005 | Escalation | Escalates lead, compliance, payout, or RM issue. | Validate category, linked entity, owner team, SLA. | Support/escalation ticket is created or updated. | Escalation modal with linked CP, category, severity, notes, owner team. | Reuse | PRD-FR-060, PRD-FR-061 |

## Persona Journey: RM / Sourcing Employee

Goal: Recruit, onboard, activate, and support CPs in the field.

| Step ID | Phase | User Action | System Check | System Response | UI Requirement | Build Screen | PRD Trace |
|---|---|---|---|---|---|---|---|
| RM-001 | Field Start | Opens RM home. | Check assigned CP prospects, active CPs, tasks, escalations, offline queue. | Shows prioritized field work. | RM home with today tasks, pending docs, stalled CPs, escalations, sync queue. | Yes | PRD-FR-020, PRD-FR-067 |
| RM-002 | CP Prospecting | Creates CP prospect after field meeting. | Validate duplicate CP/prospect, required fields, territory/source, offline state. | Prospect saved online or queued. | CP prospect form with save draft, source, territory, next follow-up, sync state. | Yes | PRD-FR-018, PRD-FR-019, PRD-FR-073 |
| RM-003 | Assisted Onboarding | Helps CP upload documents. | Check file type/size, local secure storage, document category, network. | Document uploads or enters secure queue. | Assisted onboarding screen with checklist, queued uploads, retry/cancel/delete, pending validation. | Yes | PRD-FR-008, PRD-FR-072, PRD-FR-079 |
| RM-004 | Activation | Assigns projects or triggers activation checklist. | Check CP approval/compliance state, project access, role permissions. | Projects or activation tasks are assigned where allowed. | Activation checklist with project access, first login, first employee, first lead, first visit. | Yes | PRD-FR-019, PRD-FR-020, PRD-FR-023 |
| RM-005 | Support | Opens CP escalation for lead, visit, payout, or compliance. | Validate linked CP/lead/visit/payout and RM access. | Shows status and allowed action/escalation path. | Escalation detail with linked evidence, owner team, SLA, comment/action. | Reuse | PRD-FR-060 to PRD-FR-062 |
| RM-006 | Visit Support | Schedules or supports a site visit. | Check accepted lead, slot rules, project/site rules, buyer details. | Visit request/status is created or updated. | Visit scheduling screen with lead, buyer, project, slot, proof method status. | Reuse | PRD-FR-044, PRD-FR-045, PRD-FR-049 |

## Persona Journey: Sales/Admin Ops

Goal: Keep operating rules, project access, collateral, lead conflicts, and exceptions controlled.

| Step ID | Phase | User Action | System Check | System Response | UI Requirement | Build Screen | PRD Trace |
|---|---|---|---|---|---|---|---|
| OPS-001 | Admin Start | Opens admin queue. | Check admin role and queue permissions. | Shows pending configs, conflicts, collateral, exceptions, failed notifications. | Admin queue with tabs: setup, collateral, conflicts, exceptions, audit. | Yes | PRD-FR-004, PRD-FR-060 |
| OPS-002 | Project Access | Configures CP/project access. | Check CP compliance, geography, project status, role permission. | Project access is updated and audited. | Access configuration table with CP, project, status, reason, save confirmation. | Yes | PRD-FR-023, PRD-FR-063 |
| OPS-003 | Collateral Governance | Publishes, expires, or replaces collateral. | Check approval state, version, expiry, project assignment, claim-safe fields. | Collateral status updates and expired versions are blocked from share. | Collateral manager with version, expiry, approve/expire/replace, audit note. | Yes | PRD-FR-026 to PRD-FR-028 |
| OPS-004 | Lead Conflict | Resolves lead conflict. | Fetch duplicate evidence, timestamps, owner, source, policy rules, privacy constraints. | Conflict decision is saved with reason and audit event. | Conflict detail with evidence bundle, policy reason, decision buttons, audit trail. | Yes | PRD-FR-030 to PRD-FR-036 |
| OPS-005 | Exception Handling | Overrides, suspends, reactivates, or reassigns with reason. | Check permission, policy, linked work, audit requirement. | Exception action is applied and audited. | Exception action modal with reason, affected users/leads, confirmation, audit state. | Yes | PRD-FR-010, PRD-FR-016, PRD-FR-063 |

## Persona Journey: Finance

Goal: Process payouts accurately while making CP-visible status transparent.

| Step ID | Phase | User Action | System Check | System Response | UI Requirement | Build Screen | PRD Trace |
|---|---|---|---|---|---|---|---|
| FIN-001 | Finance Start | Opens payout queue. | Check finance role, eligible booking/payout records, SLA, state machine. | Shows payout queue by state and priority. | Payout queue with eligible, invoice pending, under review, approved, scheduled, failed, disputed, clawback. | Yes | PRD-FR-054, PRD-FR-055, PRD-FR-069 |
| FIN-002 | Eligibility Review | Opens payout detail. | Fetch booking milestone, CP eligibility, invoice, GST/TDS, bank/KYC, cancellation risk. | Shows validation checklist and current payout state. | Payout detail with validation checklist, linked lead/booking, docs, deductions, risk flags. | Yes | PRD-FR-056, PRD-FR-078 |
| FIN-003 | Approval | Approves, rejects, or requests correction. | Check state transition, maker-checker rule, required reason, policy. | Payout state changes and audit event is created. | Approval action panel with approve/reject/request correction, reason, maker-checker indicator. | Yes | PRD-FR-057, PRD-FR-078 |
| FIN-004 | Payment | Schedules, marks paid/failed, or records payment reference. | Check approved state, payment reference format, reconciliation source. | Payment state updates and CP-visible status changes. | Payment action panel with scheduled date, reference, amount, failure reason. | Yes | PRD-FR-057, PRD-FR-059 |
| FIN-005 | Reconciliation | Reconciles payment or initiates clawback/dispute. | Check accounting/payment source, reconciliation event, prior payout state. | Record is reconciled, disputed, or clawed back with immutable audit. | Reconciliation panel with source reference, status, clawback/dispute reason, audit timeline. | Yes | PRD-FR-057, PRD-FR-078 |

## Persona Journey: Developer / Project Team

Goal: Keep project data, approved collateral, visit instructions, and outcomes accurate.

| Step ID | Phase | User Action | System Check | System Response | UI Requirement | Build Screen | PRD Trace |
|---|---|---|---|---|---|---|---|
| DEV-001 | Project Start | Opens project console. | Check project-team role and assigned projects. | Shows projects requiring updates or approvals. | Project console with assigned projects, stale data flags, collateral approvals, visit items. | Yes | PRD-FR-024, PRD-FR-025 |
| DEV-002 | Project Facts | Updates project facts, inventory, offers, RERA details, or site instructions. | Validate required fields, source, freshness timestamp, approval rules. | Project facts are saved or sent for approval. | Project facts form with freshness, validation, approval status, audit note. | Yes | PRD-FR-024, PRD-FR-025 |
| DEV-003 | Collateral Input | Uploads or approves collateral for CP sharing. | Check file/type/version, approval permission, expiry, claim-safe fields. | Collateral becomes pending/approved/expired according to workflow. | Collateral review screen with preview, approve/reject/expire, version, reason. | Reuse | PRD-FR-026 to PRD-FR-028 |
| DEV-004 | Visit Outcome | Confirms site visit outcome or site notes. | Check visit record, project assignment, proof status, allowed outcome fields. | Visit outcome is recorded and lead timeline updates. | Visit outcome screen with verified status, outcome, note, next action. | Reuse | PRD-FR-047, PRD-FR-048 |

## Persona Journey: CP Owner / Org Leader

Goal: Run CP firm operations with clear team control, lead ownership, booking status, payout status, and disputes.

| Step ID | Phase | User Action | System Check | System Response | UI Requirement | Build Screen | PRD Trace |
|---|---|---|---|---|---|---|---|
| CPO-001 | Owner Home | Opens CP owner home. | Check CP firm, compliance status, team, lead/payout/visit/dispute summaries, notifications, sync queue. | Shows firm operating summary and urgent actions. | CP Owner home with firm status, team alerts, leads, visits, bookings, payouts, disputes, sync queue. | Yes | PRD-FR-068, PRD-FR-071 |
| CPO-002 | Onboarding | Completes firm profile and uploads documents. | Validate required fields, file rules, queued upload state, server validation. | Profile/document status moves to draft, queued, under review, rejected, or approved. | Onboarding checklist and document upload queue with retry/cancel/delete and validation state. | Yes | PRD-FR-007 to PRD-FR-012, PRD-FR-079 |
| CPO-003 | Team Control | Invites, assigns, or deactivates employee. | Check permission, employee uniqueness, active work, reassignment need, audit. | Employee access changes and active work is reassigned where required. | Team management with invite, role/project access, deactivate, reassignment, reason. | Yes | PRD-FR-013 to PRD-FR-017 |
| CPO-004 | Project Enablement | Opens project catalog and shares approved collateral. | Check assigned projects, collateral approval/expiry, freshness, share permission. | Shows permitted projects and records approved share event. | Project catalog/detail/share kit with freshness, approved assets, blocked expired state. | Yes | PRD-FR-023 to PRD-FR-028 |
| CPO-005 | Lead Ownership | Registers or reviews firm lead. | Run required fields, duplicate detection, ownership/lock rules, online/offline state. | Lead becomes accepted, conflict, rejected, pending sync, or pending review. | Lead quick submit, result screen, firm lead dashboard, conflict detail. | Yes | PRD-FR-029 to PRD-FR-036, PRD-FR-076 |
| CPO-006 | Visit Visibility | Schedules/reviews visit and proof. | Check accepted lead, slot/site rules, proof method, geofence/fallback/audit state. | Visit schedule/proof/outcome is shown by permission. | Site visit detail with schedule, proof badge, geofence/fallback, outcome timeline. | Yes | PRD-FR-044 to PRD-FR-049, PRD-FR-077 |
| CPO-007 | Booking Visibility | Opens booking status. | Check CP attribution, RBAC, buyer data exposure, booking source. | Shows CP-safe booking milestone and payout impact. | Booking status card/detail with restricted fields, next action, payout impact. | Yes | PRD-FR-050 to PRD-FR-053 |
| CPO-008 | Payout Visibility | Opens payout ledger/detail or raises dispute. | Check finance policy, payout state machine, GST/TDS, reference, dispute rules. | Shows payout state and allows permitted dispute. | Payout ledger/detail with state timeline, deductions, references, dispute CTA. | Yes | PRD-FR-054 to PRD-FR-059, PRD-FR-078 |
| CPO-009 | Support/Audit | Opens support ticket or audit timeline. | Check linked entity, evidence, ticket SLA, audit visibility. | Ticket/timeline shows status, owner, evidence, allowed details. | Support form/detail and audit timeline panel. | Reuse | PRD-FR-060 to PRD-FR-064 |

## Persona Journey: CP Employee / Agent

Goal: Sell projects quickly using current information, protected lead registration, follow-ups, and visits.

| Step ID | Phase | User Action | System Check | System Response | UI Requirement | Build Screen | PRD Trace |
|---|---|---|---|---|---|---|---|
| CPE-001 | Agent Home | Opens CP employee home. | Check employee role, firm status, assigned projects, due tasks, notifications, sync queue. | Shows assigned work and quick actions. | Agent home with project shortcuts, lead quick submit, due follow-ups, visits, sync status. | Yes | PRD-FR-014, PRD-FR-023, PRD-FR-071 |
| CPE-002 | Project Discovery | Searches projects by buyer need. | Check assigned projects, inventory/freshness, filters, collateral status. | Shows permitted project matches. | Project search/catalog with filters, freshness, offer and inventory indicators. | Reuse | PRD-FR-023 to PRD-FR-025 |
| CPE-003 | Share | Shares approved collateral with buyer. | Check approval/version/expiry, share permission, lead/buyer context. | Approved material is shared and share event recorded. | Share kit with approved assets, channel selector, share result. | Reuse | PRD-FR-026, PRD-FR-027 |
| CPE-004 | Lead Submit | Registers lead online or offline. | Validate fields, phone format, project, duplicate rules, network. | Lead returns accepted/conflict/rejected/pending sync/pending review. | Lead quick submit, pending sync, result status, next action. | Reuse | PRD-FR-029 to PRD-FR-033, PRD-FR-076 |
| CPE-005 | Follow-Up | Adds note, task, reminder, or disposition. | Check lead access, reminder policy, offline queue. | Timeline updates online or queues sync. | Lead timeline with notes/tasks/reminders/disposition and sync state. | Yes | PRD-FR-037, PRD-FR-038, PRD-FR-073 |
| CPE-006 | Visit Proof | Schedules visit or captures permitted proof. | Check accepted lead, visit window, location permission, QR/OTP/site-desk/admin fallback. | Visit proof is verified or fallback recorded. | Visit schedule/proof screen with geofence status, fallback, outcome. | Yes | PRD-FR-044 to PRD-FR-049, PRD-FR-077 |
| CPE-007 | Status Review | Reviews assigned lead booking/payout visibility if permitted. | Check CP owner policy, employee permission, buyer/finance data exposure. | Shows allowed assigned lead status only. | Assigned lead detail with booking milestone and payout milestone if allowed. | Reuse | PRD-FR-050 to PRD-FR-056 |

## Persona Journey: CP Telecaller

Goal: Preserve basic qualification/nurture flow without building advanced call intelligence or AI scoring.

| Step ID | Phase | User Action | System Check | System Response | UI Requirement | Build Screen | PRD Trace |
|---|---|---|---|---|---|---|---|
| TEL-001 | Queue | Opens assigned follow-up queue. | Check telecaller role, assigned leads, due follow-ups, priority rules. | Shows permitted queue without advanced scoring. | Basic queue with lead, project, due time, status, priority label if configured. | Yes | PRD-FR-037, PRD-FR-038 |
| TEL-002 | Call/Disposition | Records call outcome/disposition. | Check lead access, allowed disposition fields, next action rules. | Timeline updates with disposition and next action. | Disposition form with budget, location, urgency, objection, visit intent, next follow-up. | Yes | PRD-FR-037, PRD-FR-038 |
| TEL-003 | Schedule/Escalate | Schedules follow-up/visit or escalates hot lead. | Check accepted lead, visit rules, notification target. | Task/visit/escalation is created and relevant users notified. | Follow-up/visit action panel and escalation CTA. | Reuse | PRD-FR-038, PRD-FR-041, PRD-FR-044 |
| TEL-004 | Excluded Automation | Attempts AI/call intelligence workflow. | Feature is deferred by PRD. | Do not generate AI scoring/call intelligence screens. | No screen. Preserve as deferred note only. | No | PRD alternatives and launch classification |

## Persona Journey: Buyer / Customer

Goal: Receive accurate project information, confirm interest/visit, and reuse existing buyer flows where applicable.

| Step ID | Phase | User Action | System Check | System Response | UI Requirement | Build Screen | PRD Trace |
|---|---|---|---|---|---|---|---|
| BUY-001 | Project Link | Opens CP-shared project link. | Validate link token, collateral version, project status, buyer-safe fields, CP attribution. | Shows approved project facts only. | Buyer-safe project link page with facts, offer, RERA info if allowed, CP/Justo attribution. | Yes | PRD-FR-026, PRD-FR-027, PRD-FR-052 |
| BUY-002 | Interest | Confirms interest or requests callback/site visit. | Check link validity, lead context, duplicate/privacy rules. | Interest event is recorded and CP/RM notified where permitted. | CTA form with callback/site visit request, contact confirmation, consent text. | Yes | PRD-FR-037, PRD-FR-041 |
| BUY-003 | Visit Confirmation | Confirms or verifies site visit via configured method. | Check visit booking, OTP/QR/geofence/site-desk/admin method, consent. | Visit proof event is recorded or fallback is used. | Visit confirmation screen with OTP/QR instructions and success/failure state. | Yes | PRD-FR-046, PRD-FR-047, PRD-FR-077 |
| BUY-004 | KYC/Payment | Continues into existing buyer portal where needed. | Check if existing buyer portal/payment flow is linked. | User is routed to existing buyer flow; no new expanded buyer portal screen. | Handoff screen with safe redirect and status return if available. | Reuse | PRD-FR-052 |

## Persona Journey: Compliance / Support

Goal: Validate compliance and resolve disputes with repeatable evidence and audit trails.

| Step ID | Phase | User Action | System Check | System Response | UI Requirement | Build Screen | PRD Trace |
|---|---|---|---|---|---|---|---|
| SUP-001 | Compliance Queue | Opens compliance/support queue. | Check support/compliance role, pending docs, expiries, exceptions, tickets. | Shows prioritized queue. | Queue with tabs: documents, expiries, disputes, payout issues, lead conflicts, collateral issues. | Yes | PRD-FR-010, PRD-FR-060 |
| SUP-002 | Document Review | Opens document/compliance item. | Check document upload status, validation state, CP profile, expiry, prior rejection reason. | Reviewer can approve, reject, request clarification, or flag. | Document review screen with preview, metadata, approve/reject/reason, audit timeline. | Yes | PRD-FR-008 to PRD-FR-012, PRD-FR-079 |
| SUP-003 | Dispute Evidence | Opens lead/visit/payout/support dispute. | Fetch linked evidence bundle, permissions, entity timeline, SLA. | Shows evidence and allowed resolution actions. | Evidence bundle screen with linked lead/visit/booking/payout/document, timeline, status, resolution action. | Yes | PRD-FR-060 to PRD-FR-063 |
| SUP-004 | Resolution | Resolves, escalates, suspends, or requests information. | Check policy, reason, required owner, notification, audit. | Ticket/entity state changes and notifications are sent. | Resolution panel with action, reason, owner, notification preview, audit confirmation. | Yes | PRD-FR-010, PRD-FR-061, PRD-FR-063 |
| SUP-005 | Audit Export | Exports audit evidence where permitted. | Check export permission, date/entity range, privacy constraints. | Audit export is generated or blocked with reason. | Audit export screen with filters, preview count, privacy warning, export status. | Yes | PRD-FR-064 |

## Consolidated Google Stitch Screen Inventory

Use this as the starting screen list for UI screen spec generation.

| Screen Seed | Personas | Required Core Content |
|---|---|---|
| Login / Role Selector | All app users | Credential input, role choices, active context, suspended/deactivated access state. |
| Notification Center / Deep Link Resolver | All app users | Notification list, safe preview, read/unread, category, linked entity, access-denied fallback. |
| Offline Sync Queue | CP Owner, CP Employee, RM | Queued actions, document uploads, failed/blocked/conflict states, retry/cancel/delete. |
| Leadership Dashboard | Justo Leadership | Aggregate KPIs, filters, risk exceptions, stale/empty data states. |
| Risk Exception Detail | Justo Leadership, Support | Severity, owner team, SLA, linked evidence summary, allowed drill-down. |
| Sourcing Dashboard | CP Sourcing Head | Prospect funnel, RM workload, pending docs, activation blockers, escalations. |
| CP Prospect Create/Import | CP Sourcing Head, RM | Prospect details, duplicate warning, RM assignment, follow-up. |
| RM Home | RM | Assigned CPs, tasks, pending docs, stalled activation, escalations. |
| Assisted Onboarding | RM, CP Owner | Checklist, profile fields, document upload queue, validation state. |
| Admin Queue | Sales/Admin Ops | Setup, collateral, conflicts, exceptions, failed notifications, audit. |
| Project Access Config | Sales/Admin Ops | CP/project assignment, compliance state, reason, audit. |
| Collateral Manager | Sales/Admin Ops, Developer/Project | Version, expiry, preview, approve/reject/replace/expire. |
| Lead Conflict Resolution | Sales/Admin Ops, Compliance | Duplicate evidence, policy rule, decision, reason, audit. |
| Payout Queue | Finance | Payout states, SLA, eligibility, disputed/failed/clawback filters. |
| Payout Detail / Processing | Finance, CP Owner view-only slice | Validation checklist, GST/TDS, invoice, approval, payment reference, reconciliation, audit. |
| Project Console | Developer/Project | Project facts, stale flags, inventory/offers/RERA, approval state. |
| Visit Outcome | Developer/Project, RM, CP Employee | Visit proof status, outcome, notes, next action. |
| CP Owner Home | CP Owner | Firm status, team alerts, lead/pipeline summary, payout summary, sync queue, notifications. |
| Team Management | CP Owner | Employee list, invite, role/project access, active work reassignment, deactivation. |
| Project Catalog / Detail / Share Kit | CP Owner, CP Employee, RM | Assigned projects, freshness, approved collateral, expired-share block. |
| Lead Quick Submit / Result | CP Owner, CP Employee | Phone-first capture, project selector, duplicate result, pending-sync state. |
| Firm Lead Dashboard / Lead Detail | CP Owner, CP Employee | Lead status, owner/employee attribution, timeline, conflict/dispute CTA. |
| Site Visit Schedule / Proof | CP Owner, CP Employee, RM, Buyer | Slot, buyer, proof method, geofence/fallback, result, outcome. |
| Booking Status | CP Owner, CP Employee if permitted | CP-safe milestone, next action, payout impact, restricted fields. |
| Basic Telecaller Queue | CP Telecaller | Assigned leads, due follow-ups, basic priority, no AI scoring. |
| Disposition Form | CP Telecaller | Call outcome, budget, location, urgency, objection, visit intent, next follow-up. |
| Buyer Project Link | Buyer | Approved project facts, CP/Justo attribution, CTA, safe fields only. |
| Buyer Visit Confirmation | Buyer | OTP/QR/geofence/site-desk instructions, confirmation status. |
| Compliance Queue / Document Review | Compliance/Support | Pending docs, expiries, preview, approve/reject/reason, validation state. |
| Evidence Bundle / Support Ticket | Compliance/Support, CP Owner, RM | Linked entity, category, evidence, SLA, owner, resolution timeline. |
| Audit Export | Compliance/Support | Entity/date filters, privacy warning, export status. |

## Screen Data And State Contract

This table narrows what each screen needs from source systems. Google Stitch should use these as content constraints, not as backend design.

| Screen Seed | Primary Data Objects | Source / Authority | Must-Have States |
|---|---|---|---|
| Login / Role Selector | User, roles, firm/project context | Identity/RBAC service | Loading, invalid login, no active role, multiple roles, suspended/deactivated |
| Notification Center / Deep Link Resolver | Notifications, linked entity references, read state | Notification service plus entity permission check | Empty, unread/read, deep-link allowed, access denied, linked entity missing |
| Offline Sync Queue | Queued actions, files, retry count, conflict reason | Local device queue plus sync service | Queued, syncing, synced, failed, blocked, conflict, retrying |
| Leadership Dashboard | Aggregate CP, lead, visit, booking, payout, dispute, compliance metrics | Analytics/events from Manthan and app events | Loading, empty, stale data, filtered view, restricted detail |
| Risk Exception Detail | Exception, linked entity summary, owner, SLA | Support/audit/compliance systems | Open, assigned, escalated, resolved, restricted detail |
| Sourcing Dashboard | CP prospects, RM assignment, activation status, onboarding blockers | CP prospect/lifecycle records | Empty, filtered, blocked, inactive, escalated |
| CP Prospect Create/Import | Prospect, RM, territory/source, duplicate match | CP prospect store / Manthan CP master once approved | Draft, duplicate warning, queued, submitted, failed |
| RM Home | Assigned CPs/prospects, tasks, pending docs, escalations | CP lifecycle, task, support systems | Empty day, overdue, offline cached, sync pending |
| Assisted Onboarding | CP firm profile, checklist, documents, assigned RM | CP firm/compliance records | Draft, queued upload, under review, rejected, approved, blocked |
| Admin Queue | Config items, conflicts, exceptions, failed notifications | Admin/config/support/audit systems | Empty, pending, failed, blocked, escalated |
| Project Access Config | CP firm, project, access rule, reason, audit | Project/access configuration | Pending change, saved, failed, restricted, audited |
| Collateral Manager | Project collateral, version, expiry, approval status | Project/collateral repository | Draft, pending approval, approved, expired, rejected |
| Lead Conflict Resolution | Lead, duplicate evidence, ownership ledger, policy reason | Manthan lead module plus ownership ledger | Conflict, resolved, rejected, overridden, restricted evidence |
| Payout Queue | Payout records, invoice, eligibility, SLA, dispute/clawback | Finance/payout state machine | Eligible, invoice pending, under review, approved, scheduled, paid, failed, disputed, clawback |
| Payout Detail / Processing | Payout, booking, invoice, GST/TDS, payment reference, audit | Finance/payout system plus accounting reconciliation | Needs correction, maker pending, checker pending, paid, failed, reconciled, disputed |
| Project Console | Project facts, inventory, offers, RERA details, stale flags | Manthan project/inventory modules | Fresh, stale, pending approval, rejected, restricted |
| Visit Outcome | Visit, proof, buyer, lead, project, outcome | Site visit module plus proof events | Scheduled, confirmed, verified, fallback used, no-show, completed |
| CP Owner Home | Firm profile, compliance, team, leads, visits, bookings, payouts, tickets | Aggregated from CP, lead, visit, booking, payout, support systems | Active, compliance blocked, pending sync, urgent action, no activity |
| Team Management | CP employees, roles, project access, active work | User/RBAC and CP employee model | Invited, active, suspended, deactivated, reassignment required |
| Project Catalog / Detail / Share Kit | Assigned projects, collateral, inventory, offers, share events | Project/inventory/collateral systems | Empty assignment, stale, approved share, expired share blocked |
| Lead Quick Submit / Result | Lead draft, buyer phone, project, duplicate result, ownership status | Manthan lead module plus duplicate/ownership rules | Draft, pending sync, accepted, conflict, rejected, pending review |
| Firm Lead Dashboard / Lead Detail | Firm leads, employee attribution, timeline, visits, booking/payout links | Lead module plus app events | Empty, filtered, conflict, pending sync, restricted data |
| Site Visit Schedule / Proof | Visit, slot, lead, buyer, proof method, geofence/fallback | Site visit/proof service | Scheduled, rescheduled, cancelled, verified, fallback, failed proof |
| Booking Status | Booking milestone, CP attribution, payout impact | Manthan booking/deal module | No booking, booked, documentation pending, payment pending, cancelled, restricted |
| Basic Telecaller Queue | Assigned leads, follow-up due, disposition | Lead/task/timeline systems | Empty, due, overdue, completed, escalated |
| Disposition Form | Lead, call outcome, next action, visit intent | Lead timeline/task systems | Draft, saved, queued, failed |
| Buyer Project Link | Link token, approved project facts, CP attribution | Collateral/link service with buyer-safe rules | Valid, expired, revoked, project unavailable |
| Buyer Visit Confirmation | Visit token, OTP/QR/geofence state, consent | Site visit/proof service | Pending, confirmed, failed OTP, fallback, expired |
| Compliance Queue / Document Review | Documents, profile, validation status, expiry, rejection reason | Compliance/document system | Pending review, approved, rejected, clarification requested, expired |
| Evidence Bundle / Support Ticket | Ticket, linked entity, attachments, timeline, SLA, resolution | Support/evidence/audit systems | Open, assigned, waiting on user, escalated, resolved |
| Audit Export | Audit events, date/entity filters, export job | Audit log service | Preview, generating, ready, blocked, failed |

## Persona Screen Bundle Map

This map prevents Stitch from overbuilding persona-specific duplicates. Use shared screens where `Reuse` is enough.

| Persona | Build-Specific Screens | Reuse Screens |
|---|---|---|
| Justo Leadership | Leadership Dashboard | Risk Exception Detail, Notification Center |
| CP Sourcing Head | Sourcing Dashboard, CP Prospect Create/Import | Onboarding Queue/Assisted Onboarding, Evidence Bundle |
| RM / Sourcing Employee | RM Home, CP Prospect Create/Import, Assisted Onboarding | Site Visit Schedule / Proof, Evidence Bundle, Sync Queue |
| Sales/Admin Ops | Admin Queue, Project Access Config, Lead Conflict Resolution | Collateral Manager, Evidence Bundle |
| Finance | Payout Queue, Payout Detail / Processing | Evidence Bundle, Notification Center |
| Developer / Project Team | Project Console | Collateral Manager, Visit Outcome |
| CP Owner / Org Leader | CP Owner Home, Team Management | Assisted Onboarding, Project Catalog, Lead Quick Submit, Lead Detail, Visit Detail, Booking Status, Payout Ledger, Support Ticket |
| CP Employee / Agent | CP Employee Home, Follow-Up/Disposition | Project Catalog, Share Kit, Lead Quick Submit, Site Visit Proof, Lead Detail |
| CP Telecaller | Basic Telecaller Queue, Disposition Form | Follow-Up/Visit Action Panel |
| Buyer / Customer | Buyer Project Link, Buyer Visit Confirmation | Existing buyer KYC/payment handoff |
| Compliance / Support | Compliance Queue / Document Review, Evidence Bundle / Support Ticket, Audit Export | Notification Center |

## Explicitly Not To Generate In Google Stitch

| Excluded Screen | Reason |
|---|---|
| AI voice calling, AI assistant, KHOJ/Gemini, AI scoring | Deferred in PRD and not required for the MVP trust loop. |
| CP microsites or CP-branded public pages | Excluded from launch scope in PRD. |
| Advanced telecaller call intelligence or sentiment dashboard | Deferred specialist scope; only basic telecaller queue/disposition is mapped. |
| Advanced gamification, loyalty, CP health scoring | Deferred until reliable source data exists. |
| Workforce tracking outside scheduled site-visit proof | Explicitly excluded; geofencing is limited to visit proof. |
| New full buyer portal | Buyer flow is app-linked and should reuse existing buyer/KYC/payment flows where applicable. |

## Remaining Open Constraints For UI Specs

| Constraint | Owner Needed | Why It Matters For Stitch |
|---|---|---|
| Exact lead-lock duration and duplicate priority rules | Sales/CP leadership | Affects lead result, conflict, and dispute screens. |
| Payout SLA, GST/TDS display rules, and authoritative reconciliation event | Finance/product/technology | Affects payout ledger and finance processing states. |
| Geofence radius, accuracy threshold, consent text, fallback path, retention | Product/legal/technology | Affects visit proof screens and privacy copy. |
| Document file types, size limits, retry limits, local retention, scanning | Product/technology/compliance | Affects upload queue and document review screens. |
| Buyer-facing data exposure | Product/legal | Affects buyer link and booking visibility screens. |

## Readiness For Next Artifact

This journey map is ready to feed `Justo_CP_App_UI_Screen_Specs.md` because every PRD persona now has:

- Actionable journey steps.
- Required system checks.
- Required system responses.
- Required UI surfaces/states.
- Explicit build/reuse/no-screen instruction.
- Traceability to PRD requirements or PRD launch classification.
