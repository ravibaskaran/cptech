# Google Stitch UI Screen Prompts: Justo CP App

Draft version: v0.1
Date: 2026-05-31
Prepared for: Justo Realfintech
Primary inputs: `Justo_CP_App_BRD_Draft.md` v0.4, `Justo_CP_App_PRD.md` v0.3, `Justo_CP_App_Journey_Maps.md` v0.3, and Stitch project `16963605453633474186`
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
| 01 | Shared App Foundation | `16963605453633474186` | MCP attempted; manual re-run recommended | MCP returned screen IDs `d6d94aa2ea564f0cb3e5d6df0816fa9d` and `a5ce03eab7c54be7b29217d30c7f7351`, but the user could not see generated screens in the Stitch project UI. |
| 02 | Justo Leadership | `16963605453633474186` | MCP attempted; manual re-run recommended | MCP returned screen IDs `0ee4c20b6be84f11a3054e288ccede6e` and `f996d1af51b147e3ad50c3b1ec1f62be`, but project UI visibility was not confirmed. |
| 03 | CP Sourcing Head | `16963605453633474186` | Not generated | User stopped MCP flow before completion; run manually in Stitch. |
| 04 | RM / Sourcing Employee | `16963605453633474186` | Pending generation | Pending |
| 05 | Sales / Admin Ops | `16963605453633474186` | Pending generation | Pending |
| 06 | Finance | `16963605453633474186` | Pending generation | Pending |
| 07 | Developer / Project Team | `16963605453633474186` | Pending generation | Pending |
| 08 | CP Owner / Org Leader | `16963605453633474186` | Pending generation | Pending |
| 09 | CP Employee / Agent | `16963605453633474186` | Pending generation | Pending |
| 10 | CP Telecaller | `16963605453633474186` | Pending generation | Pending |
| 11 | Buyer / Customer | `16963605453633474186` | Pending generation | Pending |
| 12 | Compliance / Support | `16963605453633474186` | Pending generation | Pending |
