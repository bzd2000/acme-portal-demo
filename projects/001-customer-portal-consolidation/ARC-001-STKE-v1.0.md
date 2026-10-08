# Stakeholder Drivers & Goals Analysis: One Acme Customer Portal

> **Template Origin**: Official | **ArcKit Version**: 6.17.5 | **Command**: `/arckit:stakeholders`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-STKE-v1.0 |
| **Document Type** | Stakeholder Drivers & Goals Analysis |
| **Project** | One Acme Customer Portal (Project 001) |
| **Classification** | Confidential |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-10-08 |
| **Last Modified** | 2026-10-08 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2027-01-08 |
| **Owner** | Enterprise Architecture team, for Annelies Claes (COO, Programme Sponsor) |
| **Reviewed By** | [PENDING] |
| **Approved By** | [PENDING] |
| **Distribution** | Programme steering committee; Architecture Board; named stakeholders in this document |

> **Classification note**: This document uses the Acme data classification scheme (Public / Internal / Confidential / Strictly Confidential). It is marked **Confidential** because it records named individuals' concerns and an assessment of how ready each person is for change. It also quotes customer and security figures from sources that handle customer personal data and security logs [AIP-C5]. Do not share it beyond the distribution list.

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-10-08 | ArcKit AI | Initial creation from `/arckit:stakeholders` command | PENDING | PENDING |

---

## Executive Summary

### Purpose

This document identifies the key stakeholders of the One Acme Customer Portal programme and their underlying drivers (motivations, concerns and pressures). It shows how those drivers become goals and which measurable outcomes will satisfy them. It links individual concerns to programme success measures, so that requirements, design decisions and the business case can be prioritised against what stakeholders actually need.

### Key Findings

Stakeholders strongly agree on the destination: one portal, one login and one customer record by 31 December 2028 [PM-C1]. Identity is the strongest point of agreement, because the COO, CIO, CISO, DPO and Head of Customer Service all gain from a single hardened customer identity. The tensions are about **timing and money**:

- **Portal B timeline**: Portal B must be migrated by 30 June 2027 [PM-C6], only three months after the platform is chosen [PM-C4].
- **Payback**: run-cost savings alone (at least EUR 458,500 a year) do not pay back a EUR 4–6M investment within the CFO's 4-year limit [SI-C5]. Contact-centre benefits must be counted and evidenced.
- **Portal A security**: Portal A has no MFA and will not be migrated until mid-2028 [PI-C4] [PM-C7], which is after the NIS2 CyberFundamentals deadline at end 2027 [SI-C14].

The portal owners support the goal but fear losing features their customers depend on (returns, EDI order upload, and temperature alerts and certificates) [SI-C19].

### Critical Success Factors

- **Portal B migrated on time.** The Liferay hosting contract ends on 30 June 2027 [PI-C9], and a firm fallback is needed if the new platform is not ready.
- **No loss of compliance-critical features.** Pharma customers' audit-proof temperature records are non-negotiable [SI-C20], and business customers' EDI order upload must keep working.
- **Evidenced benefits.** Measured reductions in "where is my shipment?" calls, handling time and run cost must support a payback of 4 years or less.
- **Security and privacy built in from the first release.** This means one hardened login with MFA, central security logging, EU-only support access, and data subject requests answered within one month.
- **All migrations and switch-offs outside the peak freeze** (15 October to 10 January) [AIP-C1], with a clear go/no-go for each business unit [SI-C3].

### Stakeholder Alignment Score

**Overall Alignment**: MEDIUM

Alignment on the objective is HIGH: every interviewed stakeholder supports one portal and one customer record. Alignment on delivery is MEDIUM because of six open conflicts (see Conflict Analysis):

- the timeline for Portal B
- payback against the investment envelope
- interim security on Portal A
- extending TrackBox while its support access is outside the EU
- a single agent view versus showing agents the minimum personal data
- keeping every existing feature versus a standard SaaS or low-code platform

All six can be resolved, but decisions are needed during discovery (by 31 March 2027).

---

## Stakeholder Identification

### Internal Stakeholders

| Stakeholder | Role/Department | Influence | Interest | Engagement Strategy |
|-------------|----------------|-----------|----------|---------------------|
| Annelies Claes | COO, Programme Sponsor [PM-C13] | HIGH | HIGH | Chairs the monthly steering committee; owns the go/no-go for each business unit |
| Marc Dubois | CFO | HIGH | HIGH | Business case owner; checkpoints at discovery close and at each funding release |
| Sofie Peeters | CIO, Chair of Architecture Board | HIGH | HIGH | Design authority through the Architecture Board; platform selection |
| Pieter Janssens | CISO | HIGH | MEDIUM | Security gate at each release; NIS2 and CyberFundamentals alignment |
| Isabelle Martin | DPO | HIGH | MEDIUM | DPIA, supplier data processing agreements, design of the agent data view |
| Nathalie Lambert | Head of Customer Service | MEDIUM | HIGH | Co-designs the agent view; owns contact-centre benefit measures |
| Koen De Smet | Portal A owner (Acme Parcel) | MEDIUM | HIGH | Feature-parity workshops; go/no-go input for Wave 3 |
| Julie Leclercq | Portal B owner (Brabant Freight) | MEDIUM | HIGH | Early migration partner; go/no-go input for Wave 1 |
| Tom Wouters | Portal C owner (Flanders Cold Chain) | MEDIUM | HIGH | Defines cold-chain compliance requirements; go/no-go input for Wave 2 |
| Architecture Board | Design authority [PM-C13] | HIGH | MEDIUM | Monthly review; decisions recorded as ADRs |
| Executive Committee | Approved the mandate on 15 September 2026 | HIGH | LOW | Quarterly summary through the Sponsor; approves changes to the envelope |
| Contact-centre agents | Customer Service | LOW | HIGH | User research, pilot group for the agent view, training |
| IT Operations | Runs Portal A in Ghent and supplier contracts | MEDIUM | MEDIUM | Transition planning, run books, switch-off and data centre exit |

### External Stakeholders

| Stakeholder | Organization | Relationship | Influence | Interest |
|-------------|--------------|--------------|-----------|----------|
| Business customers | About 9,500 business accounts across the three portals, of which 1,800 customers use more than one portal [PI-C1] [ACP-C1] | Beneficiary | MEDIUM | HIGH |
| Pharma and food cold-chain customers | Flanders Cold Chain customers subject to GDP and HACCP [PI-C6] | Beneficiary; their audit requirements set Acme's compliance needs | HIGH | HIGH |
| Consumers | 150,000 registered Portal A users [PI-C1] | Beneficiary | LOW | MEDIUM |
| Belgian Data Protection Authority (GBA/APD) | Regulator | GDPR oversight | HIGH | LOW |
| Centre for Cybersecurity Belgium (CCB) | Regulator | NIS2 oversight; owner of the CyberFundamentals framework | HIGH | LOW |
| TrackBox vendor | SaaS supplier for Portal C [PI-C3] | Incumbent supplier; contract renewal due 31 March 2027 | MEDIUM | HIGH |
| German hosting provider | Hosts Portal B on Liferay 6.2 [PI-C3] | Incumbent supplier; contract ends 30 June 2027 | LOW | MEDIUM |
| Future platform and implementation suppliers | To be selected by 31 March 2027 [PM-C4] | Supplier | MEDIUM | HIGH |

### Programme Governance Roles

> Acme Logistics NV is a Belgian private company, not a UK Government body. The UK GovS 005 and GovS 007 role tables do not apply. The equivalent Acme roles are shown below.

| Role | Holder | Responsibility | Power/Interest | Engagement Strategy |
|------|--------|---------------|----------------|---------------------|
| Programme Sponsor | Annelies Claes (COO) | Accountable for the programme's outcomes and per-business-unit go/no-go | HIGH / HIGH | Manage Closely: steering committee, decision escalation |
| Design Authority | Architecture Board (chair: Sofie Peeters, CIO) | Architecture decisions recorded as ADRs | HIGH / MEDIUM | Keep Satisfied: monthly Board, ADR reviews |
| Business case owner | Marc Dubois (CFO) | Funding, payback, supplier contracts | HIGH / HIGH | Manage Closely: funding gates |
| Security risk owner | Pieter Janssens (CISO) | Security risk acceptance, NIS2 evidence | HIGH / MEDIUM | Keep Satisfied: security gates |
| Data protection adviser | Isabelle Martin (DPO) | DPIA advice, data subject rights, supplier data agreements | HIGH / MEDIUM | Keep Satisfied: DPIA gates |
| Programme Product Owner | Not yet appointed (recommended appointment by end 2026) | Owns the backlog and feature retain/drop decisions | MEDIUM / HIGH | Keep Informed, day to day |

### Stakeholder Power-Interest Grid

```text
                          INTEREST
              Low                         High
        ┌─────────────────────┬─────────────────────────┐
        │                     │                         │
        │   KEEP SATISFIED    │   MANAGE CLOSELY        │
   High │                     │                         │
        │  • CISO             │  • COO (Sponsor)        │
        │  • DPO              │  • CFO                  │
        │  • Architecture Bd  │  • CIO                  │
 P      │  • Executive Cttee  │  • Pharma/food cold-    │
 O      │  • GBA/APD, CCB     │    chain customers      │
 W      ├─────────────────────┼─────────────────────────┤
 E      │                     │                         │
 R      │      MONITOR        │    KEEP INFORMED        │
        │                     │                         │
   Low  │  • German hosting   │  • Head of Cust. Service│
        │    provider         │  • Portal owners A/B/C  │
        │                     │  • Contact-centre agents│
        │                     │  • Business customers   │
        │                     │  • Consumers            │
        │                     │  • IT Operations        │
        │                     │  • TrackBox vendor      │
        └─────────────────────┴─────────────────────────┘
```

| Stakeholder | Power | Interest | Quadrant | Engagement Strategy |
|-------------|-------|----------|----------|---------------------|
| Annelies Claes (COO, Sponsor) | HIGH | HIGH | Manage Closely | Monthly steering committee plus fortnightly sponsor 1:1 |
| Marc Dubois (CFO) | HIGH | HIGH | Manage Closely | Business case checkpoints; monthly benefits dashboard |
| Sofie Peeters (CIO) | HIGH | HIGH | Manage Closely | Architecture Board; weekly programme sync during discovery |
| Pharma and food cold-chain customers | HIGH | HIGH | Manage Closely | Customer advisory group; validation of compliance evidence before Wave 2 |
| Pieter Janssens (CISO) | HIGH | MEDIUM | Keep Satisfied | Security gate at each release; monthly NIS2 alignment |
| Isabelle Martin (DPO) | HIGH | MEDIUM | Keep Satisfied | DPIA review at discovery close and before each wave |
| Architecture Board | HIGH | MEDIUM | Keep Satisfied | Monthly ADR submissions |
| Executive Committee | HIGH | LOW | Keep Satisfied | Quarterly summary through the Sponsor |
| GBA/APD and CCB | HIGH | LOW | Keep Satisfied | No direct engagement; keep evidence ready for audit |
| Nathalie Lambert (Head of Customer Service) | MEDIUM | HIGH | Keep Informed (active) | Co-design partner for the agent view; monthly benefits review |
| Portal owners (A, B, C) | MEDIUM | HIGH | Keep Informed (active) | Fortnightly feature-parity workshops; go/no-go input |
| Contact-centre agents | LOW | HIGH | Keep Informed | User research, pilot cohort, training |
| Business customers | MEDIUM | HIGH | Keep Informed | Migration communications in NL/FR/EN; beta programme |
| Consumers | LOW | MEDIUM | Keep Informed | In-portal notices and email before migration |
| IT Operations | MEDIUM | MEDIUM | Keep Informed | Transition and switch-off planning |
| TrackBox vendor | MEDIUM | HIGH | Keep Informed | Commercial negotiation by 31 December 2026 |
| German hosting provider | LOW | MEDIUM | Monitor | Contract notice and possible short extension |

**Quadrant Interpretation:**

- **Manage Closely** (High Power, High Interest): Key decision-makers requiring active engagement
- **Keep Satisfied** (High Power, Low or Medium Interest): Influential stakeholders needing periodic updates and clear gates
- **Keep Informed** (Low or Medium Power, High Interest): Engaged stakeholders needing regular communication. The Head of Customer Service and portal owners are managed actively because the benefits and feature parity depend on them
- **Monitor** (Low Power, Low or Medium Interest): Minimal engagement required

---

## Stakeholder Drivers Analysis

### SD-1: Annelies Claes (COO) - Present One Acme to Customers

**Stakeholder**: Annelies Claes, COO and Programme Sponsor

**Driver Category**: STRATEGIC

**Driver Statement**: "Customers see three companies. By the end of 2028 they should see one Acme." [SI-C1]

**Context & Background**: Acme grew by acquiring Brabant Freight (2021) and Flanders Cold Chain (2023), and each business unit kept its own portal. 1,800 business customers use more than one portal [ACP-C1]. As Sponsor, Annelies Claes is personally accountable to the Executive Committee for the mandate the committee approved on 15 September 2026 [PM-C13].

**Driver Intensity**: CRITICAL

**Enablers** (What would help):

- Early, visible proof of progress (Portal B migrated in 2027)
- A clear go/no-go decision for each business unit [SI-C3]
- One brand and one login introduced before full feature consolidation

**Blockers** (What would hinder):

- Portal owners defending separate business-unit experiences
- Slipping milestones that push migrations into the peak freeze

**Related Stakeholders**:

- Aligned: CIO (SD-6), Head of Customer Service (SD-7), business customers (SD-13)
- Potential tension: portal owners (SD-11)

---

### SD-2: Annelies Claes (COO) - Protect Peak Operations

**Stakeholder**: Annelies Claes, COO

**Driver Category**: RISK

**Driver Statement**: No migrations during the peak season [SI-C2], and a controlled go/no-go for each business unit [SI-C3].

**Context & Background**: Parcel volumes rise 2.3 times between mid-October and early January [ACP-C2], and group policy freezes go-lives and migrations from 15 October to 10 January [AIP-C1]. A failed migration at peak would hit revenue and the Acme brand at the moment customers are watching most closely.

**Driver Intensity**: HIGH

**Enablers** (What would help):

- Migration waves planned for February to September
- Rehearsed migrations with rollback

**Blockers** (What would hinder):

- The mandate's final switch-off date (31 December 2028) [PM-C7] falls inside the 2028/29 peak freeze
- Compressed timelines after discovery

**Related Stakeholders**:

- Aligned: Head of Customer Service, IT Operations
- Potential tension: CFO (SD-4), who wants legacy costs stopped as early as possible

---

### SD-3: Marc Dubois (CFO) - Cut Portal Run Cost by at Least 35%

**Stakeholder**: Marc Dubois, CFO

**Driver Category**: FINANCIAL

**Driver Statement**: Run cost of the three portals (EUR 1.31M a year) must drop by at least 35% [SI-C4] [PM-C8].

**Context & Background**: The three portals cost EUR 610,000 (A), EUR 420,000 (B) and EUR 280,000 (C) a year [PI-C8]. The group target is a 20% cut in IT run cost by 2029, and the portals are a visible contributor to that target.

**Driver Intensity**: CRITICAL

**Enablers** (What would help):

- A SaaS or low-code platform with predictable subscription cost
- Fast switch-off of legacy portals after each wave

**Blockers** (What would hinder):

- Long double-running of old and new platforms
- Customisation that raises the new platform's run cost

**Related Stakeholders**:

- Aligned: CIO (SD-6)
- Potential tension: portal owners (SD-11), whose requests to keep every feature add cost

---

### SD-4: Marc Dubois (CFO) - Payback Within 4 Years and No Long TrackBox Lock-In

**Stakeholder**: Marc Dubois, CFO

**Driver Category**: FINANCIAL

**Driver Statement**: Payback within 4 years. A discovery budget of EUR 350,000 is approved, and the total envelope is EUR 4–6M (indicative) [SI-C5]. Marc Dubois does not want to renew TrackBox for another 3 years if it can be avoided [SI-C6].

**Context & Background**: The TrackBox subscription renews on 31 March 2027 for 3 years [PI-C9]. The mandate requires a decision on a 12-month extension by 31 December 2026 [PM-C5]. At a 35% saving, run-cost savings are about EUR 458,500 a year, or about EUR 1.83M over 4 years. That is well short of the envelope, so the payback test depends on contact-centre and risk benefits too (see Conflict 2).

**Driver Intensity**: HIGH

**Enablers** (What would help):

- Contact-centre savings that are quantified and agreed before the business case
- A 12-month TrackBox extension on acceptable terms

**Blockers** (What would hinder):

- Benefits that cannot be measured because there are no baselines
- Scope creep beyond the mandate

**Related Stakeholders**:

- Aligned: CIO (SD-6), Head of Customer Service (SD-7) as owner of benefits
- Potential tension: DPO (SD-10) about TrackBox support access outside the EU

---

### SD-5: Sofie Peeters (CIO) - Exit End-of-Life Platforms

**Stakeholder**: Sofie Peeters, CIO

**Driver Category**: OPERATIONAL

**Driver Statement**: Liferay hosting ends in June 2027, which makes Portal B the first forced move [SI-C7]. Portal A runs on .NET Framework 4.6, which is out of support, in the Ghent data centre [PI-C3] [PI-C9].

**Context & Background**: Liferay 6.2 is out of support, Portal B averages 6.8-second page loads, and Portal B has had no new features since 2022 [PI-C10]. The Ghent data centre closes by end 2028 [AIP-C2]. The CIO carries the technology risk of these platforms until they are retired.

**Driver Intensity**: CRITICAL

**Enablers** (What would help):

- Platform chosen early enough to migrate Portal B before 30 June 2027
- A short contingency extension of the hosting contract

**Blockers** (What would hinder):

- Discovery running until 31 March 2027 [PM-C4], which leaves three months for Portal B

**Related Stakeholders**:

- Aligned: CFO (SD-3), CISO (SD-9), Portal B owner

---

### SD-6: Sofie Peeters (CIO) - Buy, Not Build, With One Customer Identity

**Stakeholder**: Sofie Peeters, CIO

**Driver Category**: STRATEGIC

**Driver Statement**: Sofie Peeters prefers a SaaS or low-code platform on the strategic cloud platform over another custom build [SI-C8], and wants one customer identity platform for all channels [SI-C9].

**Context & Background**: Group policy is reuse, then buy, then build [AIP-C6], and architecture principles 2 and 9 in ARC-000-PRIN-v1.0 support this. Portal A (built in-house in 2014) and Portal B (built by an agency in 2016) are examples of custom builds that aged badly.

**Driver Intensity**: HIGH

**Enablers** (What would help):

- A market that offers products meeting EU residency, Dutch and French, and WCAG 2.2 AA
- Agreement that differentiating cold-chain and EDI features may need targeted extension

**Blockers** (What would hinder):

- Portal owners insisting on exact copies of existing features
- Products that cannot meet EU-only support access

**Related Stakeholders**:

- Aligned: CFO (SD-3), CISO (SD-9)
- Potential tension: portal owners (SD-11, SD-12)

---

### SD-7: Nathalie Lambert (Head of Customer Service) - Fewer, Faster, First-Time-Right Contacts

**Stakeholder**: Nathalie Lambert, Head of Customer Service

**Driver Category**: OPERATIONAL

**Driver Statement**: Customer Service handles 410,000 contacts a year, and 31% are "where is my shipment?" calls [SI-C10]. Agents switch between three portals and two CRMs. Average handling time is 7 min 40 s and first-contact resolution is 64% [SI-C11].

**Context & Background**: The mandate targets 40% fewer "where is my shipment?" calls, 25% lower average handling time and at least 80% first-contact resolution [PM-C9] [PM-C10]. The group strategy targets 70% of service interactions through digital self-service [ACP-C3]. Nathalie Lambert's team absorbs every failure of the digital channels.

**Driver Intensity**: CRITICAL

**Enablers** (What would help):

- Proactive tracking notifications and self-service tracking
- One agent view across business units [PM-C2]

**Blockers** (What would hinder):

- The two CRMs are out of scope [PM-C3], so agents may still need two tools
- Limits on what agents may see (SD-10)

**Related Stakeholders**:

- Aligned: COO (SD-1), CFO (SD-4), contact-centre agents (SD-15)
- Potential tension: DPO (SD-10) about how much data agents can see

---

### SD-8: Nathalie Lambert (Head of Customer Service) - End Invoice Confusion

**Stakeholder**: Nathalie Lambert, Head of Customer Service, on behalf of multi-contract customers

**Driver Category**: CUSTOMER

**Driver Statement**: Customers with several contracts get three invoice layouts and call to ask which one is right [SI-C12].

**Context & Background**: Invoices are issued from the ERP through Peppol, and portals only show copies. Replacing the ERP is out of scope [PM-C3]. The portal can bring invoice copies together in one place, but it cannot change invoice layouts by itself.

**Driver Intensity**: MEDIUM

**Enablers** (What would help):

- One invoice list per customer across business units, with clear labels
- Finance agreeing to harmonise invoice layouts (outside programme scope)

**Blockers** (What would hinder):

- Layout differences that come from the ERP configuration of each business unit

**Related Stakeholders**:

- CFO (as owner of Finance), business customers (SD-13)

---

### SD-9: Pieter Janssens (CISO) - One Hardened Login and NIS2 Evidence

**Stakeholder**: Pieter Janssens, CISO

**Driver Category**: COMPLIANCE

**Driver Statement**: Pieter Janssens wants one hardened login and central security logging [SI-C15], and Acme must reach CyberFundamentals level Important by end 2027 [SI-C14].

**Context & Background**: Portal A has no MFA and was hit by credential stuffing in February 2025 [SI-C13], which led to 12,000 password resets [PI-C10]. Portal B's MFA is optional and Portal C enforces MFA only for administrators [PI-C4]. The mandate requires MFA for all users and makes it mandatory for business administrators [PM-C12].

**Driver Intensity**: CRITICAL

**Enablers** (What would help):

- Customer identity delivered first and shared by all channels
- Security logs forwarded centrally and treated as Strictly Confidential

**Blockers** (What would hinder):

- Portal A migration not due until 30 June 2028 [PM-C7], six months after the CyberFundamentals deadline

**Related Stakeholders**:

- Aligned: CIO (SD-6), DPO (SD-10)
- Potential tension: COO and CFO, if interim controls on Portal A add cost or delay

---

### SD-10: Isabelle Martin (DPO) - Lawful, Timely, Minimal Processing

**Stakeholder**: Isabelle Martin, DPO

**Driver Category**: COMPLIANCE

**Driver Statement**: There are 140 data subject requests a year, answered in 41 days on average against a legal limit of one month, because the data sits in three portals and two CRMs [SI-C16]. TrackBox support access from outside the EU is an open finding [SI-C17]. Agents must not see more personal data than the contact needs [SI-C18].

**Context & Background**: The GDPR deadline is being missed on average, which exposes Acme to action by the Belgian Data Protection Authority. Group policy requires vendor support access to stay in the EU/EEA [AIP-C3]. The mandate requires 100% of data subject requests answered within one month [PM-C11].

**Driver Intensity**: CRITICAL

**Enablers** (What would help):

- One customer record that can be searched for data subject requests
- Contractual EU-only support access as a condition for any TrackBox extension

**Blockers** (What would hinder):

- The CRMs staying out of scope, so data subject requests still span several systems
- A TrackBox extension with no fix for non-EU access

**Related Stakeholders**:

- Aligned: CISO (SD-9)
- Potential tension: CFO (SD-4) on the TrackBox extension, Head of Customer Service (SD-7) on the agent view

---

### SD-11: Portal Owners (A, B, C) - Keep the Features Customers Rely On

**Stakeholder**: Koen De Smet (Portal A), Julie Leclercq (Portal B), Tom Wouters (Portal C)

**Driver Category**: PERSONAL

**Driver Statement**: The portal owners fear losing features their customers rely on: the returns flow (A), EDI order upload (B), and temperature alerts and certificates (C) [SI-C19]. All three want usage data before deciding what can be dropped [SI-C21].

**Context & Background**: Each owner answers to their business unit's customers and commercial teams, and their standing depends on customers not being disrupted. Usage differs widely: Portal A has 41,000 monthly active users, Portal B 2,600 and Portal C 1,900 [PI-C2].

**Driver Intensity**: HIGH

**Enablers** (What would help):

- Usage analytics collected during discovery
- A transparent rule for which features are kept, changed or dropped

**Blockers** (What would hinder):

- Feature decisions made without data or without the owners present
- A platform that cannot support business-unit-specific capabilities

**Related Stakeholders**:

- Potential tension: CIO (SD-6), CFO (SD-3)
- Aligned: business customers (SD-13)

---

### SD-12: Tom Wouters (Portal C) - Audit-Proof Temperature Records for Pharma

**Stakeholder**: Tom Wouters, Portal C owner, on behalf of pharma and food customers

**Driver Category**: COMPLIANCE

**Driver Statement**: Pharma customers require audit-proof temperature records, and this is non-negotiable for Tom Wouters [SI-C20].

**Context & Background**: Portal C provides temperature monitoring, alerts and compliance certificates (HACCP, GDP) from a telematics feed [PI-C6] [PI-C7]. If the evidence trail is lost or questioned, pharma customers could fail their own audits and move their business elsewhere.

**Driver Intensity**: CRITICAL

**Enablers** (What would help):

- Temperature records kept in a tamper-evident form, with full history migrated
- Customer advisory group validating the new evidence before Wave 2

**Blockers** (What would hinder):

- A generic platform that treats temperature data as ordinary tracking events
- Migration that breaks the continuity of historic records

**Related Stakeholders**:

- Aligned: pharma and food customers; COO (customer retention)
- Potential tension: CIO (SD-6) if these features need custom build

---

### SD-13: Business Customers - One Account Across All Acme Services

**Stakeholder**: Business customers of all three business units

**Driver Category**: CUSTOMER

**Driver Statement**: Business customers want one login, one view of shipments, invoices and documents across parcel, freight and cold chain, in their own language.

**Context & Background**: 1,800 business customers currently use more than one portal [ACP-C1]. Portal B's French version is incomplete, and Portal C has no French at all [PI-C5], although Dutch and French are required commercially and legally [ACP-C4]. Portal B averages 6.8-second page loads [PI-C10].

**Driver Intensity**: HIGH

**Enablers** (What would help):

- Business accounts with delegated users and roles across services
- Migration that carries over users, address books and preferences

**Blockers** (What would hinder):

- Forced re-registration or loss of integrations (for example, EDI)

**Related Stakeholders**:

- Aligned: COO (SD-1), portal owners (SD-11)

---

### SD-14: Consumers - Easy Tracking and Returns, Safe Accounts

**Stakeholder**: About 150,000 registered consumers on Portal A [PI-C1]

**Driver Category**: CUSTOMER

**Driver Statement**: Consumers want to track parcels and arrange returns quickly on any device, without their account being taken over.

**Context & Background**: Portal A's credential-stuffing attack forced 12,000 password resets [PI-C10]. Consumers are the largest user group, but each uses the portal only occasionally.

**Driver Intensity**: MEDIUM

**Enablers** (What would help):

- Tracking without a login where appropriate, plus a simple returns flow
- MFA that is easy to use

**Blockers** (What would hinder):

- A complex migration that forces consumers to re-register

**Related Stakeholders**:

- Aligned: Head of Customer Service (SD-7), CISO (SD-9)

---

### SD-15: Contact-Centre Agents - One Tool, Not Five

**Stakeholder**: Customer Service agents

**Driver Category**: OPERATIONAL

**Driver Statement**: Agents want to answer a customer from one screen instead of switching between three portals and two CRMs [SI-C11].

**Context & Background**: Switching between tools drives the 7 min 40 s average handling time and a first-contact resolution rate of 64% [SI-C11]. The repeated invoice and tracking calls are the work agents find most frustrating.

**Driver Intensity**: HIGH

**Enablers** (What would help):

- An agent view that shows shipment, invoice and account status across business units
- Agents involved in design and piloting

**Blockers** (What would hinder):

- An agent view that is added on top of, rather than replacing, existing tools

**Related Stakeholders**:

- Aligned: Head of Customer Service (SD-7)
- Potential tension: DPO (SD-10) on the amount of data shown

---

## Driver-to-Goal Mapping

### Goal G-1: Migrate All Customers and Switch Off Portals A, B and C by 2028

**Derived From Drivers**: SD-1, SD-2, SD-3, SD-5, SD-13

**Goal Owner**: Annelies Claes (COO, Sponsor)

**Goal Statement**: Migrate all Portal B customers by 30 June 2027, Portal C customers by 31 March 2028 and Portal A customers by 30 June 2028, and switch off all three legacy portals by 31 December 2028 [PM-C6] [PM-C7]. Every migration must happen outside the peak freeze, and the recommended date for the final switch-off is on or before 14 October 2028.

**Why This Matters**: This is the core of the One Acme commitment. It also removes the end-of-life platforms and their run cost.

**Success Metrics**:

- **Primary Metric**: Share of active customer accounts migrated, per portal
- **Secondary Metrics**:
  - Number of legacy portals switched off (target 3)
  - Number of go/no-go decisions taken on schedule (target 3)

**Baseline**: 0% migrated; 3 live portals

**Target**: 100% migrated; 0 legacy portals live by 31 December 2028 (recommended by 14 October 2028)

**Measurement Method**: Migration dashboard from the identity and customer-record platforms, compared with each legacy user store

**Dependencies**:

- Platform chosen by 31 March 2027 [PM-C4]
- Customer identity service available before Wave 1

**Risks to Achievement**:

- Three months between platform choice and the Portal B deadline (R-1)
- A slip pushes waves into the peak freeze (R-6)

---

### Goal G-2: Cut Portal Run Cost by at Least 35% With Payback Within 4 Years

**Derived From Drivers**: SD-3, SD-4, SD-6

**Goal Owner**: Marc Dubois (CFO)

**Goal Statement**: Reduce annual portal run cost from EUR 1.31M to EUR 851,500 or less (a reduction of at least 35%) in 2029, the first full year after switch-off, with programme payback in 4 years or less [PM-C8] [SI-C5].

**Why This Matters**: This meets the CFO's cost driver and contributes to the group's 20% IT run-cost target.

**Success Metrics**:

- **Primary Metric**: Annual run cost of the customer portal estate (EUR)
- **Secondary Metrics**:
  - Cumulative net benefit compared with investment (payback year)
  - Months of double-running per wave

**Baseline**: EUR 1,310,000 a year (A EUR 610,000; B EUR 420,000; C EUR 280,000) [PI-C8]

**Target**: EUR 851,500 a year or less; payback in 4 years or less

**Measurement Method**: Finance cost centre reporting for portal licences, hosting, support and staff, reviewed every quarter

**Dependencies**:

- Contact-centre benefits accepted in the business case (see Conflict 2)
- Prompt switch-off after each wave

**Risks to Achievement**:

- Run-cost savings alone do not reach payback (R-2)
- Double-running costs if waves slip

---

### Goal G-3: Decide on the TrackBox Extension by 31 December 2026, With EU-Only Support Access

**Derived From Drivers**: SD-4, SD-10, SD-12

**Goal Owner**: Sofie Peeters (CIO), with Marc Dubois (CFO)

**Goal Statement**: By 31 December 2026, agree a 12-month TrackBox extension (to 31 March 2028) instead of a 3-year renewal [PM-C5]. The extension must contractually limit vendor support access to the EU/EEA, or the Architecture Board and DPO must approve compensating controls with a closure date.

**Why This Matters**: It avoids a 3-year lock-in [SI-C6] and closes the DPO's open finding [SI-C17].

**Success Metrics**:

- **Primary Metric**: Signed 12-month extension, with an EU-only support access clause, by 31 December 2026
- **Secondary Metrics**:
  - DPO finding on TrackBox closed (yes/no)

**Baseline**: 3-year auto-renewal due 31 March 2027; DPO finding open

**Target**: 12-month extension signed; finding closed or covered by approved compensating controls

**Measurement Method**: Contract register; DPO findings log

**Dependencies**:

- Vendor willingness to offer a 12-month term and to change how support is provided

**Risks to Achievement**:

- Vendor refuses or prices the short term at a premium (R-4)
- An extension to 31 March 2028 leaves no slack for Wave 2 (R-5)

---

### Goal G-4: Choose the Platform and Complete Discovery by 31 March 2027

**Derived From Drivers**: SD-5, SD-6, SD-11

**Goal Owner**: Sofie Peeters (CIO), through the Architecture Board

**Goal Statement**: By 31 March 2027, within the EUR 350,000 discovery budget [SI-C5], complete discovery and choose the platform and customer identity service following reuse, then buy, then build [AIP-C6]. The decision must be backed by usage data for all three portals and recorded as ADRs.

**Why This Matters**: Every later milestone depends on this decision. Usage data turns the portal owners' fears into evidence-based scope decisions [SI-C21].

**Success Metrics**:

- **Primary Metric**: Platform and identity ADRs approved by the Architecture Board by 31 March 2027
- **Secondary Metrics**:
  - Feature usage report covering 100% of key features in A, B and C
  - Discovery spend compared with EUR 350,000

**Baseline**: No platform chosen; no consolidated usage data

**Target**: Decisions approved on time and within budget

**Measurement Method**: Architecture Board minutes and ADR register; finance reporting

**Dependencies**:

- Analytics or log access on all three portals, including TrackBox
- Market engagement started by early January 2027

**Risks to Achievement**:

- Analysis paralysis while Portal B's deadline approaches (R-1)

---

### Goal G-5: One Hardened Customer Login With MFA and Central Security Logging

**Derived From Drivers**: SD-6, SD-9, SD-13, SD-14

**Goal Owner**: Pieter Janssens (CISO), with Sofie Peeters (CIO)

**Goal Statement**: By 30 June 2027 (Wave 1), launch one customer identity service that offers MFA to all users and enforces it for 100% of business administrators [PM-C12], with all authentication events sent to central security logging. Move all users onto it as their portal migrates. Put interim protection in place for Portal A logins by 31 December 2027, so that Portal A does not undermine the CyberFundamentals target.

**Why This Matters**: This closes the credential-stuffing exposure and supports the NIS2 deadline at end 2027 [SI-C14].

**Success Metrics**:

- **Primary Metric**: Share of business administrator accounts with MFA enforced
- **Secondary Metrics**:
  - Successful account takeovers through credential stuffing
  - Share of portal authentication events in central security logging

**Baseline**: Portal A has no MFA; Portal B's MFA is optional; Portal C enforces MFA for admins only [PI-C4]; one credential-stuffing incident (12,000 resets) [PI-C10]

**Target**: 100% of business administrators on MFA; 0 successful credential-stuffing takeovers; 100% of authentication events logged centrally

**Measurement Method**: Identity service reports; security monitoring

**Dependencies**:

- Identity service selected in G-4
- Funding for interim Portal A controls

**Risks to Achievement**:

- Portal A remains exposed until June 2028 (R-3)

---

### Goal G-6: Cut "Where Is My Shipment?" Calls by 40%

**Derived From Drivers**: SD-1, SD-4, SD-7, SD-13, SD-14

**Goal Owner**: Nathalie Lambert (Head of Customer Service)

**Goal Statement**: By the end of 2029, reduce "where is my shipment?" contacts from about 127,100 a year (31% of 410,000) to 76,260 a year or fewer (−40%) [SI-C10] [PM-C9], through self-service tracking and proactive notifications in all three business units.

**Why This Matters**: This is the largest single contact reason. Removing it frees agent time and raises digital self-service.

**Success Metrics**:

- **Primary Metric**: Annual "where is my shipment?" contacts
- **Secondary Metrics**:
  - Tracking self-service sessions per shipment
  - Notification opt-in rate

**Baseline**: About 127,100 a year

**Target**: 76,260 a year or fewer

**Measurement Method**: Contact-reason codes in the CRMs, reported monthly and normalised for shipment volume, because peak volumes change each year

**Dependencies**:

- Tracking events from all networks available in the new portal
- Consistent contact-reason coding across both CRMs

**Risks to Achievement**:

- Inconsistent coding of contact reasons distorts the baseline (R-8)

---

### Goal G-7: Cut Average Handling Time by 25% and Raise First-Contact Resolution to 80%

**Derived From Drivers**: SD-7, SD-8, SD-15

**Goal Owner**: Nathalie Lambert (Head of Customer Service)

**Goal Statement**: By the end of 2029, reduce average handling time from 7 min 40 s (460 s) to 5 min 45 s (345 s) or less, and raise first-contact resolution from 64% to at least 80% [SI-C11] [PM-C10], through one agent view across business units.

**Why This Matters**: This is the main source of the contact-centre savings that the business case depends on.

**Success Metrics**:

- **Primary Metric**: Average handling time (seconds)
- **Secondary Metrics**:
  - First-contact resolution (%)
  - Number of applications used per contact

**Baseline**: 460 s; 64%

**Target**: 345 s or less; at least 80%

**Measurement Method**: Contact-centre telephony and CRM reporting, monthly

**Dependencies**:

- An agent view that can reach both CRMs, even though the CRMs are out of scope [PM-C3]
- A role-based data model agreed with the DPO

**Risks to Achievement**:

- Agents still need the CRMs, so the gains are only partial (R-7)

---

### Goal G-8: Answer 100% of Data Subject Requests Within One Month

**Derived From Drivers**: SD-10

**Goal Owner**: Isabelle Martin (DPO)

**Goal Statement**: From the completion of Wave 3 (30 June 2028), answer 100% of data subject requests within one month [PM-C11], down from an average of 41 days today [SI-C16]. Interim improvements should come with each wave.

**Why This Matters**: This removes a live GDPR compliance breach.

**Success Metrics**:

- **Primary Metric**: Share of data subject requests answered within one month
- **Secondary Metrics**:
  - Average days to answer
  - Number of systems searched per request

**Baseline**: Average 41 days; 140 requests a year; 5 systems (3 portals and 2 CRMs)

**Target**: 100% answered within one month

**Measurement Method**: DPO request log, monthly

**Dependencies**:

- One customer record (G-1); an agreed process for the CRMs

**Risks to Achievement**:

- The CRMs remain separate stores that must be searched by hand

---

### Goal G-9: Keep Every Business-Critical and Compliance-Critical Feature

**Derived From Drivers**: SD-11, SD-12, SD-13

**Goal Owner**: Programme Product Owner (to be appointed), with portal owners

**Goal Statement**: Before each wave's go/no-go, deliver evidence that every feature classed as critical by the usage review in G-4 works on the new platform. This covers at least the returns flow, EDI order upload, and temperature alerts with audit-proof GDP/HACCP certificates and their full history [SI-C19] [SI-C20].

**Why This Matters**: This protects customer retention and the portal owners' trust, and is the condition for their support.

**Success Metrics**:

- **Primary Metric**: Share of critical features accepted by the portal owner and customer representatives before go/no-go
- **Secondary Metrics**:
  - Number of features dropped, each backed by usage evidence and agreed

**Baseline**: No agreed feature catalogue

**Target**: 100% of critical features accepted; 0 critical features lost

**Measurement Method**: Feature-parity register signed off at each go/no-go

**Dependencies**:

- Usage data (G-4); platform capability for business-unit-specific features

**Risks to Achievement**:

- Temperature-record integrity cannot be shown on a generic platform

---

### Goal G-10: Fully Dutch and French, and WCAG 2.2 AA, From First Release

**Derived From Drivers**: SD-1, SD-13, SD-14

**Goal Owner**: Programme Product Owner (to be appointed)

**Goal Statement**: From the first release, every customer journey is fully available in Dutch and French (English optional) [PM-C1] and meets WCAG 2.2 AA [AIP-C4].

**Why This Matters**: Both are legal and commercial requirements [ACP-C4]. Portal C customers will get French for the first time.

**Success Metrics**:

- **Primary Metric**: Share of journeys passing a WCAG 2.2 AA audit in both Dutch and French
- **Secondary Metrics**:
  - Untranslated strings in production (target 0)

**Baseline**: Portal B's French is incomplete; Portal C has no French [PI-C5]

**Target**: 100% of journeys

**Measurement Method**: Independent accessibility audit before each wave; automated checks in the pipeline

**Dependencies**:

- A platform with built-in multilingual content support

**Risks to Achievement**:

- Translation becomes a late activity and delays waves

---

## Goal-to-Outcome Mapping

### Outcome O-1: Customers Experience One Acme

**Supported Goals**: G-1, G-5, G-9, G-10

**Outcome Statement**: By the end of 2028, every Acme customer uses one portal with one login and one customer record, including the 1,800 business customers who use several portals today, and no critical feature has been lost.

**Measurement Details**:

- **KPI**: Customers with a single Acme account (%), and customer satisfaction with the portal
- **Current Value**: 0%; satisfaction baseline not yet measured (to be set in discovery)
- **Target Value**: 100%; satisfaction at or above the pre-migration baseline after each wave
- **Measurement Frequency**: Monthly during migration; quarterly afterwards
- **Data Source**: Identity service, customer record, post-journey survey
- **Report Owner**: Programme Product Owner

**Business Value**:

- **Financial Impact**: Protects revenue from multi-service business customers
- **Strategic Impact**: Delivers the first Strategy 2030 objective
- **Operational Impact**: One platform to change and support
- **Customer Impact**: One login and one view of all services, in their own language

**Timeline**:

- **Discovery (Oct 2026 – Mar 2027)**: Satisfaction baseline set; feature catalogue agreed
- **Wave 1 (Apr – Jun 2027)**: Portal B customers on one account
- **Waves 2 and 3 (Jul 2027 – Jun 2028)**: Portal C and A customers migrated
- **Sustainment (2029+)**: Satisfaction tracked every quarter

**Stakeholder Benefits**:

- **Annelies Claes (COO)**: Delivers the commitment made to the Executive Committee
- **Business customers**: One account across services
- **Portal owners**: Customers retained with no feature loss

**Leading Indicators** (early signals of success):

- Beta customer adoption in Wave 1
- Feature-parity sign-off on schedule

**Lagging Indicators** (final proof of success):

- 100% single accounts; satisfaction held or improved

---

### Outcome O-2: Portal Run Cost Reduced by at Least EUR 458,500 a Year

**Supported Goals**: G-1, G-2, G-3, G-4

**Outcome Statement**: From 2029, annual portal run cost is EUR 851,500 or less, saving at least EUR 458,500 a year compared with today.

**Measurement Details**:

- **KPI**: Portal estate run cost (EUR a year)
- **Current Value**: EUR 1,310,000
- **Target Value**: EUR 851,500 or less
- **Measurement Frequency**: Quarterly
- **Data Source**: Finance cost centre reports
- **Report Owner**: Marc Dubois (CFO)

**Business Value**:

- **Financial Impact**: At least EUR 458,500 a year, about EUR 1.83M over 4 years, plus avoiding a 3-year TrackBox renewal
- **Strategic Impact**: Contributes to the group's 20% IT run-cost reduction
- **Operational Impact**: Removes out-of-support platforms (Liferay 6.2, .NET 4.6)
- **Customer Impact**: Indirect (investment moves from maintenance to features)

**Timeline**:

- **2027**: Portal B cost (EUR 420,000) stops after 30 June 2027
- **2028**: Portal C cost (EUR 280,000) stops after 31 March 2028; Portal A cost (EUR 610,000) stops after switch-off
- **2029 (first full year)**: Full target reached
- **Sustainment**: Annual cost review against the target

**Stakeholder Benefits**:

- **Marc Dubois (CFO)**: Meets the run-cost target
- **Sofie Peeters (CIO)**: Smaller, supported estate

**Leading Indicators** (early signals of success):

- Each legacy contract ended on its planned date
- Double-running limited to three months or less per wave

**Lagging Indicators** (final proof of success):

- Run cost in 2029 accounts

---

### Outcome O-3: Lower Cost to Serve in the Contact Centre

**Supported Goals**: G-6, G-7

**Outcome Statement**: By the end of 2029, the contact centre handles about 50,840 fewer "where is my shipment?" contacts a year and resolves the rest faster. This frees roughly 18,000 agent hours a year.

**Measurement Details**:

- **KPI**: Total agent handling hours a year (contacts multiplied by average handling time)
- **Current Value**: About 52,390 hours (410,000 contacts × 460 s)
- **Target Value**: About 34,420 hours or fewer (359,160 contacts × 345 s), a saving of about 17,970 hours
- **Measurement Frequency**: Monthly
- **Data Source**: Contact-centre telephony and CRM reporting
- **Report Owner**: Nathalie Lambert (Head of Customer Service)

**Business Value**:

- **Financial Impact**: About 11 FTE of capacity, assuming 1,600 productive hours per FTE. The Head of Customer Service and the CFO must confirm the euro value in the business case using the loaded agent cost. This benefit is needed for payback (Conflict 2)
- **Strategic Impact**: Contributes to the group's 70% digital self-service target [ACP-C3]
- **Operational Impact**: Peak-season contact volumes become easier to staff
- **Customer Impact**: Fewer reasons to call; faster answers when customers do call

**Timeline**:

- **Discovery**: Contact-reason baseline validated in both CRMs
- **Wave 1 to Wave 3**: Reduction measured per business unit after each wave
- **2029**: Full target
- **Sustainment**: Monthly reporting

**Stakeholder Benefits**:

- **Nathalie Lambert**: Meets the mandate's service targets
- **Marc Dubois**: Evidence for payback
- **Agents**: Less repetitive work

**Leading Indicators** (early signals of success):

- Notification opt-in and tracking self-service rates after each wave
- Agent view adoption in the pilot group

**Lagging Indicators** (final proof of success):

- Annual contact volume, handling time and first-contact resolution

---

### Outcome O-4: Regulatory Compliance Demonstrated for the Customer Portal

**Supported Goals**: G-3, G-5, G-8, G-10

**Outcome Statement**: The customer portal estate has no open data protection findings and answers 100% of data subject requests within one month. It provides evidence of its CyberFundamentals level Important controls and meets WCAG 2.2 AA.

**Measurement Details**:

- **KPI**: Open GDPR and NIS2 findings related to the portal estate; data subject requests answered on time (%)
- **Current Value**: 1 open DPO finding (TrackBox) [SI-C17]; data subject requests answered in 41 days on average
- **Target Value**: 0 open findings; 100% on time
- **Measurement Frequency**: Monthly
- **Data Source**: DPO findings log and request log; CISO control register
- **Report Owner**: Isabelle Martin (DPO), Pieter Janssens (CISO)

**Business Value**:

- **Financial Impact**: Avoids GDPR and NIS2 penalties
- **Strategic Impact**: Delivers "compliance by design" from Strategy 2030
- **Operational Impact**: Audit evidence is produced as a normal part of operations
- **Customer Impact**: Trust; pharma customers can rely on Acme's evidence

**Timeline**:

- **By 31 Dec 2026**: TrackBox support-access issue resolved contractually (G-3)
- **By 31 Dec 2027**: Portal controls evidenced for CyberFundamentals Important
- **By 30 Jun 2028**: Data subject requests 100% on time
- **Sustainment**: Annual audit

**Stakeholder Benefits**:

- **DPO and CISO**: Findings closed; evidence available
- **Executive Committee**: Lower regulatory exposure

**Leading Indicators** (early signals of success):

- DPIA completed at discovery close
- Security logging connected in Wave 1

**Lagging Indicators** (final proof of success):

- Clean audit and regulator interactions

---

### Outcome O-5: Secure Customer Accounts

**Supported Goals**: G-5

**Outcome Statement**: No customer accounts are taken over through credential stuffing, and every business administrator signs in with MFA.

**Measurement Details**:

- **KPI**: Successful account takeovers; business administrators with MFA (%)
- **Current Value**: 1 major incident (February 2025, 12,000 resets); MFA coverage uneven across portals
- **Target Value**: 0 takeovers; 100% of business administrators on MFA
- **Measurement Frequency**: Monthly
- **Data Source**: Identity service and security monitoring
- **Report Owner**: Pieter Janssens (CISO)

**Business Value**:

- **Financial Impact**: Avoids incident cost and mass password resets
- **Strategic Impact**: Supports NIS2 obligations
- **Operational Impact**: Fewer password-reset contacts
- **Customer Impact**: Safer accounts and one login

**Timeline**:

- **Wave 1 (Jun 2027)**: Identity service live with MFA enforced for business administrators
- **By Dec 2027**: Interim Portal A protection in place
- **By Jun 2028**: All users on the new identity service
- **Sustainment**: Continuous monitoring

**Stakeholder Benefits**:

- **CISO**: One hardened login
- **Consumers and business customers**: Protected accounts

**Leading Indicators** (early signals of success):

- MFA enrolment rate per wave

**Lagging Indicators** (final proof of success):

- No account-takeover incidents over 12 months

---

### Outcome O-6: Digital Self-Service Becomes the Default Channel

**Supported Goals**: G-6, G-9, G-10

**Outcome Statement**: The portal is the main channel for tracking, booking, returns and documents, and contributes to the group target of 70% of service interactions through self-service [ACP-C3].

**Measurement Details**:

- **KPI**: Share of service interactions completed digitally without staff help
- **Current Value**: Not yet measured; baseline to be set during discovery
- **Target Value**: The portal's contribution towards 70%, with a programme-level target to be set at discovery close
- **Measurement Frequency**: Monthly
- **Data Source**: Portal analytics combined with contact-centre volumes
- **Report Owner**: Nathalie Lambert (Head of Customer Service)

**Business Value**:

- **Financial Impact**: Lower cost to serve (see O-3)
- **Strategic Impact**: Delivers the third Strategy 2030 objective
- **Operational Impact**: Demand moves away from the contact centre at peak
- **Customer Impact**: Available at any time, in Dutch, French and English

**Timeline**:

- **Discovery**: Baseline and target set
- **Waves 1–3**: Measured per business unit
- **2029+**: Sustained and reported to the Executive Committee

**Stakeholder Benefits**:

- **COO and Head of Customer Service**: Progress on strategy
- **Customers**: Faster resolution

**Leading Indicators** (early signals of success):

- Journey completion rates

**Lagging Indicators** (final proof of success):

- Group self-service share

---

## Complete Traceability Matrix

### Stakeholder → Driver → Goal → Outcome

| Stakeholder | Driver ID | Driver Summary | Goal ID | Goal Summary | Outcome ID | Outcome Summary |
|-------------|-----------|----------------|---------|--------------|------------|-----------------|
| COO | SD-1 | Present One Acme | G-1 | Migrate and switch off A, B, C | O-1 | Customers experience One Acme |
| COO | SD-1 | Present One Acme | G-10 | NL/FR and WCAG 2.2 AA | O-1 | Customers experience One Acme |
| COO | SD-2 | Protect peak operations | G-1 | Migrations outside the peak freeze | O-1 | Customers experience One Acme |
| CFO | SD-3 | Cut run cost by 35% or more | G-2 | Run cost of EUR 851,500 or less | O-2 | Save at least EUR 458,500 a year |
| CFO | SD-4 | Payback within 4 years | G-2 | Payback within 4 years | O-3 | Lower cost to serve |
| CFO | SD-4 | Avoid TrackBox lock-in | G-3 | 12-month extension | O-2 | Save at least EUR 458,500 a year |
| CIO | SD-5 | Exit end-of-life platforms | G-1 | Portal B by 30 Jun 2027 | O-2 | Save at least EUR 458,500 a year |
| CIO | SD-6 | Buy, not build; one identity | G-4 | Platform chosen by 31 Mar 2027 | O-2 | Save at least EUR 458,500 a year |
| CIO | SD-6 | One customer identity | G-5 | One hardened login | O-5 | Secure customer accounts |
| Head of Customer Service | SD-7 | Fewer, faster contacts | G-6 | 40% fewer "where is my shipment?" calls | O-3 | Lower cost to serve |
| Head of Customer Service | SD-7 | Fewer, faster contacts | G-7 | Handling time 345 s or less; first-contact resolution 80% or more | O-3 | Lower cost to serve |
| Head of Customer Service | SD-8 | End invoice confusion | G-7 | Handling time and first-contact resolution | O-3 | Lower cost to serve |
| CISO | SD-9 | Hardened login; NIS2 | G-5 | MFA and central logging | O-4 / O-5 | Compliance; secure accounts |
| DPO | SD-10 | Data subject requests on time; EU-only access | G-8 | 100% of requests within one month | O-4 | Compliance demonstrated |
| DPO | SD-10 | EU-only support access | G-3 | TrackBox EU-only clause | O-4 | Compliance demonstrated |
| Portal owners | SD-11 | Keep critical features | G-9 | 100% of critical features accepted | O-1 | Customers experience One Acme |
| Portal C owner | SD-12 | Audit-proof temperature records | G-9 | GDP/HACCP evidence preserved | O-1 / O-4 | One Acme; compliance |
| Business customers | SD-13 | One account across services | G-1, G-5, G-10 | Migration, one login, languages | O-1 / O-6 | One Acme; self-service |
| Consumers | SD-14 | Easy tracking; safe accounts | G-5, G-6 | One login; self-service tracking | O-5 / O-6 | Secure accounts; self-service |
| Contact-centre agents | SD-15 | One tool | G-7 | Agent view across business units | O-3 | Lower cost to serve |

### Conflict Analysis

**Competing Drivers**:

- **Conflict 1 (Portal B timeline)**: The CIO and CFO need Portal B migrated by 30 June 2027 (SD-5), but the mandate allows discovery to run until 31 March 2027 (G-4). That leaves three months to build, test and migrate 3,100 business accounts, including EDI order upload.
  - **Resolution Strategy**:
    - Bring the platform and identity decision forward to the end of January 2027, and run Portal B migration design during discovery.
    - Make Wave 1 a minimum viable scope for Portal B: login, booking, quotes, proof of delivery, invoices and EDI.
    - In parallel, ask the German hosting provider for a short contingency extension (3 months), to be used only if the go/no-go fails.
    - The Architecture Board should record this as an ADR.

- **Conflict 2 (Payback against envelope)**: The CFO wants payback within 4 years on a EUR 4–6M envelope (SD-4). Run-cost savings of at least EUR 458,500 a year give only about EUR 1.83M over 4 years.
  - **Resolution Strategy**:
    - Build the business case on three benefit streams: run cost, contact-centre capacity (about 17,970 hours a year, see O-3) and risk avoidance (credential-stuffing incidents, GDPR and NIS2 exposure).
    - Fix contact-reason and handling-time baselines during discovery so the benefits can be audited.
    - Size the investment towards the lower end of the envelope through buy rather than build.
    - The CFO decides at discovery close whether the case meets the 4-year test.

- **Conflict 3 (Portal A security gap)**: The CISO needs CyberFundamentals level Important by end 2027 (SD-9), but Portal A, with no MFA, is not scheduled to migrate until 30 June 2028 (G-1).
  - **Resolution Strategy**: Either:
    - **Option A**: Move Portal A users onto the new customer identity service early (identity first, portal later), or
    - **Option B**: Put interim protection in front of Portal A (bot and credential-stuffing protection, optional MFA) by 31 December 2027.

    The CISO and CIO decide during discovery. Option A brings O-5 forward, but means changing Portal A's login, which is old code.

- **Conflict 4 (TrackBox extension and non-EU support access)**: The CFO wants a 12-month TrackBox extension to avoid a 3-year renewal (SD-4), but the DPO has an open finding on TrackBox support access from outside the EU (SD-10), and group policy requires EU/EEA support access [AIP-C3].
  - **Resolution Strategy**: Make the extension conditional on a contractual EU-only support clause. If the vendor refuses, approve compensating controls (access only when Acme approves it, logged and time-limited) through the Architecture Board and DPO, with a closure date of 31 March 2028.

- **Conflict 5 (Single agent view versus minimum data)**: The Head of Customer Service wants one agent view across business units to cut handling time (SD-7, SD-15). The DPO requires that agents do not see more personal data than the contact needs (SD-10).
  - **Resolution Strategy**: Design a role-based agent view limited to the contact. By default it shows only the customer and shipment in question, with more detail revealed for a recorded reason. The DPO co-designs it, the DPIA covers it, and access is logged. Both targets can be met together.

- **Conflict 6 (Feature parity versus standard platform)**: The portal owners want to keep the features their customers rely on (SD-11, SD-12). The CIO prefers a SaaS or low-code platform (SD-6), and the CFO wants lower run cost (SD-3).
  - **Resolution Strategy**:
    - Base scope decisions on usage data [SI-C21].
    - Under reuse, then buy, then build, treat cold-chain compliance evidence and EDI order upload as candidate differentiating capabilities that may justify targeted extension or integration.
    - Drop low-usage features only with the owner's agreement, recorded in the feature-parity register.

- **Conflict 7 (Switch-off date inside peak freeze)**: The mandate sets the final switch-off for 31 December 2028 [PM-C7], which falls inside the peak freeze from 15 October 2028 to 10 January 2029 (SD-2) and at the same time as the Ghent data centre closure.
  - **Resolution Strategy**: Plan switch-off of all legacy portals by 14 October 2028. Use 31 December 2028 as the formal contingency date only, with the Sponsor's approval.

**Synergies**:

- **Synergy 1 (Identity)**: The COO's "one login" (SD-1), the CIO's one identity platform (SD-6), the CISO's hardened login (SD-9) and customers' convenience (SD-13, SD-14) are all met by G-5. Identity is the highest-value early deliverable.
- **Synergy 2 (One customer record)**: The DPO's on-time data subject requests (SD-10) and the Head of Customer Service's single view (SD-7) both depend on one customer record. Each data-quality step benefits both.
- **Synergy 3 (Platform exit)**: The CIO's end-of-life exit (SD-5) and the CFO's run-cost target (SD-3) are met by the same switch-offs, so each wave removes both risk and cost.
- **Synergy 4 (Self-service tracking)**: Proactive tracking reduces calls (SD-7), supports the self-service strategy (SD-1) and improves the customer experience (SD-13, SD-14).
- **Synergy 5 (Security and privacy controls)**: Central logging and EU-only access serve both the CISO (SD-9) and the DPO (SD-10). They should run a joint gate rather than two separate ones.

---

## Communication & Engagement Plan

### Stakeholder-Specific Messaging

#### Annelies Claes (COO, Sponsor)

**Primary Message**: One Acme is on track, wave by wave, with no risk to peak operations.

**Key Talking Points**:

- Progress against the four migration milestones
- Go/no-go criteria for each business unit and their status
- Decisions needed from the Sponsor (Conflicts 1, 3 and 7)

**Communication Frequency**: Monthly steering committee plus a fortnightly 1:1

**Preferred Channel**: Steering committee pack; one-page status

**Success Story**: Portal B customers on one Acme account by June 2027, before the Liferay contract ends.

---

#### Marc Dubois (CFO)

**Primary Message**: Run cost falls by at least 35%, and payback is evidenced, not assumed.

**Key Talking Points**:

- Run-cost path per wave and double-running cost
- Status of contact-centre benefits and their baselines
- TrackBox negotiation outcome

**Communication Frequency**: Monthly benefits dashboard; checkpoints at discovery close and at each funding release

**Preferred Channel**: Finance review meetings; dashboard

**Success Story**: Portal B costs stop on 30 June 2027 and the 12-month TrackBox extension is signed.

---

#### Sofie Peeters (CIO)

**Primary Message**: A bought platform and one identity service retire three end-of-life portals on time.

**Key Talking Points**:

- Platform options analysis and ADRs
- Portal B critical path
- Ghent data centre exit for Portal A

**Communication Frequency**: Weekly during discovery; monthly Architecture Board afterwards

**Preferred Channel**: Architecture Board; programme sync

**Success Story**: Platform ADR approved early, with Wave 1 on schedule.

---

#### Pieter Janssens (CISO)

**Primary Message**: One hardened login with MFA and central logging, and no gap at Portal A.

**Key Talking Points**:

- Identity design and MFA enrolment
- Interim Portal A protection decision
- How the portal maps to CyberFundamentals controls

**Communication Frequency**: Monthly; security gate before each release

**Preferred Channel**: Security review meeting

**Success Story**: No credential-stuffing incidents, and all business administrators on MFA.

---

#### Isabelle Martin (DPO)

**Primary Message**: One customer record makes data subject requests timely, and EU-only access is enforced by contract.

**Key Talking Points**:

- DPIA scope and status
- TrackBox clause outcome
- Design of the role-based agent view

**Communication Frequency**: Monthly; DPIA gates at discovery close and before each wave

**Preferred Channel**: Privacy review meeting

**Success Story**: TrackBox finding closed, and data subject requests answered within one month.

---

#### Nathalie Lambert (Head of Customer Service)

**Primary Message**: Fewer calls, faster answers, one agent screen, designed with your team.

**Key Talking Points**:

- Agent view pilot plan
- Benefit baselines and measurement
- Training and change plan for agents

**Communication Frequency**: Fortnightly during design; monthly benefits review

**Preferred Channel**: Workshops; benefits dashboard

**Success Story**: Pilot agents resolve tracking contacts in one screen, with measurably shorter handling time.

---

#### Portal Owners (Koen De Smet, Julie Leclercq, Tom Wouters)

**Primary Message**: No critical feature is lost; decisions are based on data and taken with you.

**Key Talking Points**:

- Usage data for your portal
- Feature-parity register and sign-off process
- Your role in your wave's go/no-go

**Communication Frequency**: Fortnightly feature-parity workshops

**Preferred Channel**: Workshops; shared feature register

**Success Story**: Your customers move with their critical features working, and no complaints.

---

#### Contact-Centre Agents

**Primary Message**: One tool replaces five, and you help shape it.

**Key Talking Points**:

- How the agent view works and what it will show
- Timeline and training

**Communication Frequency**: Monthly updates; pilot sessions

**Preferred Channel**: Team briefings; pilot group

**Success Story**: Agents ask for the new view to be rolled out faster.

---

#### Business Customers and Consumers

**Primary Message**: One Acme account for all your services, in your language, and more secure.

**Key Talking Points**:

- What changes and when, per business unit
- How to activate the new account and MFA
- Where to get help

**Communication Frequency**: Starting 8 weeks before each wave, with reminders at 4 weeks and 1 week

**Preferred Channel**: Email, in-portal notices and account managers (business customers); in Dutch, French and English

**Success Story**: High activation rates and low migration-related contact volumes.

---

#### Architecture Board, Executive Committee and External Parties

**Primary Message**: Decisions recorded and risks controlled (Board and Executive Committee). Clear contractual terms (TrackBox vendor, German hosting provider).

**Communication Frequency**: Board monthly; Executive Committee quarterly through the Sponsor; suppliers as negotiations require

**Preferred Channel**: ADRs; executive summary; commercial meetings

**Success Story**: ADRs approved without rework; contracts signed on time.

---

## Change Impact Assessment

### Impact on Stakeholders

| Stakeholder | Current State | Future State | Change Magnitude | Resistance Risk | Mitigation Strategy |
|-------------|---------------|--------------|------------------|-----------------|---------------------|
| Portal owners (A, B, C) | Own a portal and roadmap for their business unit | Feature owners within a shared group platform | HIGH | HIGH | Usage-based decisions, a feature-parity register, a role in go/no-go, and a clear future role as product owner for their domain |
| Contact-centre agents | Three portals and two CRMs | One agent view, plus the CRMs where still needed | HIGH | MEDIUM | Co-design, pilot group, training before each wave |
| Business customers | Separate logins per business unit; inconsistent languages | One account, delegated users, full NL/FR | MEDIUM | MEDIUM | Early communication, account migration, beta programme, EDI continuity |
| Pharma and food customers | Temperature evidence from TrackBox | Evidence from the new platform | HIGH | HIGH | Customer advisory group; validation of evidence and history before Wave 2 |
| Consumers | Portal A login without MFA | New login with MFA offered | MEDIUM | LOW | Simple activation, tracking without login, clear help content |
| IT Operations | Runs Portal A in Ghent; three contracts | Runs a bought platform and identity service | MEDIUM | LOW | Transition plan, run books, supplier handover |
| CISO and DPO teams | Findings open; data spread across systems | One controlled estate | LOW | LOW | Joint security and privacy gates |

### Change Readiness

**Champions** (Enthusiastic supporters):

- Annelies Claes (COO): owns the One Acme vision and sponsors the programme
- Sofie Peeters (CIO): the programme removes end-of-life platforms and introduces one identity service
- Pieter Janssens (CISO): the programme closes a known security weakness
- Isabelle Martin (DPO): the programme fixes a GDPR deadline breach
- Nathalie Lambert (Head of Customer Service): the programme directly reduces contact volumes and handling time

**Fence-sitters** (Neutral, need convincing):

- Marc Dubois (CFO): supports the cost reduction but needs a credible 4-year payback. Evidenced benefit baselines at discovery close would convince them
- Contact-centre agents: will judge on whether the new tool actually saves time. A successful pilot would convince them
- Julie Leclercq (Portal B owner): faces the first and most urgent move. A Wave 1 scope that protects EDI would convince them

**Resisters** (Opposed or skeptical):

- Tom Wouters (Portal C owner): cautious, because pharma evidence is non-negotiable and a generic platform could weaken it. Strategy: make cold-chain compliance a named design requirement, give the customer advisory group validation rights, and do not migrate without signed-off evidence
- Koen De Smet (Portal A owner): cautious about losing the returns flow for 41,000 monthly users. Strategy: use usage data, give returns priority in the backlog, and run consumer usability testing before Wave 3

---

## Risk Register (Stakeholder-Related)

### Risk R-1: Portal B Deadline Missed

**Related Stakeholders**: CIO, CFO, COO, Julie Leclercq, Brabant Freight customers

**Risk Description**: The platform is not chosen early enough to migrate Portal B before the Liferay hosting ends on 30 June 2027.

**Impact on Goals**: G-1, G-2, G-4

**Probability**: HIGH

**Impact**: HIGH

**Mitigation Strategy**: Bring the platform decision forward to January 2027; limit Wave 1 to minimum viable scope; plan migration during discovery.

**Contingency Plan**: Use a pre-negotiated 3-month hosting extension; final go/no-go by 31 May 2027.

---

### Risk R-2: Business Case Fails the 4-Year Payback Test

**Related Stakeholders**: CFO, COO, Head of Customer Service

**Risk Description**: Run-cost savings alone do not justify the envelope, and contact-centre benefits are not accepted as evidence.

**Impact on Goals**: G-2, and indirectly all goals if funding is withheld

**Probability**: MEDIUM

**Impact**: HIGH

**Mitigation Strategy**: Validate contact-centre baselines in discovery; agree the benefit-valuation method with the CFO early; aim for the lower end of the envelope.

**Contingency Plan**: Phase the funding by wave, with each release depending on benefits evidenced from the previous wave.

---

### Risk R-3: Portal A Credential-Stuffing Exposure Continues Until 2028

**Related Stakeholders**: CISO, CIO, consumers, Koen De Smet

**Risk Description**: Portal A still has no MFA until its migration in June 2028, which exposes customers and undermines the CyberFundamentals target at end 2027.

**Impact on Goals**: G-5

**Probability**: MEDIUM

**Impact**: HIGH

**Mitigation Strategy**: Decide during discovery between identity first and interim protection (Conflict 3).

**Contingency Plan**: CISO-approved risk acceptance with heightened monitoring, recorded as a formal exception.

---

### Risk R-4: TrackBox Vendor Refuses a Short Extension or EU-Only Support

**Related Stakeholders**: CFO, CIO, DPO, Tom Wouters

**Risk Description**: The vendor refuses a 12-month term or EU-only support, forcing a choice between a 3-year lock-in and a non-compliant extension.

**Impact on Goals**: G-3, G-2

**Probability**: MEDIUM

**Impact**: MEDIUM

**Mitigation Strategy**: Start negotiations in October 2026; agree acceptable compensating controls with the DPO in advance.

**Contingency Plan**: Escalate to the Sponsor and CFO. Options are a 3-year term with an early-exit clause, or compensating controls approved by the DPO.

---

### Risk R-5: No Slack for Wave 2 (Portal C)

**Related Stakeholders**: Tom Wouters, pharma and food customers, CIO

**Risk Description**: A 12-month extension ends on 31 March 2028, the same day as the Portal C migration deadline, which leaves no contingency.

**Impact on Goals**: G-1, G-9

**Probability**: MEDIUM

**Impact**: HIGH

**Mitigation Strategy**: Negotiate a monthly roll-on option after 31 March 2028; plan the Wave 2 go-live for the end of February 2028.

**Contingency Plan**: Use the roll-on option.

---

### Risk R-6: Migration Pushed Into the Peak Freeze

**Related Stakeholders**: COO, IT Operations, all customers

**Risk Description**: Delays push migrations or switch-offs into the period from 15 October to 10 January.

**Impact on Goals**: G-1

**Probability**: MEDIUM

**Impact**: HIGH

**Mitigation Strategy**: Plan all waves and switch-offs for February to September; hold a go/no-go 6 weeks before each wave.

**Contingency Plan**: Postpone to after 10 January and extend legacy contracts where possible.

---

### Risk R-7: Agent View Gains Limited Because the CRMs Are Out of Scope

**Related Stakeholders**: Head of Customer Service, agents, CFO

**Risk Description**: The two CRMs stay out of scope, so agents still switch between tools and the handling-time and first-contact-resolution gains are only partial.

**Impact on Goals**: G-7, and through O-3 also G-2

**Probability**: MEDIUM

**Impact**: MEDIUM

**Mitigation Strategy**: Design the agent view to read the relevant CRM data through interfaces, within scope.

**Contingency Plan**: Raise a change request for CRM consolidation to the steering committee.

---

### Risk R-8: Benefit Baselines Unreliable

**Related Stakeholders**: Head of Customer Service, CFO, COO

**Risk Description**: The two CRMs code contact reasons differently, so the 31% "where is my shipment?" baseline and the self-service baseline are disputed.

**Impact on Goals**: G-6, G-7

**Probability**: MEDIUM

**Impact**: MEDIUM

**Mitigation Strategy**: Harmonise contact-reason codes and validate the baseline during discovery.

**Contingency Plan**: Measure with sample studies before and after each wave.

---

## Governance & Decision Rights

### Decision Authority Matrix (RACI)

| Decision Type | Responsible | Accountable | Consulted | Informed |
|---------------|-------------|-------------|-----------|----------|
| Platform and identity selection (by 31 Mar 2027) | Enterprise Architecture team | Architecture Board (chair: CIO) | CISO, DPO, CFO, portal owners, Head of Customer Service | Steering committee, Executive Committee |
| TrackBox extension (by 31 Dec 2026) | CIO | CFO | DPO, Tom Wouters, CISO | Steering committee |
| Business case and funding releases | Programme manager | CFO | COO, CIO, Head of Customer Service | Executive Committee |
| Feature retain, change or drop | Programme Product Owner | COO (Sponsor) | Portal owners, customer representatives, CIO | Head of Customer Service |
| Go/no-go per business unit | Portal owner for that business unit | COO (Sponsor) | CIO, CISO, DPO, Head of Customer Service | Executive Committee, affected customers |
| Security risk acceptance and exceptions | CISO team | CISO | CIO, Architecture Board | Steering committee |
| DPIA approval | Programme team | COO (as business owner of the processing) | DPO | Steering committee |
| Architecture decisions (ADRs) | Enterprise Architecture team | Architecture Board | CISO, DPO, IT Operations | Steering committee |
| Legacy portal switch-off | IT Operations | CIO | Portal owner, DPO (data retention and archiving), Head of Customer Service | Customers, Executive Committee |

### Escalation Path

1. **Level 1**: Programme manager and Programme Product Owner (day-to-day delivery and backlog decisions)
2. **Level 2**: Monthly steering committee [PM-C13] (scope, timeline and budget variances; cross-business-unit conflicts)
3. **Level 3**: Annelies Claes, Sponsor (strategic direction, major conflicts, go/no-go). Design conflicts go to the Architecture Board as design authority
4. **Level 4**: Executive Committee (changes to the mandate, the EUR 4–6M envelope or the end-2028 objective)

---

## Validation & Sign-off

### Stakeholder Review

| Stakeholder | Review Date | Comments | Status |
|-------------|-------------|----------|--------|
| Annelies Claes (COO) | PENDING | — | PENDING |
| Marc Dubois (CFO) | PENDING | — | PENDING |
| Sofie Peeters (CIO) | PENDING | — | PENDING |
| Pieter Janssens (CISO) | PENDING | — | PENDING |
| Isabelle Martin (DPO) | PENDING | — | PENDING |
| Nathalie Lambert (Head of Customer Service) | PENDING | — | PENDING |
| Portal owners (A, B, C) | PENDING | — | PENDING |

### Document Approval

| Role | Name | Signature | Date |
|------|------|-----------|------|
| Project Sponsor | Annelies Claes (COO) | PENDING | PENDING |
| Business Owner | Nathalie Lambert (Head of Customer Service) | PENDING | PENDING |
| Enterprise Architect | Enterprise Architecture team | PENDING | PENDING |

---

## Appendices

### Appendix A: Stakeholder Interview Summaries

All interviews were held by the EA team in September 2026 [SI-C1].

#### Interview with Annelies Claes (COO) - September 2026

**Key Points**:

- Wants a single Acme presence by end 2028
- No migrations in peak season; a go/no-go for each business unit

**Quotes**:

- "Customers see three companies. By the end of 2028 they should see one Acme."

**Follow-up Actions**:

- Confirm go/no-go criteria per business unit
- Sponsor decision on bringing the final switch-off forward to 14 October 2028 (Conflict 7)

#### Interview with Marc Dubois (CFO) - September 2026

**Key Points**:

- Run cost must drop by at least 35%; payback within 4 years
- Discovery budget EUR 350,000; envelope EUR 4–6M indicative
- Avoid a 3-year TrackBox renewal

**Follow-up Actions**:

- Agree how contact-centre benefits are valued (Conflict 2)

#### Interview with Sofie Peeters (CIO) - September 2026

**Key Points**:

- Portal B is the first forced move (Liferay hosting ends June 2027)
- Prefers SaaS or low-code over custom build; wants one customer identity

**Follow-up Actions**:

- Plan for an earlier platform decision (Conflict 1)

#### Interview with Nathalie Lambert (Head of Customer Service) - September 2026

**Key Points**:

- 410,000 contacts a year, 31% "where is my shipment?"
- Average handling time 7 min 40 s; first-contact resolution 64%; agents use three portals and two CRMs
- Multi-contract customers confused by three invoice layouts

**Follow-up Actions**:

- Validate the contact-reason baseline across both CRMs (R-8)
- Raise invoice-layout harmonisation with Finance

#### Interview with Pieter Janssens (CISO) - September 2026

**Key Points**:

- Portal A has no MFA; credential-stuffing attack in February 2025
- CyberFundamentals level Important by end 2027; wants one hardened login and central logging

**Follow-up Actions**:

- Decide on the interim Portal A control (Conflict 3)

#### Interview with Isabelle Martin (DPO) - September 2026

**Key Points**:

- Data subject requests take 41 days on average against a one-month limit
- TrackBox non-EU support access is an open finding
- Agents should see only the data the contact needs

**Follow-up Actions**:

- Agree the TrackBox clause or compensating controls (Conflict 4)
- Co-design the agent view (Conflict 5)

#### Interview with Portal Owners (Koen De Smet, Julie Leclercq, Tom Wouters) - September 2026

**Key Points**:

- Critical features: returns (A), EDI order upload (B), temperature alerts and certificates (C)
- Pharma temperature records must be audit-proof
- Want usage data before dropping anything

**Quotes**:

- "Pharma customers require audit-proof temperature records: non-negotiable for Tom."

**Follow-up Actions**:

- Start collecting usage data in discovery (G-4)
- Set up the cold-chain customer advisory group

---

### Appendix B: Survey Results

No stakeholder or customer surveys have been run yet. A customer satisfaction baseline and an agent experience survey are recommended during discovery to support O-1 and O-3.

---

### Appendix C: References

- ARC-000-PRIN-v1.0, Acme Logistics NV Enterprise Architecture Principles (in particular principles 1, 2, 3, 9, 12, 13, 18 and 24)
- Acme Logistics NV company profile and Strategy 2030 (`000-global/policies/acme-company-profile.md`)
- Acme IT and architecture policies (`000-global/policies/acme-it-policies.md`)
- Programme mandate, stakeholder interviews and portal inventory (`001-customer-portal-consolidation/external/`)

---

## External References

> This section links content in this document back to its source documents, following the ArcKit citation instructions.

### Document Register

| Doc ID | Filename | Type | Source Location | Description |
|--------|----------|------|-----------------|-------------|
| PM | programme-mandate.md | Programme Mandate | 001-customer-portal-consolidation/external/ | Executive Committee mandate of 15 September 2026: objective, scope, milestones, targets, governance |
| SI | stakeholder-interviews.md | Interview Notes | 001-customer-portal-consolidation/external/ | EA team interview notes with nine stakeholders, September 2026 |
| PI | portal-inventory.md | Inventory | 001-customer-portal-consolidation/external/ | Current inventory of Portals A, B and C, August 2026 |
| ACP | acme-company-profile.md | Company Profile | 000-global/policies/ | Business units, customer overlap, peak season, Strategy 2030 |
| AIP | acme-it-policies.md | Policy | 000-global/policies/ | Cloud, sourcing, identity, classification, security and governance policies |

### Citations

| Citation ID | Doc ID | Page/Section | Category | Quoted Passage |
|-------------|--------|--------------|----------|----------------|
| PM-C1 | PM | Objective | Business Requirement | "Replace portals A, B and C with one customer portal and one customer record, fully in Dutch and French (English optional), by 31 December 2028." |
| PM-C2 | PM | Scope | Functional Requirement | "In: customer login, tracking, parcel and freight booking, returns, invoice and proof-of-delivery documents, temperature views for cold chain customers, customer user management, the customer service agent view, migration and switch-off of A, B and C." |
| PM-C3 | PM | Scope | Business Requirement | "Out: replacing the TMS systems, SAP S/4HANA or the CRMs; pricing changes; driver apps." |
| PM-C4 | PM | Milestones | Business Requirement | "Discovery complete and platform chosen: 31 March 2027" |
| PM-C5 | PM | Milestones | Procurement Constraint | "Decision on a 12-month TrackBox extension instead of a 3-year renewal: 31 December 2026" |
| PM-C6 | PM | Milestones | Business Requirement | "Portal B customers migrated before the Liferay hosting ends: 30 June 2027" |
| PM-C7 | PM | Milestones | Business Requirement | "Portal C customers migrated: 31 March 2028 / Portal A customers migrated: 30 June 2028 / All legacy portals switched off: 31 December 2028" |
| PM-C8 | PM | Targets | Business Requirement | "Portal run cost down at least 35% (baseline EUR 1.31M per year)" |
| PM-C9 | PM | Targets | Business Requirement | "\"Where is my shipment?\" calls down 40%" |
| PM-C10 | PM | Targets | Business Requirement | "Average handling time down 25%; first-contact resolution at least 80%" |
| PM-C11 | PM | Targets | Compliance Constraint | "100% of data subject requests answered within one month" |
| PM-C12 | PM | Targets | Security Requirement | "MFA for all users, mandatory for business administrators" |
| PM-C13 | PM | Governance | Stakeholder Need | "Sponsor: Annelies Claes (COO). Design authority: Architecture Board. Monthly steering committee." |
| SI-C1 | SI | Annelies Claes - COO | Stakeholder Need | "\"Customers see three companies. By the end of 2028 they should see one Acme.\"" |
| SI-C2 | SI | Annelies Claes - COO | Stakeholder Need | "No migrations during the peak season." |
| SI-C3 | SI | Annelies Claes - COO | Stakeholder Need | "Wants a clear go/no-go per business unit." |
| SI-C4 | SI | Marc Dubois - CFO | Stakeholder Need | "Run cost of the three portals (EUR 1.31M) must drop by at least 35%." |
| SI-C5 | SI | Marc Dubois - CFO | Stakeholder Need | "Payback within 4 years. Discovery budget EUR 350,000 approved; total envelope EUR 4-6M indicative." |
| SI-C6 | SI | Marc Dubois - CFO | Procurement Constraint | "Does not want to renew TrackBox for another 3 years if it can be avoided." |
| SI-C7 | SI | Sofie Peeters - CIO | Risk Factor | "Liferay hosting ends June 2027: Portal B is the first forced move." |
| SI-C8 | SI | Sofie Peeters - CIO | Design Decision | "Prefers a SaaS or low-code platform on Azure over another custom build." |
| SI-C9 | SI | Sofie Peeters - CIO | Design Decision | "Wants one customer identity platform for all channels." |
| SI-C10 | SI | Nathalie Lambert - Head of Customer Service | Stakeholder Need | "410,000 contacts per year; 31% are \"where is my shipment?\"." |
| SI-C11 | SI | Nathalie Lambert - Head of Customer Service | Stakeholder Need | "Agents switch between three portals and two CRMs. Average handling time 7 min 40 s; first-contact resolution 64%." |
| SI-C12 | SI | Nathalie Lambert - Head of Customer Service | Stakeholder Need | "Customers with several contracts get three invoice layouts and call to ask which one is right." |
| SI-C13 | SI | Pieter Janssens - CISO | Risk Factor | "Portal A has no MFA and was hit by credential stuffing in February 2025." |
| SI-C14 | SI | Pieter Janssens - CISO | Compliance Constraint | "NIS2: Acme is an important entity; CyFun level Important by end 2027." |
| SI-C15 | SI | Pieter Janssens - CISO | Security Requirement | "Wants one hardened login and central security logging." |
| SI-C16 | SI | Isabelle Martin - DPO | Compliance Constraint | "140 data subject requests per year, answered in 41 days on average (legal limit: one month). The data sits in three portals and two CRMs." |
| SI-C17 | SI | Isabelle Martin - DPO | Risk Factor | "TrackBox support access from outside the EU is an open finding." |
| SI-C18 | SI | Isabelle Martin - DPO | Data Requirement | "Agents must not see more personal data than the contact needs." |
| SI-C19 | SI | Portal owners | Stakeholder Need | "Fear losing features their customers rely on: A the returns flow, B the EDI order upload, C the temperature alerts and certificates." |
| SI-C20 | SI | Portal owners | Compliance Constraint | "Pharma customers require audit-proof temperature records: non-negotiable for Tom." |
| SI-C21 | SI | Portal owners | Stakeholder Need | "All three want usage data before deciding what can be dropped." |
| PI-C1 | PI | Registered users row | Business Requirement | Table row: 150,000 consumers + 4,200 business accounts (A); 3,100 business accounts (B); 2,200 business accounts (C) |
| PI-C2 | PI | Monthly active users row | Business Requirement | Table row: 41,000 (A); 2,600 (B); 1,900 (C) |
| PI-C3 | PI | Technology row | Risk Factor | Table row: .NET Framework 4.6, SQL Server, on-premises Ghent (A); Liferay 6.2 (out of support), Java, hosted by a German service provider (B); SaaS product "TrackBox", multi-tenant (C) |
| PI-C4 | PI | Login row | Security Requirement | Table row: own user database, no MFA (A); own user database, MFA optional (B); vendor login, MFA for admins only (C) |
| PI-C5 | PI | Languages row | Compliance Constraint | Table row: NL, FR, EN (A); NL, FR (French incomplete) (B); NL, EN (no French) (C) |
| PI-C6 | PI | Key features row | Functional Requirement | Table row lists the key features of each portal, including returns (A), EDI order upload (B), and temperature monitoring, alerts and compliance certificates (HACCP, GDP) (C) |
| PI-C7 | PI | Integrations row | Integration Requirement | Table row: TMS "ParcelCore", Dynamics 365 CRM, SAP S/4HANA (A); TMS "FreightMaster", Salesforce, SAP S/4HANA (B); telematics feed from trucks, SAP S/4HANA (C) |
| PI-C8 | PI | Annual run cost row | Business Requirement | Table row: EUR 610,000 (A); EUR 420,000 (B); EUR 280,000 (C). "Total run cost: EUR 1.31M per year." |
| PI-C9 | PI | Contract / end of life row | Procurement Constraint | Table row: in-house; .NET 4.6 out of support (A); hosting contract ends 30 June 2027 (B); subscription renews 31 March 2027 for 3 years (C) |
| PI-C10 | PI | Known issues row | Risk Factor | Table row: credential-stuffing attack Feb 2025, 12,000 password resets (A); slow (6.8 s average page load), no new features since 2022 (B); vendor support staff outside the EU can access data, DPA finding open (C) |
| ACP-C1 | ACP | At a glance | Stakeholder Need | "1,800 business customers use more than one portal (overlap analysis, Q2 2026)." |
| ACP-C2 | ACP | At a glance | Non-Functional Requirement | "Peak season: mid-October to early January, parcel volumes x2.3." |
| ACP-C3 | ACP | Strategy 2030 | Business Requirement | "Digital self-service as the default channel: 70% of service interactions." |
| ACP-C4 | ACP | At a glance | Compliance Constraint | "Dutch and French are required commercially and legally; English for international shippers." |
| AIP-C1 | AIP | Governance | Business Requirement | "Peak freeze: no go-lives or migrations between 15 October and 10 January." |
| AIP-C2 | AIP | Cloud and hosting | Design Decision | "The on-premises data centre in Ghent closes by end 2028." |
| AIP-C3 | AIP | Cloud and hosting | Data Requirement | "All customer data, backups, logs and vendor support access stay in the EU/EEA." |
| AIP-C4 | AIP | Security and compliance | Compliance Constraint | "New customer-facing services meet WCAG 2.2 AA." |
| AIP-C5 | AIP | Data classification | Data Requirement | "Customer personal data is Confidential. Credentials and security logs are Strictly Confidential." |
| AIP-C6 | AIP | Sourcing | Procurement Constraint | "Reuse, then buy (SaaS preferred), then build. Custom code only for differentiating capabilities." |

### Unreferenced Documents

| Filename | Source Location | Reason |
|----------|-----------------|--------|
| — | — | All consulted documents were cited |

---

**Generated by**: ArcKit `/arckit:stakeholders` command
**Generated on**: 2026-10-08
**ArcKit Version**: 6.17.5
**Project**: One Acme Customer Portal (Project 001)
**AI Model**: Claude Opus 5.5 (claude-opus-5-5)

<!-- arckit-provenance:start -->

## Build Provenance

*Stamped automatically by the ArcKit plugin's `provenance-stamp.mjs` PostToolUse hook. Complements (does not replace) the human-authored footer above. Carries only fields the model can't authoritatively self-report: build context from `.arckit/state.json` and effort levels derived from command frontmatter + the silent-downgrade matrix.*

| Field | Value |
|-------|-------|
| Requested Effort | `high` |
| Effective Effort | _unknown — model not parsed from existing footer_ |
| Stamped at | 2026-10-08T06:13:01.360Z |

<!-- arckit-provenance:end -->
