# Analytics, Tracking & Product Metrics Review — Product Architecture Council

## Review Summary

The Justo CP App documentation provides directional indicators for tracking product health but lacks a structured product analytics implementation plan. While success metrics are listed in both the BRD and the PRD (§10), they represent high-level business KPIs rather than developer-ready event schemas. The documents do not define a singular North Star Metric, lack a detailed event tracking plan (events, properties, and triggers), fail to specify the analytics toolchain (e.g., PostHog, Mixpanel, Firebase), and omit crucial specifications for offline event queueing and privacy-compliant tracking. Currently, the analytics model is insufficient to drive product-led growth (PLG) or evaluate detailed user behavior.

---

## Strengths

### 1. High-Level KPI Definitions Are Structured [high]
**Source:** `Justo_CP_App_BRD_Draft.md` §3.3 (Success Metrics, lines 106–119), `Justo_CP_App_PRD.md` §10 (Metrics and Success Criteria).

The success metrics tables are well-structured and cover critical operational dimensions: CP onboarding rate, CP activation rate, lead quality, site visit conversion, payout SLA adherence, and CP retention. The metrics map directly back to the business objectives defined in the Business Brief.

### 2. Sourcing Leadership Dashboards Specified [moderate]
**Source:** `Justo_CP_App_PRD.md` §7.14 (PRD-FR-080 to PRD-FR-086, lines 521–531).

The PRD defines explicit requirement items for a sourcing dashboard filterable by time period (rank, score, trend indicators) and a cross-persona leadership dashboard with bar charts, line trends, and heatmaps. This ensures that the frontend design will include placeholder views for business intelligence.

---

## Critical Issues (Must Fix)

### C1. Absence of a Singular North Star Metric [high]
**Source:** `Justo_CP_App_Business_Brief.md` §3.3 (lines 106–119), `Justo_CP_App_PRD.md` §10.

While multiple metrics are listed, the product lacks a unifying **North Star Metric** that aligns product, engineering, and business efforts around CP engagement.
* **Impact:** Without a North Star Metric, product development risks optimizing secondary metrics (e.g., app downloads or raw lead submissions) instead of the core value exchange (successful transactions and trust).
* **Recommendation:** Define the North Star Metric as: **"Monthly Active Channel Partners (MACPs) executing at least one verified site-visit."** This directly measures the core loop transition from registration to active sourcing and visit verification, aligning CP sourcing, sales, and product.

### C2. Missing Event Tracking Plan and Schema [high]
**Source:** Entire document set — [Missing evidence].

There is no event tracking spreadsheet or schema mapping specific user actions to analytics events. 
* **Impact:** Engineers will implement inconsistent, ad-hoc tracking events (e.g., one page tracking `leadSub` and another `submit-lead`), resulting in fragmented, unusable data in the analytics tool.
* **Recommendation:** Incorporate an initial **Event Tracking Plan** in the PRD. Define the core event lifecycle with properties:
  * Event: `cp_registration_initiated` | Properties: `sourcing_channel`, `device_os`.
  * Event: `kyc_documents_submitted` | Properties: `document_types_array`, `upload_duration_ms`.
  * Event: `lead_created` | Properties: `project_id`, `lead_source`, `is_offline`.
  * Event: `site_visit_verified` | Properties: `verification_method` (QR/OTP/Geofence), `delay_from_schedule_mins`.
  * Event: `payout_disbursed` | Properties: `amount_inr`, `cycle_duration_days`.

### C3. Lack of Offline Event Queueing Protocol [high]
**Source:** `ARCHITECTURE.md` §2.4 (lines 85–96).

The application is built as offline-first. However, while the business data syncs via PowerSync, there is no mention of how **product analytics events** are captured when the client is offline.
* **Impact:** If an agent submits a lead or browses a project catalog while offline, those analytics events will be lost if not stored locally. This makes it impossible to accurately measure offline usage patterns or calculate step-by-step conversion funnels.
* **Recommendation:** Specify that the KMP client must include a local SQLite-backed analytics outbox (e.g., using PostHog local caching). Events triggered offline must be queued, timestamped with the actual occurrence time (not the sync time), and batch-synced to the analytics server once a network connection is re-established.

---

## Major Issues (Should Fix)

### M1. Analytics Stack and SDK Strategy is Undefined [moderate]
**Source:** `ARCHITECTURE.md` §2.2 (Tech Stack Table).

The tech stack table lists Edge, Compute, Database, Object Storage, and deployment tools, but completely omits the analytics tracking tool.
* **Impact:** Product managers and developers cannot plan SDK footprint size, API payloads, or compute integration.
* **Recommendation:** Select and document the analytics stack. For a startup, **PostHog** (self-hosted or cloud) is recommended due to its open-source nature, built-in session recording, heatmaps, and SQL access to raw events. Alternatively, specify Firebase Analytics for mobile-first client tracking.

### M2. Missing Funnel and Cohort Definitions [moderate]
**Source:** `Justo_CP_App_PRD.md` §10.

Success metrics mention "onboarding completion rate" and "activation rate" but do not define the specific steps that constitute the funnel.
* **Impact:** Product teams cannot run bottleneck analysis to see where users drop off.
* **Recommendation:** Define the two primary funnels:
  1. **CP Onboarding Funnel:** App Installed -> OTP Verified -> Firm Details Entered -> Documents Uploaded -> Compliance Approved -> First Sourcing Action.
  2. **Lead-to-Payout Transaction Funnel:** Lead Submitted -> Site Visit Scheduled -> Visit Verified -> Booking Confirmed -> Invoice Uploaded -> Payout Cleared.
  Specify Cohort Analysis dimensions: by RM owner, by micro-market (e.g., Pune vs. Thane), and by CP size (Individual vs. Corporate).

---

## Minor Issues (Nice to Fix)

### N1. Privacy Leak in Analytics Payload [low]
**Source:** `Justo_CP_App_PRD.md` §9 (data privacy notes).

The document lacks rules around PII masking in tracking events.
* **Impact:** Developers might accidentally send CP phone numbers, PANs, or Buyer names in analytics event properties, violating the DPDPA.
* **Recommendation:** Mandate that no plain PII (names, phone numbers, Aadhaar, PAN) shall ever be sent in custom event properties. Use hashed identifiers (SHA-256) for users and firms.

---

## Missing Items

| Missing Item | Severity | Why It Matters |
|---|---|---|
| North Star Metric definition | Critical | Product lacks focus; teams may optimize secondary metrics |
| Event tracking plan and schema schema | Critical | Leads to fragmented, dirty tracking data during build |
| Offline analytics event queue protocol | Critical | Offline actions are lost, breaking funnel metrics |
| Analytics tool choice and SDK strategy | Major | Developers cannot write initialization code |
| Funnel step definitions | Major | Blocks bottleneck identification in onboarding |
| PII masking rules in analytics | Minor | Compliance risk under DPDP Act |

---

## Recommendations

### R1. Adopt PostHog as the Startup Analytics Standard (Priority: High)
Integrate the PostHog SDK (or Segment-equivalent wrapper) into the KMP Client. It supports session replay, which is highly useful to debug the first 100 CPs' user experience problems in the field.

### R2. Detail the Offline Analytics Cache Schema (Priority: High)
Define a separate SQLite table `local_analytics_events` to queue events when network state is offline. Ensure events carry an `occurred_at` timestamp.

### R3. Draft the Event Tracking Plan Spreadsheet (Priority: Before Phase 2)
Produce a clean tracking spreadsheet mapping every screen in `Justo_CP_App_UI_Stitch_Prompts.md` to a corresponding tracking event.

---

## Score (out of allocated points)

**Score: 3.5 / 7**

**Justification:**

| Dimension | Weight | Score | Notes |
|---|---|---|---|
| North Star Metric definition | 20% | 0/10 | Absent; no single metric alignment |
| Event tracking plan & schema | 30% | 2/10 | Directional KPIs are listed; no schemas or properties |
| Offline analytics queue | 20% | 0/10 | Entirely missing; offline events are lost |
| Analytics stack and SDK selection | 15% | 4/10 | Dashboards specified; tool choice and SDKs left open |
| Funnel and cohort definitions | 15% | 7/10 | General conversion rates noted, but lack formal steps |

**Weighted Score: 3.5/7** — The business metrics are correct, but the technical tracking architecture is absent. Resolving the North Star Metric (C1), drafting the event schemas (C2), and defining the offline queuing database model (C3) are necessary next steps.

---

*Review completed: 2026-06-14 | Reviewer: Analytics & Tracking Domain | Documents reviewed: Justo_CP_App_PRD.md §10 (1093 lines), Justo_CP_App_BRD_Draft.md §3.3 (850 lines), ARCHITECTURE.md §2 (155 lines), Justo_CP_App_Journey_Maps.md (407 lines)*
