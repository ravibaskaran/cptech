# Justo CP App: End-to-End Implementation Plan

This document outlines the logical phases for building the Justo CP App from scratch, leveraging the approved Lean Startup architecture (Rust, Kotlin Multiplatform, PowerSync, Postgres) and ignoring any previously built demo UIs. 

The plan is structured around the core personas and the sequential "trust loop" defined in the PRD.

## User Review Required

> [!IMPORTANT]
> Please review the proposed phases below. We will begin execution starting with **Phase 1: Foundation & Identity**, which sets up the application skeleton, database, and authentication. Do you agree with this phase breakdown?

## Open Questions

> [!NOTE]
> 1. **Authentication Provider:** Will we use a 3rd-party auth provider (like Firebase Auth, Supabase Auth, or Auth0) to issue JWTs, or should we build custom email/OTP authentication directly in the Rust backend?
> 2. **Design System:** Since we are ignoring the previous UI, do you have a preferred design system or aesthetic direction for the native UIs (e.g., Material 3 for Android, Human Interface Guidelines for iOS), or should I propose a premium, modern design language?

---

## Proposed Implementation Phases

### Phase 1: Foundation & Identity (The "Skeleton")
**Goal:** Establish the technical foundation, cross-platform architecture, and Role-Based Access Control (RBAC) to ensure secure routing and data access.
* **Personas:** All (Foundational)
* **Backend (Rust):** Setup Axum server, Postgres DB with `sqlx` migrations, PowerSync integration, JWT middleware, and Role models.
* **Client (KMP + Native):** Setup Kotlin Multiplatform shared module (Networking, SQLite/PowerSync local DB). Setup Android (Compose) and iOS (SwiftUI) shells.
* **UI/UX Focus:** Login screen, OTP/Password entry, Role selection (if multiple roles), and routing to empty role-specific home screens.

### Phase 2: CP Onboarding & Compliance
**Goal:** Enable CP Owners to register their firms, submit compliance documents, and allow Admins/RMs to approve and activate them.
* **Personas:** CP Owner, RM (Relationship Manager), Admin/Ops
* **Backend:** CP Firm & Employee schemas, Document upload endpoints (to Cloudflare R2), Approval state machine.
* **Client:** Offline-first draft for registration. Background upload queue for heavy documents (RERA, PAN, GST).
* **UI/UX Focus:** CP Registration wizard, Document upload UI with retry/resume states, RM dashboard for pending approvals, Admin compliance queue.

### Phase 3: Project Enablement & Collateral
**Goal:** Give activated CPs access to fresh project inventory and approved marketing materials.
* **Personas:** CP Owner, CP Employee, Developer/Project Team
* **Backend:** Project, Inventory, and Collateral schemas. Admin publishing APIs.
* **Client:** PowerSync offline caching of project data. Native sharing intents (WhatsApp, Email).
* **UI/UX Focus:** Project catalog list and details, filtered by role. Collateral share kit UI. Admin publishing dashboard.

### Phase 4: Lead Ownership & The Trust Loop
**Goal:** Allow CPs to register leads quickly, guaranteeing offline reliability and resolving duplicates fairly.
* **Personas:** CP Owner, CP Employee, Admin/Ops
* **Backend:** Lead ingestion, Duplicate detection logic, Lock expiry, Conflict resolution APIs.
* **Client:** Fast, phone-first lead capture form. Sync queue management (showing pending/synced/conflict states).
* **UI/UX Focus:** Lead registration form, Lead pipeline board, Conflict resolution screens (for Admin), Lead timeline/activity history.

### Phase 5: Site Visit Verification
**Goal:** Prove site visits to protect CP commissions and attribute walk-ins correctly.
* **Personas:** CP Employee, Developer/Site Team
* **Backend:** Visit scheduling, QR/OTP generation and validation, Geofence coordinate verification.
* **Client:** Location permission handling, QR scanner, Push notifications for visit updates via FCM/APNs.
* **UI/UX Focus:** Visit scheduling calendar, QR code display/scanner, Geofence check-in button, Visit outcome logging.

### Phase 6: Booking & Payout Transparency
**Goal:** Provide visibility into booking milestones and payout statuses without exposing sensitive finance data or losing finance control.
* **Personas:** CP Owner, Finance
* **Backend:** Booking milestone syncing (stubbed until Manthan integration), Payout ledger, Finance state machine (Maker-Checker).
* **Client:** Read-only payout ledger, Invoice upload.
* **UI/UX Focus:** CP Owner financial dashboard, Payout status timeline (Eligible -> Invoice Pending -> Approved -> Paid), Finance approval queue.

---

## Verification Plan

### Automated Tests
- **Backend:** Unit tests for Rust handlers, integration tests for Postgres queries, and RBAC permission checks.
- **Client:** Unit tests for KMP domain logic and PowerSync conflict resolution.

### Manual Verification
- Deploying the Rust backend to a staging environment (using Kamal).
- Running Android and iOS simulators to verify native UI routing, offline sync behaviors, and role-based access.
