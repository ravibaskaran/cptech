# Quality Assurance & Testing Review — Product Architecture Council

## Review Summary

The Quality Assurance and Testing strategy for the Justo CP App is in an early draft state. While the Universal Screen State Contract (§9, line 99) in the Journey Maps provides a testable framework for UI consistency, the PRD lacks requirement-level acceptance criteria for the majority of its functional requirements. Key gaps include: a lack of Gherkin scenarios for 60% of the requirement groups, the absence of a test strategy (unit, integration, E2E, performance, and security), undefined testing procedures for offline sync and data conflicts, and no device/OS testing matrix. Currently, the documentation is not QA-ready and cannot support an automated test-driven development (TDD) workflow.

---

## Strengths

### 1. Testable Universal Screen States [high]
**Source:** `Justo_CP_App_Journey_Maps.md` §9 (Common App Foundation, lines 99–103).

The Journey Maps define a strict UI contract: every screen must support six core states: Loading, Empty, Success/Fresh, Stale/Offline, Error, and Validation. This provides the QA team with a clear, repeatable checklist to verify on every single screen during UI inspections.

### 2. Functional Requirements are Uniquely Identified [high]
**Source:** `Justo_CP_App_PRD.md` §7 (Requirements, lines 354–539).

All functional requirements are assigned a unique ID (e.g., `PRD-FR-001` through `PRD-FR-094`). This unique identification is a prerequisite for requirement traceability mapping and allows QA to track test coverage in test management systems (e.g., Jira, TestRail).

---

## Critical Issues (Must Fix)

### C1. Missing Requirement-Level Acceptance Criteria [high]
**Source:** `Justo_CP_App_PRD.md` §7 (Requirements Tables).

The requirements tables in §7 contain "ID", "Requirement", "Priority", and "Goals" columns. They lack an **Acceptance Criteria** column.
* **Impact:** Without explicit acceptance criteria for each requirement, developers and QA engineers will interpret success differently. Testing will be subjective, leading to bugs slipping through to production and extended UAT cycles.
* **Recommendation:** Expand the requirements tables in §7 to include an "Acceptance Criteria" column or reference Gherkin scenarios for every "Must" priority requirement.

### C2. Incomplete Gherkin Scenarios for Core Features [high]
**Source:** `Justo_CP_App_PRD.md` §7 (Requirements, lines 354–539).

Gherkin syntax (`Given-When-Then`) is used for some requirement groups, but it is missing for approximately 60% of the functional requirements. Critical flows like geofenced site-visit proof, queued document uploads, and payout invoicing lack any testable scenarios.
* **Impact:** Automation QA engineers cannot write automated E2E tests (e.g., using Appium or Playwright) without clear Gherkin inputs, delaying automated regression runs.
* **Recommendation:** Write explicit Gherkin scenarios for the critical MVP features.
  * *Example for Geofenced Site Visit:*
    ```gherkin
    Scenario: CP employee checks in for site visit inside the geofence
      Given CP employee is at the physical project site
      And the mobile app shows the visit status is "Scheduled"
      When the CP employee clicks "Verify Check-in"
      And the device GPS location is within 100 meters of project coordinates
      Then the app verifies the location
      And changes the visit status to "Verified"
      And syncs the verification event to the backend
    ```

### C3. No Offline & Synchronization Testing Strategy [high]
**Source:** `ARCHITECTURE.md` §2.4 (Sync flows).

The system is highly dependent on offline-first capabilities via PowerSync and SQLDelight. However, there is no plan for how QA will test this behavior.
* **Impact:** Offline behavior is notorious for edge-case bugs (e.g., outbox queue blockages, clock skew mismatches, sync loops, database locks). Without a dedicated sync testing strategy, the app will crash in low-connectivity zones in Maharashtra.
* **Recommendation:** Define the offline testing protocol: (1) Network throttling and latency injection parameters (e.g., using Charles Proxy or Android Emulator network speed controls), (2) Outbox queue validation (verifying data survives app crash/kill mid-sync), (3) Local database state inspection tools (viewing local encrypted SQLite tables during tests).

---

## Major Issues (Should Fix)

### M1. Lack of a Device & OS Matrix [moderate]
**Source:** Entire document set.

The CP App is target-built for Android and iOS in Maharashtra, which has a highly fragmented Android device ecosystem (low-cost Xiaomi, Realme, Samsung devices with customized OS skins). The documents contain no device testing matrix.
* **Impact:** The app may run perfectly on developer Emulators but crash or suffer UI truncation on low-spec real-world devices in the field.
* **Recommendation:** Add a Device/OS Testing Matrix specifying the minimum support targets and core test pool. For example:
  * Android: OS 10 to 14 (focusing on low-RAM devices with MIUI, Realme UI).
  * iOS: iOS 16 and 17.
  * Include testing on actual physical devices (not just emulators) for geofencing and camera-based document uploads.

### M2. Undefined Performance and Load Testing Benchmarks [moderate]
**Source:** `ARCHITECTURE.md` §1 (Target Scale, line 8).

The architecture states a target scale of 10–20 RPS, but the PRD does not define performance benchmarks for the client.
* **Impact:** The app may load slowly over 3G/4G networks, frustrating CPs and causing them to disengage.
* **Recommendation:** Define performance benchmarks in the PRD:
  * Maximum local-first query render time: < 100ms.
  * Maximum payload sync duration on standard 4G connection: < 3 seconds for 10 leads.
  * Battery and data consumption limits per 8-hour shift.

---

## Minor Issues (Nice to Fix)

### N1. UAT Plan Lacks Field Test Parameters [low]
**Source:** `Justo_CP_App_PRD.md` §12 (Rollout Plan).

The rollout plan outlines alpha/beta releases but lacks parameters for UAT validation.
* **Impact:** Beta testing will yield generic feedback ("App is slow," "Button not working") rather than structured validation of user journeys.
* **Recommendation:** Define a 5-day structured field UAT process. Assign 3 RMs and 5 CP owners to execute specific tasks in the field (e.g., onboard an employee, submit a lead, complete a site visit) and verify that the system outputs match the expected results.

---

## Missing Items

| Missing Item | Severity | Why It Matters |
|---|---|---|
| Requirement-level acceptance criteria | Critical | Subjective testing and high bug counts |
| Gherkin scenarios for 60% of core MVP features | Critical | Blocks QA automation and E2E test scripting |
| Offline and sync test cases (latency/crash injection) | Critical | High risk of sync failures and data loss in field |
| Target device and OS testing matrix | Major | App crashes on low-spec Android devices in Maharashtra |
| Client-side performance benchmarks (render time, payload size) | Major | Slow offline UI response breaks the user experience |
| Structured UAT field validation scripts | Minor | Beta testers will not execute edge case validation |

---

## Recommendations

### R1. Complete the Gherkin Scenario Suite (Priority: High)
Add Gherkin scenarios to the PRD for all core MVP features, focusing on Lead Locks, Site Visits, and Payout Invoicing.

### R2. Define the Sync Testing Protocol (Priority: High)
Draft explicit test cases for testing network state transitions: Online -> Offline -> Online. Include test scenarios where the app process is terminated during a sync write loop.

### R3. Setup a Hardware Test Pool (Priority: Medium)
Acquire 2-3 low-cost Android physical devices widely used by real estate agents in Maharashtra to run manual UI tests, validating contrast and button responsiveness.

---

## Score (out of allocated points)

**Score: 2.2 / 5**

**Justification:**

| Dimension | Weight | Score | Notes |
|---|---|---|---|
| Acceptance criteria completeness | 30% | 4/10 | Requirements are uniquely ID'd; lack individual criteria |
| Gherkin scenarios availability | 30% | 3/10 | 60% of scenarios are missing for core MVP features |
| Offline & Sync testing readiness | 20% | 2/10 | Offline states defined, but test execution is omitted |
| Test strategy & Device matrix | 20% | 3/10 | No device matrix or performance benchmarks |

**Weighted Score: 2.2/5** — The requirements are well-structured, but the document lacks the testing specifications needed for a QA team to execute. Completing the Gherkin scenarios (C2) and detailing the offline test cases (C3) will raise this score significantly.

---

*Review completed: 2026-06-14 | Reviewer: QA & Testing Domain | Documents reviewed: Justo_CP_App_PRD.md §7, §12 (1093 lines), Justo_CP_App_Journey_Maps.md (407 lines), ARCHITECTURE.md §2 (155 lines), .planning/REQUIREMENTS.md (220 lines)*
