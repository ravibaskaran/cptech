# Research: Stack And Source Materials

## Domain

Justo CP App BRD: a business requirements document for a Channel Partner mobile app and operating model that sits on top of Project Manthan CRM.

## Working Stack For BRD Production

- **Primary artifact format**: Markdown. [high]
  - Rationale: versionable, reviewable, diffable, and compatible with GSD planning artifacts.
- **Source corpus**: `docs/` proposals and SoWs plus `Justo_CP_App_Business_Brief.md`. [high]
  - Rationale: the BRD must not invent scope beyond the business brief and underlying proposal evidence.
- **Evidence style**: confidence-tagged claims and proposal-gap language. [high]
  - Rationale: stakeholder review needs separation between confirmed document facts, market inference, and open assumptions.
- **Traceability approach**: BRD sections should map to requirements IDs, personas, lifecycle stages, and vendor-gap rows. [high]
  - Rationale: this makes the document usable for SoW annexure drafting and vendor negotiation.

## Target Technical Ecosystem To Reflect In The BRD

- **Existing Manthan backend**: NestJS/Node.js, Postgres, Azure in later SoWs; original proposal also referenced ReactJS, NestJS, MongoDB/Postgres, AWS, Flutter. [high]
- **CP mobile proposal baseline**: React Native mobile approach in I9 CP Tech proposal. [high]
- **Existing operational integrations**: CTI, WhatsApp/SMS/email, Razorpay/payment flows, Decentro/CIBIL/KYC, Zoho Sign, AI chatbot hooks, CP import/export, lead-gen connectors, J Verse/site-visit hooks. [high]
- **Potential CP app capabilities**: lead lock, project catalog, site-visit proof, CP employee management, commission ledger, CP sourcing/RM dashboard, compliance document vault, CP branded sharing, AI/nudge/campaign capabilities. [high]

## What Not To Use As The BRD Baseline

- Do not treat vendor architecture proposals as accepted target architecture. [high]
- Do not treat AI voice/campaign automation as mandatory MVP. [high]
- Do not treat generic CRM feature lists as sufficient CP lifecycle coverage. [high]
- Do not write the BRD as a procurement verdict; write it as requirements and gap analysis. [high]

## Research Confidence

High for local-document facts; moderate for external market pattern synthesis; low for any vendor implementation ability not explicitly stated in their proposals.
