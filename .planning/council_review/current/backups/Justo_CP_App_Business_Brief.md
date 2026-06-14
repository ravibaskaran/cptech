# Justo CP App Business Brief

Date: 2026-05-30  
Scope: CP app strategy for Justo's move toward becoming a large regional channel partner in Maharashtra, later extensible across India.

## 1. Evidence Base And Confidence

- [high] Local documents reviewed: `docs/Manthan Proposal IndexNine.docx`, Project Manthan Phase 1/2/2.4/3 SoWs, and vendor proposals from Auum, TSPL/Triazine, and I9/Indexnine.
- [high] External research used: MahaRERA agent guidance, RERA broker compliance articles, and current Indian CP/broker technology products including Hookfish, DealALead, Broker365, Relmo, Zakeli, Leadvio, Qvoo, PropStackX, LeadCall, CoClose, and related CP/broker platforms.
- [moderate] This brief maps vendor gaps against the written proposals only. A vendor may be able to implement a gap if explicitly contracted, but the gap is not materially specified in the submitted document.

Key external references:

- [MahaRERA guidance for agents](https://maharera.maharashtra.gov.in/guidance-for-agents)
- [Housing.com RERA guide for real estate agents](https://housing.com/news/will-rera-impact-real-estate-agents/)
- [Housing.com common buyer problems with agents](https://housing.com/news/common-problems-home-buyers-face-with-real-estate-agents/)
- [Hookfish broker-developer platform](https://hookfish.in/)
- [DealALead B2B real estate network](https://www.dealalead.com/)
- [Broker365 Indian broker CRM](https://www.broker365.in/)
- [Relmo CP app/developer operating system](https://www.relmo.co/)
- [Leadvio real estate CRM](https://leadvio.in/)
- [Zakeli real estate CRM](https://zakeli.com/)
- [Qvoo real estate CRM](https://qvoo.io/)

## 2. Executive Brief

[high] Justo should treat the CP app as a CP operating system, not only as a mobile front end to Project Manthan. Manthan already covers CRM primitives: lead intake, lead scoring/routing, CP tagging, CP CRUD, CP portal, buyer portal, white-label portals, token/payment workflows, WhatsApp/SMS/email/CTI, KYC/payment integrations, site-visit workflows, dashboards, reports, and CP app extension scope.

[high] The unmet strategic layer is the full CP network lifecycle: CP sourcing, verification, activation, training, project enablement, lead ownership protection, site-visit proof, booking visibility, commission/payout transparency, performance management, renewal, and offboarding.

[high] To become a regional CP in Maharashtra, Justo needs three connected operating loops:

1. CP acquisition and enablement loop: source, verify, onboard, train, activate, and retain CP firms and their employees.
2. Transaction loop: project discovery, lead capture, lead lock, customer engagement, site visit, booking, documents, invoicing, payout.
3. Trust loop: transparent inventory, auditable lead ownership, RERA/KYC/GST/bank compliance, payout ledger, dispute resolution, and performance scoring.

[moderate] The strongest written vendor fit for Manthan extension is I9 because it directly builds on existing Manthan modules and data assumptions. The broadest CP operating-system vision is Auum. TSPL is the most AI-forward but least granular on Justo-specific lifecycle and Manthan integration.

## 3. Manthan Baseline

[high] Manthan's original proposal describes a broad real estate CRM covering lead management, qualification, sales pipeline tracking, inventory, project onboarding, marketing, billing/accounting, sourcing, corporate/developer/customer tech, and CP management.

[high] Manthan's proposed CP Tech module includes CP onboarding, leads, visits, conflict management, bookings, invoicing, collaterals, branded collaterals, broadcasting, and incentive plans across web and mobile interfaces.

[high] Phase 1 delivered platform scaffolding, RBAC/user management, lead CRUD/scoring, communication channels, lead-gen connectors, CP tagging/CRUD APIs, audit logs, import/export, smart lists, tasks, notifications, and J Verse/site-visit integration hooks.

[high] Phase 2 delivered or scoped portal management, white-label configuration, CP CRUD/RBAC/approval, CP referral links and QR codes, referral codes, CP portal login/registration/profile/dashboard/lead management, buyer portal, KYC/payment/token allocation, CP employee provisioning, Decentro/CIBIL/Zoho/KYC integrations, CP import/export, travel desk/pickup workflows, and AI chatbot support.

[high] Phase 2.4 added EOI dashboard, token selection/purchase, order summary, drip campaign filters, offline payment workflow, and WhatsApp integration.

[high] Phase 3 strengthened dashboards/reports, bulk actions, auto-dialer integration, custom fields, workflow management, walk-in experience, lead/contact/deal operations, smart lists, reassignment/share/clone/import/export, bulk marketing, and activity logs.

[high] The I9 CP Tech proposal dated 06-Apr-2026 frames the CP mobile app as React Native mobile only, with existing modules plus new additions: advanced auth, global dashboard, advanced funnel, KHOJ integration, AI data pipelines, AI voice agent, automated brokerage, Meta/Google campaign management, geofenced QR site verification, nudge engine, and advanced reporting.

## 4. Personas And Lifecycle

### 4.1 Persona Map

| Persona | Primary Goal | App Responsibilities | Outside-App Responsibilities |
|---|---|---|---|
| Justo leadership | Scale CP-led sales and regional distribution | Review dashboards, conversion, CP productivity, payout exposure, regional growth | Vendor governance, commercial strategy, CP policy, market expansion |
| Justo CP sourcing head | Build and manage CP network | Approve CPs, monitor sourcing funnel, assign RMs, review activation and attrition | Recruit CP firms, negotiate commercials, resolve escalations |
| Justo RM/sourcing employee | Activate CPs and drive output | Add CP prospects, verify documents, map CPs to projects, track visits, follow up on inactive CPs | Field meetings, relationship management, developer/CP coordination |
| Justo sales/admin ops | Run operational workflows | Configure projects, inventory, token/payment flow, role access, campaigns, notifications | Internal SOP, data correction, operational exception handling |
| Justo finance | Control invoices and payouts | Validate booking, approve CP invoice, track GST/TDS/payment status, reconcile ledger | Tally/accounting, bank payments, dispute resolution |
| Developer/project team | Provide sellable inventory and project updates | Publish project details, collateral, inventory, pricing, offers, site visit slots | Site readiness, sales desk operations, project approvals |
| CP owner/org leader | Grow brokerage revenue with Justo | Register firm, add employees, access inventory, assign leads, track bookings and payouts | Manage agency team, customer relationships, local marketing |
| CP employee/agent | Convert customers | Browse projects, share collaterals, add leads, schedule visits, update stages, view assigned leads | Customer calls, WhatsApp follow-ups, site visits, negotiation |
| CP telecaller | Qualify and nurture leads | Work lead queue, disposition calls, schedule follow-ups/site visits | Calling activity, WhatsApp/email follow-up |
| Buyer/customer | Evaluate and buy property | Receive links, complete KYC/payment, confirm site visit, see project details where exposed | Physical visit, document signing, payment decisions |
| Compliance/support | Reduce regulatory and service risk | Check RERA/KYC/GST/bank docs, audit logs, consent, complaints | Legal review, escalation handling, regulatory response |

### 4.2 Justo CP Sourcing Lifecycle

1. Identify target micro-market and CP segment. [moderate] Priority segmentation should include micro-market, developer/project specialization, price-band fit, historical sales, RERA status, digital maturity, and existing team size.
2. Source CP candidates. [moderate] Sources include referrals, broker associations, developer introductions, digital campaigns, site-event walk-ins, and competitor CP networks.
3. Capture prospect CP record. [high] Required fields should include firm identity, owner, RERA registration, GST/PAN, bank details, address, team size, locations served, project/category focus, and documents.
4. Verify and approve. [high] Maharashtra real estate agents must register with MahaRERA before facilitating sale/purchase/advertising/brokerage for registered projects, so RERA validation should be a first-class workflow.
5. Contract and commercial setup. [moderate] Configure brokerage slabs, incentive plans, payout milestones, clawback rules, lead-lock expiry, conflict rules, and data/privacy terms.
6. Map CP to Justo structure. [high] CP should be mapped to RM, region/cluster, project access, inventory visibility, campaign permissions, and employee seats.
7. Enable and train. [moderate] Provide project pitch packs, RERA-compliant collateral, inventory/pricing, objection handling, WhatsApp share kits, site-visit SOPs, and CP Academy content.
8. Activate. [high] Activation should be measured by first login, first employee added, first project viewed/shared, first lead submitted, first site visit, first booking, and first payout.
9. Manage performance. [high] Track lead-to-visit, visit-to-booking, duplicate/conflict rate, response time, inactive leads, cancellation rate, payout status, and CP satisfaction.
10. Retain, upgrade, suspend, or offboard. [moderate] Renewal/retention should use performance bands, compliance status, payout disputes, and RM feedback.

### 4.3 CP Firm Lifecycle

1. Discover Justo opportunity.
2. Register firm and owner.
3. Submit RERA/GST/PAN/bank/KYC documents.
4. Receive approval or rejection with reason.
5. Sign terms and commercial plan.
6. Configure profile, brand, employees, and permissions.
7. Access project catalog, inventory, offers, and collaterals.
8. Submit/lock leads.
9. Schedule and prove site visits.
10. Track lead movement, booking, payment, documents, commission, and payout.
11. Raise disputes or support tickets.
12. Renew, expand to more projects/regions, or offboard.

### 4.4 CP Employee Lifecycle

1. CP owner invites employee or imports users.
2. Employee verifies phone/email and completes profile.
3. CP owner assigns role: owner/admin/manager/agent/telecaller/finance observer.
4. Justo or CP owner assigns project/region/lead access.
5. Employee completes mandatory training and compliance acknowledgement.
6. Employee handles leads, calls, site visits, documents, and follow-ups.
7. App tracks response time, activity, conversion, site visits, and bookings.
8. CP owner reallocates leads when employee is inactive or exits.
9. Employee is deactivated; audit trail and lead ownership stay intact.

## 5. CP Pain Points In India

| Pain Point | Evidence/Reason | Technology Opportunity |
|---|---|---|
| Stale or fake inventory | [moderate] Current broker-tech products market "verified inventory" and "real-time price lists" because inventory trust is a recurring broker problem. | Live inventory, price/version stamping, developer-approved collateral, expiry warnings |
| Lead ownership disputes | [high] Manthan and vendor proposals repeatedly include conflict management, duplicate detection, lead locking, and audit trails. | Lead lock, duplicate detection, cooling-off windows, ownership ledger, dispute queue |
| Commission uncertainty and delayed payouts | [high] Broker-focused products emphasize commission tracking, payout ledgers, and no commission disputes. | Booking-linked payout ledger, invoice status, GST/TDS support, SLA timers, payout notifications |
| Fragmented communication | [high] Manthan already scopes CTI, WhatsApp, SMS, email, templates, notifications, and call logs. | Unified communication timeline, consent capture, call recording link, WhatsApp-first workflows |
| Compliance confusion | [high] MahaRERA requires real estate agent registration before acting in sale/purchase/advertising/brokerage for registered projects. Housing.com also notes penalties and documentation/account obligations. | RERA validation, renewal reminders, document vault, compliance checklist, audit-ready logs |
| Low lead quality and follow-up leakage | [moderate] Broker CRMs market lead inboxes, smart routing, follow-up reminders, and site-visit tracking as core value. | Lead scoring, AI summaries, follow-up nudges, stale-lead rescue, telecaller queues |
| CP employee management is weak | [high] Manthan Phase 2 only scopes CP employee provisioning; broader employee lifecycle, targets, permissions, attrition, and reassignment need explicit design. | CP org hierarchy, seat control, role permissions, target dashboards, exit workflow |
| Marketing ROI is opaque | [moderate] Auum and I9 both propose campaign/source attribution and Meta/Google campaign management. | Campaign budget, referral links, source ROI, CP-branded microsites, attribution ledger |
| Site-visit proof is weak | [high] I9 proposes geofencing and QR handshake; Auum proposes QR/OTP visitor check-in and visit logs. | QR/OTP check-in, geofence, visit outcome, buyer feedback, visit-to-booking analytics |
| Trust deficit with buyers | [moderate] Public buyer-facing commentary around brokers often centers on hidden charges, poor transparency, misleading claims, poor communication, and legal/document issues. | RERA-compliant collateral, transparent fee disclosures, project factsheet, audit trail |

## 6. Technology Landscape And Gaps

### 6.1 Current Technology Categories

- Horizontal CRMs adapted to real estate. [moderate] Tools such as LeadSquared/Sell.Do-type systems are strong for pipeline and marketing automation but often require real-estate-specific customisation for CP commissions, inventory, site visits, and brokerage splits.
- Broker-first CRMs. [moderate] Products such as Broker365, Zakeli, Qvoo, Realit, XceedCRM, Leadvio, and LeadCall focus on lead capture, inventory, WhatsApp follow-up, site visits, pipeline, team performance, and commissions.
- B2B broker-developer networks. [moderate] Hookfish, DealALead, Klozit, CoClose, and similar platforms position around verified inventory, broker onboarding, site visits, direct builder connection, and commission protection.
- Developer operating systems with CP tools. [moderate] Relmo, SQFT/SquareFeetConnect, PropStackX, and similar systems combine developer CRM, CP portal/app, homeowner/buyer touchpoints, inventory, payments, and reporting.

### 6.2 Unaddressed Gaps Across The Market

- [moderate] Many tools solve CP productivity, but fewer solve Justo's own CP sourcing engine: CP prospecting, RM field activity, CP activation funnels, CP attrition, and CP relationship health.
- [moderate] Most products show commission tracking, but payout proof needs integration with booking validation, finance approval, GST/TDS, invoice, Tally/accounting, and bank payment status.
- [moderate] Most CP apps do not make compliance a core daily workflow: RERA expiry, KYC recertification, consent logs, marketing-claim controls, and audit-ready evidence.
- [moderate] Lead locking often exists, but the operating rules are the product: duplicate matching, source priority, direct-vs-CP override, expiry, reassignment, dispute evidence, and escalation rights.
- [moderate] CP employee lifecycle is usually underbuilt: internal team hierarchy, lead allocation, sub-agent attribution, employee exit, reassignment, co-broking splits, and CP-owner controls.
- [moderate] Inventory trust is still fragmented unless the source is the developer/Manthan inventory system with price/version freshness, unit lock/token status, and collateral approval.

## 7. Technology Opportunity Map

| Business Need | Product Capability | Manthan Baseline | Gap To Specify |
|---|---|---|---|
| Recruit CPs at scale | CP prospect CRM, RM visit tracking, recruitment funnel | Sourcing Tech in proposal; RM tracking proposed | No detailed CP sourcing prospect lifecycle in vendor CP proposals |
| Approve only eligible CPs | RERA/GST/PAN/bank/KYC workflow | CP approval, KYC integrations exist in Manthan | RERA validation, renewal alerts, rejection reasons, compliance audit |
| Activate CPs quickly | Guided onboarding, CP Academy, first-action checklist | CP portal/app, training docs | No structured activation funnel or learning workflow |
| Protect CP effort | Lead lock, duplicate detection, conflict management | Manthan CP conflict management; I9/Auum lead lock | Need explicit ownership rules, expiry, cooling-off, appeals |
| Convert leads | Mobile lead entry, WhatsApp/call, site visits, nudges | Strong Manthan communication and lead modules | Need CP-first UX, offline/low-connectivity, employee queueing |
| Prove site visits | QR/OTP, geofence, site logs, buyer feedback | I9 geofence/QR; Auum QR/OTP | Need operational SOP and dispute linkage |
| Build CP trust | Payout ledger, invoice, commission SLA | CP invoicing/payments in Manthan proposal; I9/Auum/TSPL include commission | Need finance integration, GST/TDS, milestone rules, payout proof |
| Grow Justo's network | CP scoring, RM dashboards, regional heatmaps | Dashboards and CP performance proposed | Need sourcing analytics and CP health score |
| Reduce buyer risk | Approved collateral, RERA factsheets, promise control | Collateral repository/branded collateral | Need claim governance and buyer-visible transparency |

## 8. Vendor Proposal Mapping

### 8.1 Summary Comparison

| Dimension | Auum | TSPL/Triazine | I9/Indexnine |
|---|---|---|---|
| Strategic fit | [moderate] Broad CP OS vision with CP mobile app, project/inventory, lead CRM, lead lock, site visits, communications, AI assistant, microsites, marketing, commission, workforce tools | [moderate] AI-enabled CP platform with lead, site visit, AI calling, CP performance, commission, analytics | [high] Direct extension of Project Manthan and existing modules |
| Manthan integration certainty | [moderate] Mentions connecting to existing CRM/CP admin | [low] Generic integration statement; no Manthan-specific module mapping | [high] Built on existing Manthan scope and names existing modules |
| CP app depth | [high] Mobile app, project discovery, leads, bookings, CP branding, AI assistant | [moderate] Mobile app and dashboards listed, but less granular | [high] Mobile app with auth, dashboard, funnel, brokerage, campaigns, geofence, AI |
| CP sourcing/RM lifecycle | [moderate] Has team/workforce geo tracking in Phase 2 | [low] Not materially specified | [low] Not materially specified beyond CP/user onboarding |
| CP employee lifecycle | [moderate] Team hierarchy and RBAC in Phase 2 | [moderate] Broker/agent persona exists | [moderate] Org leader vs individual CP RBAC; CP users already exist in Manthan |
| Lead ownership/conflict | [high] Lead locking, direct-vs-CP identification, duplicate detection, audit trail | [moderate] Assignment and lifecycle tracking, but conflict rules not detailed | [high] Existing conflict management plus advanced funnel |
| Site-visit proof | [high] QR/OTP check-in, visit logs, feedback | [moderate] scheduling and visit-to-booking tracking | [high] geofencing and QR handshake |
| Commission/payout | [high] Phase 2 brokerage, GST invoice, payout lifecycle | [high] commission/incentive engine with finance approval | [high] automated brokerage, GST invoice, slab calculation, payout tracking |
| AI | [high] Agentic AI assistant "Shanaya", voice/text actions, campaign builder | [high] AI voice calling, transcript processing, lead scoring | [high] KHOJ, AI pipelines, Gemini, AI voice agent |
| Commercials | [high] INR 1.45419 crore total, Phase 1 INR 65 lakh, Phase 2 INR 80.419 lakh | [high] INR 1.8 crore plus taxes, 8-9 months | [high] INR 73.58 lakh plus GST, 6 weeks, support extra |
| Key risk | [moderate] Larger new platform and IP/licensing constraints may create integration and ownership risk | [moderate] AI-heavy and generic scope may under-specify operational details | [moderate] Fast timeline and Manthan dependence may underbuild differentiated CP network product |

### 8.2 Auum Gaps

- [high] Auum's proposal is feature-rich, but several strategic functions are deferred to Phase 2: brokerage/commission, workforce geo tracking, CP microsites, marketing automation, telephony/call intelligence, and advanced analytics.
- [moderate] CP sourcing lifecycle is not explicit: CP prospecting, RM recruitment funnel, CP activation funnel, CP health score, CP retention, and offboarding need scope language.
- [moderate] The proposal says CP registration connects to existing CRM, but detailed Manthan data model/API dependency, migration, ownership of source of truth, and failure handling are not specified.
- [moderate] Compliance workflow is limited to security/KYC data handling references; RERA registration validation/renewal, claim governance, CP document expiry, and compliance audit are not explicit.
- [moderate] IP terms provide a usage license after payment while proprietary frameworks/prebuilt modules/AI datasets remain Auum property. This needs legal review if Justo wants long-term platform control.

### 8.3 TSPL/Triazine Gaps

- [high] TSPL provides the least granular functional backlog among the three vendor proposals.
- [moderate] The proposal is heavily centered on AI voice calling and microservices architecture, but under-specifies CP sourcing, CP onboarding detail, CP employee lifecycle, lead conflict rules, document workflows, Manthan integration, and finance/accounting integration.
- [moderate] Multi-tenant SaaS and offline-capable design are positioned as architecture principles, but the proposal does not explain how these fit the existing Manthan single-tenant assumptions.
- [moderate] The proposal lists dashboards and services but not detailed acceptance criteria for CP trust workflows: lead ownership, site-visit proof, payout SLA, invoice lifecycle, RERA validation, and dispute resolution.
- [moderate] The cost is the highest single proposal at INR 1.8 crore plus taxes, with 8-9 month delivery, so Justo should require a much more detailed backlog before treating it as comparable to I9 or Auum.

### 8.4 I9/Indexnine Gaps

- [high] I9 has the strongest continuity with Manthan and the lowest integration ambiguity because it explicitly references existing modules and adds CP app scope over them.
- [moderate] The CP app proposal assumes a fast-tracked 6-week delivery. That timeline is risky for deep CP persona work, field validation, CP owner/employee workflows, and differentiated CP network design unless the scope remains narrow.
- [high] I9's proposal assumes single tenancy and no white-labeling/multi-tenancy at platform layer. This is acceptable if the app is Justo-owned, but it is a constraint if Justo later wants to operate multiple brands, projects, regions, or partner ecosystems with strict tenant isolation.
- [moderate] CP sourcing and RM lifecycle are not materially specified in the CP app proposal, despite being central to Justo's goal of becoming a regional CP.
- [moderate] Compliance workflows beyond KYC/GST invoice support are not explicit: RERA registration, renewal, advertising-claim governance, CP document expiry, and audit evidence need to be added.
- [moderate] CP employee lifecycle is only partially covered through RBAC/org leader vs individual CP and existing CP users; employee invitation, activation, reassignment on exit, sub-agent performance, and internal split attribution need explicit design.

## 9. Recommended Product Definition

### 9.1 MVP For Maharashtra Regional CP Play

[high] MVP should prioritize trust, activation, and transaction completion over broad AI features.

1. CP firm onboarding: RERA, GST, PAN, bank, KYC, agreement, approval/rejection, renewal reminders.
2. CP employee management: invite, role, project access, active/inactive, lead reassignment, employee performance.
3. Project catalog: approved projects, inventory, pricing/offers, RERA details, collateral, share kits, version freshness.
4. Lead submission and lock: phone dedupe, ownership rules, direct-vs-CP conflict, expiry, dispute workflow.
5. Site visit workflow: schedule, QR/OTP/geofence proof, buyer feedback, site desk outcome, visit-to-booking conversion.
6. Communication timeline: WhatsApp/SMS/email/call log, follow-up reminders, templates, consent.
7. Booking visibility: lead stage, token/payment, KYC/documents, unit status, next action.
8. Commission/payout ledger: slab, invoice, GST/TDS, validation, approval, payment status, SLA timer.
9. Justo sourcing/RM dashboard: CP prospect funnel, onboarding ageing, activation metrics, CP health score, regional heatmap.
10. Admin and audit: RBAC, audit logs, export, support tickets, compliance exceptions.

### 9.2 Differentiators Beyond Standard CP Apps

- [moderate] CP trust score: combines compliance, lead quality, response time, visit conversion, cancellation, dispute rate, and payout history.
- [moderate] Payout promise: visible payout SLA and milestone explanation for every booking.
- [moderate] Inventory freshness badge: every unit/price/collateral item carries last-updated and source-of-truth metadata from Manthan.
- [moderate] CP Academy: project-specific training, pitch certification, objection-handling scripts, RERA-compliant claims.
- [moderate] Claim-safe collateral: CP can only share approved brochures, price sheets, offers, and WhatsApp creatives.
- [moderate] RM field productivity: RM visit logs, geotagged CP meetings, activation tasks, CP recruitment targets.
- [moderate] Dispute-grade evidence: ownership log, call/site-visit trail, buyer confirmation, CP employee attribution, finance approval.

## 10. Vendor Gap Checklist To Use Before Selection

Ask every vendor to respond in writing to these items:

1. [high] Which system is the source of truth for CP, CP employee, lead, project, inventory, booking, invoice, and payout?
2. [high] How will the CP app integrate with current Manthan APIs/data models?
3. [high] What exact lead-lock/conflict rules are included, including duplicate matching, expiry, override, and audit?
4. [high] How are RERA registration, renewal, GST/PAN/bank verification, and document expiry handled?
5. [high] What is the CP owner vs CP employee permission model?
6. [high] What happens when a CP employee exits while holding active leads?
7. [high] How are site visits proven and connected to commission eligibility?
8. [high] How does payout tracking connect to booking validation, invoice, GST/TDS, Tally/accounting, and payment status?
9. [high] What offline/low-connectivity behavior is supported on Android/iOS?
10. [high] What App Store/Play Store, device, notification, and release-management responsibilities are included?
11. [high] What production support, incident SLA, analytics, audit, and data-export guarantees are included?
12. [high] Who owns source code, generated designs, AI prompts/workflows, models, and reusable platform components?

## 11. Recommended Vendor Position

[moderate] If Justo wants the fastest path to a CP app on top of Manthan, I9 should be the baseline vendor because it owns or understands the current Manthan implementation and has already scoped the mobile extension.

[moderate] If Justo wants a larger CP operating system and can absorb platform/integration risk, Auum has the richest written product vision, especially CP branding, AI assistant, microsites, marketing, workforce intelligence, and analytics.

[moderate] TSPL should not be selected from the current proposal alone unless it submits a more granular backlog. Its AI voice platform concept is useful, but the current proposal is too generic for Justo's CP lifecycle and Manthan integration risk.

[high] Regardless of vendor, Justo should add a CP Network Lifecycle annexure to the SoW. The current proposals cover app features, but Justo's business goal depends on network acquisition, CP trust, lead ownership, compliance, payout transparency, and RM productivity.

## 12. Immediate Next Steps

1. [high] Convert this brief into an SoW annexure with acceptance criteria for the CP lifecycle, not just feature names.
2. [high] Run 8-12 CP interviews in Maharashtra: 3 large CP firms, 3 mid-size CPs, 2 independent brokers, 2 CP employees/telecallers, and 2 Justo RMs/sourcing employees.
3. [high] Ask I9, Auum, and TSPL to fill the same gap checklist in section 10.
4. [high] Create a scorecard with weights: Manthan integration 25%, CP lifecycle depth 25%, lead/payout trust 20%, delivery risk 15%, commercial/IP/support 15%.
5. [moderate] Build the MVP first around onboarding, lead lock, inventory, site visit, booking visibility, and payout ledger; treat AI voice/campaign automation as second-wave capabilities unless they directly improve activation or conversion.
