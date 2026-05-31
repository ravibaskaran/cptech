# Journey Maps: Justo CP App

Draft version: v0.1
Date: 2026-05-31
Prepared for: Justo Realfintech
Primary inputs: `Justo_CP_App_BRD_Draft.md` v0.4 and `Justo_CP_App_PRD.md` v0.3
Artifact sequence: BRD -> PRD -> Persona-wise Journey Maps -> Google Stitch UI Screen Specs/Prototype

## Scope

This draft covers the primary persona only: **CP Owner / Org Leader**.

The CP Owner is treated as the primary persona because the PRD identifies this role as launch core and gives it responsibility for firm onboarding, employee control, project access, lead oversight, booking visibility, payout transparency, and dispute escalation.

This journey map is intentionally limited to the MVP trust loop defined in the PRD:

- CP onboarding and compliance.
- CP employee control.
- Project enablement.
- Lead ownership.
- Site-visit scheduling and proof visibility.
- Booking visibility.
- Full payout processing visibility.
- Notifications, offline queue, and support/dispute escalation.

## Source Traceability

| Source | Relevant Sections |
|---|---|
| `Justo_CP_App_PRD.md` | MVP Scope Gate, CP Owner persona, Role-Based Entry Principle, PRD-FR-001 to PRD-FR-079, NFRs, Acceptance Criteria |
| `Justo_CP_App_BRD_Draft.md` | CP Owner journey, launch MVP proof points, role/permission matrix, MVP must include |

## Primary Persona

| Field | Definition |
|---|---|
| Persona | CP Owner / Org Leader |
| Core job | Manage CP firm onboarding, employees, leads, visits, bookings, payouts, and disputes with clear ownership and status. |
| Primary pain points | Low team control, lead ownership anxiety, payout opacity, limited visibility after lead submission, scattered escalation handling. |
| MVP success outcome | CP Owner can run the firm relationship with Justo without repeatedly calling RM/finance for basic status. |

## Journey Map

### Phase: Access And Role Entry

| Step ID | User Action | System Check | System Response | UI Requirement | PRD Trace |
|---|---|---|---|---|---|
| CP-O-001 | CP Owner opens the app and signs in with a single credential. | Validate credential, active user status, assigned role(s), CP firm association, device/session state. | User is authenticated and routed to CP Owner role home if role is active. | Login screen, loading state, role-resolution state, safe error state for failed login. | PRD-FR-001, PRD-FR-002, PRD-FR-004 |
| CP-O-002 | CP Owner has more than one assigned role/context and selects CP Owner. | Check active roles, default role, permitted CP firm contexts. | App sets CP Owner as active role context for the session. | Role selector with role name, firm name, and clear active context indicator. | PRD-FR-003 |
| CP-O-003 | CP Owner role is suspended, expired, or deactivated. | Check role status, CP firm status, compliance block policy. | App blocks restricted data/actions and shows support/escalation path. | Access-denied screen with status reason where policy permits and support CTA. | PRD-FR-005, PRD-FR-006, PRD-FR-012 |

### Phase: Firm Onboarding And Compliance

| Step ID | User Action | System Check | System Response | UI Requirement | PRD Trace |
|---|---|---|---|---|---|
| CP-O-010 | CP Owner starts or resumes firm onboarding. | Fetch CP firm profile, onboarding checklist, missing fields, compliance status, assigned RM. | App shows current onboarding state and next required action. | Onboarding dashboard with status, checklist, missing items, assigned RM, save/resume state. | PRD-FR-007, PRD-FR-009 |
| CP-O-011 | CP Owner enters or edits firm profile details. | Validate required fields, format, duplicates where configured, RM/source attribution. | Valid data is saved as draft or submitted depending on user action and connectivity. | Firm profile form with required indicators, inline validation, save draft, submit. | PRD-FR-007, PRD-FR-071, PRD-FR-073 |
| CP-O-012 | CP Owner uploads RERA, GST, PAN, bank, KYC, or required compliance document. | Check file type, size limit, role permission, document category, network state, local storage availability. | If online, upload begins. If offline/poor network, file enters secure upload queue. Compliance remains pending validation. | Document upload screen with category, allowed formats, file state, queued/uploading/synced/failed/validation status, retry/cancel/delete. | PRD-FR-008, PRD-FR-072, PRD-FR-079, PRD-NFR-016 |
| CP-O-013 | CP Owner submits onboarding profile for review. | Check required profile fields, required documents, queued upload status, compliance blockers. | If complete and synced, status becomes under review. If uploads pending, app shows blocked/pending sync state. | Submit review screen with pre-submit checklist, blockers, pending upload warning, confirmation state. | PRD-FR-009, PRD-FR-073, PRD-FR-074 |
| CP-O-014 | CP Owner receives document rejection or clarification request. | Notification event references rejected document, reason code, reviewer decision, permitted resubmission action. | App deep-links to the rejected document and shows reason and resubmission path. | In-app notification detail, document rejection banner, reason, resubmit CTA, RM/support contact. | PRD-FR-009, PRD-FR-039, PRD-FR-040, PRD-FR-041 |
| CP-O-015 | CP Owner's compliance document is near expiry. | Check document expiry date and reminder policy. | App shows renewal reminder and required action. | Compliance status card with expiry date, renewal CTA, notification history. | PRD-FR-011, PRD-FR-040 |

### Phase: Team Control

| Step ID | User Action | System Check | System Response | UI Requirement | PRD Trace |
|---|---|---|---|---|---|
| CP-O-020 | CP Owner opens team management. | Fetch CP employees, roles, status, project access, pending invites, active work counts. | App shows employee list and current access state. | Team screen with employee cards/table, role, status, assigned projects, active leads/tasks. | PRD-FR-013, PRD-FR-014, PRD-FR-017 |
| CP-O-021 | CP Owner invites or imports a CP employee. | Check CP Owner permission, employee contact uniqueness, allowed role types, CP firm status. | Invite is created and employee appears as pending/active according to onboarding state. | Invite employee form with contact fields, role selection, project access, status feedback. | PRD-FR-013, PRD-FR-014 |
| CP-O-022 | CP Owner assigns or changes employee role/project access. | Check allowed permissions, project access rules, compliance state, audit requirement. | Employee permissions update and audit event is created. | Role/access editor with before/after summary, affected projects, save confirmation. | PRD-FR-014, PRD-FR-063 |
| CP-O-023 | CP Owner deactivates an employee. | Check employee active leads/tasks, historical attribution, reassignment requirement, deactivation policy. | Employee access is blocked; active work must be reassigned or handled by configured policy; historical attribution remains. | Deactivate confirmation with active work summary, reassignment selector, reason field, audit confirmation. | PRD-FR-015, PRD-FR-016, PRD-FR-063 |

### Phase: Project Enablement

| Step ID | User Action | System Check | System Response | UI Requirement | PRD Trace |
|---|---|---|---|---|---|
| CP-O-030 | CP Owner opens assigned project catalog. | Check CP firm status, role permission, geography, project assignment, inventory/collateral availability. | App displays only permitted projects. | Project catalog with filters, assigned project cards, availability, last-updated timestamp. | PRD-FR-023, PRD-FR-025 |
| CP-O-031 | CP Owner opens project detail. | Fetch permitted project facts, inventory, price band, offers, RERA details, site instructions, commission summary where permitted. | App shows CP-safe project detail. | Project detail screen with facts, freshness indicator, approved collateral, commission summary if permitted. | PRD-FR-024, PRD-FR-025 |
| CP-O-032 | CP Owner shares approved collateral. | Check collateral approval status, expiry/version, share permission, buyer/lead context if available. | App shares only approved current collateral and records share event. | Share kit screen with approved assets, expiry/version badge, channel selector, share confirmation. | PRD-FR-026, PRD-FR-027 |
| CP-O-033 | CP Owner attempts to share expired or unapproved collateral. | Check collateral status and version. | App blocks sharing and points to current approved material if available. | Blocked share state with reason, current collateral CTA, support/admin contact if needed. | PRD-FR-026, PRD-FR-028 |

### Phase: Lead Ownership

| Step ID | User Action | System Check | System Response | UI Requirement | PRD Trace |
|---|---|---|---|---|---|
| CP-O-040 | CP Owner registers a lead. | Check CP Owner permission, required lead fields, buyer phone format, project selection, network state. | Online submission starts duplicate check; offline submission enters pending-sync state. | Lead quick submit screen with phone-first capture, project selector, buyer details, pending-sync warning if offline. | PRD-FR-029, PRD-FR-071, PRD-FR-076 |
| CP-O-041 | System evaluates submitted lead. | Run configured duplicate detection, ownership/lock rules, direct-vs-CP rules, CP/employee attribution. | Lead returns accepted, conflict, rejected, pending sync, or pending review. | Lead result screen with status, reason, ownership/lock info where allowed, next action. | PRD-FR-030, PRD-FR-031, PRD-FR-032, PRD-FR-033 |
| CP-O-042 | CP Owner reviews firm lead pipeline. | Fetch firm leads by permission, status, owner/employee attribution, next action, visit/booking/payout linkage. | App shows pipeline grouped by actionable status. | Firm lead dashboard with accepted/conflict/rejected/pending sync filters, owner, next action, latest activity. | PRD-FR-017, PRD-FR-032, PRD-FR-037 |
| CP-O-043 | CP Owner opens a conflicted lead. | Fetch conflict reason category, evidence visible to CP, dispute eligibility, privacy constraints. | App shows reason and allowed dispute/escalation action without exposing unauthorized personal data. | Lead conflict detail with status, reason, timeline, evidence upload, dispute CTA. | PRD-FR-033, PRD-FR-035, PRD-FR-036 |
| CP-O-044 | CP Owner raises lead ownership dispute. | Validate linked lead, dispute category, evidence attachments, CP permission, support ticket rules. | Dispute ticket is created and linked to the lead ownership ledger. | Dispute form with evidence upload, category, description, linked lead timeline, submitted state. | PRD-FR-035, PRD-FR-060, PRD-FR-061, PRD-FR-062 |

### Phase: Follow-Up And Notifications

| Step ID | User Action | System Check | System Response | UI Requirement | PRD Trace |
|---|---|---|---|---|---|
| CP-O-050 | CP Owner creates or reviews follow-up task for a lead. | Check lead permission, task ownership, reminder policy, offline state. | Task/note is saved online or queued for sync if offline. | Lead timeline with notes, tasks, reminder date, sync status, edit/delete where permitted. | PRD-FR-037, PRD-FR-038, PRD-FR-071, PRD-FR-073 |
| CP-O-051 | CP Owner receives critical notification. | Check role visibility, notification category, deep-link target, OS permission state. | Native push is sent where allowed; in-app notification is always retained. | Notification center with unread/read state, category, timestamp, deep link target, safe payload text. | PRD-FR-039, PRD-FR-040, PRD-FR-041, PRD-FR-043 |
| CP-O-052 | CP Owner opens notification for lead conflict, payout, visit, document rejection, or support update. | Validate current role permission and linked entity access. | App opens exact allowed screen or safe access-denied state. | Deep-linked screen landing with context banner and fallback access-denied state. | PRD-FR-041, PRD-FR-006 |

### Phase: Site Visit Scheduling And Proof Visibility

| Step ID | User Action | System Check | System Response | UI Requirement | PRD Trace |
|---|---|---|---|---|---|
| CP-O-060 | CP Owner requests or schedules a site visit for an accepted lead. | Check lead accepted state, project/site rules, slot availability, CP permission, buyer details. | Visit request/schedule is created with status and notifications to relevant users. | Schedule visit screen with lead, project, slot, buyer contact, confirmation status. | PRD-FR-044, PRD-FR-045, PRD-FR-049 |
| CP-O-061 | CP Owner reviews visit proof status. | Fetch visit proof method, timestamp, verifier, geofence/QR/OTP/site-desk/admin status, fallback reason where relevant. | App shows proof status and linked evidence visible by permission. | Visit detail screen with proof badge, method, timestamp, outcome, fallback reason, timeline. | PRD-FR-046, PRD-FR-047, PRD-FR-077 |
| CP-O-062 | Geofence proof fails for permitted visit user and fallback is used. | Check permission denial, accuracy failure, visit window, fallback proof method. | App records fallback method and reason in audit trail. CP Owner sees proof status, not unauthorized device/location details. | Visit proof status state with fallback reason, verified/unverified badge, support CTA if unresolved. | PRD-FR-046, PRD-FR-077, PRD-FR-063 |
| CP-O-063 | CP Owner reviews visit outcome. | Fetch outcome entered by permitted site/project user, next action, lead/booking linkage. | App updates lead timeline and visit state. | Visit outcome section with interested/dropped/reschedule/booked status, notes if visible, next action. | PRD-FR-048, PRD-FR-037 |

### Phase: Booking Visibility

| Step ID | User Action | System Check | System Response | UI Requirement | PRD Trace |
|---|---|---|---|---|---|
| CP-O-070 | CP Owner opens booking status for a firm lead. | Check CP firm attribution, RBAC, buyer data exposure policy, booking source status. | App shows CP-safe booking milestone and next action. | Booking status screen/card with milestone, allowed details, next action, restricted-data placeholders. | PRD-FR-050, PRD-FR-051, PRD-FR-052 |
| CP-O-071 | Booking cancellation or eligibility-impacting event occurs. | Check booking event, payout eligibility dependency, notification visibility. | Booking status and payout state update; CP Owner receives notification if permitted. | Booking event banner, payout impact note, notification center entry, timeline update. | PRD-FR-053, PRD-FR-041 |

### Phase: Payout Processing Visibility

| Step ID | User Action | System Check | System Response | UI Requirement | PRD Trace |
|---|---|---|---|---|---|
| CP-O-080 | CP Owner opens payout ledger. | Check CP firm permission, eligible transactions, finance policy, payout state machine, sensitive data restrictions. | App shows payout records and current status allowed by policy. | Payout ledger with status, project/lead/booking link, amount basis, deductions, invoice state, expected/paid date where configured. | PRD-FR-054, PRD-FR-055, PRD-FR-056 |
| CP-O-081 | CP Owner reviews payout detail. | Fetch payout audit state, invoice status, GST/TDS, approval/rejection reason, payment reference, reconciliation state, clawback/dispute state. | App shows finance-controlled payout state without allowing unauthorized finance actions. | Payout detail screen with state timeline, reason codes, documents, references, dispute CTA. | PRD-FR-056, PRD-FR-057, PRD-FR-078 |
| CP-O-082 | CP Owner submits payout dispute. | Validate payout record, dispute category, supporting evidence, ticket rules, duplicate active dispute. | Payout dispute ticket is created and linked to payout record and evidence bundle. | Payout dispute form with linked payout, evidence upload, category, description, submitted state. | PRD-FR-058, PRD-FR-060, PRD-FR-061, PRD-FR-062 |
| CP-O-083 | Finance updates payout status. | Check finance state transition, maker-checker rule, payment/reconciliation reference, audit event. | CP Owner sees updated payout status and receives notification if permitted. | Payout status update banner, notification center item, timeline/audit visible fields. | PRD-FR-057, PRD-FR-078, PRD-FR-041 |

### Phase: Offline Queue And Sync Recovery

| Step ID | User Action | System Check | System Response | UI Requirement | PRD Trace |
|---|---|---|---|---|---|
| CP-O-090 | CP Owner opens sync queue. | Fetch local queued actions and server reconciliation state: queued, syncing, synced, failed, blocked, conflict. | App shows each queued action and allowed recovery action. | Sync queue screen with action type, entity, status, retry/cancel/delete, last attempt, error reason. | PRD-FR-073, PRD-FR-074, PRD-FR-075 |
| CP-O-091 | CP Owner retries failed document upload. | Check connectivity, session validity, file availability, file rules, retry count. | Upload retries; compliance status remains pending until server validation succeeds. | Upload queue item with retry progress, failure reason, validation pending state. | PRD-FR-079, PRD-FR-074 |
| CP-O-092 | Offline lead submission syncs after reconnect. | Run server duplicate detection and lead ownership rules. | Lead becomes accepted/conflict/rejected/pending review; ownership is final only after server response. | Pending-sync lead card updates to final status with reason and next action. | PRD-FR-076, PRD-FR-030, PRD-FR-031 |

### Phase: Support And Audit

| Step ID | User Action | System Check | System Response | UI Requirement | PRD Trace |
|---|---|---|---|---|---|
| CP-O-100 | CP Owner raises a support ticket from a lead, visit, booking, payout, document, or project context. | Validate linked entity, category, severity, attachments, duplicate ticket policy. | Ticket is created with linked evidence and status. | Contextual support form with prefilled entity, category, severity, attachment upload, submitted state. | PRD-FR-060, PRD-FR-061 |
| CP-O-101 | CP Owner reviews support ticket status. | Fetch ticket owner, SLA, latest status, resolution, linked evidence visibility. | App shows status and next expected action. | Ticket detail with SLA, status, owner/team, timeline, linked entity, resolution notes where visible. | PRD-FR-061, PRD-FR-062 |
| CP-O-102 | CP Owner views audit-relevant timeline for lead, visit, payout, or document. | Check entity access, audit visibility, privacy restrictions. | App shows allowed audit events and hides restricted internal details. | Timeline/audit panel with actor type, timestamp, status change, reason, evidence link where permitted. | PRD-FR-036, PRD-FR-063 |

## Google Stitch Screen Seeds

These are screen seeds derived strictly from the CP Owner journey above. They are not visual designs yet.

| Screen Seed | Journey Steps | Required Screen Content |
|---|---|---|
| Login / Role Resolution | CP-O-001 to CP-O-003 | Credential input, role selector, active role, access-denied state. |
| CP Owner Home | CP-O-010, CP-O-020, CP-O-042, CP-O-080, CP-O-090 | Firm status, team alerts, lead/pipeline summary, payout summary, sync queue status, notifications. |
| Onboarding Checklist | CP-O-010 to CP-O-015 | Profile status, document checklist, missing items, queued upload states, rejection reasons, renewal reminders. |
| Document Upload Queue | CP-O-012, CP-O-013, CP-O-091 | File category, file state, retry/resume/cancel/delete, validation pending, failure reason. |
| Team Management | CP-O-020 to CP-O-023 | Employee list, invite form, role/project access, active work reassignment, deactivation reason. |
| Project Catalog | CP-O-030 to CP-O-033 | Assigned project cards, freshness, project detail, approved collateral, blocked expired share state. |
| Lead Quick Submit | CP-O-040 to CP-O-041 | Phone-first fields, project selector, online/offline state, submission result. |
| Firm Lead Dashboard | CP-O-042 to CP-O-044 | Lead status filters, owner/employee attribution, conflict detail, dispute CTA. |
| Notification Center | CP-O-051 to CP-O-052 | Notification list, read/unread, category, safe preview, deep-link behavior. |
| Site Visit Detail | CP-O-060 to CP-O-063 | Schedule state, proof method, geofence/fallback status, outcome, timeline. |
| Booking Status | CP-O-070 to CP-O-071 | CP-safe milestone, next action, restricted fields, payout impact. |
| Payout Ledger And Detail | CP-O-080 to CP-O-083 | Status list, payout detail, GST/TDS/deductions, approval/payment/reconciliation state, dispute CTA. |
| Sync Queue | CP-O-090 to CP-O-092 | Queued actions, status, retry/cancel/delete, conflict/blocked reason. |
| Support Ticket | CP-O-100 to CP-O-102 | Linked entity, category, severity, evidence, SLA, status timeline, resolution. |

## Explicitly Not Mapped For CP Owner MVP

| Not Mapped | Reason |
|---|---|
| AI voice calling, AI assistant, KHOJ/Gemini, AI scoring | Deferred in PRD and not required for the MVP trust loop. |
| CP microsites or CP-branded public pages | Excluded from launch scope in PRD. |
| Advanced telecaller queue/call intelligence | CP telecaller is a deferred specialist persona in PRD. |
| Advanced analytics, gamification, loyalty, CP health scoring | Deferred until reliable source data exists. |
| Workforce tracking outside scheduled site-visit proof | Explicitly excluded; geofencing is limited to visit proof. |
| Full buyer portal expansion | Buyer experience is app-linked, not CP Owner MVP. |

## Readiness For Next Artifact

This journey map is ready to feed Google Stitch UI screen specs because every step includes:

- A specific CP Owner action.
- A system check or business rule.
- A concrete system response.
- A required UI surface/state.
- PRD requirement traceability.

Next artifact: `Justo_CP_App_UI_Screen_Specs.md`.
