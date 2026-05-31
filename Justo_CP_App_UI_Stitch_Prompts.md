# Google Stitch UI Screen Prompts: Justo CP App

Draft version: v0.4
Date: 2026-05-31
Prepared for: Justo Realfintech
Primary inputs: `Justo_CP_App_BRD_Draft.md` v0.5, `Justo_CP_App_PRD.md` v0.5, `Justo_CP_App_Journey_Maps.md` v0.5, and Stitch project `16963605453633474186`
Artifact sequence: BRD -> PRD -> Persona-wise Journey Maps -> Google Stitch UI Screen Specs/Prototype

## Stitch Project Read Confirmation

[high] The Stitch MCP can read project `16963605453633474186` titled `CP Tech Native App Port`.

[high] The project exposes these current artifacts:

| Artifact | Stitch Screen / Asset | Read Status | Key Design Rule Used |
|---|---|---|---|
| `DESIGN.md` | Screen title `DESIGN.md` plus active mobile design markdown | Read | CP Tech Digital mobile style with Manrope, deep navy, lime accent, white cards, 8dp radius |
| `WIREFRAMES.md` | Screen title `WIREFRAMES.md` | Read | Android Material 3 top app bar, bottom navigation, cards, outlined inputs, 48dp touch targets |
| Color palette | Design system `CP Tech Digital` and mobile design markdown | Read | Primary `#121417`, secondary/accent `#b8ff4d`, surface `#f9f9ff`, cards `#ffffff`, outline `#d3daea` |

## Global Stitch Prompt Rules

Use these rules in every Stitch generation:

- Generate Android mobile app screens in Material 3 style.
- Use the existing `CP Tech Digital` visual direction: professional, corporate-modern, Manrope typography, high-contrast dark primary, lime accent, white card surfaces, 8dp radius, 16dp margins, 8dp spacing grid, 48dp minimum tap targets.
- Use India-ready content: dates in `dd/mm/yyyy`, currency with `₹`, Indian numbering such as `₹12.5 lakh`, `₹1.2 crore`, and phone examples like `+91 98765 43210`.
- Support internationalization readiness for Middle East and ASEAN: avoid hard-coded layout assumptions, keep labels short, allow text expansion, support RTL-safe alignment where possible, and use locale-safe date/currency labels.
- Each generated screen must show loading, empty, error, access-denied, offline cached, pending-sync, conflict/blocked, or audit-visible states where relevant.
- Do not generate AI calling, AI scoring, CP microsites, advanced gamification, workforce tracking outside scheduled visit proof, or full buyer portal screens.
- Arrange each persona flow horizontally, left to right, as connected Android mobile screens. Start each persona below the prior persona when multiple persona flows are generated on the same canvas.

## Stitch Prompt 01: Shared App Foundation

"Design an Android flow for all Justo CP App personas trying to sign in, choose an active role, open notifications, and recover queued offline work.

**Vibe:** Professional, corporate-modern, mobile operations app, similar in clarity to Linear and Material 3 admin apps, using the existing CP Tech Digital design system.

**Screens to Generate:**
1. **Login:** Android mobile login screen with CP Tech logo, Text Field: Mobile Number or Email (Required), Text Field: Password or OTP (Required), Button: Sign in, Link: Forgot password, error state for invalid credentials, suspended access message.
2. **Role Selector:** Card-based role picker after one credential login. Show roles: CP Owner, CP Employee, RM, Finance. Include active firm/project context, Badge: Multiple roles, Button: Continue, access-denied state for deactivated role.
3. **Notification Center:** List of notifications with read/unread state, category chips for Lead, Visit, Payout, Document, Support, safe preview text, timestamp `31/05/2026`, deep-link row, empty state.
4. **Deep Link Resolver / Access Denied:** Transition screen showing permission check, allowed target preview, blocked target message, Button: Back to Home, Button: Contact Support.
5. **Offline Sync Queue:** Queue list with Lead draft, Document upload, Visit note. Status chips: Queued, Syncing, Failed, Conflict. Buttons: Retry, Cancel, Delete. Show cached timestamp and no-network banner.

**Design System:** Use Material 3 Android components. Primary color: `#121417`. Accent color: `#b8ff4d`. Surface: `#f9f9ff`. Cards: `#ffffff`. Outline: `#d3daea`. Typography: Manrope.

**Connections:** User taps Sign in on Login to go to Role Selector. User taps Continue to go to role home placeholder. User taps bell icon to Notification Center. User taps a notification to Deep Link Resolver. User taps Sync Queue from offline banner.

**Dev-Ready Inputs:** Mobile Number or Email (Required, text/email/tel), Password or OTP (Required, secure/number), Role Card (Required selection), Retry/Cancel/Delete queue action buttons.

**Constraints:** Do not create persona-specific business dashboards in this shared flow. Show India formatting with `dd/mm/yyyy`, `₹`, lakh/crore labels where sample values appear. Keep text expansion safe for Middle East and ASEAN localization."

## Stitch Prompt 02: Justo Leadership

"Design an Android flow for Justo Leadership trying to monitor CP business health and risk without seeing unnecessary operational detail.

**Vibe:** Executive, precise, KPI-heavy but calm, similar to a mobile business intelligence app using Material 3.

**Screens to Generate:**
1. **Leadership Dashboard:** Aggregate KPI dashboard with cards for Active CPs, Accepted Leads, Verified Visits, Bookings, Payout SLA, Open Disputes, Compliance Exceptions. Include date filter `01/05/2026 - 31/05/2026`, city filter Mumbai/Pune/Nagpur, and stale data chip.
2. **Filtered Performance View:** Filter panel for City, Cluster, RM, Project, CP Segment, Date Range. Input: Date Range (Required), Multi-select Chips: City/Cluster/RM/Project, Button: Apply Filters.
3. **Risk Exception Queue:** Ranked list of risks with severity, owner team, SLA, linked entity count. Include examples: payout delay `₹2.4 lakh`, failed sync, document expiry, lead dispute.
4. **Risk Exception Detail:** Summary-only detail view with accountable team, current SLA, allowed drill-down, privacy-safe evidence summary, audit timestamp, Button: Escalate.

**Design System:** Use Material 3 Android components. Primary color: `#121417`; accent `#b8ff4d`; white cards with subtle borders.

**Connections:** User opens Leadership Dashboard, taps filters to Filtered Performance View, applies filters back to dashboard, taps Open Disputes card to Risk Exception Queue, taps a high-severity row to Risk Exception Detail.

**Dev-Ready Inputs:** Date Range (Required), City/Cluster/RM/Project/CP Segment filter chips, Escalation Note (Optional multiline text), Escalate Button.

**Constraints:** Aggregate data only. Do not show restricted buyer PII or finance raw data. Use Indian numbering and dates. Allow text expansion for international markets."

## Stitch Prompt 03: CP Sourcing Head

"Design an Android flow for a CP Sourcing Head trying to build, assign, activate, and govern the CP network.

**Vibe:** Field-management command center, professional and dense, similar to a mobile CRM pipeline app.

**Screens to Generate:**
1. **Sourcing Dashboard:** Funnel cards for New Prospects, Assigned to RM, Docs Pending, Under Review, Activated, Stalled. Include RM workload list, activation blockers, Button: Add CP Prospect.
2. **CP Prospect Create / Import:** Form with Text Field: CP Firm Name (Required), Text Field: Owner Mobile (Required, tel), Text Field: RERA Number (Optional), Dropdown: Source (Required), Dropdown: Territory (Required), Dropdown: Assign RM (Required), duplicate warning panel.
3. **Onboarding Governance Queue:** List of CPs by status: Missing Docs, Under Review, Rejected, Blocked, Approved. Show CP name, RM, ageing, next action.
4. **Activation Detail:** Checklist for first login, employee added, project access assigned, first lead, first visit. Show RM notes, blocker chip, Button: Escalate.
5. **Escalation Modal:** Bottom sheet with linked CP, Category (Lead, Compliance, Payout, RM), Severity, Owner Team, Notes (Required multiline), Button: Create Ticket.

**Design System:** Material 3 Android, CP Tech Digital, primary `#121417`, accent `#b8ff4d`.

**Connections:** Add CP Prospect opens prospect form. Successful submit returns to dashboard with pending status. Tapping queue item opens Activation Detail. Tapping Escalate opens Escalation Modal.

**Dev-Ready Inputs:** Firm Name (Required text), Owner Mobile (Required tel), RERA Number (Optional text), Source (Required dropdown), Territory (Required dropdown), Assign RM (Required dropdown), Notes (Required multiline).

**Constraints:** No CP health scoring or gamification. Keep this to sourcing, onboarding blockers, activation, and escalation only."

## Stitch Prompt 04: RM / Sourcing Employee

"Design an Android flow for an RM / Sourcing Employee trying to recruit CPs, assist onboarding, upload documents in poor network, and support visits.

**Vibe:** Mobile-first field operations, quick-action heavy, professional, similar to a field-sales CRM.

**Screens to Generate:**
1. **RM Home:** Today view with assigned CP prospects, pending documents, stalled CPs, escalations, offline sync banner, FAB: Add CP Prospect.
2. **CP Prospect Form:** Text Field: CP Firm Name (Required), Owner Name (Required), Mobile (Required tel), Territory (Required), Source (Required dropdown), Next Follow-up Date (Required, dd/mm/yyyy), Button: Save Online / Queue Offline.
3. **Assisted Onboarding:** CP checklist with Firm Profile, PAN/GST, RERA, Bank Details, KYC. Include upload rows with queued/uploading/failed states and Button: Add Document.
4. **Queued Document Upload:** Upload detail with File Picker (Required), Document Type (Required dropdown), File Size Limit note, Buttons: Retry, Cancel, Delete, Status: Pending server validation.
5. **Site Visit Support:** Schedule visit screen with Lead, Buyer Mobile, Project, Slot Date/Time, Proof Method chips: QR, OTP, Geofence, Site Desk, Admin Fallback; Button: Schedule Visit.

**Design System:** Material 3 Android, primary `#121417`, accent `#b8ff4d`, white cards, 8dp radius.

**Connections:** FAB opens CP Prospect Form. Save Offline routes to Offline Sync Queue. Tapping pending docs opens Assisted Onboarding. Add Document opens Queued Document Upload. Visit task opens Site Visit Support.

**Dev-Ready Inputs:** CP Firm Name (Required), Owner Name (Required), Mobile (Required tel), Territory (Required dropdown), Source (Required dropdown), Next Follow-up Date (Required date), Document Type (Required dropdown), File Picker (Required), Visit Slot Date/Time (Required).

**Constraints:** Document upload cannot show compliance complete until server validation succeeds. Geofence appears only for scheduled visits and shows consent/fallback."

## Stitch Prompt 05: Sales / Admin Ops

"Design an Android flow for Sales/Admin Ops trying to control project access, collateral, lead conflicts, and operational exceptions.

**Vibe:** Compact admin console on mobile, dense but readable, similar to Material 3 enterprise admin apps.

**Screens to Generate:**
1. **Admin Queue:** Tabbed queue with Setup, Collateral, Conflicts, Exceptions, Audit. Show counts, failed notifications, blocked changes, and priority chips.
2. **Project Access Config:** Searchable list of CP firms and projects. Controls: CP Selector (Required), Project Selector (Required), Access Toggle, Reason (Required text), Button: Save Access.
3. **Collateral Manager:** Collateral list with version, expiry date, approval state, preview thumbnail, actions Approve, Replace, Expire, Reject, audit note.
4. **Lead Conflict Resolution:** Evidence screen with duplicate leads, timestamps, CP owner, employee attribution, source, policy rule, restricted PII masking, decision buttons: Accept, Reject, Override.
5. **Exception Action Modal:** Bottom sheet requiring Action Type, Reason (Required multiline), affected users/leads summary, confirmation checkbox, Button: Apply and Audit.

**Design System:** Material 3 Android, primary `#121417`, accent `#b8ff4d`.

**Connections:** Admin Queue tabs navigate to respective work items. Project access row opens Project Access Config. Collateral row opens Collateral Manager. Conflict row opens Lead Conflict Resolution. Override opens Exception Action Modal.

**Dev-Ready Inputs:** CP Selector (Required search), Project Selector (Required search), Access Toggle, Reason (Required), Audit Note (Required for reject/override), Confirmation Checkbox (Required for exception).

**Constraints:** Do not create broad system settings. Keep screens limited to project access, collateral governance, lead conflict, exception action, and audit."

## Stitch Prompt 06: Finance

"Design an Android flow for Finance trying to process CP payouts accurately with full status transparency and audit discipline.

**Vibe:** Finance operations, controlled, checklist-driven, similar to a banking operations mobile console.

**Screens to Generate:**
1. **Payout Queue:** Status tabs: Eligible, Invoice Pending, Under Review, Approved, Scheduled, Paid, Failed, Disputed, Clawback. Show CP name, project, amount `₹2.4 lakh`, SLA, priority.
2. **Payout Detail / Eligibility:** Detail screen with booking milestone, CP eligibility, invoice, GST/TDS, bank/KYC, cancellation risk, validation checklist.
3. **Approval Action:** Maker-checker panel with Buttons: Approve, Reject, Request Correction. Text Field: Reason (Required for reject/correction), Checkbox: I confirm policy checks.
4. **Payment Scheduling:** Inputs for Scheduled Date (Required dd/mm/yyyy), Payment Reference (Required when paid), Amount (Required currency), Failure Reason (Required when failed).
5. **Reconciliation / Clawback:** Reconciliation status panel with source reference, paid/reconciled/disputed/clawback state, reason field, immutable audit timeline.

**Design System:** Material 3 Android, primary `#121417`, accent `#b8ff4d`, error `#ba1a1a`.

**Connections:** Tapping a Payout Queue item opens Payout Detail. Approve opens Approval Action. Approved payout opens Payment Scheduling. Paid payout opens Reconciliation / Clawback.

**Dev-Ready Inputs:** Reason (Required conditional multiline), Scheduled Date (Required date), Payment Reference (Required text when paid), Amount (Required currency), Failure/Clawback Reason (Required conditional).

**Constraints:** Full payout processing is in scope. Show maker-checker and audit. Do not show CP-editable finance controls."

## Stitch Prompt 07: Developer / Project Team

"Design an Android flow for Developer / Project Team trying to keep project facts, inventory, collateral, and visit outcomes current.

**Vibe:** Project operations and approvals, clean and structured, similar to a mobile content operations dashboard.

**Screens to Generate:**
1. **Project Console:** Assigned projects list with stale data flags, inventory updates due, collateral approvals, visit outcome items. Include search and status chips.
2. **Project Facts Form:** Inputs for Project Name (Read-only), Inventory Status (Required dropdown), Offer Text (Optional), RERA Details (Required), Site Instructions (Required multiline), Freshness Timestamp.
3. **Collateral Review:** Preview card with file, version, expiry, claim-safe fields, buttons Approve, Reject, Expire, Replace, Reason field.
4. **Visit Outcome:** Visit detail with proof status, buyer masked phone, lead, project, outcome selector, note field, Button: Save Outcome.

**Design System:** Material 3 Android, primary `#121417`, accent `#b8ff4d`.

**Connections:** Tapping stale project opens Project Facts Form. Tapping collateral item opens Collateral Review. Tapping visit item opens Visit Outcome.

**Dev-Ready Inputs:** Inventory Status (Required dropdown), RERA Details (Required text), Site Instructions (Required multiline), Expiry Date (Required date for collateral), Outcome (Required dropdown), Visit Note (Optional multiline).

**Constraints:** Do not generate developer marketing pages. Keep buyer-safe claims and approval status visible."

## Stitch Prompt 08: CP Owner / Org Leader

"Design an Android flow for CP Owner / Org Leader trying to run the CP firm: compliance, team, leads, visits, bookings, payouts, disputes, and sync.

**Vibe:** Business owner control center, trusted and transparent, similar to a mobile fintech operations dashboard.

**Screens to Generate:**
1. **CP Owner Home:** Firm status, compliance status, team alerts, leads summary, visits, bookings, payout summary `₹3.6 lakh due`, disputes, notification bell, sync queue chip.
2. **Team Management:** Employee list with roles, project access, active work counts, Button: Invite Employee, actions Deactivate/Reassign. Input: Employee Mobile (Required tel), Role (Required dropdown), Project Access (Required multi-select).
3. **Lead Quick Submit / Result:** Phone-first lead form with Buyer Mobile (Required tel), Buyer Name (Optional), Project (Required), Budget (Optional currency), Button: Submit Lead. Result states: Accepted, Conflict, Rejected, Pending Sync, Pending Review.
4. **Firm Lead Detail:** Lead timeline with owner/employee attribution, follow-up, visit, conflict/dispute CTA, booking link if available, restricted buyer data labels.
5. **Payout Ledger / Dispute:** Payout list and detail with status timeline, deductions GST/TDS, payment reference, expected date, Button: Raise Dispute, linked evidence.

**Design System:** Material 3 Android, CP Tech Digital, primary `#121417`, accent `#b8ff4d`.

**Connections:** Home cards route to Team Management, Lead Quick Submit, Firm Lead Detail, and Payout Ledger. Conflict status opens Lead Detail. Raise Dispute opens support ticket pattern.

**Dev-Ready Inputs:** Employee Mobile (Required tel), Role (Required dropdown), Project Access (Required multi-select), Buyer Mobile (Required tel), Project (Required dropdown), Budget (Optional currency), Dispute Reason (Required multiline).

**Constraints:** CP owner can manage firm users and view payout transparency but cannot bypass finance controls. Keep offline and pending-sync status visible."

## Stitch Prompt 09: CP Employee / Agent

"Design an Android flow for CP Employee / Agent trying to sell projects quickly with current info, protected lead submission, follow-ups, and site visit proof.

**Vibe:** Fast field-sales mobile app, project-first, thumb-friendly, similar to modern property search plus CRM apps.

**Screens to Generate:**
1. **Agent Home:** Assigned project shortcuts, lead quick submit CTA, due follow-ups, upcoming visits, sync status, bottom nav Home/Search/Leads/Profile.
2. **Project Catalog / Detail:** Search and filters for location, budget `₹80 lakh - ₹1.5 crore`, BHK, possession. Project card with freshness, inventory, offer, RERA, approved collateral indicator.
3. **Share Kit:** Approved assets list, expired-share blocked state, channel selector WhatsApp/SMS/Copy Link, buyer context selector, Button: Share Approved Kit.
4. **Lead Quick Submit:** Buyer Mobile (Required tel), Buyer Name (Optional), Project (Required), Source (Required), Consent Checkbox, Button: Register Lead; result chip accepted/conflict/rejected/pending sync.
5. **Visit Proof / Follow-Up:** Visit schedule with slot, proof method, geofence consent, QR/OTP entry, fallback selector, outcome note, next follow-up date.

**Design System:** Material 3 Android, primary `#121417`, accent `#b8ff4d`, property cards with white surfaces and subtle borders.

**Connections:** Agent Home project shortcut opens Project Catalog / Detail. Share CTA opens Share Kit. Register Lead opens Lead Quick Submit. Accepted lead opens Visit Proof / Follow-Up.

**Dev-Ready Inputs:** Search (Optional text), Budget Range (Optional range), BHK (Optional chips), Buyer Mobile (Required tel), Source (Required dropdown), Consent Checkbox (Required), OTP (Required number when selected), Fallback Reason (Required conditional), Next Follow-up Date (Optional date).

**Constraints:** Only approved collateral can be shared. Do not show AI scoring or call intelligence. Geofence is only for scheduled visit proof."

## Stitch Prompt 10: CP Telecaller

"Design an Android flow for CP Telecaller trying to work a basic follow-up queue, record disposition, and schedule next action without AI scoring.

**Vibe:** Simple, queue-driven, low-friction call workflow, similar to a lightweight mobile CRM task list.

**Screens to Generate:**
1. **Basic Telecaller Queue:** Assigned leads list with project, due time, status, basic priority label, overdue chip, no AI score. Filters: Due Today, Overdue, Completed.
2. **Lead Call Detail:** Lead detail with masked buyer phone, project, prior timeline, Button: Start Call, Button: Add Disposition.
3. **Disposition Form:** Inputs for Call Outcome (Required dropdown), Budget (Optional currency), Location (Optional), Urgency (Optional dropdown), Objection (Optional text), Visit Intent (Required yes/no), Next Follow-up Date (Required dd/mm/yyyy).
4. **Schedule / Escalate Panel:** Action panel to schedule follow-up, request site visit, or escalate hot lead. Include Notify RM toggle and Button: Save Action.

**Design System:** Material 3 Android, primary `#121417`, accent `#b8ff4d`.

**Connections:** Tapping queue row opens Lead Call Detail. Add Disposition opens Disposition Form. Visit Intent yes opens Schedule / Escalate Panel.

**Dev-Ready Inputs:** Call Outcome (Required dropdown), Visit Intent (Required segmented control), Next Follow-up Date (Required date), Notify RM (Optional toggle), Escalation Note (Required if escalate).

**Constraints:** Do not generate AI call intelligence, sentiment, transcript summary, auto scoring, or dialer automation beyond basic call/detail/disposition screens."

## Stitch Prompt 11: Buyer / Customer

"Design an Android mobile web/link flow for Buyer / Customer trying to view a CP-shared project link, confirm interest, and complete visit confirmation safely.

**Vibe:** Buyer-safe, lightweight, trustworthy property information flow, similar to a premium real estate mobile landing detail page but operational, not marketing-heavy.

**Screens to Generate:**
1. **Buyer Project Link:** Approved project facts only: project name, location, price range `₹85 lakh - ₹1.4 crore`, BHK, RERA number, offer, CP/Justo attribution, freshness date `31/05/2026`.
2. **Interest / Callback Form:** Inputs for Name (Required), Mobile (Required tel), Preferred Callback Date (Optional dd/mm/yyyy), Consent Checkbox (Required), Buttons: Request Callback, Request Site Visit.
3. **Visit Confirmation:** Visit slot detail, site address, CP/Justo contact, OTP/QR instructions, Button: Confirm Visit, fallback info.
4. **Visit Proof Result:** Success/failure state with OTP verified, QR scanned, geofence confirmed, or fallback used. Show next step and privacy-safe confirmation.

**Design System:** Material 3 mobile web style, CP Tech Digital, primary `#121417`, accent `#b8ff4d`.

**Connections:** Buyer opens shared link to Buyer Project Link. Taps Request Site Visit to Interest / Callback Form. Submitted request opens Visit Confirmation. Confirm Visit opens Visit Proof Result.

**Dev-Ready Inputs:** Name (Required text), Mobile (Required tel), Preferred Callback Date (Optional date), Consent Checkbox (Required), OTP (Required number when selected).

**Constraints:** This is not a full buyer portal. Show approved project facts only and preserve CP attribution."

## Stitch Prompt 12: Compliance / Support

"Design an Android flow for Compliance / Support trying to validate documents, resolve disputes, review evidence, and export audit records.

**Vibe:** Controlled compliance operations, evidence-first, similar to a mobile case management console.

**Screens to Generate:**
1. **Compliance / Support Queue:** Tabs: Documents, Expiries, Disputes, Payout Issues, Lead Conflicts, Collateral Issues. Show SLA, owner, severity, ageing, and queue count.
2. **Document Review:** Document preview card, metadata, CP profile summary, upload status, validation state, prior rejection reason, buttons Approve, Reject, Request Clarification, Flag.
3. **Evidence Bundle / Support Ticket:** Linked lead/visit/booking/payout/document, entity timeline, attachments, SLA, owner team, resolution status, comment field.
4. **Resolution Action:** Action bottom sheet with Resolution Type (Required), Reason (Required multiline), Notify Originator toggle, Button: Resolve and Audit.
5. **Audit Export:** Filters for Entity Type, Date Range, CP Firm, Privacy Warning checkbox, Button: Generate Export, statuses Preview/Generating/Ready/Blocked/Failed.

**Design System:** Material 3 Android, primary `#121417`, accent `#b8ff4d`, error `#ba1a1a`.

**Connections:** Queue item opens Document Review or Evidence Bundle. Reject/Resolve opens Resolution Action. Audit tab opens Audit Export.

**Dev-Ready Inputs:** Resolution Type (Required dropdown), Reason (Required multiline), Date Range (Required), Entity Type (Required dropdown), Privacy Warning Checkbox (Required), Notify Originator (Optional toggle).

**Constraints:** Keep evidence and audit visible. Do not expose restricted PII beyond role permission. Do not create unrelated support knowledge-base screens."

## Stitch Generation Log

| Prompt | Persona / Flow | Stitch Project | Status | QA Notes |
|---|---|---|---|---|
| 01 | Shared App Foundation | `16963605453633474186` | Generated | Shared login, role selector, notifications, access control, and offline sync screens generated in the target project; visibility confirmed after the user refreshed/stopped the prior flow. Representative screen IDs include `d6d94aa2ea564f0cb3e5d6df0816fa9d`, `5399e0926cc444c7b047c2dc4894ed98`, `3a3bbfd5c05a4785946c4de36f253383`, `298462d996494f59b24ca2a7593575d4`, `a5ce03eab7c54be7b29217d30c7f7351`. |
| 02 | Justo Leadership | `16963605453633474186` | Generated | Leadership dashboard, filters, risk queue, and risk detail generated in the target project. Representative screen IDs: `0ee4c20b6be84f11a3054e288ccede6e`, `5b4b7f3c59254270bf6187eaed8bc065`, `49a138cda353400e9c055a560fc2d728`, `f996d1af51b147e3ad50c3b1ec1f62be`. |
| 03 | CP Sourcing Head | `16963605453633474186` | Generated | User screenshot plus Stitch inventory confirmed Sourcing Dashboard, CP Prospect Create / Import, Onboarding Governance Queue, Activation Detail, and Escalation Modal. Representative screen IDs: `45d1368ec1934d02be860af1d81baa34`, `d9f06d3b23b34efe9ef8dd4239047ba0`, `3c441dd1b9ed47619e99d09a02baa50b`, `cda6243d0dfe4c2a9230d5c697773fc4`, `18e8b5e19ee14a089e8f2a728939afd3`. |
| 04 | RM / Sourcing Employee | `16963605453633474186` | Generated | RM Home, CP Prospect Form, Assisted Onboarding Progress, Queued Document Upload Detail, and Site Visit Support generated. Representative screen IDs include `7f25cfd668064422969b20a357733bb4`, `156ad1c42b7a4aa0a6a97d4fdbae1e56`. |
| 05 | Sales / Admin Ops | `16963605453633474186` | Generated | Admin Queue, Project Access Config, Collateral Manager, Lead Conflict Resolution, and Exception Action generated. Representative screen IDs include `710e1434518f403fb1cda79090ccba8b`, `133965e886bf44e1b0a488a29547718f`. |
| 06 | Finance | `16963605453633474186` | MCP timed out; manual Stitch execution required | Finance generation timed out after 120 seconds. Per Stitch MCP tool instruction, the timed-out call was not retried; follow-up project checks did not return a clear Finance screen. Keep this prompt ready for manual execution in Stitch because full payout processing remains in scope. |
| 07 | Developer / Project Team | `16963605453633474186` | Generated | Project Console, Project Facts Form, Collateral Review, and Visit Outcome generated. Representative screen IDs include `d03738d79a894d3e8867ed91c12230c6`, `846ab4743bd648729d6939acf7a93cf3`. |
| 08 | CP Owner / Org Leader | `16963605453633474186` | Generated | CP Owner Home, Team Management, Lead Quick Submit, Firm Lead Detail, and Payout Ledger generated. Representative screen IDs include `e8450d724098452ab9facf0958bae73e`, `3e2aa216f8e64fb2baf92b9647a377b0`. |
| 09 | CP Employee / Agent | `16963605453633474186` | Generated | Agent Home, Project Catalog, Share Kit, Lead Quick Submit, and Visit Proof / Follow-up generated. Representative screen IDs include `2088f2db56ca4a3697993aa408bed27b`, `1bbffc2f0f17495f82c9e8d6b6799754`. |
| 10 | CP Telecaller | `16963605453633474186` | Generated after QA correction | First pass generated Lead Call Detail and Disposition Form; QA found missing Telecaller Queue and Schedule / Escalate, then a corrective generation added them. Representative screen IDs: `83a34a26615c42deb2b0e9a2dc2bf307`, `a34d830ea28340cda392ab087a860336`, `37cc609dcd1a45eca9c43322c28ce494`, `d27752b973624df897965cc70c42264c`. |
| 11 | Buyer / Customer | `16963605453633474186` | Generated | Stitch reported the four-screen Buyer Project Link, Interest / Callback Form, Visit Confirmation, and Visit Proof Result flow generated horizontally in the target project. Representative screen IDs include `482bb21ea5ec4aedaf446571238d9306`, `9a0c88f846d548e698d1bec29af148fa`. |
| 12 | Compliance / Support | `16963605453633474186` | Generated | Stitch reported the five-screen Compliance Queue, Document Review, Evidence Bundle, Resolution Action, and Audit Export flow generated in the target project. Representative screen IDs include `03a61b7135974e598e1b72e958d9d3d7`, `40e47256d92242f88b24fd0fbe7daf4a`. |

## Open Stitch Action

[high] Prompt 06 Finance still needs manual execution in the Stitch UI because the MCP generation timed out and the Stitch MCP instruction prohibits retrying a timed-out `generate_screen_from_text` call. The Finance prompt remains part of this artifact and must not be removed or de-scoped; full payout processing is a core product differentiator.

---

## Expanded Screen Flows: Full Journey Coverage

The following sections expand each persona's screen flow to ~12 screens, covering the complete end-to-end journey from entry to goal completion, including variants (empty, error, loading, success states) and edge cases. New screens are marked `[NEW]`. Existing screens are marked `[EXISTING]`.

---

### Expanded Screens: Shared App Foundation (Prompt 01)

#### Full Ordered Screen Sequence (12 screens)

| # | Screen Name | Status | Description |
|---|---|---|---|
| 1 | `Shared_01_Login` | [EXISTING] | Android mobile login screen with CP Tech logo, Text Field: Mobile Number or Email (Required), Text Field: Password or OTP (Required), Button: Sign in, Link: Forgot password, error state for invalid credentials, suspended access message. |
| 2 | `Shared_02_OTP_Verification` | [NEW] | OTP input screen with 6-digit code field, countdown timer (60s), Resend OTP link, masked mobile/email display, error state for invalid/expired OTP, Button: Verify. |
| 3 | `Shared_03_Password_Reset` | [NEW] | Password reset flow with mobile/email input, OTP verification step, new password field with strength meter, confirm password, success confirmation, Button: Reset Password. |
| 4 | `Shared_04_Role_Selector` | [EXISTING] | Card-based role picker after one credential login. Show roles: CP Owner, CP Employee, RM, Finance. Include active firm/project context, Badge: Multiple roles, Button: Continue, access-denied state for deactivated role. |
| 5 | `Shared_05_Role_Switcher_Active` | [NEW] | In-app role switcher showing current active role, available roles, firm context switch, confirmation when switching roles changes project access, Button: Switch Role. |
| 6 | `Shared_06_Notification_Center` | [EXISTING] | List of notifications with read/unread state, category chips for Lead, Visit, Payout, Document, Support, safe preview text, timestamp `31/05/2026`, deep-link row, empty state. |
| 7 | `Shared_07_Notification_Empty` | [NEW] | Empty notification state with illustration, "No notifications yet" message, pull-to-refresh indicator, category chip: All (disabled when empty). |
| 8 | `Shared_08_Deep_Link_Resolver` | [EXISTING] | Transition screen showing permission check, allowed target preview, blocked target message, Button: Back to Home, Button: Contact Support. |
| 9 | `Shared_09_Offline_Sync_Queue` | [EXISTING] | Queue list with Lead draft, Document upload, Visit note. Status chips: Queued, Syncing, Failed, Conflict. Buttons: Retry, Cancel, Delete. Show cached timestamp and no-network banner. |
| 10 | `Shared_10_Profile_Management` | [NEW] | User profile screen with avatar, name, mobile, email, firm name, role, last login, Button: Edit Profile, Button: Change Password, privacy notice link. |
| 11 | `Shared_11_Settings` | [NEW] | Settings screen with toggles: Push Notifications, Email Notifications, Language (EN/HI/MR), Dark Mode, Data Saver, About, Version, Logout button, privacy policy link. |
| 12 | `Shared_12_Session_Expired` | [NEW] | Session expired overlay with message "Your session has expired for security", last activity timestamp, Button: Sign In Again, offline-safe cached data indicator. |

#### Journey Flow
```
Login → OTP Verification → Password Reset (if needed) → Role Selector → Role Switcher (in-app)
→ [Persona Home] → Notification Center → Notification Empty (variant)
→ Deep Link Resolver → Offline Sync Queue → Profile Management → Settings → Session Expired
```

---

### Expanded Screens: Justo Leadership (Prompt 02)

#### Full Ordered Screen Sequence (12 screens)

| # | Screen Name | Status | Description |
|---|---|---|---|
| 1 | `Leadership_01_Dashboard` | [EXISTING] | Aggregate KPI dashboard with cards for Active CPs, Accepted Leads, Verified Visits, Bookings, Payout SLA, Open Disputes, Compliance Exceptions. Include date filter `01/05/2026 - 31/05/2026`, city filter Mumbai/Pune/Nagpur, and stale data chip. |
| 2 | `Leadership_02_Dashboard_Loading` | [NEW] | Skeleton loading state for dashboard KPI cards, shimmer animation on charts, "Loading latest data..." message, stale data timestamp visible. |
| 3 | `Leadership_03_Dashboard_Empty` | [NEW] | Empty dashboard state with "No data available for selected period" message, date range selector, Button: Adjust Filters, onboarding hint for new users. |
| 4 | `Leadership_04_Filtered_Performance_View` | [EXISTING] | Filter panel for City, Cluster, RM, Project, CP Segment, Date Range. Input: Date Range (Required), Multi-select Chips: City/Cluster/RM/Project, Button: Apply Filters. |
| 5 | `Leadership_05_Drill_Down_Region` | [NEW] | Drill-down view by region/city showing CP count, lead volume, visit rate, booking conversion, payout status per city. Tap row to expand to cluster level. |
| 6 | `Leadership_06_Drill_Down_Project` | [NEW] | Project-level drill-down showing project name, developer, assigned CPs, lead pipeline, visit proof rate, booking status, collateral freshness. |
| 7 | `Leadership_07_CP_Network_Health` | [NEW] | CP network health summary: Active CPs, Stalled CPs, New CPs (30d), Compliance Complete %, Avg Activation Time. Sortable list with status chips. |
| 8 | `Leadership_08_Trend_Comparison` | [NEW] | Trend chart comparing current period vs previous period for leads, visits, bookings, payouts. Toggle: Week/Month/Quarter. Export button. |
| 9 | `Leadership_09_Risk_Exception_Queue` | [EXISTING] | Ranked list of risks with severity, owner team, SLA, linked entity count. Include examples: payout delay `₹2.4 lakh`, failed sync, document expiry, lead dispute. |
| 10 | `Leadership_10_Risk_Exception_Detail` | [EXISTING] | Summary-only detail view with accountable team, current SLA, allowed drill-down, privacy-safe evidence summary, audit timestamp, Button: Escalate. |
| 11 | `Leadership_11_Export_Share` | [NEW] | Export/share panel with format selector (PDF, Excel), date range, entity filter, privacy warning checkbox, Button: Generate Export, status: Generating/Ready/Sent. |
| 12 | `Leadership_12_Error_State` | [NEW] | Error state for dashboard with "Unable to load data" message, retry button, offline cached data timestamp, contact support link. |
| 13 | `Leadership_13_Cross_Persona_Dashboard` | [NEW] | Cross-persona performance dashboard with KPI cards per persona (Sourcing, RM, CP Owner, Telecaller, Compliance, Finance). Each card shows primary metric, trend sparkline, and delta vs previous period. Include bar chart comparing persona performance, heatmap grid by city/project, period selector (Week/Month/Quarter). PRD Trace: PRD-FR-085, PRD-FR-088. |
| 14 | `Leadership_14_Persona_Detail_Team` | [NEW] | Drill-down from persona KPI card showing team member list. Table columns: Rank, Name/Avatar, Role, Score, Trend (↑/↓/→), Comparison to Average. Tap row to expand to individual detail. Include persona selector at top, time filter, sort options. PRD Trace: PRD-FR-086. |
| 15 | `Leadership_15_Performance_Export` | [NEW] | Export panel with format selector (PDF/PNG), date range picker, persona filter chips, entity scope selector (All/Region/City/Project), privacy warning checkbox, Button: Generate Export. Show export status: Queued/Generating/Ready/Failed. Include download link when ready. PRD Trace: PRD-FR-087, PRD-NFR-019. |
| 16 | `Leadership_16_Period_Comparison` | [NEW] | Period comparison view with toggle: Current vs Previous Week/Month/Quarter. Show delta indicators (↑ green, ↓ red, → gray) for each KPI. Include trend sparklines, percentage change labels, and comparison bar charts. PRD Trace: PRD-FR-088. |

#### Journey Flow
```
Dashboard → Dashboard Loading (variant) → Dashboard Empty (variant) → Filtered Performance View
→ Drill Down Region → Drill Down Project → CP Network Health → Trend Comparison
→ Risk Exception Queue → Risk Exception Detail → Export/Share → Error State (variant)
→ Cross-Persona Dashboard → Persona Detail with Team → Performance Export → Period Comparison
```

---

### Expanded Screens: CP Sourcing Head (Prompt 03)

#### Full Ordered Screen Sequence (12 screens)

| # | Screen Name | Status | Description |
|---|---|---|---|
| 1 | `SourcingHead_01_Dashboard` | [EXISTING] | Funnel cards for New Prospects, Assigned to RM, Docs Pending, Under Review, Activated, Stalled. Include RM workload list, activation blockers, Button: Add CP Prospect. |
| 2 | `SourcingHead_02_Dashboard_Loading` | [NEW] | Skeleton loading state for funnel cards and RM workload list, shimmer animation, "Syncing CP network data..." message. |
| 3 | `SourcingHead_03_CP_Prospect_List` | [NEW] | Searchable CP prospect list with filters: Status (All/New/Assigned/Pending/Activated/Stalled), RM, Territory, Source. Sort by: Newest, Name, Status. Bulk actions: Assign RM, Export. |
| 4 | `SourcingHead_04_CP_Prospect_Create` | [EXISTING] | Form with Text Field: CP Firm Name (Required), Text Field: Owner Mobile (Required, tel), Text Field: RERA Number (Optional), Dropdown: Source (Required), Dropdown: Territory (Required), Dropdown: Assign RM (Required), duplicate warning panel. |
| 5 | `SourcingHead_05_CP_Prospect_Detail` | [NEW] | CP prospect detail view with firm profile, owner info, RERA status, assigned RM, onboarding progress, document checklist, activation blockers, action buttons: Edit, Assign RM, Escalate. |
| 6 | `SourcingHead_06_Onboarding_Governance_Queue` | [EXISTING] | List of CPs by status: Missing Docs, Under Review, Rejected, Blocked, Approved. Show CP name, RM, ageing, next action. |
| 7 | `SourcingHead_07_Activation_Detail` | [EXISTING] | Checklist for first login, employee added, project access assigned, first lead, first visit. Show RM notes, blocker chip, Button: Escalate. |
| 8 | `SourcingHead_08_Activation_Progress` | [NEW] | Detailed activation timeline showing each milestone date, RM actions taken, pending items, SLA countdown, Button: Send Reminder to CP, Button: Mark Stalled. |
| 9 | `SourcingHead_09_RM_Workload_View` | [NEW] | RM workload dashboard showing assigned CPs per RM, pending docs per RM, activation rate, average time to activation. Sortable list with performance indicators. |
| 10 | `SourcingHead_10_Inactive_CP_Management` | [NEW] | List of inactive CPs (no leads/visits in 60 days) with last activity date, reason chip, action buttons: Reactivate, Deactivate, Reassign. |
| 11 | `SourcingHead_11_Escalation_Modal` | [EXISTING] | Bottom sheet with linked CP, Category (Lead, Compliance, Payout, RM), Severity, Owner Team, Notes (Required multiline), Button: Create Ticket. |
| 12 | `SourcingHead_12_Bulk_Import` | [NEW] | Bulk CP prospect import screen with file upload (CSV/Excel), field mapping preview, validation errors list, Button: Import, progress indicator, success/failure summary. |
| 13 | `SourcingHead_13_Sourcing_Leaderboard` | [NEW] | Gamified leaderboard for sourcing managers (head + employees). Show rank, name/avatar initials, score breakdown (CPs onboarded, documents verified, CP employees added, activation rate), trend indicator (↑/↓/→), time filter chips (Day/Week/Month/Quarter). Highlight own rank if viewing as RM. Include team average comparison line. PRD Trace: PRD-FR-080, PRD-FR-081, PRD-NFR-018. |
| 14 | `SourcingHead_14_RM_Performance_Detail` | [NEW] | Individual RM performance detail screen. Metric cards: CPs Onboarded, Documents Verified, CP Employees Added, Activation Rate. Trend chart over time. Comparison to team average with delta indicators. Recent activity timeline. Button: View CPs Assigned. PRD Trace: PRD-FR-084. |
| 15 | `SourcingHead_15_Document_First_Verification` | [NEW] | First-level verification queue for uploaded CP documents. List with document thumbnail, CP name, document type, upload date, file size, basic validation status (file type OK, size OK, readable). Action buttons: Approve (first-level), Reject (with reason), Escalate to Compliance. Filter: Pending/Approved/Rejected. PRD Trace: PRD-FR-082. |
| 16 | `SourcingHead_16_CP_Onboarding_Assistant` | [NEW] | Guided onboarding workflow for a specific CP. Step-by-step checklist: Firm Profile → PAN/GST → RERA → Bank Details → KYC → First Employee → First Project → First Lead. Each step shows status (Pending/In Progress/Complete), required documents, RM actions. Include document upload CTA, verification status, activation trigger. PRD Trace: PRD-FR-083. |

#### Journey Flow
```
Dashboard → Dashboard Loading (variant) → CP Prospect List → CP Prospect Create → CP Prospect Detail
→ Onboarding Governance Queue → Activation Detail → Activation Progress → RM Workload View
→ Inactive CP Management → Escalation Modal → Bulk Import
→ Sourcing Leaderboard → RM Performance Detail → Document First-Verification → CP Onboarding Assistant
```

---

### Expanded Screens: RM / Sourcing Employee (Prompt 04)

#### Full Ordered Screen Sequence (12 screens)

| # | Screen Name | Status | Description |
|---|---|---|---|
| 1 | `RM_01_Home` | [EXISTING] | Today view with assigned CP prospects, pending documents, stalled CPs, escalations, offline sync banner, FAB: Add CP Prospect. |
| 2 | `RM_02_Home_Loading` | [NEW] | Skeleton loading state for today view cards, shimmer animation on lists, offline indicator if no network. |
| 3 | `RM_03_CP_Prospect_Form` | [EXISTING] | Text Field: CP Firm Name (Required), Owner Name (Required), Mobile (Required tel), Territory (Required), Source (Required dropdown), Next Follow-up Date (Required, dd/mm/yyyy), Button: Save Online / Queue Offline. |
| 4 | `RM_04_CP_Prospect_Detail` | [NEW] | CP prospect detail with firm info, owner contact, RERA status, document checklist progress, onboarding stage, assigned projects (if activated), action buttons: Edit, Upload Doc, Schedule Visit. |
| 5 | `RM_05_Assisted_Onboarding` | [EXISTING] | CP checklist with Firm Profile, PAN/GST, RERA, Bank Details, KYC. Include upload rows with queued/uploading/failed states and Button: Add Document. |
| 6 | `RM_06_Queued_Document_Upload` | [EXISTING] | Upload detail with File Picker (Required), Document Type (Required dropdown), File Size Limit note, Buttons: Retry, Cancel, Delete, Status: Pending server validation. |
| 7 | `RM_07_Meeting_Log` | [NEW] | Meeting log for CP prospect with date, location, notes, next action, follow-up date. Button: Add Meeting, Button: Mark Contacted. Empty state for no meetings yet. |
| 8 | `RM_08_Task_List` | [NEW] | Task list for assigned CPs: Follow-up due, Document pending, Visit to schedule, Escalation to create. Priority chips: High/Medium/Low. Filter: Today/This Week/Overdue. |
| 9 | `RM_09_Site_Visit_Support` | [EXISTING] | Schedule visit screen with Lead, Buyer Mobile, Project, Slot Date/Time, Proof Method chips: QR, OTP, Geofence, Site Desk, Admin Fallback; Button: Schedule Visit. |
| 10 | `RM_10_Visit_History` | [NEW] | Visit history list for assigned CPs with date, project, buyer (masked), proof status, outcome. Filter: All/Verified/Pending/Failed. Sort by date. |
| 11 | `RM_11_Performance_View` | [NEW] | RM performance summary: CPs assigned, CPs activated, leads generated, visits verified, bookings. Comparison to target. Period selector. |
| 12 | `RM_12_Escalation_Detail` | [NEW] | Escalation detail for CP issue with category, severity, owner team, timeline, actions taken, Button: Update Status, Button: Close Escalation. |
| 13 | `RM_13_Document_First_Verification` | [NEW] | First-level verification screen for uploaded CP documents. Show document preview thumbnail, file type, size, upload date. Basic validation checks: file type OK, size within limit, readable/not corrupted. Action buttons: Approve (first-level), Reject (with reason dropdown), Escalate to Compliance. Include CP name, document type, and next step indicator. PRD Trace: PRD-FR-082. |
| 14 | `RM_14_CP_Onboarding_Assistant` | [NEW] | Guided onboarding workflow for a specific CP. Step-by-step checklist with progress indicator: Firm Profile → PAN/GST → RERA → Bank Details → KYC → First Employee → First Project → First Lead. Each step shows status chip (Pending/In Progress/Complete), required documents, and RM action CTA. Include document upload button, verification status, and activation trigger. Offline-safe with sync queue indicator. PRD Trace: PRD-FR-083. |
| 15 | `RM_15_Sourcing_Leaderboard_Own` | [NEW] | Personal position on sourcing leaderboard. Show own rank (highlighted), score breakdown (CPs onboarded, documents verified, activation rate), trend indicator, time filter (Day/Week/Month). Include team ranking list with top 5 and own position highlighted. Comparison to team average with delta indicator. PRD Trace: PRD-FR-080, PRD-FR-081, PRD-NFR-018. |
| 16 | `RM_16_Self_Performance_Detail` | [NEW] | Own detailed performance view. Metric cards: CPs Onboarded, Documents Verified, CP Employees Added, Activation Rate. Trend chart over selected period. Comparison to team average with delta indicators (↑/↓/→). Recent activity timeline showing last 10 actions. Goal progress bars if targets configured. PRD Trace: PRD-FR-084. |

#### Journey Flow
```
Home → Home Loading (variant) → CP Prospect Form → CP Prospect Detail → Assisted Onboarding
→ Queued Document Upload → Meeting Log → Task List → Site Visit Support → Visit History
→ Performance View → Escalation Detail
→ Document First-Verification → CP Onboarding Assistant → Sourcing Leaderboard (own) → Self Performance Detail
```

---

### Expanded Screens: Sales / Admin Ops (Prompt 05)

#### Full Ordered Screen Sequence (12 screens)

| # | Screen Name | Status | Description |
|---|---|---|---|
| 1 | `AdminOps_01_Admin_Queue` | [EXISTING] | Tabbed queue with Setup, Collateral, Conflicts, Exceptions, Audit. Show counts, failed notifications, blocked changes, and priority chips. |
| 2 | `AdminOps_02_Queue_Loading` | [NEW] | Skeleton loading state for queue tabs, shimmer animation on list items, "Loading admin tasks..." message. |
| 3 | `AdminOps_03_Project_List` | [NEW] | Searchable project list with status chips: Active/Paused/Expired. Show project name, developer, assigned CPs, collateral freshness. Button: Add Project. |
| 4 | `AdminOps_04_Project_Access_Config` | [EXISTING] | Searchable list of CP firms and projects. Controls: CP Selector (Required), Project Selector (Required), Access Toggle, Reason (Required text), Button: Save Access. |
| 5 | `AdminOps_05_Lead_Rule_Config` | [NEW] | Lead conflict rule configuration with rule name, priority window (days), attribution logic (First/Last/Override), auto-resolve toggle, Button: Save Rule. |
| 6 | `AdminOps_06_Collateral_Manager` | [EXISTING] | Collateral list with version, expiry date, approval state, preview thumbnail, actions Approve, Replace, Expire, Reject, audit note. |
| 7 | `AdminOps_07_Visit_Proof_Config` | [NEW] | Visit proof method configuration per project: enable/disable QR, OTP, Geofence, Site Desk, Admin Fallback. Geofence radius input, consent text preview. |
| 8 | `AdminOps_08_Lead_Conflict_Resolution` | [EXISTING] | Evidence screen with duplicate leads, timestamps, CP owner, employee attribution, source, policy rule, restricted PII masking, decision buttons: Accept, Reject, Override. |
| 9 | `AdminOps_09_User_Role_Management` | [NEW] | User/role management list with name, role, firm, status (Active/Suspended), last login. Actions: Edit Role, Suspend, Reset Password. Button: Invite User. |
| 10 | `AdminOps_10_Audit_Log_View` | [NEW] | Audit log list with action type, user, timestamp, entity affected, IP address. Filters: Date Range, User, Action Type. Button: Export Audit. |
| 11 | `AdminOps_11_Exception_Action_Modal` | [EXISTING] | Bottom sheet requiring Action Type, Reason (Required multiline), affected users/leads summary, confirmation checkbox, Button: Apply and Audit. |
| 12 | `AdminOps_12_Bulk_Operations` | [NEW] | Bulk operation screen for project access, collateral expiry, user suspension. File upload or multi-select, preview changes, confirmation checkbox, Button: Apply Bulk. |

#### Journey Flow
```
Admin Queue → Queue Loading (variant) → Project List → Project Access Config → Lead Rule Config
→ Collateral Manager → Visit Proof Config → Lead Conflict Resolution → User Role Management
→ Audit Log View → Exception Action Modal → Bulk Operations
```

---

### Expanded Screens: Finance (Prompt 06)

#### Full Ordered Screen Sequence (12 screens)

| # | Screen Name | Status | Description |
|---|---|---|---|
| 1 | `Finance_01_Payout_Queue` | [EXISTING] | Status tabs: Eligible, Invoice Pending, Under Review, Approved, Scheduled, Paid, Failed, Disputed, Clawback. Show CP name, project, amount `₹2.4 lakh`, SLA, priority. |
| 2 | `Finance_02_Queue_Loading` | [NEW] | Skeleton loading state for payout queue tabs, shimmer animation on list items, "Loading payout data..." message. |
| 3 | `Finance_03_Payout_SLA_Dashboard` | [NEW] | Payout SLA summary: Due Today, Overdue, Scheduled This Week, Failed Pending Retry. SLA breach count, average processing time. Export button. |
| 4 | `Finance_04_Payout_Detail` | [EXISTING] | Detail screen with booking milestone, CP eligibility, invoice, GST/TDS, bank/KYC, cancellation risk, validation checklist. |
| 5 | `Finance_05_Invoice_List` | [NEW] | Invoice list for CP payouts with invoice number, CP name, amount, GST, TDS, status (Received/Pending/Rejected), upload date. Button: Upload Invoice. |
| 6 | `Finance_06_GST_TDS_Detail` | [NEW] | GST/TDS detail for payout with GSTIN, invoice match status, TDS rate, TDS amount, deduction summary, Button: Request Correction from CP. |
| 7 | `Finance_07_Approval_Action` | [EXISTING] | Maker-checker panel with Buttons: Approve, Reject, Request Correction. Text Field: Reason (Required for reject/correction), Checkbox: I confirm policy checks. |
| 8 | `Finance_08_Payment_Scheduling` | [EXISTING] | Inputs for Scheduled Date (Required dd/mm/yyyy), Payment Reference (Required when paid), Amount (Required currency), Failure Reason (Required when failed). |
| 9 | `Finance_09_Bank_Reconciliation` | [NEW] | Bank reconciliation screen with payment reference, bank statement match status, amount variance, Button: Mark Reconciled, Button: Flag Discrepancy. |
| 10 | `Finance_10_Dispute_Detail` | [NEW] | Payout dispute detail with dispute reason, raised by, evidence attachments, linked booking, status timeline, Button: Resolve Dispute, Button: Escalate. |
| 11 | `Finance_11_Reconciliation_Clawback` | [EXISTING] | Reconciliation status panel with source reference, paid/reconciled/disputed/clawback state, reason field, immutable audit timeline. |
| 12 | `Finance_12_Payment_History` | [NEW] | Payment history list with date, CP name, amount, reference, status (Success/Failed/Reversed). Filters: Date Range, Status, CP. Export button. |

#### Journey Flow
```
Payout Queue → Queue Loading (variant) → Payout SLA Dashboard → Payout Detail → Invoice List
→ GST/TDS Detail → Approval Action → Payment Scheduling → Bank Reconciliation
→ Dispute Detail → Reconciliation/Clawback → Payment History
```

---

### Expanded Screens: Developer / Project Team (Prompt 07)

#### Full Ordered Screen Sequence (12 screens)

| # | Screen Name | Status | Description |
|---|---|---|---|
| 1 | `Developer_01_Project_Console` | [EXISTING] | Assigned projects list with stale data flags, inventory updates due, collateral approvals, visit outcome items. Include search and status chips. |
| 2 | `Developer_02_Console_Loading` | [NEW] | Skeleton loading state for project console, shimmer animation on project cards, "Loading project data..." message. |
| 3 | `Developer_03_Project_List` | [NEW] | Full project list with filters: Active/Paused/Expired, City, Developer. Sort by: Name, Last Updated, Stale Flag. Show project thumbnail, location, CP count. |
| 4 | `Developer_04_Project_Facts_Form` | [EXISTING] | Inputs for Project Name (Read-only), Inventory Status (Required dropdown), Offer Text (Optional), RERA Details (Required), Site Instructions (Required multiline), Freshness Timestamp. |
| 5 | `Developer_05_Inventory_Management` | [NEW] | Inventory management screen with unit type, available/total count, price range, possession date, Button: Update Inventory. Show last updated timestamp. |
| 6 | `Developer_06_Offer_Scheme` | [NEW] | Offer/scheme management with offer title, description, validity dates, applicable units, Button: Add Offer, Button: Expire Offer. Preview how offer appears to CPs. |
| 7 | `Developer_07_Collateral_List` | [NEW] | Collateral list with file type, version, approval status, expiry date, Button: Upload New, Button: Request Approval. Filter: Approved/Pending/Expired. |
| 8 | `Developer_08_Collateral_Review` | [EXISTING] | Preview card with file, version, expiry, claim-safe fields, buttons Approve, Reject, Expire, Replace, Reason field. |
| 9 | `Developer_09_Visit_Slot_Management` | [NEW] | Visit slot configuration with date, time slots, max visitors per slot, site contact, Button: Add Slot, Button: Close Slot. Show booked/available count. |
| 10 | `Developer_10_Visit_Outcome` | [EXISTING] | Visit detail with proof status, buyer masked phone, lead, project, outcome selector, note field, Button: Save Outcome. |
| 11 | `Developer_11_Visit_Outcome_Detail` | [NEW] | Detailed visit outcome with proof method used, timestamp, geofence status (if applicable), buyer feedback (if any), lead status update, Button: Edit Outcome. |
| 12 | `Developer_12_Project_Performance` | [NEW] | Project performance dashboard: leads received, visits verified, booking rate, CP activity, collateral views. Period selector, export button. |

#### Journey Flow
```
Project Console → Console Loading (variant) → Project List → Project Facts Form → Inventory Management
→ Offer Scheme → Collateral List → Collateral Review → Visit Slot Management → Visit Outcome
→ Visit Outcome Detail → Project Performance
```

---

### Expanded Screens: CP Owner / Org Leader (Prompt 08)

#### Full Ordered Screen Sequence (12 screens)

| # | Screen Name | Status | Description |
|---|---|---|---|
| 1 | `CPOwner_01_Home` | [EXISTING] | Firm status, compliance status, team alerts, leads summary, visits, bookings, payout summary `₹3.6 lakh due`, disputes, notification bell, sync queue chip. |
| 2 | `CPOwner_02_Home_Loading` | [NEW] | Skeleton loading state for home dashboard cards, shimmer animation, offline indicator if no network, cached data timestamp. |
| 3 | `CPOwner_03_Firm_Profile` | [NEW] | Firm profile with firm name, RERA number, PAN/GST, bank details, compliance status, Button: Edit Profile, Button: Upload Document. Show compliance checklist progress. |
| 4 | `CPOwner_04_Team_Management` | [EXISTING] | Employee list with roles, project access, active work counts, Button: Invite Employee, actions Deactivate/Reassign. Input: Employee Mobile (Required tel), Role (Required dropdown), Project Access (Required multi-select). |
| 5 | `CPOwner_05_Employee_Detail` | [NEW] | Employee detail with name, role, project access, leads submitted, visits completed, performance summary, Button: Edit Access, Button: Deactivate. |
| 6 | `CPOwner_06_Lead_Quick_Submit` | [EXISTING] | Phone-first lead form with Buyer Mobile (Required tel), Buyer Name (Optional), Project (Required), Budget (Optional currency), Button: Submit Lead. Result states: Accepted, Conflict, Rejected, Pending Sync, Pending Review. |
| 7 | `CPOwner_07_Firm_Lead_Detail` | [EXISTING] | Lead timeline with owner/employee attribution, follow-up, visit, conflict/dispute CTA, booking link if available, restricted buyer data labels. |
| 8 | `CPOwner_08_Visit_List` | [NEW] | Visit list for firm with date, project, buyer (masked), proof status, outcome. Filter: All/Verified/Pending/Failed. Sort by date. Button: Schedule Visit. |
| 9 | `CPOwner_09_Booking_Status` | [NEW] | Booking status screen with booking ID, project, buyer (masked), milestone timeline (Booked → Documentation → Payment → Completed), expected date, Button: View Details. |
| 10 | `CPOwner_10_Payout_Ledger` | [EXISTING] | Payout list and detail with status timeline, deductions GST/TDS, payment reference, expected date, Button: Raise Dispute, linked evidence. |
| 11 | `CPOwner_11_Dispute_Detail` | [NEW] | Dispute detail with dispute reason, raised date, status, evidence attachments, linked payout, resolution timeline, Button: Add Evidence, Button: Close Dispute. |
| 12 | `CPOwner_12_Support_Ticket` | [NEW] | Support ticket list and detail with category, priority, status, timeline, Button: Raise Ticket, Button: Add Comment. Filter: Open/Closed/All. |
| 13 | `CPOwner_13_Firm_Dashboard` | [NEW] | Dedicated CP Owner dashboard (firm-wide performance). KPI cards: Leads Generated, Visits Completed, Bookings Closed, Payout Earned `₹3.6 lakh`, Team Activity, Compliance Status. Trend charts for leads/visits/bookings over time. Team activity summary showing top performers. Compliance status indicator. Payout summary with next expected date. PRD Trace: PRD-FR-089. |
| 14 | `CPOwner_14_Project_Leaderboard` | [NEW] | Per-project leaderboard filtered to own firm. Ranked list of CP employees within firm. Columns: Rank, Employee Name/Avatar, Leads Generated, Visits Completed, Bookings Closed, Payout Earned, Trend (↑/↓/→). Time filter chips: Day/Week/Month/Quarter. Own rank highlighted if viewing as employee. Tap row to view employee detail. PRD Trace: PRD-FR-090, PRD-NFR-018. |
| 15 | `CPOwner_15_Performance_Comparison` | [NEW] | Performance comparison view. Firm metrics compared to project average, city average, or top performers (anonymized where policy requires). Show benchmark lines on charts, delta indicators (↑/↓/→), percentage change labels. Period selector: Week/Month/Quarter. PRD Trace: PRD-FR-093. |
| 16 | `CPOwner_16_Employee_Performance_Detail` | [NEW] | Individual employee performance detail. Metric cards: Leads Submitted, Visits Scheduled, Bookings Attributed, Follow-up Completion Rate. Trend chart over time. Comparison to firm average with delta indicators. Recent activity timeline. Button: View Leads, Button: View Visits. PRD Trace: PRD-FR-084. |

#### Journey Flow
```
Home → Home Loading (variant) → Firm Profile → Team Management → Employee Detail
→ Lead Quick Submit → Firm Lead Detail → Visit List → Booking Status → Payout Ledger
→ Dispute Detail → Support Ticket
→ Firm Dashboard → Project Leaderboard → Performance Comparison → Employee Performance Detail
```

---

### Expanded Screens: CP Employee / Agent (Prompt 09)

#### Full Ordered Screen Sequence (12 screens)

| # | Screen Name | Status | Description |
|---|---|---|---|
| 1 | `CPEmployee_01_Agent_Home` | [EXISTING] | Assigned project shortcuts, lead quick submit CTA, due follow-ups, upcoming visits, sync status, bottom nav Home/Search/Leads/Profile. |
| 2 | `CPEmployee_02_Home_Loading` | [NEW] | Skeleton loading state for agent home, shimmer animation on project cards and lead list, offline indicator. |
| 3 | `CPEmployee_03_Project_Catalog` | [EXISTING] | Search and filters for location, budget `₹80 lakh - ₹1.5 crore`, BHK, possession. Project card with freshness, inventory, offer, RERA, approved collateral indicator. |
| 4 | `CPEmployee_04_Project_Detail` | [NEW] | Detailed project view with full description, amenities, floor plans, location map, price breakdown, RERA details, Button: Share, Button: Submit Lead. |
| 5 | `CPEmployee_05_Share_Kit` | [EXISTING] | Approved assets list, expired-share blocked state, channel selector WhatsApp/SMS/Copy Link, buyer context selector, Button: Share Approved Kit. |
| 6 | `CPEmployee_06_Lead_Quick_Submit` | [EXISTING] | Buyer Mobile (Required tel), Buyer Name (Optional), Project (Required), Source (Required), Consent Checkbox, Button: Register Lead; result chip accepted/conflict/rejected/pending sync. |
| 7 | `CPEmployee_07_Lead_List` | [NEW] | Lead list with status chips: New/Follow-up/Visit Scheduled/Booked/Lost. Filter: Today/This Week/All. Sort by: Newest, Follow-up Due, Status. |
| 8 | `CPEmployee_08_Lead_Detail_Timeline` | [NEW] | Lead detail with full timeline: submitted, follow-ups, visits, booking status. Buyer info (masked), project, attribution, Button: Add Follow-up, Button: Schedule Visit. |
| 9 | `CPEmployee_09_Follow_Up_List` | [NEW] | Follow-up task list with due date, lead name, project, action type (Call/Visit/Message), Button: Mark Done, Button: Reschedule. Filter: Today/Overdue/Upcoming. |
| 10 | `CPEmployee_10_Visit_Proof` | [EXISTING] | Visit schedule with slot, proof method, geofence consent, QR/OTP entry, fallback selector, outcome note, next follow-up date. |
| 11 | `CPEmployee_11_Visit_List` | [NEW] | Visit list with date, project, buyer (masked), proof status, outcome. Filter: Upcoming/Completed/Failed. Sort by date. Button: Schedule New Visit. |
| 12 | `CPEmployee_12_Profile_Settings` | [NEW] | Profile and settings screen with name, mobile, role, project access (read-only), performance summary, Button: Change Password, notification preferences, logout. |
| 13 | `CPEmployee_13_Personal_Dashboard` | [NEW] | Dedicated CP Employee dashboard (personal performance). KPI cards: Leads Submitted, Visits Scheduled, Bookings Attributed, Follow-up Completion Rate. Trend chart over time. Comparison to firm average with delta indicator. Quick actions: Submit Lead, Schedule Visit. PRD Trace: PRD-FR-091. |
| 14 | `CPEmployee_14_Project_Leaderboard` | [NEW] | Per-project leaderboard (global or firm-scoped per policy). Ranked list of CP employees. Columns: Rank, Name/Avatar, Leads, Visits, Bookings, Trend (↑/↓/→). Time filter chips: Day/Week/Month/Quarter. Own rank highlighted. Tap row to view detail (anonymized where policy requires). PRD Trace: PRD-FR-090, PRD-NFR-018. |
| 15 | `CPEmployee_15_Performance_Comparison` | [NEW] | Performance comparison view. Personal metrics compared to firm average, project average, or top performers (anonymized). Show benchmark lines, delta indicators, percentage change. Period selector. PRD Trace: PRD-FR-093. |
| 16 | `CPEmployee_16_Self_Performance_Detail` | [NEW] | Own detailed performance view. Metric breakdown: Leads by project, Visits by proof method, Booking conversion rate, Follow-up completion. Trend charts over time. Recent activity timeline. Goal progress bars if targets configured. PRD Trace: PRD-FR-084. |

#### Journey Flow
```
Agent Home → Home Loading (variant) → Project Catalog → Project Detail → Share Kit
→ Lead Quick Submit → Lead List → Lead Detail Timeline → Follow-Up List → Visit Proof
→ Visit List → Profile/Settings
→ Personal Dashboard → Project Leaderboard → Performance Comparison → Self Performance Detail
```

---

### Expanded Screens: CP Telecaller (Prompt 10)

#### Full Ordered Screen Sequence (12 screens)

| # | Screen Name | Status | Description |
|---|---|---|---|
| 1 | `Telecaller_01_Queue` | [EXISTING] | Assigned leads list with project, due time, status, basic priority label, overdue chip, no AI score. Filters: Due Today, Overdue, Completed. |
| 2 | `Telecaller_02_Queue_Loading` | [NEW] | Skeleton loading state for telecaller queue, shimmer animation on lead rows, "Loading assigned leads..." message. |
| 3 | `Telecaller_03_Queue_Empty` | [NEW] | Empty queue state with illustration, "No leads assigned" message, pull-to-refresh indicator, Button: Check Back Later. |
| 4 | `Telecaller_04_Lead_Call_Detail` | [EXISTING] | Lead detail with masked buyer phone, project, prior timeline, Button: Start Call, Button: Add Disposition. |
| 5 | `Telecaller_05_Lead_Detail_Full` | [NEW] | Full lead detail with buyer name (masked), project, budget, location, source, lead age, prior call history, notes, Button: Edit Lead (limited fields). |
| 6 | `Telecaller_06_Call_History` | [NEW] | Call history list with date, time, duration, outcome, lead name. Filter: Today/This Week/All. Sort by date. Button: Log Manual Call. |
| 7 | `Telecaller_07_Disposition_Form` | [EXISTING] | Inputs for Call Outcome (Required dropdown), Budget (Optional currency), Location (Optional), Urgency (Optional dropdown), Objection (Optional text), Visit Intent (Required yes/no), Next Follow-up Date (Required dd/mm/yyyy). |
| 8 | `Telecaller_08_Follow_Up_List` | [NEW] | Follow-up list with due date, lead name, project, last call outcome, Button: Call Now, Button: Mark Done. Filter: Today/Overdue/Upcoming. |
| 9 | `Telecaller_09_Schedule_Escalate` | [EXISTING] | Action panel to schedule follow-up, request site visit, or escalate hot lead. Include Notify RM toggle and Button: Save Action. |
| 10 | `Telecaller_10_Visit_Schedule_Detail` | [NEW] | Visit schedule detail with slot date/time, site address, buyer confirmation status, proof method, Button: Confirm Visit, Button: Reschedule. |
| 11 | `Telecaller_11_Escalation_Detail` | [NEW] | Escalation detail with lead, escalation reason, RM notified status, escalation date, Button: Update Status, Button: Close Escalation. |
| 12 | `Telecaller_12_Performance_View` | [NEW] | Telecaller performance summary: calls made, dispositions logged, visits scheduled, conversion rate. Period selector, comparison to target. |
| 13 | `Telecaller_13_Dashboard` | [NEW] | Dedicated telecaller dashboard. KPI cards: Calls Made Today, Dispositions Logged, Visit Intent Rate, Follow-up Completion, Escalations. Call volume chart (bar chart by day). Conversion funnel: Calls → Dispositions → Visit Intent → Visits Scheduled. Follow-up completion gauge. Escalation count with trend. PRD Trace: PRD-FR-092. |
| 14 | `Telecaller_14_Call_Performance_Detail` | [NEW] | Detailed call performance view. Metric breakdown: Calls by outcome (Connected/No Answer/Busy/Wrong Number), Dispositions by category (Hot/Warm/Cold/Lost), Visit intent rate, Escalation rate. Trend charts over time. Goal progress bars. Recent call timeline. PRD Trace: PRD-FR-084. |
| 15 | `Telecaller_15_Performance_Comparison` | [NEW] | Performance comparison view. Personal metrics compared to team average or top performers (anonymized). Show benchmark lines, delta indicators, percentage change. Period selector. PRD Trace: PRD-FR-093. |
| 16 | `Telecaller_16_Leaderboard` | [NEW] | Telecaller leaderboard (if configured). Ranked list with own rank highlighted. Columns: Rank, Name/Avatar, Calls Made, Dispositions, Visit Intent Rate, Trend (↑/↓/→). Time filter: Day/Week/Month. Score breakdown showing weighted metrics. PRD Trace: PRD-FR-080, PRD-FR-081, PRD-NFR-018. |

#### Journey Flow
```
Queue → Queue Loading (variant) → Queue Empty (variant) → Lead Call Detail → Lead Detail Full
→ Call History → Disposition Form → Follow-Up List → Schedule/Escalate → Visit Schedule Detail
→ Escalation Detail → Performance View
→ Dashboard → Call Performance Detail → Performance Comparison → Leaderboard
```

---

### Expanded Screens: Buyer / Customer (Prompt 11)

#### Full Ordered Screen Sequence (12 screens)

| # | Screen Name | Status | Description |
|---|---|---|---|
| 1 | `Buyer_01_Project_Link` | [EXISTING] | Approved project facts only: project name, location, price range `₹85 lakh - ₹1.4 crore`, BHK, RERA number, offer, CP/Justo attribution, freshness date `31/05/2026`. |
| 2 | `Buyer_02_Project_Gallery` | [NEW] | Project image gallery with swipeable photos, floor plans, amenities icons, location map thumbnail. Button: Request More Photos. |
| 3 | `Buyer_03_Price_Calculator` | [NEW] | Price calculator with base price, floor rise, parking, GST estimate, registration estimate, total estimate. Disclaimer: "Estimates only, final price from developer." |
| 4 | `Buyer_04_Interest_Callback_Form` | [EXISTING] | Inputs for Name (Required), Mobile (Required tel), Preferred Callback Date (Optional dd/mm/yyyy), Consent Checkbox (Required), Buttons: Request Callback, Request Site Visit. |
| 5 | `Buyer_05_Callback_Confirmation` | [NEW] | Callback request confirmation with "We'll call you back" message, expected callback time, CP/Justo contact info, Button: Modify Request, Button: Cancel Request. |
| 6 | `Buyer_06_Visit_Confirmation` | [EXISTING] | Visit slot detail, site address, CP/Justo contact, OTP/QR instructions, Button: Confirm Visit, fallback info. |
| 7 | `Buyer_07_Visit_Reminder` | [NEW] | Visit reminder screen with countdown, site address, directions link, what to bring list, contact number, Button: Reschedule, Button: Cancel Visit. |
| 8 | `Buyer_08_Visit_Proof_Result` | [EXISTING] | Success/failure state with OTP verified, QR scanned, geofence confirmed, or fallback used. Show next step and privacy-safe confirmation. |
| 9 | `Buyer_09_Visit_History` | [NEW] | Visit history list with date, project, status (Scheduled/Completed/No-Show), proof status. Button: Schedule New Visit. |
| 10 | `Buyer_10_KYC_Form` | [NEW] | KYC form with Name (Required), PAN (Required), Aadhaar (Optional), Address (Required), Button: Submit KYC. Show privacy notice, data usage consent. |
| 11 | `Buyer_11_Support_Contact` | [NEW] | Support/contact screen with CP contact (masked), Justo support number, FAQ link, Button: Call Support, Button: Email Support, Button: Chat (if available). |
| 12 | `Buyer_12_Error_State` | [NEW] | Error state for project link with "Link expired or invalid" message, Button: Contact CP, Button: Browse Projects (if available), privacy notice. |

#### Journey Flow
```
Project Link → Project Gallery → Price Calculator → Interest/Callback Form → Callback Confirmation
→ Visit Confirmation → Visit Reminder → Visit Proof Result → Visit History → KYC Form
→ Support/Contact → Error State (variant)
```

---

### Expanded Screens: Compliance / Support (Prompt 12)

#### Full Ordered Screen Sequence (12 screens)

| # | Screen Name | Status | Description |
|---|---|---|---|
| 1 | `Compliance_01_Queue` | [EXISTING] | Tabs: Documents, Expiries, Disputes, Payout Issues, Lead Conflicts, Collateral Issues. Show SLA, owner, severity, ageing, and queue count. |
| 2 | `Compliance_02_Queue_Loading` | [NEW] | Skeleton loading state for compliance queue tabs, shimmer animation on list items, "Loading compliance data..." message. |
| 3 | `Compliance_03_Dashboard` | [NEW] | Compliance dashboard with SLA compliance %, open items by category, items resolved this period, average resolution time, breach alerts. |
| 4 | `Compliance_04_Document_List` | [NEW] | Document list with filters: Status (Pending/Approved/Rejected/Expired), Document Type, CP Firm. Sort by: Upload Date, Expiry Date. Bulk actions: Approve, Reject. |
| 5 | `Compliance_05_Document_Review` | [EXISTING] | Document preview card, metadata, CP profile summary, upload status, validation state, prior rejection reason, buttons Approve, Reject, Request Clarification, Flag. |
| 6 | `Compliance_06_Dispute_List` | [NEW] | Dispute list with category (Lead/Payout/Booking), status (Open/Under Review/Resolved/Escalated), raised by, date, SLA. Sort by severity, date. |
| 7 | `Compliance_07_Evidence_Bundle` | [EXISTING] | Linked lead/visit/booking/payout/document, entity timeline, attachments, SLA, owner team, resolution status, comment field. |
| 8 | `Compliance_08_Support_Ticket_Detail` | [NEW] | Support ticket detail with ticket ID, category, priority, status, raised by, timeline, comments, attachments, Button: Update Status, Button: Resolve. |
| 9 | `Compliance_09_SLA_Monitoring` | [NEW] | SLA monitoring dashboard with items by SLA status: On Track/At Risk/Breached. SLA countdown per item, Button: Escalate Breached. |
| 10 | `Compliance_10_Resolution_Action` | [EXISTING] | Action bottom sheet with Resolution Type (Required), Reason (Required multiline), Notify Originator toggle, Button: Resolve and Audit. |
| 11 | `Compliance_11_Audit_Log_Detail` | [NEW] | Detailed audit log with action, user, timestamp, entity, before/after values, IP address. Filters: Date Range, User, Entity Type. Button: Export. |
| 12 | `Compliance_12_Audit_Export` | [EXISTING] | Filters for Entity Type, Date Range, CP Firm, Privacy Warning checkbox, Button: Generate Export, statuses Preview/Generating/Ready/Blocked/Failed. |

#### Journey Flow
```
Queue → Queue Loading (variant) → Dashboard → Document List → Document Review → Dispute List
→ Evidence Bundle → Support Ticket Detail → SLA Monitoring → Resolution Action → Audit Log Detail
→ Audit Export
```

---

## Summary: Screen Count per Persona

| Persona | Existing Screens | New State / Edge Screens | New Gamification / Leaderboard Screens | Total Screens |
|---|---|---|---|---|
| Shared App Foundation | 5 | 7 | — | 12 |
| Justo Leadership | 4 | 8 | 4 | 16 |
| CP Sourcing Head | 5 | 7 | 4 | 16 |
| RM / Sourcing Employee | 5 | 7 | 4 | 16 |
| Sales / Admin Ops | 5 | 7 | — | 12 |
| Finance | 5 | 7 | — | 12 |
| Developer / Project Team | 4 | 8 | — | 12 |
| CP Owner / Org Leader | 5 | 7 | 4 | 16 |
| CP Employee / Agent | 5 | 7 | 4 | 16 |
| CP Telecaller | 4 | 8 | 4 | 16 |
| Buyer / Customer | 4 | 8 | — | 12 |
| Compliance / Support | 5 | 7 | — | 12 |
| **TOTAL** | **56** | **88** | **24** | **168** |

---

## Stitch MCP Execution Log - 31/05/2026

Target project: `16963605453633474186`

Design system used for all MCP calls: `CP Tech Digital` (`assets/a4fcff9ba89d4126a1be6a3518716a4e`)

### Inventory Clarification

The expanded prompt file contains `112` `[NEW]` screens, not `24`. The `24` count refers only to the gamification / leaderboard / dashboard additions. All `112` `[NEW]` screens remain required for complete persona journeys.

### Persona Generation Status

| Persona / Bundle | MCP Status | Validation Status | Notes |
|---|---|---|---|
| Shared App Foundation | Generated | Partially verified by screen list | Stitch reported all 7 new shared screens generated. Representative confirmed screens include `OTP Verification - CP Tech Android`, `Password Reset - CP Tech Android`, `Role Switcher - CP Tech Android`, `Notifications Empty - CP Tech Android`, `Profile Management - CP Tech Android`, `Settings - CP Tech Android`, and `Session Expired - CP Tech Android`. |
| Justo Leadership | Generated after timeout recovery | Partially verified by screen list and successful final two-screen response | The first two Leadership calls timed out but created the required state/drill-down screens in the project. Confirmed screens include `Leadership_02_Dashboard_Loading`, `Leadership_03_Dashboard_Empty`, `Leadership_05_Drill_Down_Region`, `Leadership_06_Drill_Down_Project`, `Leadership_07_CP_Network_Health`, `Leadership_08_Trend_Comparison`, `Leadership_11_Export_Share`, `Leadership_12_Error_State`, `Leadership_15_Performance_Export`, and `Leadership_16_Period_Comparison`. Final MCP response successfully created `Leadership_13_Cross_Persona_Dashboard` and `Leadership_14_Persona_Detail_Team`. |
| CP Sourcing Head | Submitted to Stitch; MCP timed out | Visual QA pending | Full 11-screen bundle submitted: loading, prospect list/detail, activation progress, RM workload, inactive CP management, bulk import, sourcing leaderboard, RM detail, document first verification, onboarding assistant. The project listing endpoint timed out afterward, so visual verification is pending. |
| RM / Sourcing Employee | Submitted to Stitch; MCP timed out | Visual QA pending | Full 11-screen bundle submitted: loading, CP detail, meeting log, tasks, visit history, performance, escalation detail, document verification, onboarding assistant, leaderboard, self performance. |
| Sales / Admin Ops | Submitted to Stitch; MCP timed out | Visual QA pending | Full 7-screen bundle submitted: loading, project list, lead rule config, visit proof config, user roles, audit log, bulk operations. |
| Finance | Generated | MCP response verified | Stitch generated all 7 Finance screens: `Finance_02_Queue_Loading`, `Finance_03_Payout_SLA_Dashboard`, `Finance_05_Invoice_List`, `Finance_06_GST_TDS_Detail`, `Finance_09_Bank_Reconciliation`, `Finance_10_Dispute_Detail`, `Finance_12_Payment_History`. Prompt 06 remains in scope and is no longer a manual-generation blocker from this run. |
| Developer / Project Team | Submitted to Stitch; MCP timed out | Visual QA pending | Full 8-screen bundle submitted: loading, project list, inventory, offers, collateral list, visit slot management, visit outcome detail, project performance. |
| CP Owner / Org Leader | Submitted to Stitch; MCP timed out | Visual QA pending | Full 11-screen bundle submitted: loading, firm profile, employee detail, visits, booking status, disputes, support, firm dashboard, project leaderboard, comparison, employee performance. |
| CP Employee / Agent | Submitted to Stitch; MCP timed out | Visual QA pending | Full 11-screen bundle submitted: loading, project detail, lead list/detail, follow-ups, visits, profile/settings, personal dashboard, leaderboard, comparison, self performance. |
| CP Telecaller | Submitted to Stitch; MCP timed out | Visual QA pending | Full 12-screen bundle submitted: loading, empty queue, full lead detail, call history, follow-ups, visit schedule, escalation detail, performance, dashboard, call detail, comparison, leaderboard. |
| Buyer / Customer | Submitted to Stitch; MCP timed out | Visual QA pending | Full 8-screen lightweight buyer-link bundle submitted. Scope remains limited to shared project link, callback, visit, KYC, support, and error states; no full buyer portal was introduced. |
| Compliance / Support | Submitted to Stitch; MCP timed out | Visual QA pending | Full 7-screen bundle submitted: loading, dashboard, document list, dispute list, support ticket detail, SLA monitoring, audit log detail. |

### Final QA Status

Final cross-persona sign-off is **complete** as of 31/05/2026.

QA method:

1. Opened the Stitch UI canvas for project `16963605453633474186` in Chrome.
2. Extracted the visible Stitch canvas device titles from the loaded project UI.
3. Compared every `[NEW]` screen name in this Markdown file against visible Stitch screen titles.
4. Performed a visual canvas pass at zoomed-out project level to confirm the generated mobile screens render as grouped Android frames and use the CP Tech Digital visual system.
5. Checked the visible project text for disallowed scope terms: AI scoring, AI calling, CP microsites, and full buyer portal.

QA result:

| Check | Result |
|---|---|
| Required `[NEW]` screens in spec | 112 |
| Required `[NEW]` screens present by exact title in Stitch | 112 |
| Missing required `[NEW]` screens | 0 |
| Visible device frames in Stitch canvas | 186 |
| Unique visible device titles in Stitch canvas | 177 |
| Restricted-scope text hits | 0 |

Note: the canvas contains duplicate device frames from earlier timed-out/recovered generations. These were not deleted because the instruction was not to modify or delete existing screens. Required exact-title screens are present and can be used as the authoritative handoff set.

### Canvas Presentation Cleanup - 31/05/2026

User request: remove duplicate generated frames where safe, arrange the Stitch canvas horizontally by persona journey, and add decision-maker-readable persona headings.

Execution result:

| Cleanup Item | Status | Evidence / Notes |
|---|---|---|
| Duplicate removal / decluttering | Partially complete | The signed-in Stitch UI agent accepted the cleanup instruction and reported that duplicate device frames and legacy human-readable duplicate screens were removed while retaining authoritative versions. |
| Persona row arrangement | Partially complete | `get_project` now shows device frames distributed across distinct row bands, including row y-positions around `2899`, `4039`, `5527`, `6994`, `8278`, `10569`, `13620`, `14965`, `17255`, `19158`, `21638`, `23288`, `27632`, and `29067`. This is materially cleaner than the earlier clustered/timed-out canvas. |
| Decision-maker headings | Incomplete | Stitch generated `Heading 1` through `Heading 12`, but placed the heading frames together in a separate bottom row near `y=32026` instead of attaching each heading above its persona row. |
| Reference area | Partially complete | Stitch reported that design/reference assets were consolidated into a reference area. Visual QA still needs a final human check after heading placement is fixed. |
| Final presentation readiness | Not yet complete | The canvas is cleaner, but not yet decision-maker-ready because persona headings are not positioned beside their journeys. |

Manual follow-up required in Stitch:

1. Move `Heading 1` through `Heading 12` from the bottom heading row to the top/left of the matching persona rows.
2. Ensure the rows are ordered for review as: Shared App Foundation, Justo Leadership, CP Sourcing Head, RM / Sourcing Employee, Sales / Admin Ops, Finance, Developer / Project Team, CP Owner / Org Leader, CP Employee / Agent, CP Telecaller, Buyer / Customer, Compliance / Support.
3. After heading placement, run one visual scan at 5-8% zoom and confirm no row overlaps, no duplicate rows are visible, and exact-title authoritative screens remain in the intended journey rows.

Constraint note: the currently exposed Stitch MCP tools support project/screen reads, screen generation, variants, screen edits, and design system application. They do not expose a direct screen-instance delete or canvas-coordinate update mutation. Canvas cleanup was therefore executed through the signed-in Stitch UI agent. The UI agent completed decluttering and row grouping, but did not reliably accept the targeted follow-up command to reposition only the heading frames.

### Persona Sign-Off

| Persona / Bundle | Required New Screens | Exact Title Presence | Visual QA | Sign-Off |
|---|---:|---|---|---|
| Shared App Foundation | 7 | 7/7 | Pass | Complete |
| Justo Leadership | 12 | 12/12 | Pass | Complete |
| CP Sourcing Head | 11 | 11/11 | Pass | Complete |
| RM / Sourcing Employee | 11 | 11/11 | Pass | Complete |
| Sales / Admin Ops | 7 | 7/7 | Pass | Complete |
| Finance | 7 | 7/7 | Pass | Complete |
| Developer / Project Team | 8 | 8/8 | Pass | Complete |
| CP Owner / Org Leader | 11 | 11/11 | Pass | Complete |
| CP Employee / Agent | 11 | 11/11 | Pass | Complete |
| CP Telecaller | 12 | 12/12 | Pass | Complete |
| Buyer / Customer | 8 | 8/8 | Pass | Complete |
| Compliance / Support | 7 | 7/7 | Pass | Complete |

---

## Next Steps

1. Complete the manual Stitch heading placement noted in `Canvas Presentation Cleanup - 31/05/2026`.
2. Use the exact-title screens listed in this file as the authoritative design handoff set.
3. Ignore duplicate non-authoritative generated frames unless a designer explicitly chooses to reuse them.
4. Proceed to persona-wise UI review / product walkthrough before PRD-to-engineering decomposition after the heading row cleanup is complete.
5. Keep gamification / leaderboard screens in scope for Leadership, Sourcing, RM, CP Owner, CP Employee, and Telecaller. Keep scoring transparent and auditable; do not add unrelated AI scoring, CP microsites, or workforce tracking outside scheduled visit proof.
