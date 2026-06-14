# Engineering Feasibility & Implementation Review — Product Architecture Council

## Review Summary

The engineering feasibility of the Justo CP App is heavily impacted by the selection of a highly complex, polyglot technology stack (Kotlin Multiplatform + Rust + PowerSync + Traefik + Postgres). While this stack offers industry-leading performance, cost-efficiency, and synchronization capabilities, it introduces severe development risks for a startup-stage team. The stack departs from the React Native approach proposed by the vendor (I9) and introduces Rust to a NestJS/Node.js team. Furthermore, the documents lack a developer onboarding guide, CI/CD pipeline definitions, API contract specifications, and database schema drafts. The implementation timeline is undefined, and the operational complexity of self-hosting replication engines (PowerSync) is under-estimated.

---

## Strengths

### 1. Unified Mobile Core via KMP [high]
**Source:** `ARCHITECTURE.md` §2.3 (System diagram client edge, line 42).

Using Kotlin Multiplatform (KMP) to write the core domain logic, local SQLite management, and sync handling once—while leaving the UI native (Compose Multiplatform / SwiftUI)—is a strong architectural pattern. It ensures 100% business logic consistency between Android and iOS apps, eliminating the "dual-codebase drift" common in startup mobile development.

### 2. High-Performance Compute Tier [high]
**Source:** `ARCHITECTURE.md` §2.2 (line 27).

Deploying a compiled language (Rust) for the API tier on commodity VPS instances guarantees sub-millisecond route execution and minimal memory usage. At 10–20 RPS, this API tier will run at less than 5% CPU utilization on a single app node, preventing the need for auto-scaling nodes.

### 3. Clear Deploy Orchestration via Kamal [high]
**Source:** `ARCHITECTURE.md` §2.5 (lines 97–103).

Choosing Kamal for container orchestration is highly practical. It removes the need for Kubernetes administration while providing zero-downtime rolling deploys Traefik configuration, and simple environment variables management. It represents a mature DevOps decision for small engineering teams.

---

## Critical Issues (Must Fix)

### C1. High Polyglot Friction: KMP + Rust + NestJS [high]
**Source:** `ARCHITECTURE.md` §2.2 (line 27), `STRUCTURE.md` (lines 19–23), `Justo_CP_App_PRD.md` §9 (Technical Notes, line 811).

The current engineering ecosystem for this project spans:
* Node.js/NestJS (existing Manthan codebase).
* Kotlin/Swift (KMP mobile core and native UI).
* Rust (new API compute tier).
* SQL (Postgres + SQLDelight SQLite).
* **Impact:** For a startup team, managing three distinct programming languages (TypeScript, Kotlin, Rust) across the backend and mobile tiers will severely slow down development velocity. A developer cannot easily work full-stack. Debugging cross-system integration issues will require specialized knowledge, creating single points of failure in the engineering team.
* **Recommendation:** Consolidate the backend stack. The API tier should be written in Node.js/TypeScript (reusing NestJS modules from Manthan) to allow the existing team to contribute immediately. Alternatively, if KMP is the mobile standard, the backend could use Kotlin/JVM (e.g., Ktor framework) to share model code directly between the mobile client and the backend via Kotlin serialization.

### C2. Missing Developer Environment Setup and Onboarding Guide [high]
**Source:** `STRUCTURE.md` (ALL sections) — [Missing evidence].

`STRUCTURE.md` maps the file layout but does not define how a developer boots the project locally.
* **Impact:** Onboarding new developers will take weeks of manual configuration, troubleshooting mismatched SDK versions, and resolving local database connection errors.
* **Recommendation:** Add a `DEVELOPER.md` guide at the root detailing: (1) Mandatory local tooling (JDK 17+, Android SDK, Xcode, Rustup toolchain), (2) A local docker-compose environment running PostgreSQL 16 and a local PowerSync replica, (3) Seeding scripts to populate dummy project and lead records in Postgres, (4) Direct commands to boottrapsTraefik and verify the local WebSocket sync.

### C3. No Mobile Compilation and CI/CD Pipeline Definitions [high]
**Source:** Entire document set — [Missing evidence].

Compiling and shipping KMP apps requires specific build agents: a macOS agent with Xcode to compile the iOS target, and an Android SDK runner to compile the Android target. The documents contain no CI/CD configuration guidelines.
* **Impact:** Releases will be built manually on developers' laptops, leading to the "works on my machine" syndrome, lack of automated build testing, and security risks associated with developers manually holding signing certificates.
* **Recommendation:** Define the CI/CD pipeline requirements: (1) Use GitHub Actions with macOS runners for iOS builds and Linux runners for Android, (2) Implement fastlane to automate code-signing (iOS provisioning profiles, Android keystores) and shipment to TestFlight and Google Play Console, (3) Mandate automated Linting and Unit test gates before merging PRs.

---

## Major Issues (Should Fix)

### M1. Under-Estimated PowerSync Operations Overhead [moderate]
**Source:** `ARCHITECTURE.md` §2.2 (line 28), §2.4 (lines 92–96).

The blueprint specifies self-hosting PowerSync.
* **Impact:** Running PowerSync in production requires establishing Postgres logical replication (logical decoding), managing replication slots, and monitoring the WAL queue size. If the WAL queue grows too large (due to a disconnected replica or laggy sync container), it will cause Postgres to exhaust disk space on the primary DB VM, bringing down the entire system.
* **Recommendation:** Include an operations section for PowerSync: (1) Enforce strict alerts on WAL replication lag and slot sizes, (2) Document a manual replication slot reset runbook, (3) Evaluate the feasibility of using PowerSync Cloud (managed) during the pilot phase to offload infrastructure management.

### M2. Undefined API Contract Strategy [moderate]
**Source:** `ARCHITECTURE.md` §2.3 (line 76).

The Mobile-to-Backend Command API is labeled "Command API (REST/gRPC)". The exact interface contract sharing protocol is not specified.
* **Impact:** Mismatched data contracts between mobile (KMP) and backend (Rust/NestJS) developers will result in integration failures and delayed sprints.
* **Recommendation:** Specify **OpenAPI/Swagger** as the contract tool. The backend must generate an `openapi.json` schema on compilation, and the mobile client must use OpenAPI generator tools to compile typed networking clients in KMP, preventing manual contract definition errors.

---

## Minor Issues (Nice to Fix)

### N1. Missing Database Migration Tooling [low]
**Source:** `ARCHITECTURE.md` §2.5 (HA and DB promotion notes).

While database failover is addressed, schema migration is not mentioned.
* **Impact:** Running schema updates in production will result in database downtime or synchronization failures if the mobile client expects fields that aren't yet migrated.
* **Recommendation:** Specify a database migration tool (e.g., `dbmate` or NestJS migrations) and mandate that all migrations must be backward-compatible (non-destructive) to allow older client versions to query the DB without crashing.

---

## Missing Items

| Missing Item | Severity | Why It Matters |
|---|---|---|
| Development team stack alignment analysis | Critical | Projects risk stall due to learning curves |
| Local developer environment onboarding guide (`DEVELOPER.md`) | Critical | Extended onboarding times for engineering hires |
| Mobile CI/CD pipeline and code-signing specifications | Critical | Slow, manual, and unsecure release compilation |
| PowerSync operations monitoring and WAL runbooks | Major | High risk of Postgres disk exhaustion due to WAL lag |
| API contract sharing tool (OpenAPI/Swagger) | Major | Handshake failures between mobile and API tiers |
| Database schema migration tool selection | Minor | Schema changes cause production database lockups |

---

## Recommendations

### R1. Align Backend Compute Tier with Node.js/TypeScript (Priority: High)
To maximize team velocity, change the API compute tier framework from Rust/Axum to Node.js/NestJS. NestJS can be deployed via Docker and Kamal just as easily, matches the team's existing expertise, and allows code reuse with Manthan modules.

### R2. Add a Local Developer Environment Docker Setup (Priority: High)
Create a docker-compose environment in the workspace that developers can launch with `docker-compose up` to run local Postgres and PowerSync instances for testing.

### R3. Outline the Mobile CI/CD Pipeline (Priority: Medium)
Integrate GitHub Actions workflows that compile the KMP app on push to `main` and leverage fastlane to automate beta distribution.

---

## Score (out of allocated points)

**Score: 3.8 / 8**

**Justification:**

| Dimension | Weight | Score | Notes |
|---|---|---|---|
| Tech stack feasibility & alignment | 30% | 4/10 | KMP is solid; Rust Axum represents high polyglot risk |
| Dev environment setup documentation | 20% | 1/10 | No local onboarding or boot steps provided |
| CI/CD and mobile release paths | 20% | 0/10 | No build pipelines, signing, or fastlane mentioned |
| PowerSync operational overhead | 15% | 6/10 | PowerSync integrated, but operations/WAL risks ignored |
| API contracts and DB migrations | 15% | 7/10 | Command API listed; no contract tools or migrations defined |

**Weighted Score: 3.8/8** — The core architecture is performant, but the engineering operations and developer experience are major gaps. Re-evaluating the Rust compute tier (C1), adding a local dev guide (C2), and defining CI/CD pipelines (C3) will raise this score dramatically.

---

*Review completed: 2026-06-14 | Reviewer: Engineering Feasibility Domain | Documents reviewed: ARCHITECTURE.md §2 (155 lines), STRUCTURE.md (103 lines), Justo_CP_App_PRD.md §9 (1093 lines), .planning/implementation_plan.md (5054 lines), .planning/ROADMAP.md (4916 lines)*
