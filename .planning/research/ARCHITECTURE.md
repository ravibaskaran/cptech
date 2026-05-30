# Research: BRD Architecture And Information Flow

## BRD Structure Pattern

The BRD should be structured as a decision document rather than a feature inventory.

1. Executive summary.
2. Business objectives and success metrics.
3. Evidence base and assumptions.
4. Current-state Manthan baseline.
5. Persona map.
6. Lifecycle maps.
7. Pain points and technology opportunities.
8. Capability requirements.
9. Vendor proposal mapping.
10. Gaps, risks, and decision questions.
11. MVP and phased recommendations.
12. Appendices: source documents, glossary, vendor checklist, open questions.

## Source-To-BRD Flow

1. `docs/` and `Justo_CP_App_Business_Brief.md` provide source evidence.
2. GSD `PROJECT.md` constrains the objective and out-of-scope boundaries.
3. Research artifacts identify standard expected sections and risks.
4. `REQUIREMENTS.md` defines what the BRD draft must contain.
5. `ROADMAP.md` sequences the work into coarse phases.
6. BRD draft becomes the first milestone output.

## Conceptual Business Architecture To Represent

### Existing Manthan Layer

- Leads, CP records, portal management, buyer portal, communication channels, KYC/payment/token flows, dashboards, workflows, site visits, and integrations. [high]

### CP App Layer

- CP mobile app and optional web/admin views for CP owner, CP employee, Justo RM, Justo finance, and admin personas. [high]

### CP Operating Layer

- CP sourcing, onboarding, compliance, activation, employee management, lead ownership, site-visit proof, booking visibility, payout trust, performance management, and support. [high]

### Governance Layer

- RERA/GST/PAN/bank/KYC validation, document expiry, audit logs, claim-safe collateral, consent, dispute evidence, role access, and finance approval. [high]

## Recommended Build Order For The BRD

1. Lock BRD purpose, audience, assumptions, and evidence base.
2. Baseline Manthan delivered/current scope.
3. Define personas and lifecycle maps.
4. Convert pain points into capability requirements.
5. Map vendors against required capabilities.
6. Write MVP/phase recommendations and decision checklist.

## Boundary Notes

- The BRD can describe integration needs and source-of-truth ownership, but should not specify low-level API contracts unless a later technical annexure is requested. [high]
- The BRD should separate "required in v1" from "strategic differentiator" and "deferred". [high]
