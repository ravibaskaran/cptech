# Technical Architecture Review — Product Architecture Council

## Review Summary

The Technical Architecture Blueprint (`ARCHITECTURE.md`) presents a highly pragmatic, cost-disciplined, and modern architecture optimized for an early-stage startup. The choice of Kotlin Multiplatform (KMP) for the frontend, coupled with Traefik, active-active API nodes, and a primary/replica PostgreSQL database setup, provides excellent live redundancy for a target scale of 10–20 RPS at an estimated infrastructure cost of under $30/month. The GSD planning framework layers are clearly separated from the application architecture. However, the document has several critical gaps: it does not justify the introduction of a new language (Rust/Axum) into a Node.js/NestJS shop, lacks a detailed conflict resolution strategy for the offline-first write path, fails to define the authentication/identity flow, and lacks capacity, monitoring, and API contract specifications.

---

## Strengths

### 1. Excellent Cost-to-Resilience Ratio [high]
The proposed architecture (§2.2, lines 23–34) achieves high availability (HA) compute and a warm standby database replica for an estimated $24.00/month. For an early-stage pilot, avoiding expensive cloud-native managed services (like Amazon RDS Multi-AZ or EKS) while maintaining live redundancy (Active-Active Traefik/Axum and Postgres Streaming Replication) is an outstanding architectural decision that matches the budget constraints of a startup.

### 2. Enforceable NFRs at the Top [high]
In accordance with user feedback, the Non-Functional Requirements (§1, lines 3–10) are now placed at the very top of the blueprint. The inclusion of the critical guardrail that "No implementation in any phase should begin until journey screens are ready and the underlying architecture strictly supports these NFRs" (line 5) establishes a strong governance baseline for downstream engineering teams.

### 3. Clear System Topology and Data Flow [high]
The Mermaid system diagram (§2.3, lines 38–81) clearly maps out the system boundaries from the KMP client edge down to the data tier. The write path (§2.4, lines 85–90) using a Postgres-backed outbox with Tokio background workers executing `SKIP LOCKED` queries is an elegant, lightweight alternative to complex message brokers like Kafka or RabbitMQ.

### 4. Pragmatic Deployment and Database Failover [high]
The choice of Kamal (§2.5, lines 97–103) for zero-downtime container orchestration on bare VMs is highly appropriate for startups looking to avoid Kubernetes complexity. The database failover remediation plan (§2.6, lines 112–116) correctly identifies WAL lag risk and outlines a manual promotion strategy for the Replica DB that keeps downtime under 2 minutes.

---

## Critical Issues (Must Fix)

### C1. Missing Tech Stack Alignment and Team Feasibility Analysis [high]
**Source:** `ARCHITECTURE.md` §2.2 (Tech Stack Table, line 27), `STRUCTURE.md` (lines 19–23), `Justo_CP_App_PRD.md` §9 (Technical Notes, line 811).

The blueprint specifies Rust (Axum framework) for the API compute tier. However, the existing Manthan backend is written in Node.js/NestJS (`STRUCTURE.md` line 20, PRD line 811). 
* **Impact:** Introducing Rust creates a significant polyglot burden for a small startup team. Rust has a steep learning curve, slower development velocity for CRUD operations, and a smaller hiring pool compared to Node.js/TypeScript. Axum and Rust add operational overhead (e.g., compile times, lack of shared libraries with NestJS) that is hard to justify for a 10–20 RPS application.
* **Recommendation:** Re-evaluate the backend language choice. If the current team is proficient in Node.js/NestJS, the API compute tier should use Node.js/NestJS. NestJS can easily handle 10–20 RPS on a single $4 VPS. If performance/safety is the primary driver, Go is a faster-to-learn alternative. If Rust is retained, document the explicit team readiness plan, local compile times, and shared validation rules.

### C2. Incomplete Offline-First Conflict Resolution Strategy [high]
**Source:** `ARCHITECTURE.md` §1 (line 10), §2.4 (lines 85–90), `Justo_CP_App_PRD.md` §15 (lines 1073–1075).

The document promises a fully secure, offline-first client architecture using PowerSync (§1, line 10; §2.2, line 28). However:
* The write path (§2.4) assumes KMP POSTs a batch to the edge and the DB handles idempotency. It does not define how **data conflicts** (e.g., two agents editing the same lead info while offline, or an offline site visit submission colliding with an online lead lock expiry) are resolved.
* It does not specify client-side schema migrations (how local SQLite changes sync when the backend schema changes).
* **Impact:** Without a conflict resolution protocol, synchronization will result in silent data overwrites, broken lead attribution, or duplicate DB records, breaking the trust loop.
* **Recommendation:** Specify a conflict resolution matrix. Define the rules for write-conflicts (e.g., "Last-Write-Wins" vs. "Version-Based Merging" vs. "RM/Admin Manual Resolution"). Detail Traversal sync retry backoff limits and local DB schema migration strategies using SQLDelight.

### C3. Undefined Authentication & Token Flow Architecture [high]
**Source:** `ARCHITECTURE.md` §1 (Authentication, lines 7–8), `Justo_CP_App_PRD.md` §9 (Source-of-Truth Rules, line 819).

The NFR section states that authentication must support MS 365, Google ID, and Indian phone numbers (SMS/WhatsApp) using Zitadel or Logto. However:
* There is no technical architecture showing how the KMP client obtains, stores, and refreshes tokens.
* The synchronization engine (PowerSync) relies on JWT claims for Row-Level Security (RLS) replication (§2.4, line 94), but the token validation flow between Traefik, the identity provider, and PowerSync is not mapped.
* **Impact:** Authentication is a core security barrier. Leaving it as a deferred choice without a token flow blueprint introduces integration risk during Phase 2.
* **Recommendation:** Define the identity federation architecture. Create a sequence diagram showing how the mobile client logs in, how the custom backend maps federated identity to Manthan user records, and how the JWT is validated by PowerSync to enforce RLS.

---

## Major Issues (Should Fix)

### M1. Lack of a Capacity Plan [moderate]
**Source:** Entire document set.

The architecture lists the target scale as 10–20 RPS but provides no capacity sizing for:
* **Database storage growth:** Estimate of DB size growth per 1,000 active CPs (leads, logs, visits).
* **WAL log sizes:** Postgres WAL generation rate, affecting streaming replication and replication lag.
* **Object storage (Cloudflare R2):** Average size and count of document uploads (KYC PDF, photos) and local retention duration.
* **Impact:** Disk exhaustion is listed as a node crash risk (§2.6, line 115). Without capacity planning, a sudden influx of KYC document uploads or log accumulation can easily bring down a $4 App Node.
* **Recommendation:** Add a basic capacity sheet estimating database disk footprint (bytes per lead, visit, and audit log), WAL write throughput, and R2 object storage usage over a 12-month pilot.

### M2. Missing Monitoring and Observability Design [moderate]
**Source:** `ARCHITECTURE.md` §2.6 (lines 110–116).

The blueprint lists "monitor pg_stat_replication" as a remediation for WAL lag (line 114) and logs pruning for disk exhaustion, but does not define:
* The observability stack (e.g., Prometheus, Grafana, Traefik access logs, error tracking like Sentry).
* Health-check endpoints for the load balancer to determine node failure.
* Alert thresholds (e.g., DB replication lag > 5 seconds, disk space > 85%, API error rate > 2%).
* **Impact:** Without a monitoring design, hardware failures or replication lags will only be detected when users report app failures.
* **Recommendation:** Define a minimalist monitoring stack suitable for a startup budget (e.g., self-hosted Glances, basic Traefik metrics, or cheap SaaS integrations like Better Stack / Sentry) and outline Traefik health-check targets.

---

## Minor Issues (Nice to Fix)

### N1. Explicit API Contract Standard Is Missing [low]
**Source:** `ARCHITECTURE.md` §2.3 (Mermaid flow notes gRPC/REST, line 76).

The system topology diagram mentions "Command API (REST/gRPC)" in line 76. The document does not specify whether REST (JSON) or gRPC (Protocol Buffers) is the team's standard.
* **Impact:** Mobile and backend teams might implement mismatched API standards, delaying integration.
* **Recommendation:** Standardize on REST/JSON for the Command API to align with standard NestJS/Node.js web frameworks, and document OpenAPI/Swagger as the schema-sharing protocol.

---

## Missing Items

| Missing Item | Severity | Why It Matters |
|---|---|---|
| Tech stack integration justification (Rust vs. Node.js team) | Critical | High developer onboarding cost and risk of project delay |
| Offline-first conflict resolution protocol | Critical | Risk of silent data loss or overwritten records on sync |
| Authentication and JWT exchange flow | Critical | Essential for security validation and PowerSync RLS setup |
| Monitoring and observability architecture | Major | Necessary to detect VM failure, disk exhaustion, or replication lag |
| Capacity plan (Disk, WAL, R2 storage growth) | Major | Prevents DB node crash due to running out of space |
| Traefik health-check configurations | Minor | Traefik needs defined endpoints to execute failover |
| API interface specification standard (REST/OpenAPI) | Minor | Streamlines backend-frontend contract development |

---

## Recommendations

### R1. Align Backend Stack with Current Team Expertise (Priority: High)
Before beginning implementation, confirm the development team's backend language expertise. If the team already manages NestJS/Node.js for Manthan, reuse NestJS. If performance is critical, use Go due to its rapid onboarding timeline. Avoid Rust unless the team is already proficient in it.

### R2. Detail the PowerSync RLS Rules and JWT Exchange (Priority: High)
Draft the specific Row-Level Security (RLS) rules for Postgres that PowerSync will sync to SQLite. Define the token handshake process: Client -> Identity Provider (Logto/Zitadel) -> Token -> API -> Custom JWT with CP metadata -> PowerSync.

### R3. Define the Outbox Write Flow and Lead Lock States (Priority: High)
Flesh out the write queue logic. If an offline client writes a lead that is duplicate or conflicted, the local DB must support a `PENDING_SYNC` state. Define Traefik retries, and document the backend verification flow that transitions a lead from `PENDING_VERIFICATION` to `CONFLICT` or `LOCKED`.

### R4. Draft Traefik Health-Check and Observability Setup (Priority: Medium)
Specify Traefik's health check interval and timeout settings for the API Nodes. Document simple system cron jobs to prune docker logs and alert on VM disk capacity.

---

## Score (out of allocated points)

**Score: 10.5 / 15**

**Justification:**

| Dimension | Weight | Score | Notes |
|---|---|---|---|
| Appropriateness for scale (10-20 RPS) | 20% | 10/10 | Stack is lightweight, highly performant, and cost-effective |
| Tech stack justification | 20% | 5/10 | Rust Axum choice is unaligned with NestJS team expertise |
| Offline-first design completeness | 20% | 6/10 | Read sync path is clear; write path conflict resolution is undefined |
| HA and failover strategy | 20% | 9/10 | Clear active-active compute and manual replica promotion plan |
| Auth, capacity, and observability | 20% | 5/10 | Gaps in identity token flows, disk sizing, and metrics stack |

**Weighted Score: 10.5/15** — The architecture is highly cost-effective and structurally clean for a startup. Resolving the team stack alignment (C1), detailing offline conflict resolution (C2), and defining the authentication JWT flow (C3) will raise this to a near-perfect score.

---

*Review completed: 2026-06-14 | Reviewer: Technical Architecture Domain | Documents reviewed: ARCHITECTURE.md (155 lines), STRUCTURE.md (103 lines), Justo_CP_App_PRD.md §8-9 (1093 lines), .planning/research/ARCHITECTURE.md (60 lines), .planning/research/STACK.md (35 lines)*
