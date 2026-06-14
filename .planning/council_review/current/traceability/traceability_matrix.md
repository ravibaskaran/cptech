# Product Architecture Council (PAC) — Requirement Traceability Matrix

## 1. Executive Summary

This document establishes the end-to-end traceability matrix for the Justo CP App initiative. It maps the business capabilities defined in the Business Requirements Document (BRD) to the functional requirements in the Product Requirements Document (PRD), and correlates them with the persona journey steps in the Journey Maps. 

Crucially, it incorporates the **PAC Debate Verdicts** (reconciled in `debate_minutes.md`), showing the deferred boundaries (desktop portal reuse vs. mobile app build) and persona simplification rules (focusing on RM, CP Owner, and CP Employee).

---

## 2. Business Capability to PRD Traceability Matrix

This table maps the core business capabilities (defined in BRD Section 10) to the corresponding functional requirements in the PRD (Section 7), identifying the implementation status based on the PAC-approved MVP gate.

| BRD Capability | Description | PRD Functional Requirement ID | Implement Scope (Mobile App vs. Desktop CRM) | Status |
| :--- | :--- | :--- | :--- | :--- |
| **CP-CAP-001** | CP Firm Onboarding & Registration | `PRD-FR-007`, `PRD-FR-009`, `PRD-FR-011` | Mobile App UI Wizard (CP Owner / RM) | **Validated (MVP)** |
| **CP-CAP-002** | Compliance Doc Upload & Vault | `PRD-FR-008`, `PRD-FR-079` | Mobile App Upload + Local SQLite outbox | **Validated (MVP) - SQLCipher required** |
| **CP-CAP-003** | Compliance Review & Verification | `PRD-FR-010`, `PRD-FR-012`, `PRD-FR-082` | **Desktop CRM Portal only** (Compliance Role) | **Reconfigured (Deferred Mobile UI)** |
| **CP-CAP-004** | CP Employee Invite & Management | `PRD-FR-013`, `PRD-FR-014`, `PRD-FR-016` | Mobile App UI (CP Owner context) | **Validated (MVP)** |
| **CP-CAP-005** | CP Employee Exit & Reassignment | `PRD-FR-015`, `PRD-FR-016` | Mobile App (Reassign on delete) | **Validated (MVP)** |
| **CP-CAP-006** | Sourcing & RM Activity Logs | `PRD-FR-018`, `PRD-FR-019`, `PRD-FR-022` | Mobile App UI (RM Home screen) | **Validated (MVP)** |
| **CP-CAP-007** | Project Catalog & Access | `PRD-FR-023`, `PRD-FR-024`, `PRD-FR-025` | Mobile App UI (CP & RM) | **Validated (MVP)** |
| **CP-CAP-008** | Collateral Manager & Sharing | `PRD-FR-026`, `PRD-FR-027` | Mobile App UI (Share intent handler) | **Validated (MVP)** |
| **CP-CAP-009** | Collateral Publishing | `PRD-FR-028` | **Desktop CRM Portal only** (Admin Role) | **Reconfigured (Deferred Mobile UI)** |
| **CP-CAP-010** | Phone-First Lead Registration | `PRD-FR-029`, `PRD-FR-078` | Mobile App UI (CP & RM) | **Validated (MVP)** |
| **CP-CAP-011** | Lead Deduplication & Locking | `PRD-FR-030`, `PRD-FR-031`, `PRD-FR-032` | Mobile App + Backend normalized checks | **Validated (MVP) - Fuzzy matching added** |
| **CP-CAP-012** | Lead Conflict Resolution | `PRD-FR-033`, `PRD-FR-034` | **Desktop CRM Portal only** (Admin/Ops Role) | **Reconfigured (Deferred Mobile UI)** |
| **CP-CAP-013** | Lead Dispute Filing | `PRD-FR-035`, `PRD-FR-036` | Mobile App UI (CP Owner dispute file) | **Validated (MVP)** |
| **CP-CAP-014** | Geofenced Site Visit Check-in | `PRD-FR-044`, `PRD-FR-046`, `PRD-FR-047` | Mobile App UI (CP Employee GPS verification) | **Validated (MVP) - Multi-factor OTP/QR** |
| **CP-CAP-015** | Visit Outcome Logging | `PRD-FR-045`, `PRD-FR-048` | Mobile App UI (RM & CP Employee) | **Validated (MVP)** |
| **CP-CAP-016** | Payout Status Visibility | `PRD-FR-073`, `PRD-FR-074` | Mobile App UI (CP Owner read-only ledger) | **Validated (MVP) - 24-hr session TTL** |
| **CP-CAP-017** | Payout Processing & Verification | `PRD-FR-075`, `PRD-FR-076` | **Desktop CRM Portal only** (Finance Role) | **Reconfigured (Deferred Mobile UI)** |
| **CP-CAP-018** | Sourcing Leaderboard & Badges | `PRD-FR-080`, `PRD-FR-081` | Mobile App UI (RM and CP Owner gamification) | **Validated (MVP)** |
| **CP-CAP-019** | Leadership Analytics Dashboard | `PRD-FR-085`, `PRD-FR-086` | **Desktop CRM Portal only** (Leadership Role) | **Reconfigured (Deferred Mobile UI)** |

---

## 3. PRD Requirement to Journey Step Traceability Matrix

This table maps individual functional requirements (PRD-FR) to the specific step IDs and action logs in `Justo_CP_App_Journey_Maps.md`.

| PRD Requirement ID | Functional Requirement Description | Journey Map Section / Step ID | Target User Interface | Verification Target |
| :--- | :--- | :--- | :--- | :--- |
| `PRD-FR-001` | Sign in with single credential & role | CP Owner Journey - Step 1 | Login Screen | Authentication payload validation |
| `PRD-FR-002` | Role-based home screen routing | RM Journey - Step 1 | Home Dashboard | Navigation state check |
| `PRD-FR-005` | Block suspended role from local cache | RM / CP Common - Security | Local App Lock | 24-hour key expiration |
| `PRD-FR-007` | CP firm profile registration | CP Owner Onboarding - Step 2 | Reg Wizard | Form submission validation |
| `PRD-FR-008` | Document collection (PAN, RERA, GST) | CP Owner Onboarding - Step 3 | Upload Queue | File upload outbox retry |
| `PRD-FR-013` | Invite and import CP employees | CP Owner Team Mgr - Step 1 | Team List | Invitation email/SMS trigger |
| `PRD-FR-016` | Reassign leads of deactivated employee | CP Owner Team Mgr - Step 3 | Reassign dialog | DB lead owner mutation |
| `PRD-FR-023` | View assigned projects catalog | CP Employee Selling - Step 1 | Project Grid | PowerSync SQLite filter check |
| `PRD-FR-026` | Share approved collateral | CP Employee Selling - Step 3 | Collateral Tab | Native share sheet execution |
| `PRD-FR-029` | Phone-first lead registration | CP Employee Lead - Step 1 | Add Lead | Duplicate search trigger |
| `PRD-FR-031` | Return conflict/accepted states | CP Employee Lead - Step 2 | Status Modal | Deduplication response code |
| `PRD-FR-035` | File lead ownership dispute | CP Owner Disputes - Step 1 | Raise Dispute | File upload (evidence bundle) |
| `PRD-FR-044` | Schedule site visit | CP Employee Visit - Step 1 | Calendar Form | Schedule verification event |
| `PRD-FR-046` | Capture geofenced visit proof | CP Employee Visit - Step 3 | Check-in Screen | GPS coordinates vs. Mock location |
| `PRD-FR-073` | View payout ledger and status | CP Owner Payouts - Step 1 | Finance Tab | Read-only SQLCipher decrypt |
| `PRD-FR-079` | Queue file uploads locally | CP Owner Onboarding - Outbox | Upload Screen | Background job pause/resume |
| `PRD-FR-080` | Sourcing Leaderboard (RM / CP) | RM Dashboard - Step 2 | Leaderboard | Rank aggregation query |

---

## 4. PAC Scope Control Guardrails

### A. Strict Out-of-Scope Rule (No Code build)
The following requirements from `Justo_CP_App_PRD.md` are **formally deferred** from the Mobile Application codebase and will be implemented only within the **Project Manthan (CRM) desktop admin interface** to protect MVP timelines:
1. `PRD-FR-010` (CP Firm administrative approval workflows)
2. `PRD-FR-034` (Lead conflict resolution administrative override)
3. `PRD-FR-061` to `PRD-FR-065` (Telecaller lead queue management)
4. `PRD-FR-075` to `PRD-FR-077` (Finance payout check/verify state machine)
5. `PRD-FR-085` to `PRD-FR-086` (Cross-persona executive analytics dashboards)

### B. Mobile App Target Footprint
The final compiled mobile package (Kotlin Multiplatform shared binary + Jetpack Compose UI for Android + SwiftUI UI for iOS) will target:
* Android: support for Android 10+ (API level 29) on physical test devices.
* iOS: support for iOS 16+.
* Local storage: Encrypted SQLite database using SQLCipher.

---

*Traceability Matrix approved by the Product Architecture Council | 2026-06-14*
