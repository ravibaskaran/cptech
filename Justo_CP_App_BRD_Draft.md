# Business Requirements Document: Justo CP App

Draft version: v0.4
Date: 2026-05-31  
Prepared for: Justo Realfintech  
Artifact sequence: BRD -> PRD -> Persona-wise Journey Maps -> Google Stitch UI Screen Specs/Prototype

## 1. Executive Summary

Justo wants to become a large retail/channel partner player in Maharashtra first and later expand across India. The CP app is a strategic instrument for that ambition, but only if it is scoped as a CP operating system and not merely as a mobile lead-entry extension to Project Manthan.

Launching Android and iOS apps is not the business outcome. The business outcome is whether Maharashtra CPs give Justo more qualified leads, more verified visits, more bookings, and more repeat engagement because Justo is easier, safer, and more financially transparent to work with than competing developer or CP networks.

The business will succeed if Justo solves the trust and operating-friction problems that make CPs disengage today: uncertain inventory, lead ownership disputes, weak site-visit proof, opaque payout timelines, poor CP employee control, fragmented communication, and limited visibility into what happens after a lead is submitted. The business will fail if the app becomes another generic CRM surface that asks CPs to enter data without giving them faster access to inventory, stronger claim protection, clearer payouts, and practical selling support.

Project Manthan already provides a meaningful CRM foundation: leads, CP tagging, CP CRUD, CP portal, buyer portal, token/payment workflows, communication channels, KYC/payment integrations, dashboards, reports, workflows, and site-visit adjacency. The missing layer is not basic CRM. The missing layer is a full CP network lifecycle: CP sourcing, verification, activation, employee management, project enablement, lead ownership, site-visit proof, booking visibility, commission transparency, dispute handling, performance management, renewal, and offboarding.

The vendor proposals show three different paths:

- **I9/Indexnine** is the strongest Manthan-continuity option because its CP app proposal explicitly references existing Manthan modules, existing covered scope, and new CP mobile additions. Its risk is that a fast-tracked six-week delivery can underbuild the deeper CP lifecycle that Justo needs to win.
- **Auum** has the broadest CP operating-system product vision: CP mobile app, project/inventory, lead CRM, lead locking, site visits, communication, AI assistant, microsites, workforce tools, commission, telephony, analytics, and marketing automation. Its risk is platform/integration/IP complexity and the fact that several trust-critical features sit outside its first delivery tranche.
- **TSPL/Triazine** has the strongest AI-calling narrative and a broad microservices architecture. Its risk is that the proposal is materially less granular on Justo-specific CP sourcing, Manthan integration, lead conflict rules, CP employee lifecycle, compliance, and payout operations.

## Scope Gatekeeper Addendum: Launch MVP Boundary

The launch MVP objective is narrower than the full CP operating-system vision: prove that a controlled Maharashtra CP pilot can trust Justo for the core transaction loop from CP onboarding to project access, lead protection, site-visit proof, booking visibility, and payout status. Anything that does not directly improve this trust loop should be excluded from launch planning unless it is already available in Manthan with near-zero incremental build.

### Launch MVP Must Prove

| Launch Proof Point | Required Outcome |
|---|---|
| Verified CP can start working | CP firm and CP employees can be onboarded, approved, assigned projects, and activated. |
| CP can sell from current information | CP users can view current assigned projects and share only approved collateral. |
| CP can protect a lead | CP users can submit a lead and receive accepted, conflict, rejected, or pending-sync status with reason and next action. |
| Justo can verify a visit | CP/RM/site users can schedule and confirm site visits with launch-approved proof. |
| CP can see transaction progress | CP owner can see CP-safe booking milestones and payout status without calling RM/finance for every update. |
| Justo can control risk | Admin, support, compliance, and finance users can audit lead, visit, collateral, compliance, and payout decisions. |

### Launch MVP Cuts

| Cut From Launch | Keep For Later Only If |
|---|---|
| AI voice calling, AI assistant, KHOJ/Gemini workflows, AI campaign generation | Core lead, visit, and payout workflows are stable and measurable. |
| CP microsites and CP-branded public pages | Leadership explicitly funds a marketing-distribution workstream after the trust loop works. |
| Advanced telecaller queue, call intelligence, sentiment, and automated scoring | Manual follow-up timeline and basic dispositions are already adopted. |
| Advanced analytics, CP health scoring, gamification, and loyalty | Basic KPI reporting proves reliable source data. |
| Workforce geo-tracking outside site-visit proof | Legal/HR review approves location capture beyond a buyer visit context. |
| Multi-tenant/white-label platform architecture | Justo first proves its own CP network operating model. |
| Full buyer portal expansion | Existing buyer portal can be linked safely; buyer-facing CP app scope stays limited to approved project links and visit confirmation. |

### Launch Differentiators With Guardrails

These capabilities are core differentiators and must remain in scope, but they need strict guardrails so they do not become uncontrolled engineering surfaces.

| Differentiator | Why It Stays In Scope | Guardrails |
|---|---|---|
| Geofenced site-visit proof | Strengthens visit attribution and reduces manual dispute handling | Capture only during scheduled/active visit windows, require role permission and device consent, store timestamp/accuracy/proof method, support QR/OTP/site-desk/admin fallback, avoid continuous employee tracking. |
| Queued document uploads | Field onboarding breaks when network is poor; queued uploads reduce RM/CP friction | Restrict file type/size, show upload queue state, encrypt local files, retry/resume safely, allow cancel/delete before sync, virus/malware scan server-side where available, never mark compliance complete until server validation succeeds. |
| Full payout processing | Payout transparency is a loyalty differentiator only if finance can act inside the workflow | Use a finance-controlled state machine, maker-checker approval, GST/TDS fields, invoice validation, payment reference, reconciliation state, clawback/dispute states, and full audit trail. |

### Journey Map Readiness Gate

When journey maps are created, every persona step must pass this test: "Does this directly improve CP onboarding, project enablement, lead ownership, site-visit proof, booking visibility, payout transparency, or operational control?" If not, keep it as deferred context and do not turn it into a Google Stitch screen.

## 2. Business Thesis: Why This Can Win Or Fail

### 2.1 Why It Can Win

| Success Driver | Why It Matters | Product Implication |
|---|---|---|
| Justo can become the trusted operating layer between developers and CPs | CPs need reliable inventory, transparent lead ownership, and visible payouts | Make trust workflows first-class, not back-office exceptions |
| Manthan already contains core CRM primitives | Justo does not need to rebuild lead, portal, communication, and KYC foundations from zero | Reuse Manthan aggressively; extend only where CP lifecycle gaps exist |
| CPs are motivated by speed, certainty, and money | CP adoption follows practical value, not app novelty | Optimize for faster project discovery, protected leads, verified visits, payout visibility |
| Maharashtra has clear RERA compliance context | Compliance can become a trust signal if embedded into onboarding and collateral governance | Add RERA validation, renewal, claim-safe collateral, and audit-ready logs |
| Vendor competition gives leverage | Three proposals reveal overlapping capabilities and gaps | Use the BRD to force comparable SoW responses and reduce ambiguity |

### 2.2 Why It Can Fail

| Failure Mode | What It Looks Like | Mitigation |
|---|---|---|
| Generic CRM trap | CPs see another app for data entry, while they still work on WhatsApp and Excel | Build around CP job-to-be-done: inventory, lead lock, visit proof, booking visibility, payout |
| Trust gap remains unsolved | CPs submit leads but still do not trust ownership, booking status, or payout status | Require audit ledger, source-of-truth clarity, dispute workflow, payout SLA visibility |
| Manthan integration ambiguity | Vendor creates duplicate CP/project/lead/payout data instead of extending Manthan | Define system-of-record ownership before build |
| AI distraction | AI calling/campaign automation consumes budget before CP trust workflows are solved | Treat AI as v2 unless tied to activation, conversion, or follow-up rescue |
| CP employee lifecycle ignored | CP owner cannot control team access, lead attribution, employee exit, or sub-agent performance | Model CP firm as an organization with employees, roles, lead ownership, and deactivation |
| Compliance treated as uploads only | RERA/GST/PAN/KYC docs exist but are not validated, renewed, or used in governance | Add compliance lifecycle with expiry, exceptions, renewal, and audit trail |
| Field adoption ignored | RMs and CPs do not adopt because flows do not match field reality | Design for WhatsApp-first behavior, quick entry, reminders, low-friction mobile workflows |

## 3. Strategic Objectives

### 3.1 Primary Objective

Enable Justo to build, activate, and govern a scalable CP network in Maharashtra by giving CP firms, CP employees, Justo sourcing teams, and finance teams a trusted digital operating layer connected to Project Manthan.

### 3.2 Business Outcomes

- Increase number of active CP firms and active CP employees.
- Improve CP time-to-first-lead, time-to-first-site-visit, time-to-first-booking, and time-to-first-payout.
- Reduce lead ownership disputes and manual escalations.
- Improve site-visit verification and visit-to-booking traceability.
- Increase CP confidence in commission and payout timelines.
- Improve RM productivity in CP sourcing, activation, and performance management.
- Provide leadership with a city/cluster/CP-level operating dashboard.
- Establish a vendor-neutral capability baseline for PRD and SoW negotiation.

### 3.3 Success Metrics

| Metric | Definition | Business Signal |
|---|---|---|
| CP onboarding completion rate | Approved CPs completing all required onboarding steps | Onboarding friction |
| CP activation rate | Approved CPs completing first lead/site visit/booking milestone | Network quality |
| CP employee activation rate | Invited employees completing profile, training, and first activity | CP firm penetration |
| Lead acceptance rate | Submitted leads accepted without conflict | Data quality and CP trust |
| Lead conflict rate | Submitted leads entering conflict/dispute state | Ownership rules quality |
| Lead-to-site-visit conversion | CP leads converted into verified visits | Sales productivity |
| Site-visit-to-booking conversion | Verified visits converted into bookings | CP quality and project fit |
| Payout SLA adherence | Eligible payouts paid within promised window | CP trust |
| RM activation productivity | CPs activated per RM per period | Sourcing efficiency |
| CP satisfaction | CP sentiment around inventory, lead ownership, support, payout | Retention predictor |

## 4. Evidence Base And Assumptions

### 4.1 Local Source Corpus

- `docs/Manthan Proposal IndexNine.docx`
- Manthan CRM SoWs dated 7 May, 10 Nov, 16 Feb, and 21 Jan.
- `docs/Auum Justo Proposal CP App.pdf`
- `docs/TSPL_Business_Proposal_Justo_AI_CP_Platform.pdf`
- `docs/CP tech proposal from I9.pdf`
- `Justo_CP_App_Business_Brief.md`
- `.planning/PROJECT.md`
- `.planning/REQUIREMENTS.md`
- `.planning/STATE.md`

### 4.2 External Market Evidence Used

- MahaRERA guidance confirms real estate agents need prior registration before dealing in sale/purchase, advertising, or brokerage for registered projects in Maharashtra.
- Current India-focused broker/CP CRM products market lead management, real-time inventory, WhatsApp automation, site-visit tracking, team performance, commission tracking, and payout visibility as core broker/CP pain points.
- CP/broker tooling sites such as Leadvio, Broker365, XceedCRM, Catination, MDoc, Klozit, SQFT/SquareFeetConnect, and DaeBuild repeatedly position lead capture, site visits, inventory, commission, team, and CP portal capabilities as market expectations.

### 4.3 Working Assumptions

- [high] Project Manthan remains the core CRM foundation.
- [high] The CP app must support Android and iOS.
- [high] Maharashtra is the initial launch market.
- [high] The BRD should be detailed enough to derive the PRD.
- [moderate] I9 is the likely lowest-friction extension path because it knows Manthan.
- [moderate] Auum has the broadest product vision but higher integration and IP ambiguity.
- [moderate] TSPL needs a more granular backlog before its proposal can be fairly compared.

## 5. Current Manthan Baseline

### 5.1 Manthan Capabilities Relevant To CP App

| Area | Existing/Scoped Manthan Capability | BRD Interpretation |
|---|---|---|
| Core platform | App scaffolding, authentication, RBAC, user/project/role association, audit logs | Reuse as platform base |
| Lead management | Lead CRUD, scoring, assignment, pipeline, smart lists, bulk edit/reassign, custom fields, activity logs | Extend for CP lead lock and conflict rules |
| Communication | Email, SMS, WhatsApp, CTI, call logs, templates, notifications | Reuse for CP/customer timeline |
| CP management | CP tagging, CP CRUD APIs, CP approval, CP portal, referral code/link/QR, CP employee provisioning | Extend into firm and employee lifecycle |
| Portal/payment | White-label portal, buyer portal, token selection, payment links, Razorpay, offline payment | Reuse for booking/payment visibility |
| KYC/document | Manual KYC upload, Decentro/CIBIL, Zoho Sign, booking documents | Extend into CP compliance and payout eligibility |
| Site visit | Site-visit hooks, walk-in experience, travel/pickup workflows | Extend into CP visit proof and commission eligibility |
| Inventory/project | Inventory status, project metadata, docs, offers/schemes, portal configuration | Convert into CP-friendly project catalog |
| Analytics | Dashboards, reports, productivity, MIS, CP performance/insights in proposal | Extend into CP health, RM productivity, payout SLA |
| AI | AI follow-up, AI calling bot, AI note-to-task, scoring, transcripts, WhatsApp/email content | Defer unless tied to high-value CP workflows |

### 5.2 Reuse / Configure / Extend / Add

| Capability | Treatment | Notes |
|---|---|---|
| Login/RBAC | Reuse/configure | Need CP owner, CP employee, RM, finance, admin role model |
| CP firm profile | Extend | Current CP CRUD is insufficient for lifecycle, compliance, activation |
| CP employee management | Extend | Need invitation, role, attribution, deactivation, reassignment |
| Lead capture | Reuse/extend | Add duplicate rules, ownership lock, CP employee attribution |
| Site visit | Extend | Add QR/OTP/geofence/site-desk/admin proof and outcome for launch with consent, fallback, and audit guardrails |
| Project catalog | Extend | CP-friendly discovery, share kits, inventory freshness, RERA facts |
| Payout | Add/extend | Need CP-visible ledger plus finance-controlled payout processing lifecycle |
| CP sourcing | Add/extend | Need prospect funnel, RM activity, and activation status for launch; advanced CP health scoring later |
| Compliance | Add/extend | RERA/GST/PAN/bank/KYC renewal and exception workflows |
| AI | Defer/optional | Use after trust workflows are stable |

## 6. Vendor Proposal Review

### 6.1 Summary

| Dimension | Auum | TSPL/Triazine | I9/Indexnine |
|---|---|---|---|
| Strategic posture | Broad CP operating system | AI-enabled CP platform | Manthan extension / CP mobile app |
| Proposal strength | Rich product modules and CP-first ideas | AI calling and modular architecture | Existing Manthan continuity |
| Core risk | Integration, IP, later-tranche dependency | Generic scope, high cost, lifecycle gaps | Six-week scope may be shallow |
| Commercial/timeline | INR 65L first tranche, INR 80.419L later tranche, total INR 1.45419Cr; 18 + 24 weeks indicated | INR 1.8Cr plus taxes; 8-9 months; significant recurring third-party costs | INR 73.58L plus GST; 6 weeks; support extra |

### 6.2 Auum

**What Auum covers well**

- CP mobile app for project discovery, lead submission, booking tracking, sales-team interaction, notifications, and activity tracking.
- Project/property management, project sharing, inventory, pricing, offers, media.
- Lead CRM, lead stages, activity timeline, lead source tracking.
- Lead locking and conflict prevention: direct-vs-CP identification, phone locking, duplicate detection, ownership management, audit trail.
- CP registration management integrated with existing CRM/CP admin, bulk CP import, RM assignment.
- Site visit digitization with scheduling, QR/OTP check-in, walk-in registration, visit logs, feedback.
- Agentic AI assistant for voice/text commands, creating leads, scheduling visits, updating status, audit logging.
- Later-tranche commission, workforce intelligence, RBAC, telecaller operations, marketing automation, microsites, telephony, analytics.

**Gaps to clarify**

- CP sourcing lifecycle is not explicit enough: prospecting, field acquisition, RM activation funnel, retention, suspension, offboarding.
- Manthan integration is stated but not specified at data ownership/API level.
- Several trust-critical features are outside the first tranche: brokerage/commission, team/geo tracking, telecaller operations, marketing, microsites, telephony intelligence, analytics.
- Compliance is framed mainly as security/KYC handling; RERA validation, renewal, and claim governance need explicit scope.
- IP terms need review because proprietary frameworks, prebuilt modules, and AI datasets remain Auum property.

**Best use**

Auum is useful as a product-vision benchmark and potential build partner if Justo is willing to run deeper integration discovery and negotiate ownership/source-of-truth terms.

### 6.3 TSPL/Triazine

**What TSPL covers well**

- Mobile-first, AI-enabled CP platform vision.
- Lead management, site visit scheduling, CP performance, commission/payout, incentives, analytics.
- Web portal personas: admin, CP owner, broker/agent, finance team.
- AI calling flow: trigger call, route audio, transcribe, generate context reply, record, summarize, update lead score, suggest site visit.
- AI intelligence: budget, location, urgency, sentiment, competitor mentions, site visit intent, hot/warm/cold classification.
- Commission engine: rule configuration, slab payouts, booking validation, finance approval.

**Gaps to clarify**

- CP sourcing and RM lifecycle are not materially specified.
- Manthan integration is not mapped to existing modules.
- CP employee lifecycle is shallow.
- Lead conflict, duplicate rules, ownership lock, override, expiry, and disputes are not granular.
- Compliance is not deep enough for RERA/GST/PAN/bank renewal and audit.
- Multi-tenant SaaS posture conflicts with Manthan single-tenant assumptions unless explicitly reconciled.
- Cost and timeline are high relative to detail provided.

**Best use**

TSPL is useful as a benchmark for AI calling and analytics ideas, but should not be treated as implementation-ready without a detailed capability backlog and Manthan integration plan.

### 6.4 I9/Indexnine

**What I9 covers well**

- Directly builds on already covered Manthan scope: CP onboarding, basic leads, conflict management, bookings, visits, invoicing, incentive plans, collaterals, broadcasting, loyalty/gamification.
- Adds advanced auth, global dashboard, advanced funnel, KHOJ integration, AI data pipelines, AI voice agent, automated brokerage, campaign management, geofenced QR validation, nudge engine, advanced reporting.
- Uses React Native mobile app approach only, NestJS/Node.js backend, Postgres, Azure.
- Clearly prices existing and new modules and proposes a six-week sprint plan.

**Gaps to clarify**

- Six-week delivery is aggressive for the depth of lifecycle needed.
- CP sourcing and RM lifecycle are not materially specified despite being central to Justo's business goal.
- CP employee lifecycle is only partial: org leader vs individual CP is not enough.
- RERA validation/renewal and compliance lifecycle are not explicit.
- Single-tenant assumption may constrain future multi-region/white-label/partner ecosystem expansion.
- AI/KHOJ/Gemini scope needs business prioritization; it should not crowd out trust workflows.

**Best use**

I9 is the baseline implementation comparator because of Manthan continuity. Justo should make I9 prove the deeper lifecycle and acceptance criteria rather than accepting the proposal as a complete CP operating system.

## 7. Rewards And Risks

### 7.1 Rewards

| Reward | Description | What Must Be True |
|---|---|---|
| CP network scale | Justo can onboard and activate more CP firms faster | Onboarding, compliance, project access, activation funnel work |
| Higher conversion | CPs can discover inventory, register leads, schedule visits, and follow up faster | Project catalog, lead lock, communication, nudges, site visit workflows work |
| CP trust | CPs believe their leads and payouts are protected | Ownership ledger, payout visibility, dispute workflow work |
| Finance control | Payouts are transparent without losing approval discipline | Commission rules, invoice, GST/TDS, approval, reconciliation work |
| Better vendor leverage | Justo can compare proposals against its own capability model | BRD and PRD become SoW annexure inputs |
| Market defensibility | Justo builds a controlled CP distribution layer rather than depending on ad hoc broker relationships | CP lifecycle, RM dashboards, CP health scoring work |

### 7.2 Risks

| Risk | Severity | Why It Matters | Mitigation |
|---|---|---|---|
| CPs do not adopt | High | App fails if it adds data entry without practical value | Make CP benefit visible in first session: inventory, share kit, lead lock, status |
| Manthan duplication | High | Duplicate systems create data conflict and vendor dependency | Define source-of-truth matrix before PRD signoff |
| Lead disputes continue | High | This is a core CP trust breaker | Build precise lead ownership policy and evidence ledger |
| Payout opacity continues | High | CPs follow money; unclear payouts reduce loyalty | CP-visible payout ledger with SLA and finance status |
| Compliance gaps | High | RERA/KYC/GST errors create legal and trust risks | Compliance lifecycle, renewal, claim governance |
| Overbuilding AI | Medium | AI can consume cost before trust workflows are stable | AI as v2 unless tied to measurable lead activation or follow-up rescue |
| Vendor lock-in | Medium | Proprietary frameworks or unclear IP can constrain Justo later | Contractual ownership, export, API, and source-code clauses |
| Weak CP employee model | Medium | CP owner cannot govern team behavior | Org hierarchy, roles, attribution, deactivation, reassignment |

## 8. Persona Journeys

The following journeys are intentionally granular enough to feed the PRD. Each journey describes the person's current burden, what the app should simplify, and the expected PRD implications. PRD conversion should preserve this structure: trigger, actor goal, app action, outside-app action, Manthan/system event, data created, decision point, exception path, and success measure.

### 8.1 Justo Leadership

**Goal:** Scale regional CP-led business while controlling risk, conversion, and payout exposure.

**Current pain points**

- Business performance is fragmented across CRM, finance, sourcing teams, and vendor reports.
- Leadership cannot easily see whether CP growth is quality growth or only vanity onboarding.
- Vendor proposals are not directly comparable.

**App / platform journey**

| Step | In-App Experience | Outside-App Context | Pain Removed |
|---|---|---|---|
| 1. Open leadership dashboard | View region, city, cluster, project, RM, and CP funnel | Weekly review or business war room | Reduces manual report consolidation |
| 2. Inspect CP network health | See active CPs, inactive CPs, activation ageing, lead quality, visit/bookings, payout SLA | Decide where to push sourcing | Separates real network strength from onboarding count |
| 3. Review conversion funnel | Lead -> accepted -> visit -> booking -> payout | Compare projects and CP cohorts | Identifies where conversion breaks |
| 4. Review risk dashboard | Lead disputes, payout delays, RERA exceptions, compliance expiries | Escalate to operations/legal/finance | Makes hidden trust risks visible |
| 5. Review vendor gaps | See what current vendor scope covers/misses | Negotiate SoW or change requests | Prevents vague vendor commitments |

**PRD implications**

- Leadership dashboards need CP network health, conversion, payout, compliance, and dispute views.
- Drill-down must work by region, city, cluster, project, RM, CP firm, and time period.
- Dashboard should distinguish active CPs from merely registered CPs.

**Journey mechanics**

| Trigger | System/Data Created | Decision Point | Exception Path | Success Measure |
|---|---|---|---|---|
| Weekly/monthly business review | Executive dashboard filters and saved views | Which region/project/RM/CP cohort needs intervention? | Missing or stale metrics are flagged to ops/product owner | Leadership can identify top bottleneck within one review session |

### 8.2 Justo CP Sourcing Head

**Goal:** Build and manage a productive CP network.

**Current pain points**

- CP recruitment may happen informally through personal networks, events, calls, or field visits.
- Hard to know which CPs are stuck in verification, untrained, inactive, or underperforming.
- RM effort may be invisible or inconsistently recorded.

**App / platform journey**

| Step | In-App Experience | Outside-App Context | Pain Removed |
|---|---|---|---|
| 1. Create CP sourcing plan | Define target market, project focus, CP segment, target count | Business expansion planning | Converts vague sourcing into measurable funnel |
| 2. Assign RMs | Allocate CP prospects or territories to RMs | Team management | Makes ownership clear |
| 3. Monitor prospect funnel | Prospect -> contacted -> documents pending -> approved -> activated | Daily sourcing review | Shows bottlenecks |
| 4. Review activation | First login, first employee, first lead, first site visit, first booking | Coaching and escalation | Shows whether CPs are actually useful |
| 5. Manage retention | See inactive CPs, payout disputes, poor lead quality, compliance expiry | Relationship repair or suspension | Makes churn preventable |

**PRD implications**

- Need CP prospect object before approved CP object.
- Need RM assignment, CP stage, activation checklist, ageing, reminders, and notes.
- Need CP health score combining activity, conversion, compliance, disputes, and payouts.

**Journey mechanics**

| Trigger | System/Data Created | Decision Point | Exception Path | Success Measure |
|---|---|---|---|---|
| New market/project launch or CP network target | CP prospect, RM assignment, activation checklist | Approve, nurture, suspend, or offboard CP? | CP stuck in docs/training/inactivity queue | CP activation ageing decreases and active CP ratio increases |

### 8.3 Justo RM / Sourcing Employee

**Goal:** Recruit CPs, activate them, and keep them productive.

**Current pain points**

- Field work is hard to prove and track.
- RM has to chase CPs for documents, training, first lead, first visit, and project updates.
- CPs ask the RM for status on leads, bookings, and payouts because the system is not CP-visible enough.

**App / platform journey**

| Step | In-App Experience | Outside-App Context | Pain Removed |
|---|---|---|---|
| 1. Add CP prospect | Quick mobile form with firm, owner, phone, market, RERA status, source | Meeting at office/site/event | Avoids later data re-entry |
| 2. Log meeting | Geotag/time-stamp note, next action, documents promised | Field visit | Makes RM activity measurable |
| 3. Trigger onboarding link | Send CP registration/document link over WhatsApp | CP owner continues on phone | Reduces manual document collection |
| 4. Track pending tasks | Dashboard of CPs missing RERA/GST/bank/training/first lead | Daily follow-up | Prioritizes effort |
| 5. Activate CP | Assign projects, share pitch kit, track first lead/visit | Coaching CP | Creates structured activation |
| 6. Handle escalation | View lead/payout/site-visit issue and route to ops/finance | CP calls RM | Reduces blind follow-up |

**PRD implications**

- RM mobile view must be fast and field-friendly.
- Need CP prospect stages, task reminders, meeting logs, and WhatsApp triggers.
- Need escalation visibility without giving RM unrestricted finance/admin powers.

**Journey mechanics**

| Trigger | System/Data Created | Decision Point | Exception Path | Success Measure |
|---|---|---|---|---|
| RM meets or contacts a CP prospect | Prospect record, meeting note, next task, document link | Is CP worth approving and activating? | Missing documents, invalid RERA, inactive after approval | RM moves CP from prospect to first lead/site visit faster |

### 8.4 Justo Sales / Admin Operations

**Goal:** Configure and run the operational system reliably.

**Current pain points**

- Project, inventory, collateral, offers, access, and workflows change often.
- Incorrect configuration creates wrong CP promises and downstream disputes.
- Manual exception handling grows with CP network scale.

**App / platform journey**

| Step | In-App Experience | Outside-App Context | Pain Removed |
|---|---|---|---|
| 1. Configure CP project access | Select project, CP cohorts, visibility, offers, collateral | Launch/project operations | Prevents blanket access mistakes |
| 2. Publish inventory/collateral | Versioned price sheet, unit availability, approved brochures | Developer/project updates | Reduces stale sharing |
| 3. Configure lead rules | Lock duration, duplicate rules, direct-vs-CP priority, override rights | Commercial/legal policy | Makes disputes rule-based |
| 4. Configure site visit proof | QR/OTP/site-desk/admin check-in | Site operations | Standardizes visit evidence |
| 5. Manage exceptions | Rejected leads, duplicate conflicts, failed notifications, document issues | Ops desk | Reduces unresolved queue |

**PRD implications**

- Admin needs policy configuration screens with audit logs.
- Any change to lead ownership, offer, commission, or collateral must be versioned.
- Exception queues need ownership and SLA.

**Journey mechanics**

| Trigger | System/Data Created | Decision Point | Exception Path | Success Measure |
|---|---|---|---|---|
| Project/inventory/offer/workflow change | Versioned config, audit log, access rule | Publish, hold, rollback, or restrict? | Bad config, stale price, wrong access, notification failure | CPs only see current approved project and workflow data |

### 8.5 Justo Finance

**Goal:** Pay correctly, control risk, and reduce payout escalations.

**Current pain points**

- CPs ask for payout status before finance has complete validation.
- Commission rules vary by project, slab, milestone, booking status, and deduction.
- GST/TDS/invoice/reconciliation create friction if not visible.

**App / platform journey**

| Step | In-App Experience | Outside-App Context | Pain Removed |
|---|---|---|---|
| 1. View payout queue | Eligible bookings, pending validations, invoice needed, finance approval pending | Finance operations | Prioritizes work |
| 2. Validate booking | Confirm booking, payment milestone, cancellation risk, CP eligibility | CRM/accounting check | Reduces wrong payouts |
| 3. Review invoice | GST details, invoice amount, TDS, deductions, bank details | Accounting compliance | Reduces rework |
| 4. Approve/reject | Status and reason visible to CP/RM as permitted | Finance approval | Stops opaque escalations |
| 5. Reconcile payment | Payment reference, date, amount, ledger status | Bank/Tally/accounting | Creates payout proof |

**PRD implications**

- Need CP-visible payout status but finance-controlled approval.
- Need payout status taxonomy: not eligible, eligible, invoice pending, under review, approved, scheduled, paid, rejected, disputed.
- Need Tally/accounting integration requirements or interim export/reconciliation.

**Journey mechanics**

| Trigger | System/Data Created | Decision Point | Exception Path | Success Measure |
|---|---|---|---|---|
| Booking reaches commission-eligible stage | Payout record, invoice request/status, approval log | Approve, reject, hold, or dispute? | Missing invoice, KYC mismatch, cancellation risk, bank issue | Eligible payouts have visible status and SLA adherence |

### 8.6 Developer / Project Team

**Goal:** Provide accurate, sellable project information and site capacity.

**Current pain points**

- CPs sell with stale price sheets, outdated collateral, or unconfirmed availability.
- Site teams may not know whether a visitor is CP-attributed.
- Offer/project changes create confusion.

**App / platform journey**

| Step | In-App Experience | Outside-App Context | Pain Removed |
|---|---|---|---|
| 1. Publish project facts | RERA number, location, configuration, price bands, inventory, offers | Project update | Creates approved source |
| 2. Approve collateral | Brochure, WhatsApp creatives, price sheet, pitch points | Marketing/legal approval | Reduces claim risk |
| 3. Manage visit slots | Available slots, blackout dates, site-desk capacity | Site operations | Reduces bad scheduling |
| 4. Confirm visit outcome | Attended/no-show/interested/booked, notes | Site-desk follow-up | Improves attribution |
| 5. Update inventory | Unit status, blocked/booked/released | Sales desk | Prevents stale inventory |

**PRD implications**

- CP catalog must show only approved and current project facts.
- Site visit outcome must feed lead and commission eligibility.
- Inventory freshness and collateral versioning are required trust features.

**Journey mechanics**

| Trigger | System/Data Created | Decision Point | Exception Path | Success Measure |
|---|---|---|---|---|
| Project information changes | Inventory version, collateral version, site slot rules | Publish to all CPs or selected cohorts? | Project data stale, offer withdrawn, site capacity full | CPs share only current approved project information |

### 8.7 CP Owner / Org Leader

**Goal:** Increase brokerage revenue with confidence that leads, employees, and payouts are protected.

**Current pain points**

- CP owner has limited visibility after submitting a lead.
- CP owner may not know which employee generated what value.
- Payout uncertainty makes relationship with developer/Justo fragile.
- Project information is spread across WhatsApp, PDFs, calls, and portals.

**App journey**

| Step | In-App Experience | Life Simplification |
|---|---|---|
| 1. Register firm | Mobile-friendly firm registration with RERA/GST/PAN/bank/KYC checklist | No repeated document chasing |
| 2. Track approval | See pending/approved/rejected items and reasons | Knows exactly what blocks activation |
| 3. Add team | Invite employees, set roles, assign projects | Controls team access |
| 4. Browse projects | See approved catalog, inventory freshness, offers, collateral, commission policy | Stops searching WhatsApp for latest material |
| 5. Share project | Share approved collateral/referral link with tracking | Safer marketing and attribution |
| 6. Register lead | Submit lead, see accepted/conflict/rejected status and lock expiry | Trusts ownership |
| 7. Monitor pipeline | See team leads, visits, bookings, stuck items | Manages team performance |
| 8. Track payout | View eligible amount, invoice, approval, expected date, paid status | Reduces payout anxiety |
| 9. Raise dispute/support | Submit evidence for lead/payout/site issue | Structured escalation |

**PRD implications**

- CP owner dashboard must combine firm compliance, team activity, lead pipeline, site visits, bookings, and payouts.
- CP owner needs team-level attribution and controls.
- The app must explain status and next action, not only show status.

**Journey mechanics**

| Trigger | System/Data Created | Decision Point | Exception Path | Success Measure |
|---|---|---|---|---|
| CP owner joins or reviews business | Firm profile, employee records, lead/booking/payout dashboard | Where should owner focus team effort? | Rejected docs, employee exit, lead dispute, payout delay | Owner can manage team and revenue without calling RM for every status |

### 8.8 CP Employee / Agent

**Goal:** Convert customers quickly with accurate project information and minimal admin work.

**Current pain points**

- Agent depends on stale PDFs, forwarded messages, and calls to RMs.
- Lead submission feels risky if ownership is unclear.
- Follow-ups are scattered across WhatsApp, calls, notes, and memory.
- Visit scheduling and proof can be manual.

**App journey**

| Step | In-App Experience | Life Simplification |
|---|---|---|
| 1. Login and see assigned projects | Project cards with price, inventory, offers, pitch, collateral | Knows what to sell today |
| 2. Search matching project | Filter by location, budget, configuration, possession, offer | Faster buyer matching |
| 3. Share approved collateral | WhatsApp share kit, referral link, project facts | No manual PDF hunting |
| 4. Register lead | Quick phone-first lead capture, duplicate check, lock result | Immediate ownership clarity |
| 5. Follow up | Reminders, call/WhatsApp timeline, notes, next best action | Fewer lost follow-ups |
| 6. Schedule visit | Available slots, customer confirmation, QR/OTP | Less coordination overhead |
| 7. Update outcome | Interested/not interested/reschedule/booked, notes | Pipeline stays current |
| 8. See commission status | If permitted, see booking/payout milestone | Motivation and clarity |

**PRD implications**

- CP employee mobile UI must optimize for speed: project search, share, lead capture, follow-up, visit schedule.
- Need offline/poor-network fallback for field use.
- Need clear error states for duplicate/conflict leads.

**Journey mechanics**

| Trigger | System/Data Created | Decision Point | Exception Path | Success Measure |
|---|---|---|---|---|
| Buyer inquiry or follow-up | Lead record, share event, call/note, visit request | Register, follow up, schedule visit, or drop? | Duplicate/conflict lead, stale inventory, no visit slot | Agent can move from inquiry to protected lead/visit quickly |

### 8.9 CP Telecaller

**Goal:** Qualify and nurture CP/customer leads systematically.

**Current pain points**

- Lead queues and follow-ups may live in spreadsheets or generic CRM views.
- Call outcomes are not consistently connected to site visits and booking intent.
- Missed follow-ups directly hurt conversion.

**App journey**

| Step | In-App Experience | Life Simplification |
|---|---|---|
| 1. Open queue | Leads sorted by priority, due follow-up, hot/warm/cold | No manual list management |
| 2. Call from app | Click-to-call, call mask/record if enabled | Faster outreach |
| 3. Capture disposition | Budget, location, urgency, objection, visit intent | Structured qualification |
| 4. Schedule follow-up/visit | Next action created automatically | Fewer dropped leads |
| 5. Escalate hot lead | Notify CP owner/agent/RM | Faster conversion |

**PRD implications**

- Telecaller queue can be v2 if MVP focuses on CP owner/agent, but requirements should preserve the role model.
- AI summaries can help here later, but manual disposition must work first.

**Journey mechanics**

| Trigger | System/Data Created | Decision Point | Exception Path | Success Measure |
|---|---|---|---|---|
| Lead enters telecaller queue or follow-up due | Disposition, call log, next action, visit intent | Continue nurture, schedule visit, escalate, or mark lost? | No answer, wrong number, low intent, duplicate | Follow-up leakage reduces and qualified visits increase |

### 8.10 Buyer / Customer

**Goal:** Get accurate project information and complete required steps with trust.

**Current pain points**

- Buyers may receive inconsistent claims from different CPs.
- KYC/payment/site-visit confirmation can feel fragmented.
- Buyer may not know whether the CP is authorized or RERA-compliant.

**App-linked journey**

| Step | Buyer Experience | Life Simplification |
|---|---|---|
| 1. Receives approved project link | Project facts, offer, RERA details, CP/Justo attribution | More trust in shared material |
| 2. Confirms interest | Simple CTA for callback/site visit | Less back-and-forth |
| 3. Completes KYC/payment where needed | Secure buyer portal/payment flow | Controlled transaction path |
| 4. Attends site visit | QR/OTP/site-desk confirmation | Clear visit attribution |
| 5. Receives follow-up | Approved messages and next steps | Less confusion |

**PRD implications**

- Buyer-facing links must be claim-safe and approved.
- Buyer confirmation can strengthen dispute evidence.
- Avoid exposing internal CP/finance data to buyers.

**Journey mechanics**

| Trigger | System/Data Created | Decision Point | Exception Path | Success Measure |
|---|---|---|---|---|
| Buyer receives CP-shared link or visit request | Buyer interaction, confirmation, KYC/payment event where relevant | Proceed, request callback, schedule visit, or drop? | Mismatched info, payment failure, visit no-show | Buyer receives accurate project info and next steps |

### 8.11 Compliance / Support

**Goal:** Reduce regulatory, data, and operational risk.

**Current pain points**

- Documents can be uploaded but not operationally governed.
- Expiry, renewal, advertising claims, consent, and disputes are hard to audit.
- Support issues are scattered across calls and WhatsApp.

**App / platform journey**

| Step | In-App Experience | Pain Removed |
|---|---|---|
| 1. Review compliance queue | Pending RERA/GST/PAN/bank/KYC, expiries, exceptions | No hidden non-compliance |
| 2. Approve/reject docs | Reasoned decision and audit log | Cleaner onboarding |
| 3. Monitor claim-safe collateral | Only approved materials can be shared | Reduces misleading claims |
| 4. Handle disputes | Lead/payout/site evidence bundle | Faster resolution |
| 5. Export audit evidence | Document trail for leadership/legal | Better governance |

**PRD implications**

- Compliance lifecycle must include expiry, renewal, exception, and audit.
- Support/dispute ticketing can be lightweight but must be tied to evidence.

**Journey mechanics**

| Trigger | System/Data Created | Decision Point | Exception Path | Success Measure |
|---|---|---|---|---|
| Compliance expiry, disputed lead, payout issue, complaint | Ticket, evidence bundle, decision log | Approve, reject, escalate, suspend, or close? | Missing evidence, policy ambiguity, regulatory issue | Disputes resolve with audit evidence and repeatable policy |

## 9. Role And Permission Matrix

| Capability | Leadership | CP Sourcing Head | RM | Ops/Admin | Finance | Developer/Project | CP Owner | CP Employee | Telecaller | Support/Compliance |
|---|---|---|---|---|---|---|---|---|---|---|
| View executive dashboards | View | View | Limited | View | View finance slice | Limited project slice | No | No | No | View risk slice |
| Create CP prospect | No | Create | Create | Create | No | No | No | No | No | No |
| Approve CP firm | No | Approve/recommend | Recommend | Process | No | No | No | No | No | Validate docs |
| Manage CP employees | No | View | View | Admin support | No | No | Create/manage own firm | Own profile only | Own profile only | Audit |
| Configure project access | No | Recommend | Recommend | Configure | No | Provide input | View assigned | View assigned | View assigned | Audit |
| Submit lead | No | No | On behalf if policy allows | Admin exception | No | No | Create/view firm leads | Create/view assigned leads | Create/view assigned queue | Audit |
| Override lead conflict | No | Approve/escalate | Recommend | Execute | No | No | Dispute only | Dispute only | No | Review evidence |
| Schedule/verify site visit | View | View | Schedule/support | Configure/override | No | Confirm outcome | Schedule/view | Schedule/view | Schedule/view | Audit |
| View booking status | View | View | View assigned | Admin view | Finance view | Project view | View own firm | View assigned | Limited | Audit |
| Approve payout | No | No | No | No | Approve/reject | No | No | No | No | Audit |
| View payout status | Summary | Summary | Assigned CP summary | Admin view | Full | No | Own firm | If allowed by owner | No | Audit |
| Publish collateral | No | Recommend | Recommend | Publish | No | Provide/approve input | Share approved only | Share approved only | Share approved only | Audit claims |
| Manage support/disputes | View | Escalate | Escalate | Resolve ops issues | Resolve finance issues | Resolve project issues | Raise/view own | Raise/view assigned | Raise/view assigned | Own compliance/support |

## 10. Capability Requirements

### 10.1 MVP Capabilities

| Capability | Why MVP | Core Acceptance Direction |
|---|---|---|
| CP firm onboarding and compliance | No trusted network without verified CPs | CP can register, submit docs, see approval status, receive rejection reasons |
| CP employee management | CP is an organization, not one login | CP owner can invite, assign roles, deactivate, and reassign active work |
| Project catalog and approved collateral | CPs need reliable sellable inventory | CP sees assigned projects, freshness indicators, and approved share kit |
| Lead submission and lock | CP trust depends on ownership clarity | Lead accepted/conflicted/rejected/pending-sync with reason and audit trail |
| Site visit scheduling and proof | Visit attribution drives conversion and commission | Visit can be scheduled, verified by QR/OTP/geofence/site-desk/admin proof, and outcome captured |
| Communication timeline | Follow-up leakage is a conversion killer | Lightweight notes, reminders, and integrated communication events where already available |
| Booking visibility | CP needs to know what happened after visit | CP-safe booking milestone and next action visible by permission |
| Commission/payout processing | Money drives CP loyalty | CP sees eligibility/status/reason while finance can approve, reject, schedule, mark paid, reconcile, and dispute with audit |
| Justo sourcing/RM activation view | Justo needs scalable CP acquisition | RM sees CP prospects, activation tasks, pending docs, and escalations |
| Admin/audit/support foundation | Scale requires controls | Admin can manage core policies, exceptions, audit logs, and evidence-backed tickets |

### 10.2 v2 / Deferred Capabilities

- AI voice calling and full autonomous call handling.
- AI campaign builder and retargeting.
- CP-branded microsites.
- Advanced telecaller operations.
- Full marketing budget optimization.
- CP marketplace/network effects.
- Advanced workforce intelligence and geo-tracking.
- Advanced leadership analytics, gamification, loyalty, and CP health scoring beyond simple KPI reporting.
- Workforce geo-tracking beyond scheduled site-visit proof.
- Full buyer portal expansion beyond safe project links, visit confirmation, and reuse of existing buyer flows.
- Multi-tenant/white-label platform architecture beyond Justo's own CP network.

### 10.3 Capability Acceptance Criteria For PRD

| Capability | Acceptance Criteria Direction |
|---|---|
| CP onboarding | CP can submit required docs, see missing items, receive approval/rejection reason, and know next activation step |
| RERA compliance | System captures RERA status, expiry/renewal where applicable, and blocks/flags non-compliant CP states according to policy |
| CP employee exit | CP owner/admin can deactivate employee and reassign active leads without losing attribution history |
| Inventory freshness | CP sees last-updated timestamp/source and cannot share expired collateral or withdrawn offers |
| Lead lock | Lead submission returns accepted/conflict/rejected state with reason, lock owner, expiry, and dispute path |
| Site-visit proof | Visit has scheduled slot, verification event, outcome, and evidence linked to lead and commission eligibility |
| Payout ledger | CP sees commission eligibility, invoice state, approval state, expected date, paid date, deductions, and dispute state |
| RM dashboard | RM sees CP prospect funnel, pending activation tasks, inactive CPs, and escalations |
| Claim-safe collateral | Only approved project facts/collateral can be shared from the app, with versioning and audit |
| Dispute evidence | Dispute view bundles timestamps, owner, source, communication, visit, booking, and finance evidence |

## 11. Source-Of-Truth Matrix

| Entity | Likely Source Of Truth | Open Question |
|---|---|---|
| CP firm | Manthan CP master extended for lifecycle | Does CP prospect exist before approved CP master? |
| CP employee | Manthan user/CP employee model | How are employee exits and lead reassignment handled? |
| Project | Manthan project/inventory modules | How fresh is inventory and pricing data? |
| Collateral | Manthan/project document repository | Who approves claim-safe collateral? |
| Lead | Manthan lead module | What exact duplicate and lock rules apply? |
| Site visit | Manthan site-visit/walk-in modules extended | Which proof method is authoritative? |
| Booking | Manthan booking/deal module | What status is CP-visible? |
| Commission rule | Manthan finance/CP incentive configuration | Who configures and approves changes? |
| CP invoice | Finance/accounting system or Manthan finance module | What is Tally integration status? |
| Payout | Finance/accounting/bank reconciliation | What payment status is CP-visible? |
| Support/dispute | New or extended Manthan workflow | What SLA and escalation rules apply? |

| Audit logs | Manthan/common audit layer | Which events are mandatory: lead lock, override, payout approval, collateral publish, CP deactivation? |

## 12. Vendor Comparison Against Required Business Outcome

| Required Outcome | Auum | TSPL | I9 | BRD Position |
|---|---|---|---|---|
| Fast Manthan extension | Medium | Low | High | I9 is baseline comparator |
| Rich CP operating-system vision | High | Medium | Medium | Auum sets product benchmark |
| CP sourcing/RM lifecycle | Medium-low | Low | Low | Must be added to any SoW |
| CP employee lifecycle | Medium | Low-medium | Medium-low | Must be explicit in PRD |
| Lead ownership trust | High | Medium | High | Strong overlap; policy detail still needed |
| Site-visit proof | High | Medium | High | MVP requirement |
| Commission/payout trust | High in later tranche | Medium-high | High | MVP or near-MVP; not optional |
| Compliance lifecycle | Medium-low | Low-medium | Medium-low | RERA renewal/audit must be added |
| AI | High | High | High | Useful but not MVP center |
| Delivery confidence | Medium | Low-medium | Medium | Depends on scope discipline |

## 13. PRD-Ready Functional Themes

The PRD should convert this BRD into requirements under these themes:

1. Identity, roles, and permissions.
2. CP firm onboarding and compliance.
3. CP employee/team management.
4. Justo CP sourcing and RM operations.
5. Project catalog, inventory, and collateral.
6. Lead registration, dedupe, ownership, and disputes.
7. Communication and follow-up timeline.
8. Site visit scheduling, proof, and outcome.
9. Booking visibility.
10. Commission, invoice, and payout ledger.
11. Analytics, CP health, and leadership dashboards.
12. Support, audit, and compliance governance.
13. Deferred AI/campaign/microsite capabilities.

## 14. Open Decision Register Before PRD

| Decision | Why It Matters | Owner Needed |
|---|---|---|
| Lead-lock expiry duration | Determines CP trust and conflict volume | Sales/CP leadership |
| Direct-vs-CP lead priority | Prevents escalation and duplicate disputes | Sales leadership/legal |
| CP override authority | Controls who can break ownership locks | Ops/sales leadership |
| Commission eligibility milestone | Drives payout expectations | Finance/sales |
| Payout SLA | Determines CP-visible promise | Finance/leadership |
| GST/TDS handling | Required for accurate payout ledger | Finance |
| RERA validation source | Determines compliance workflow | Legal/compliance |
| CP employee exit policy | Prevents lead leakage and attribution disputes | CP sourcing/ops |
| CP suspension policy | Controls non-compliant or low-quality CPs | CP sourcing/legal |
| Buyer-facing data exposure | Prevents overexposure of internal data | Product/legal |
| AI v1 scope | Prevents AI overbuild | Leadership/product |
| Vendor implementation path | Determines architecture and SoW detail | Leadership/procurement |

### Open Questions

1. Is I9 the default build partner, or are all three vendors being evaluated equally?
2. What exact market within Maharashtra is the first launch target?
3. What CP volume and CP employee volume should v1 support?
4. What is the current lead ownership policy: lock duration, direct-vs-CP priority, cooling-off period, overrides?
5. What is the current commission policy by project, slab, booking stage, cancellation, clawback, GST/TDS?
6. What payout SLA can Justo credibly promise?
7. Which Manthan APIs and data models are production-ready for mobile app integration?
8. What is the authoritative RERA validation workflow?
9. Which CP-branded collateral formats, if any, are required at launch, excluding CP microsites?
10. Which buyer-facing actions are allowed in launch without expanding the buyer portal?
11. What support model will handle CP disputes?
12. Which AI features have a measurable business case for v1?
13. What geofence radius, accuracy threshold, consent text, fallback path, and retention rule should apply to site-visit proof?
14. Which payout actions are processed in Manthan versus finance/accounting systems, and what reconciliation event is authoritative?
15. What file types, size limits, retry limits, and local retention rules apply to queued document uploads?

## 15. Recommended MVP Definition

MVP should be judged by whether CPs trust and use the app, not by number of modules.

### MVP Must Include

- CP firm onboarding and compliance status.
- CP employee invitation, role, and deactivation.
- Project catalog with current inventory and approved share collateral.
- Lead submission with duplicate check and clear ownership status.
- Site visit scheduling and proof, including geofence with QR/OTP/site-desk/admin fallback.
- Lightweight communication and follow-up timeline.
- CP-safe booking status visibility.
- Full commission/payout processing with CP-visible ledger, finance approval, payment reference, reconciliation, clawback/dispute states, and audit.
- Queued document uploads for onboarding/compliance with secure local storage, upload state, retry/resume, and server-side validation.
- RM sourcing and activation view.
- Admin/audit/dispute foundation for core trust workflows.

### MVP Should Exclude Unless Already Cheap In Manthan

- Full AI calling automation.
- Advanced campaign budget optimization.
- CP microsites.
- Full marketplace features.
- Advanced geo workforce surveillance.
- Multi-tenant SaaS expansion.
- Advanced telecaller operations and call intelligence.
- Advanced analytics, gamification, loyalty, and CP health scoring beyond launch KPI reporting.
- Full buyer portal expansion.
- Workforce geo-tracking outside scheduled site-visit proof.

## 16. Stakeholder Review Checklist

- [ ] Leadership agrees the app is a CP operating system, not a generic CRM shell.
- [ ] CP sourcing validates the CP prospecting and activation lifecycle.
- [ ] RMs validate field workflows and CP follow-up realities.
- [ ] Finance validates payout lifecycle and what can be exposed to CPs.
- [ ] Sales/admin ops validates project, inventory, collateral, lead, and site visit controls.
- [ ] Product/technology validates Manthan source-of-truth assumptions.
- [ ] Legal/compliance validates RERA, KYC, data, and claim governance.
- [ ] Procurement validates vendor comparison language and follow-up checklist.

## 17. Immediate Next Steps

1. Validate this BRD with Justo leadership, CP sourcing, RM, finance, ops, product, and compliance stakeholders.
2. Convert unresolved questions into a decision log.
3. Create a vendor clarification pack for Auum, TSPL, and I9.
4. Use the scope-gated BRD and PRD to create persona-wise journey maps.
5. Derive Google Stitch-ready UI screen specs from those journey maps.

---
*Draft status: v0.4, scope-gated for persona-wise journey map creation with geofencing, queued document uploads, and full payout processing restored as core differentiators pending stakeholder validation and open-question resolution.*
