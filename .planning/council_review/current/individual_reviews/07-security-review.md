# Security & Compliance Review — Product Architecture Council

## Review Summary

The security and compliance aspects of the Justo CP App are partially addressed but show significant gaps under both modern security engineering principles and Indian regulatory frameworks (specifically DPDPA 2023 and MahaRERA guidelines). While the RBAC model is comprehensive (§9, lines 658–672) and basic NFRs for authentication are stated, there is no threat model or attack tree, local data-at-rest encryption for the offline-first SQLite database is undefined, API protection mechanisms are absent, and there are no explicit consent management or data retention/deletion protocols to comply with the DPDP Act. Security is currently treated as a checklist rather than a secure-by-design architectural tier.

---

## Strengths

### 1. Granular Role-Based Access Control (RBAC) [high]
**Source:** `Justo_CP_App_BRD_Draft.md` §9 (lines 658–672), `Justo_CP_App_PRD.md` §6 (Personas).

The Role and Permission Matrix (§9) is highly detailed, mapping 11 roles against 11 critical capabilities. It correctly isolates sensitive actions: only Finance can approve payouts, only CP Sourcing Head can approve firms, and CP Employees are restricted to their own profiles and assigned leads. The PRD reinforces this by requiring server-side enforcement (§9, line 819).

### 2. Multi-Provider Authentication Requirement [high]
**Source:** `ARCHITECTURE.md` §1 (Authentication, lines 7–8), `Justo_CP_App_PRD.md` §9 (line 819).

The NFRs mandate support for MS 365, Google ID, and Indian phone number-based login (via SMS/WhatsApp). Offloading authentication to standard providers (and preferring self-hosted solutions like Zitadel/Logto) reduces the risk of password database exposure and credential stuffing attacks.

### 3. Separation of Sensitive Financial Functions [high]
**Source:** `Justo_CP_App_BRD_Draft.md` §9 (lines 669–670).

The matrix separates payout approval from visibility. Finance holds the sole authority to "approve/reject" payouts (line 669), and CPs are restricted from viewing other firms' payout ledgers. This is a solid control against internal collusion and payout leakage.

---

## Critical Issues (Must Fix)

### C1. Non-Compliance with the Indian Digital Personal Data Protection Act (DPDPA) 2023 [high]
**Source:** Entire document set — [Missing evidence].

The CP App handles significant amounts of Personal Identifiable Information (PII) — including CP Owner PAN, Aadhaar, bank details, and Buyer/Customer names, phone numbers, and loan documents. 
* **Impact:** Under DPDPA 2023, collecting and processing PII without explicit, itemized, and withdrawable consent, or failing to provide data deletion ("right to be forgotten") mechanisms, carries severe financial penalties (up to ₹250 crore). The current documents lack any requirement for consent loggers, privacy notice UI, or account deletion flows.
* **Recommendation:** Add a mandatory compliance section in the PRD detailing: (1) An explicit consent gateway during CP onboarding and Buyer document upload, (2) A secure Consent Log Store (recording timestamp, version of notice, and scope of consent), (3) An "Account Deletion / Right to Erasure" workflow that purges or anonymizes PII from client cache and backend databases upon offboarding (subject to RERA record-retention laws).

### C2. Lack of Offline Local Cache Encryption [high]
**Source:** `ARCHITECTURE.md` §1 (line 10), §2.3 (Topology diagram, line 43).

The client edge uses local SQLite database tables via SQLDelight to support offline-first usage. 
* **Impact:** CP agents and RMs will have cached lead lists, PII, and site visit logs stored locally on their mobile devices. If a phone is lost, stolen, or compromised, a plain SQLite database is trivial to extract, resulting in data exfiltration.
* **Recommendation:** Mandate that the local SQLite database must be encrypted at rest using **SQLCipher** (integrated via SQLDelight driver). The encryption key must be securely generated and stored using the device's hardware keystore (Android Keystore / iOS Keychain), tied to user authentication, and never written to plain storage.

### C3. Opaque Payout Security and Lack of Bank Validation [high]
**Source:** `Justo_CP_App_BRD_Draft.md` §8.5 (Finance Journey), `Justo_CP_App_PRD.md` §7.13 (payout visibility, lines 509–520).

The documents define workflows for uploading invoices and triggering payouts but lack technical security controls around the bank account registration and payout trigger mechanisms.
* **Impact:** High risk of payout fraud. If an RM's credentials are compromised, they could modify a CP's registered bank account details in the database, redirecting payments. Lacking a "maker-checker" double-authorization for bank changes will result in direct financial loss.
* **Recommendation:** Implement: (1) **Penny Drop Verification:** Integrating a service (e.g., Decentro) to deposit ₹1 and verify that the bank account name matches the RERA/PAN certificate name automatically, (2) **Dual Authorization (Maker-Checker):** Any addition or modification of bank details by an RM or CP Owner must remain in a `PENDING_VERIFICATION` state until validated by a separate Compliance/Ops administrator, (3) OTP-based confirmation sent to the registered CP Owner phone for all banking modifications.

---

## Major Issues (Should Fix)

### M1. Vulnerability to API Manipulation and Weak Rate Limiting [moderate]
**Source:** `ARCHITECTURE.md` §2.2 (Traefik LB, line 26), §2.3 (lines 76–77).

While Cloudflare DNS provides basic DDoS protection, there are no defined API gateway security policies.
* **Impact:** CPs or external actors can reverse-engineer the API endpoints and bypass the client application to scrape the project catalog, automate lead submissions, or brute-force OTP logins.
* **Recommendation:** Specify API gateway policies: (1) strict rate limiting (e.g., max 5 OTP requests per minute per IP, max 60 API reads per minute per user token), (2) request signature validation, (3) Web Application Firewall (WAF) rules on Cloudflare to block automated scraping.

### M2. Unsecure KYC and Document Upload Pipeline [moderate]
**Source:** `Justo_CP_App_PRD.md` §7.13 (PRD-FR-079, line 519), `ARCHITECTURE.md` §2.3 (R2 direct upload, line 77).

The client edge uploads files directly to Cloudflare R2 object storage.
* **Impact:** Allowing direct client upload to R2 without strict validation opens up vectors for uploading malware (e.g., PDF exploits) that could infect administrative terminals reviewing KYC documents.
* **Recommendation:** Implement secure upload protocols: (1) Clients must request short-lived (e.g., 5-minute expiry) pre-signed upload URLs from the API Node, (2) The upload endpoint must restrict mime-types to PDF and image formats (JPEG/PNG) and enforce a 5MB size ceiling, (3) An asynchronous antivirus scanning container must scan all uploaded documents in R2 before they are accessible to Compliance/Admin users.

---

## Minor Issues (Nice to Fix)

### N1. Audit Trail Lacks Security Log Specification [low]
**Source:** `Justo_CP_App_PRD.md` §9 (Source-of-Truth Rules, line 819).

The requirement for an audit trail is directionally noted, but there is no technical definition of what events must be logged.
* **Impact:** Security incidents (failed login attempts, RBAC policy bypasses, bank detail overrides) will lack the forensic logs needed for post-mortem analysis.
* **Recommendation:** Create a "Security Log Schema" in the PRD. The system must log: timestamp, actor ID, IP address, device fingerprint, event type (e.g., `AUTH_FAILURE`, `BANK_MODIFIED`, `PAYOUT_APPROVED`), old value, new value, and success/failure outcome. Security logs must be write-once (append-only) and shipped to a secure, separate log aggregation service.

---

## Missing Items

| Missing Item | Severity | Why It Matters |
|---|---|---|
| DPDPA 2023 Consent and Erasure requirements | Critical | Severe regulatory penalties (up to ₹250Cr) for non-compliance |
| SQLite local database encryption design | Critical | Stolen mobile devices expose cached customer PII |
| Bank account validation and dual-authorization | Critical | Direct risk of financial fraud and redirected payouts |
| API Rate limiting and scraping defense guidelines | Major | Protects project inventory and lead database from scraping |
| Document upload virus scanner integration | Major | Prevents malware uploads from infecting admin users |
| Append-only security event audit log | Minor | Crucial for forensic incident response and audit compliance |

---

## Recommendations

### R1. Mandate DPDPA Compliance (Priority: Immediate)
Integrate explicit consent checkboxes on all customer and agent facing screens where PII is entered. Establish a secure audit trail of consent and include a "Delete My Account" option in the CP Owner mobile settings that triggers a database purge.

### R2. Secure the Local Storage (Priority: Immediate)
Update the client-side architecture specification to require SQLCipher for SQLite storage. Secure the encryption key using iOS Keychain and Android KeyStore.

### R3. Add Payout Guardrails (Priority: Before Phase 2)
Incorporate Decentro penny-drop verification for CP bank details and enforce a strict administrative maker-checker workflow for account verification before any payouts are scheduled.

---

## Score (out of allocated points)

**Score: 5.5 / 10**

**Justification:**

| Dimension | Weight | Score | Notes |
|---|---|---|---|
| RBAC completeness and enforcement | 30% | 8/10 | Well-detailed matrix, but lacks implementation details |
| Secure auth flows | 20% | 7/10 | Good provider diversity; lacks JWT exchange design |
| Data-at-rest & in-transit security | 20% | 4/10 | HTTPS is assumed; local cache encryption is omitted |
| Regulatory compliance (DPDPA/RERA) | 20% | 2/10 | DPDPA consent and deletion flows are completely absent |
| Audit trail and threat model | 10% | 3/10 | General audit needs noted, but security log specification is missing |

**Weighted Score: 5.5/10** — While the user-level permission scoping is strong, the absence of local data encryption, bank details validation, and DPDPA compliance represents a severe security liability. Resolving Critical Issues C1-C3 is mandatory before UI generation or development sign-off.

---

*Review completed: 2026-06-14 | Reviewer: Security & Compliance Domain | Documents reviewed: ARCHITECTURE.md §1-2 (155 lines), Justo_CP_App_PRD.md §7.13, §9 (1093 lines), Justo_CP_App_BRD_Draft.md §9, §10 (850 lines), Justo_CP_App_Journey_Maps.md (407 lines)*
