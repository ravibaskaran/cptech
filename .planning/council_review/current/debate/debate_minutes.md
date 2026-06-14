# Product Architecture Council (PAC) — Debate & Reconciliation Minutes

**Date:** 2026-06-14  
**Status:** Completed  
**Council Panel:** Business Strategy, BRD Quality, PRD Quality, Persona Journey, UX Design, Technical Architecture, Security & Compliance, Analytics, QA & Testing, Engineering Feasibility, and Red Team.

---

## 1. Executive Summary of Debates

The Product Architecture Council convened to debate and reconcile critical contradictions identified across the v0.5 draft artifacts of the Justo CP App initiative. The council focused on aligning the core product scope with engineering reality, security guardrails, and regulatory requirements before proceeding to final document updates or visual UI generation.

Six major contradictions were debated. The resolved decisions below now form the authoritative directive for the updated product documentation.

---

## 2. Reconciled Debates & Core Decisions

### Debate 1: The Persona Scope Mismatch (Business & Journeys vs. PRD)
* **Contradiction:** The `Justo_CP_App_PRD.md` defines a simplified MVP targeting only 3 primary personas (Relationship Manager, CP Owner/Employee, and Buyer/Customer for document upload). However, `Justo_CP_App_Journey_Maps.md` and the original BRD specify detailed journeys, handoff tables, and screen specs for all 11 personas (including Leadership, Sourcing Head, Ops, Finance, Support, and Telecallers).
* **The Debate:** The Business and Sourcing domains argued that all 11 personas are required to prove the "operating loops" in the pilot. Engineering and QA argued that designing, testing, and shipping 11 distinct persona interfaces in Phase 2 would delay launch by at least 6 months.
* **Reconciliation Verdict:** 
  1. **Strict 3-Persona MVP Gate:** The mobile application UI scope will be restricted strictly to **three personas**: (a) CP Owner (representing the firm), (b) CP Employee (doing field selling), and (c) Justo RM (managing CP activation and verification).
  2. **Deferred Mobile Interfaces:** Justo Leadership, CP Sourcing Head, Finance, Compliance/Support, and Telecallers will **not** have dedicated screens in the CP App. Their workflows will be handled by configuring existing screens and dashboards within the core **Project Manthan (CRM) desktop portal**.
  3. **Buyer Flow Simplification:** The Buyer/Customer document upload journey will be a single, lightweight web link (SMS/WhatsApp triggered) that uploads files directly into the CRM, avoiding any mobile app registration for the customer.

---

### Debate 2: Mobile-First Admin Views vs. Operational Reality (UX vs. Architecture)
* **Contradiction:** The Journey Maps specify in-app screens for complex back-office roles like Finance processing payouts and Ops resolving lead conflicts. The UX review calls out that managing multi-column tables, RERA documents, and batch payments on a mobile screen is a major usability risk.
* **The Debate:** Architecture proposed native mobile views to ensure offline readiness for all roles. UX and Ops argued that back-office operations (Finance, Compliance, Ops) are always performed on desktop computers at Justo headquarters, and building mobile interfaces for these roles is a waste of capital.
* **Reconciliation Verdict:**
  1. **Back-Office is Desktop-Only:** All administrative, compliance, conflict resolution, and payout approval interfaces are classified as **out-of-scope for the mobile app**.
  2. **Manthan Extension:** These capabilities will be built as custom desktop modules/views in the existing Project Manthan CRM admin portal.
  3. **Mobile Notifications only:** RMs and Sourcing Heads will receive push notifications on mobile with deep links to the CRM desktop portal for critical items.

---

### Debate 3: Tech Stack Polyglot Risk (Architecture vs. Engineering)
* **Contradiction:** `ARCHITECTURE.md` proposes a backend API tier written in Rust (Axum framework) to achieve maximum performance. The Engineering review warns that introducing Rust to an engineering team that currently maintains a Node.js/NestJS stack (for Manthan) represents a severe delivery and maintenance risk.
* **The Debate:** Technical Architecture argued that Rust ensures sub-millisecond route speeds and ultra-low hosting costs ($4/month App Nodes). Engineering argued that the time spent training developers on Rust memory management, lifetimes, and compiling KMP-Rust bindings would break the pilot timeline.
* **Reconciliation Verdict:**
  1. **Consolidate on Node.js/NestJS:** The API compute tier framework is changed from Rust/Axum to **Node.js/NestJS**. This allows direct code reuse (types, schemas, validation logic) from the Manthan codebase and ensures the existing team can immediately build the endpoints.
  2. **Infrastructure Retention:** The load-balanced active-active VM deployment strategy via Traefik and Kamal 2 is retained. A NestJS backend easily handles 10–20 RPS on a $4 VPS, keeping infrastructure costs under $30/month.

---

### Debate 4: Offline Payout Visibility vs. Session Expiry (Security/Red Team vs. Journeys)
* **Contradiction:** The Journey Maps and PRD require CPs to have full, offline visibility into payout status and lead details. The Security and Red Team reviews highlight that if a CP employee is suspended, their local offline cache remains readable indefinitely, presenting a data leak risk.
* **The Debate:** Business wanted maximum offline capability to support CPs working in remote areas. Red Team argued that suspended agents holding active customer PII offline violates data security policies and the Indian DPDP Act.
* **Reconciliation Verdict:**
  1. **Local Encryption Mandate:** The local SQLite database must be encrypted using **SQLCipher**.
  2. **24-Hour TTL Session Keys:** The local encryption key must be rotated every 24 hours. The app must ping the API node to refresh the key. If the client remains offline for more than 24 hours, the local session expires, locking the cache until online authentication succeeds.
  3. **Remote Purge:** A remote "wipe" command must be sent via WebSocket when a user is suspended, executing a database deletion the moment the app detects a network connection.

---

### Debate 5: Brand Identity vs. Accessibility Standards (UX vs. Design System)
* **Contradiction:** The brand palette in `Justo_CP_App_UI_Stitch_Prompts.md` specifies lime green (`#b8ff4d`) as the primary brand color on light backgrounds. The UX review states this color fails the basic WCAG AA contrast ratio of 4.5:1, which would prevent UI generation sign-off and create readability issues in the field.
* **The Debate:** Branding stakeholders wanted to retain the vibrant, modern lime green color. UX and accessibility specialists argued that field agents operating in bright sunlight in Maharashtra will not be able to read white text or dark text on lime green buttons.
* **Reconciliation Verdict:**
  1. **Adjust Brand Palette:** The design system will adopt a **"Dark Lime / Forest Green"** or an adjusted teal color for primary interactive elements (buttons, active tabs) to satisfy WCAG AA contrast compliance.
  2. **Vibrant Accent Usage:** The lime green color (`#b8ff4d`) is restricted strictly to decorative, non-text accent borders, sync indicator dots, or icons accompanied by clear, accessible text labels in a high-contrast dark gray.

---

### Debate 6: Regulatory Compliance Bottleneck (Security vs. Business Outcomes)
* **Contradiction:** The Business Brief and BRD focus on frictionless CP onboarding and lead submission to maximize conversion. The Security review notes that the lack of explicit consent management, privacy notices, and data erasure rights violates the Indian Digital Personal Data Protection Act (DPDPA) 2023.
* **The Debate:** Business worried that adding consent checkboxes and privacy popups would increase onboarding friction and lower registration rates. Compliance insisted that launch without consent tracking presents a massive regulatory risk.
* **Reconciliation Verdict:**
  1. **Integrated Consent Gateway:** A single, frictionless consent screen will be built into the onboarding flow (one-tap approval of privacy terms).
  2. **Secure Consent Logger:** Every user approval must be logged in a backend database (`consent_logs`) recording timestamp, IP, and policy version.
  3. **Privacy Hashing:** Lead phone numbers and PII sent to analytics tracking systems (Mixpanel/PostHog) must be masked or hashed via SHA-256 server-side.

---

## 3. Reconciliation Matrix

| Area | Original Position (v0.5 Drafts) | PAC Verdict (Reconciled Baseline) | Target Artifact |
|---|---|---|---|
| **MVP Personas** | 11 Personas with mobile flows | **3 Personas** (RM, CP Owner, CP Employee) | `PRD` §6, `Journey Maps` §4 |
| **Back-Office UI** | Mobile app screens for Finance & Ops | **Desktop-only** in Project Manthan CRM | `Journey Maps` §5, `PRD` §11 |
| **API Backend** | Rust / Axum framework | **Node.js / NestJS** framework | `ARCHITECTURE.md` §2.2 |
| **Offline Cache** | Plain SQLite cache | **SQLCipher** with **24-hr TTL keys** | `ARCHITECTURE.md` §2.4, `PRD` §9 |
| **Interactive Color** | Lime green `#b8ff4d` on light bg | **High-contrast Teal/Dark Green** | `Stitch Prompts` Design System |
| **Data Privacy** | No explicit consent or erasure | **DPDPA Consent gateway & logs** | `PRD` §7.13, `BRD` §8 |

---

*Minutes approved by the Product Architecture Council Coordinator | 2026-06-14*
