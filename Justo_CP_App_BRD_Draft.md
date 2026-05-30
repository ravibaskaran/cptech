# Business Requirements Document: Justo CP App

Draft version: v0.1  
Date: 2026-05-30  
Prepared for: Justo Realfintech  
Primary source: `Justo_CP_App_Business_Brief.md`

## 1. Executive Summary

Justo wants to become a large retail/channel partner player in Maharashtra and later expand across India. The proposed CP app should support this strategy by helping Justo attract, onboard, activate, manage, and retain channel partners and their employees.

The app should not be treated as only a mobile CRM interface. It should be scoped as a CP operating system on top of Project Manthan's CRM, covering CP sourcing, compliance, project discovery, lead ownership, site-visit proof, booking visibility, commission transparency, performance management, and dispute-grade auditability.

Project Manthan already provides several CRM primitives. The BRD therefore focuses on what must be reused, configured, extended, or added so that the CP app supports Justo's business model rather than duplicating generic CRM functionality.

## 2. Business Objectives

### 2.1 Primary Objective

Enable Justo to build and operate a scalable CP network in Maharashtra by giving CP firms and their employees a trusted digital operating layer connected to Manthan.

### 2.2 Secondary Objectives

- Improve CP onboarding, activation, and retention.
- Reduce lead ownership disputes and duplicate conflicts.
- Improve site-visit proof and booking traceability.
- Make commission and payout status transparent to CPs and controlled for Justo finance.
- Give Justo sourcing/RM teams a CP recruitment and performance management cockpit.
- Provide a common capability baseline for comparing Auum, TSPL, and I9 proposals.

### 2.3 Success Metrics

| Metric | Definition | Initial Target Direction |
|---|---|---|
| CP activation rate | Approved CPs completing first lead/site visit/booking milestone | Increase |
| Lead conflict rate | Leads entering duplicate/conflict workflow | Decrease |
| Lead-to-site-visit conversion | CP leads converted into verified site visits | Increase |
| Site-visit-to-booking conversion | Verified visits converted into bookings | Increase |
| Payout SLA adherence | Eligible CP payouts completed within defined SLA | Increase |
| CP employee productivity | Active employees with meaningful lead/site visit activity | Increase |
| RM productivity | CP sourcing/activation tasks completed per RM | Increase |
| CP satisfaction | CP sentiment around inventory, trust, support, and payouts | Increase |

## 3. Evidence Base And Assumptions

### 3.1 Source Documents

- `docs/Manthan Proposal IndexNine.docx`
- `docs/Justo-CRM-Phase 1-SOW-7th May.docx.pdf`
- `docs/Justo-CRM-Phase 2 SOW-10th Nov.docx.pdf`
- `docs/Justo-CRM-Phase 2.4 SOW-16 Feb.docx.pdf`
- `docs/Justo-CRM-Phase 3 SOW-21st Jan.docx.pdf`
- `docs/Auum Justo Proposal CP App.pdf`
- `docs/TSPL_Business_Proposal_Justo_AI_CP_Platform.pdf`
- `docs/CP tech proposal from I9.pdf`
- `Justo_CP_App_Business_Brief.md`

### 3.2 Working Assumptions

- [high] Project Manthan remains the core CRM foundation.
- [high] The CP app must be available on Android and iOS.
- [high] Maharashtra is the first market focus; India expansion comes later.
- [high] CP lifecycle depth is more important than a generic mobile lead-entry app.
- [moderate] I9 is the lowest-friction Manthan extension path because its proposal directly references current Manthan modules.
- [moderate] Auum has the broadest CP operating-system vision but requires sharper Manthan integration and IP/source-of-truth review.
- [moderate] TSPL has a strong AI voice concept but needs a more granular CP lifecycle and Manthan integration backlog before it can be compared fairly.

## 4. Current Manthan Baseline

### 4.1 Existing Or Scoped Capabilities

| Area | Manthan Baseline | BRD Implication |
|---|---|---|
| Lead management | Lead CRUD, scoring, pipeline, smart lists, assignment, bulk actions, custom fields | Reuse and extend for CP lead lock/conflict rules |
| CP management | CP tagging, CP CRUD APIs, CP approval, CP portal, referral codes, referral links, QR | Extend into full CP firm lifecycle and CP sourcing funnel |
| CP employees | CP users/employees can be provisioned | Extend into employee lifecycle, roles, lead reassignment, performance |
| Communication | Email, SMS, WhatsApp, CTI/call logs, notifications, templates | Reuse for CP/customer communication timeline and follow-up nudges |
| Buyer/project portals | Buyer portal, white-label portal, token/payment flows, EOI | Reuse where CP lead/buyer actions enter payment/token flows |
| KYC/payment | KYC upload/validation, Razorpay, Decentro/CIBIL, Zoho Sign | Extend into CP compliance and payout eligibility |
| Site visits | Site-visit hooks, travel/pickup workflows, walk-in experience | Extend into QR/OTP/geofence proof and commission eligibility |
| Dashboards/reports | Dashboard/reporting, bulk actions, activity logs | Extend into CP health, RM sourcing, payout SLA, vendor-relevant reporting |
| AI/chatbot | AI chatbot integration and proposed KHOJ/Gemini/voice workflows | Defer unless directly supporting activation, lead quality, or trust |

### 4.2 Source-Of-Truth Questions

The BRD must resolve or flag the system of record for:

- CP firm profile.
- CP owner and CP employee users.
- CP documents and compliance status.
- Project catalog and inventory.
- Lead ownership and conflict log.
- Site visit proof.
- Booking status.
- Commission rule.
- CP invoice.
- Finance approval and payout status.

## 5. Personas

| Persona | Goal | In-App Responsibilities | Outside-App Responsibilities |
|---|---|---|---|
| Justo leadership | Scale CP-led sales and regional distribution | Review dashboards, growth, conversion, payout exposure, CP productivity | Strategy, vendor governance, market expansion |
| CP sourcing head | Build the CP network | Approve CPs, assign RMs, monitor activation and attrition | Recruit CP firms, manage commercial policies, resolve escalations |
| RM/sourcing employee | Activate CPs and drive output | Add CP prospects, verify docs, map CPs to projects, log visits, track activity | Field meetings, CP relationship management, developer coordination |
| Sales/admin ops | Run daily platform operations | Configure projects, roles, inventory visibility, workflows, notifications | SOPs, exception handling, operational data correction |
| Finance | Control invoices and payouts | Validate booking, review invoice, track GST/TDS/payment/reconciliation | Accounting, bank payment, payout dispute resolution |
| Developer/project team | Provide sellable inventory | Publish project details, pricing, inventory, collateral, offers, site slots | Project readiness, sales desk coordination |
| CP owner/org leader | Grow brokerage revenue | Register firm, add employees, assign leads, track bookings/payouts | Manage agency team, customer relationships, local marketing |
| CP employee/agent | Convert customers | Browse projects, share collateral, add leads, schedule visits, update stages | Calls, WhatsApp follow-ups, site visits, negotiation |
| CP telecaller | Qualify and nurture leads | Work queues, disposition calls, schedule follow-ups and site visits | Calling and follow-up discipline |
| Buyer/customer | Evaluate and buy property | Receive links, complete KYC/payment, confirm visit, view relevant project info | Physical visits, documents, payments |
| Compliance/support | Reduce operational/regulatory risk | Check documents, audit logs, support tickets, complaints | Legal review, regulatory response, escalations |

## 6. Lifecycle Requirements

### 6.1 Justo CP Sourcing Lifecycle

1. Identify target micro-market and CP segment.
2. Source CP candidates through referrals, associations, developer networks, digital campaigns, events, and field activity.
3. Capture CP prospect record.
4. Verify RERA, GST, PAN, bank, identity, address, team size, and operating market.
5. Approve, reject, or return for correction with reason.
6. Configure commercial plan, brokerage slab, incentives, lead-lock policy, and project access.
7. Map CP to RM, region/cluster, projects, inventory visibility, and employee seats.
8. Enable CP through training, project pitch packs, compliant collateral, and first-action checklist.
9. Measure activation by first login, employee add, project view/share, lead, site visit, booking, and payout.
10. Track performance and retain, upgrade, suspend, or offboard.

### 6.2 CP Firm Lifecycle

1. Discover Justo opportunity.
2. Register firm and owner.
3. Submit compliance and bank documents.
4. Receive approval/rejection.
5. Accept agreement and commercial plan.
6. Configure profile, brand, employees, and permissions.
7. Access projects, inventory, pricing, offers, and collaterals.
8. Submit and lock leads.
9. Schedule and prove site visits.
10. Track booking, documents, invoice, commission, and payout.
11. Raise support/dispute tickets.
12. Renew, expand, suspend, or offboard.

### 6.3 CP Employee Lifecycle

1. CP owner invites or imports employee.
2. Employee verifies phone/email and completes profile.
3. Owner assigns role and access.
4. Justo or CP owner assigns project/lead access.
5. Employee completes required training/compliance acknowledgement.
6. Employee handles leads, calls, visits, documents, and follow-ups.
7. App tracks performance.
8. Leads are reassigned when employee becomes inactive or exits.
9. Employee is deactivated while audit trail remains intact.

### 6.4 Lead Ownership Lifecycle

1. CP submits lead.
2. System dedupes by phone and other identifiers.
3. System checks direct-vs-CP, existing owner, cooling-off period, and source priority.
4. Lead is accepted, rejected, or sent to conflict workflow.
5. Ownership lock is created with expiry and audit log.
6. Ownership can be overridden only through authorized workflow.
7. Disputes show evidence: timestamp, source, CP employee, communication, visit, buyer confirmation, and booking linkage.

### 6.5 Site Visit Lifecycle

1. Lead requests or is scheduled for site visit.
2. Slot/project/site desk confirms availability.
3. Visit is verified through QR, OTP, geofence, or site desk check-in.
4. Outcome and buyer feedback are captured.
5. Visit evidence links to booking eligibility and commission rules.
6. No-show, reschedule, cancellation, and dispute events are logged.

### 6.6 Commission And Payout Lifecycle

1. Booking reaches commission-eligible stage.
2. System applies project-specific brokerage rules and incentive slabs.
3. Booking is validated.
4. CP invoice is generated or requested with GST/TDS handling.
5. Finance approves or rejects with reason.
6. Payment is processed and reconciled.
7. CP sees payout stage, expected date, amount, deductions, and dispute path.

## 7. Pain Points And Technology Opportunities

| Pain Point | Business Risk | Technology Requirement |
|---|---|---|
| Stale or fake inventory | CP distrust, buyer dissatisfaction, wasted effort | Live inventory, price freshness, collateral versioning |
| Lead ownership disputes | CP churn, manual escalation, loss of trust | Lead lock, duplicate detection, conflict workflow, audit ledger |
| Delayed/opaque payouts | CP disengagement, finance escalations | Booking-linked payout ledger, invoice status, SLA, payment tracking |
| Fragmented communication | Follow-up leakage and poor conversion | Unified timeline for calls, WhatsApp, SMS, email, notes |
| Compliance burden | Regulatory and onboarding risk | RERA/GST/PAN/bank/KYC validation, expiry, renewal, document vault |
| Weak CP employee controls | Leakage, poor accountability, lead loss on attrition | Org hierarchy, roles, employee performance, lead reassignment |
| Weak site-visit proof | Commission disputes and false attribution | QR/OTP/geofence proof, site logs, buyer feedback |
| Opaque marketing ROI | Inefficient spend and weak attribution | Referral links, source tracking, campaign ROI |
| Buyer trust gaps | Lower conversion and reputational risk | Approved collateral, transparent project factsheets, claim governance |

## 8. Capability Requirements

### 8.1 MVP Capabilities

1. CP firm onboarding and compliance.
2. CP employee management.
3. Project catalog and approved collateral.
4. Lead submission, dedupe, lock, and conflict workflow.
5. Site visit scheduling and proof.
6. Communication timeline and follow-up reminders.
7. Booking visibility.
8. Commission/payout ledger.
9. Justo sourcing/RM dashboard.
10. Admin, audit, support, and exception workflows.

### 8.2 Deferred Capabilities

- AI voice calling.
- AI campaign builder.
- CP microsites.
- Advanced marketing automation.
- Marketplace/network features.
- Advanced workforce intelligence.
- Multi-tenant/white-label expansion beyond current Justo-owned app needs.

## 9. Vendor Proposal Mapping

| Dimension | Auum | TSPL/Triazine | I9/Indexnine |
|---|---|---|---|
| Manthan integration | Partially specified: connects to existing CRM/CP admin | Weakly specified: generic integration | Strongest: explicitly builds on Manthan modules |
| CP sourcing/RM lifecycle | Partial: workforce geo tracking in Phase 2 | Not materially specified | Not materially specified |
| CP employee lifecycle | Partial: team hierarchy/RBAC | Partial: broker/agent personas | Partial: org leader vs individual CP; CP users exist |
| Lead ownership/conflict | Strong: lead lock, duplicate detection, audit | Moderate: assignment/status, weak conflict detail | Strong: existing conflict management plus advanced funnel |
| Site-visit proof | Strong: QR/OTP check-in, logs, feedback | Moderate: scheduling and visit-to-booking | Strong: geofence and QR handshake |
| Commission/payout | Strong: brokerage, GST invoice, payout lifecycle | Strong: commission engine and finance approval | Strong: automated brokerage, GST invoice, payout tracking |
| Compliance lifecycle | Partial: KYC/security references | Partial: KYC/doc management | Partial: KYC/GST, but RERA/renewal not explicit |
| AI | Strong assistant/campaign vision | Strong AI calling vision | Strong KHOJ/Gemini/voice agent vision |
| Delivery risk | Larger platform and IP/integration questions | Generic scope, high cost, 8-9 months | Fast 6-week timeline may underbuild lifecycle depth |

## 10. Vendor Clarification Checklist

1. Which system is source of truth for CP, CP employee, lead, project, inventory, booking, invoice, and payout?
2. What exact Manthan APIs/data models will the app use?
3. What exact lead-lock and conflict rules are included?
4. How are RERA registration, renewal, GST/PAN/bank verification, and document expiry handled?
5. What is the CP owner vs employee permission model?
6. What happens when a CP employee exits with active leads?
7. How are site visits proven and tied to commission eligibility?
8. How does payout tracking connect to booking validation, invoice, GST/TDS, Tally/accounting, and payment status?
9. What offline or low-connectivity mobile behavior is supported?
10. What App Store/Play Store release responsibilities are included?
11. What support, SLA, analytics, audit, and export guarantees are included?
12. Who owns source code, designs, AI workflows/prompts, models, and reusable components?

## 11. Risks And Dependencies

| Risk | Impact | Mitigation |
|---|---|---|
| BRD becomes generic CRM scope | Misses Justo's CP operating model | Keep CP lifecycle as primary structure |
| Manthan source-of-truth ambiguity | Integration disputes and duplicate systems | Require source-of-truth matrix |
| AI over-scoping | Delays MVP and distracts from trust workflows | Defer AI unless tied to activation/conversion/trust |
| CP employee lifecycle under-specified | Weak accountability and lead leakage | Add employee lifecycle and reassignment requirements |
| Payout workflow under-specified | CP distrust and finance escalations | Require payout ledger, SLA, GST/TDS, reconciliation |
| Vendor gap analysis overclaims | Procurement friction | Use "not specified in proposal" language |

## 12. Open Questions

1. What is the exact BRD audience: internal leadership, vendor alignment, board-level approval, or SoW annexure drafting?
2. Which Manthan instance and APIs are available for CP app integration today?
3. Is I9 the default implementation partner unless displaced, or are all three vendors being evaluated equally?
4. What is the intended MVP timeline and budget envelope?
5. How many CPs and CP employees should v1 support in Maharashtra?
6. Which markets within Maharashtra are priority for launch?
7. What is the current CP commission policy, payout SLA, GST/TDS treatment, and dispute process?
8. What RERA validation source and operating process will Justo use?
9. Does Justo want CP-branded microsites in v1 or later?
10. What level of AI is acceptable in v1?

## 13. Recommended Next Artifacts

1. CP interview guide for Maharashtra CPs, CP employees, and Justo RMs.
2. SoW annexure with CP lifecycle acceptance criteria.
3. Vendor scorecard with weights and evidence.
4. Manthan source-of-truth matrix.
5. Product requirements document after BRD review.

## 14. Stakeholder Review Checklist

- [ ] Leadership agrees with business objective and MVP priority.
- [ ] CP sourcing team validates the CP sourcing and activation lifecycle.
- [ ] Sales/admin ops validates lead, site visit, booking, and exception workflows.
- [ ] Finance validates commission, invoice, GST/TDS, approval, payout, and dispute lifecycle.
- [ ] Product/technology validates Manthan source-of-truth assumptions.
- [ ] Procurement/vendor owner validates the vendor comparison method.
- [ ] Legal/compliance validates RERA, KYC, data, and claims governance needs.

---
*Draft status: Ready for internal review and gap comments.*
