# Justo CP App Planning

## What This Is

This project creates the business and product planning artifacts for Justo's Channel Partner app and operating model. The app is intended to sit on top of Project Manthan's CRM and help Justo become a large regional channel partner in Maharashtra first, then expand across India.

The artifact sequence is: BRD -> PRD -> Product Roadmap/Phases -> Journey Maps -> UI Screen Specs/Prototype. The BRD must translate the existing Manthan scope, the Phase 1/2/2.4/3 SoWs, the Auum/TSPL/I9 vendor proposals, and CP market pain-point research into a clear business, persona, lifecycle, capability, and gap-analysis document that Justo can use for vendor alignment and product scoping.

## Core Value

The planning artifacts must make the CP network lifecycle explicit enough that Justo can scope, compare, design, and negotiate the CP app as a business operating system rather than as a generic mobile CRM add-on.

## Requirements

### Validated

(None yet - ship to validate)

### Active

- [ ] Produce a BRD draft grounded in the local Manthan proposal, delivered SoWs, and the three vendor proposals.
- [ ] Define all core personas and distinguish what each persona does inside the app versus outside the app.
- [ ] Deep-dive Justo's CP sourcing lifecycle from CP prospecting through approval, activation, performance management, retention, suspension, and offboarding.
- [ ] Deep-dive CP firm and CP employee lifecycles, including onboarding, roles, activity, lead ownership, performance, exit, and reassignment.
- [ ] Map Indian CP pain points to technology-addressable gaps, with special attention to Maharashtra/RERA, inventory trust, lead ownership, site-visit proof, commission transparency, and CP employee management.
- [ ] Compare the Auum, TSPL, and I9 proposals against the required CP lifecycle and technology capabilities.
- [ ] Identify what Project Manthan already covers, what must be configured or extended, and what should be added to any future SoW annexure.
- [ ] Produce a decision-useful structure that can support vendor negotiation, internal stakeholder review, and product scoping.
- [ ] Translate the approved BRD into a PRD with product requirements, roles, permissions, workflows, integrations, source-of-truth rules, non-functional requirements, and acceptance criteria.
- [ ] Convert the PRD into product delivery phases and capability sequencing.
- [ ] Produce journey maps aligned to the product phases.
- [ ] Produce UI screen specs/prototype guidance aligned to the product phases.

### Out of Scope

- Implementing the CP app - this project is for BRD, PRD, product roadmap, journey maps, and UI specs/prototype artifacts first.
- Selecting a final vendor without stakeholder review - the BRD can recommend evaluation criteria and gaps, but procurement needs a separate decision process.
- Treating AI voice/campaign automation as mandatory MVP scope - these are second-wave unless they directly support CP activation, conversion, or trust.
- Rewriting Project Manthan architecture - the BRD should identify integration and source-of-truth needs, not redesign Manthan end to end.

## Context

Justo wants to become a large retail/channel partner player in Maharashtra and later across India. The business hypothesis is that a CP app on Android and iOS can help attract, activate, and retain CPs by giving them better project discovery, lead registration, lead protection, site-visit management, booking visibility, and commission/payout transparency.

Project Manthan is the underlying CRM program delivered by Indexnine. The high-level Manthan proposal describes a broad real estate CRM covering lead management, qualification, sales pipeline tracking, inventory, project onboarding, marketing, billing/accounting, sourcing, corporate/developer/customer tech, and CP management.

Delivered or scoped Manthan phases already include platform scaffolding, RBAC/user management, lead CRUD/scoring, communication channels, lead-gen connectors, CP tagging/CRUD APIs, audit logs, import/export, smart lists, tasks, notifications, CP portal, buyer portal, white-label portal management, CP approval, referral links/QR/referral codes, KYC/payment/token flows, CP employee provisioning, Decentro/CIBIL/Zoho/KYC integrations, CP import/export, travel desk/pickup workflows, EOI/token/payment enhancements, WhatsApp integration, dashboards, bulk actions, custom fields, workflow management, walk-in experience, and activity logs.

The initial business brief concludes that the missing strategic layer is the full CP network lifecycle: CP sourcing, verification, activation, training, project enablement, lead ownership protection, site-visit proof, booking visibility, commission/payout transparency, performance management, renewal, and offboarding.

The three vendor proposals differ materially:

- I9/Indexnine has the strongest continuity with Manthan and the lowest integration ambiguity because its CP app proposal directly references existing Manthan modules.
- Auum has the broadest CP operating-system vision, including CP branding, AI assistant, microsites, marketing, workforce intelligence, analytics, lead locking, site visits, and commission workflows.
- TSPL/Triazine is AI-forward, especially around AI voice calling and microservices, but its proposal is less granular on Justo-specific CP lifecycle and Manthan integration.

External market review indicates recurring CP pain points around stale inventory, lead ownership disputes, delayed or opaque commission payouts, fragmented communication, RERA/KYC/GST compliance, low lead quality, poor CP employee controls, weak marketing attribution, weak site-visit proof, and buyer trust issues.

## Constraints

- **Source-of-truth**: The BRD must anchor claims in `Justo_CP_App_Business_Brief.md` and the documents under `docs/` - this prevents proposal drift.
- **Business stage**: First deliverable is a BRD draft - no app implementation or vendor contracting artifacts unless requested later.
- **Platform dependency**: The CP app is expected to sit on top of Project Manthan's CRM, so requirements must call out Manthan integration and source-of-truth ownership.
- **Market sequence**: Maharashtra comes first, later India expansion - RERA/MahaRERA, local CP behavior, and regional operations matter for v1.
- **Vendor evaluation**: Vendor gaps should be stated as gaps in written proposals, not as claims that a vendor cannot build a feature.
- **Privacy/compliance**: CP, buyer, KYC, call, and payout data require careful handling; the BRD should avoid storing or exposing secrets and should call out audit/compliance needs.
- **Workflow**: Use the canonical repo path `D:\onedrive\Onedrive - Justo\OneDrive - JUSTO REALFINTECH PRIVATE LIMITED\dev\cptech` when resolving project identity.

## Key Decisions

| Decision | Rationale | Outcome |
|----------|-----------|---------|
| Treat the CP app as a CP operating system, not only a mobile CRM shell | Justo's goal depends on CP acquisition, trust, lifecycle, payouts, and operating controls, not only lead entry | - Pending |
| Use I9 as the baseline integration comparator | I9 owns or understands the current Manthan implementation and submitted a Manthan-linked CP app proposal | - Pending |
| Keep AI voice/campaign automation as second-wave unless directly tied to activation/conversion/trust | The brief identifies onboarding, lead lock, inventory, site visit, booking visibility, and payout ledger as higher-confidence MVP needs | - Pending |
| Produce a BRD before PRD, roadmap, journey maps, and UI specs | Stakeholders need agreement on personas, lifecycle, scope, vendor gaps, and acceptance criteria first | - Pending |
| Use Vertical MVP for GSD roadmap structure | Each phase should produce a stakeholder-reviewable artifact in the sequence BRD -> PRD -> Product Roadmap/Phases -> Journey Maps -> UI Screen Specs/Prototype | - Pending |

## Evolution

This document evolves at phase transitions and milestone boundaries.

**After each phase transition** (via `$gsd-transition`):
1. Requirements invalidated? -> Move to Out of Scope with reason
2. Requirements validated? -> Move to Validated with phase reference
3. New requirements emerged? -> Add to Active
4. Decisions to log? -> Add to Key Decisions
5. "What This Is" still accurate? -> Update if drifted

**After each milestone** (via `$gsd-complete-milestone`):
1. Full review of all sections
2. Core Value check - still the right priority?
3. Audit Out of Scope - reasons still valid?
4. Update Context with current state

---
*Last updated: 2026-05-30 after artifact-chain goal update*
