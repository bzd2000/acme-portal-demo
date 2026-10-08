# Project Requirements: One Acme Customer Portal

> **Template Origin**: Official | **ArcKit Version**: 6.17.5 | **Command**: `/arckit:requirements`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-REQ-v1.0 |
| **Document Type** | Business and Technical Requirements |
| **Project** | One Acme Customer Portal (Project 001) |
| **Classification** | Confidential |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-10-08 |
| **Last Modified** | 2026-10-08 |
| **Review Cycle** | Monthly |
| **Next Review Date** | 2026-11-07 |
| **Owner** | Enterprise Architecture team, for Annelies Claes (COO, Programme Sponsor) |
| **Reviewed By** | [PENDING] |
| **Approved By** | [PENDING] |
| **Distribution** | Project Team, Architecture Team, Architecture Board, programme steering committee |

> **Classification note**: This document uses the Acme data classification scheme (Public / Internal / Confidential / Strictly Confidential) [AIP-C7]. It is marked **Confidential** because it contains the investment envelope and supplier negotiation positions. For an RFP, prepare a vendor-facing extract without the Budget section or Conflicts C-1, C-2 and C-5, and share it under NDA.

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-10-08 | ArcKit AI | Initial creation from `/arckit:requirements` command | [PENDING] | [PENDING] |

## Document Purpose

This document sets out the business, functional, non-functional, integration and data requirements for the One Acme Customer Portal. It is the baseline for:

- platform and identity selection by 31 March 2027
- RFP and statement-of-work documents
- vendor evaluation
- design reviews by the Architecture Board
- acceptance testing at each migration wave

Every requirement traces back to the programme mandate, the stakeholder goals in ARC-001-STKE-v1.0, the success criteria in ARC-001-ADMP-v1.0 and the Acme architecture principles in ARC-000-PRIN-v1.0.

**Requirement ID scheme**:

| Prefix | Requirement type |
|--------|------------------|
| BR | Business |
| FR | Functional |
| NFR-P | Performance |
| NFR-A | Availability |
| NFR-S | Scalability |
| NFR-SEC | Security |
| NFR-C | Compliance |
| NFR-U | Usability |
| NFR-M | Maintainability |
| NFR-I | Interoperability |
| INT | Integration |
| DR | Data |

**Priority** uses MoSCoW: MUST_HAVE, SHOULD_HAVE, COULD_HAVE, WONT_HAVE.

---

## Executive Summary

### Business Context

Acme Logistics NV grew by acquisition, and each of its three business units still runs its own customer portal [PI-C3]:

| Portal | Business unit | Technology and status |
|--------|---------------|-----------------------|
| A "MyAcme" | Acme Parcel | In-house .NET application in the Ghent data centre |
| B "FreightView" | Brabant Freight | Liferay 6.2 site, out of support, hosting contract ends 30 June 2027 |
| C "ColdTrack" | Flanders Cold Chain | SaaS subscription ("TrackBox") |

Together they cost EUR 1.31M a year to run [PI-C8]. They give customers three logins and three experiences: 1,800 business customers use more than one portal [ACP-C1], and contact-centre agents switch between three portals and two CRMs [SI-C11].

On 15 September 2026 the Executive Committee mandated replacing Portals A, B and C with one customer portal and one customer record, fully in Dutch and French (English optional), by 31 December 2028 [PM-C1]. This delivers the Strategy 2030 commitment to "One Acme": one brand, one login, one customer record [ACP-C5]. It also contributes to the group's run-cost and digital self-service targets.

The programme is under real time pressure:

- **Portal B**: its hosting ends on 30 June 2027 [SI-C7].
- **Portal C**: its TrackBox subscription renews for 3 years on 31 March 2027 unless a 12-month extension is agreed [PI-C9] [SI-C6].
- **Portal A**: it has no MFA and was hit by credential stuffing in February 2025 [SI-C13].
- **Data subject requests**: they take 41 days on average to answer, against a one-month legal limit [SI-C16].

### Objectives

- Replace Portals A, B and C with one customer portal, one customer login and one customer record by 31 December 2028 [PM-C1]
- Cut portal run cost by at least 35% with payback within 4 years [PM-C5] [SI-C5]
- Cut contact-centre demand and handling effort through self-service and one agent view [PM-C6] [PM-C7]
- Meet GDPR, NIS2, accessibility and language obligations by design [PM-C8] [PM-C9]
- Keep every feature customers rely on, in particular returns (Portal A), EDI order upload (Portal B), and temperature alerts and certificates (Portal C) [SI-C19]

### Expected Outcomes

- **Run cost**: portal run cost of EUR 851,500 a year or less in 2029, down from EUR 1,310,000
- **"Where is my shipment?" contacts**: 76,260 a year or fewer, down 40% from about 127,100
- **Average handling time**: 345 s or less, down 25% from 460 s
- **First-contact resolution**: at least 80%, up from 64%
- **Data subject requests**: 100% answered within one month, down from an average of 41 days
- **MFA**: enforced for 100% of business administrators, with no successful credential-stuffing takeovers
- **Feature continuity**: no business-critical feature lost at any migration wave

### Project Scope

**In Scope** [PM-C2]:

- **Customer journeys**: customer login, tracking, parcel and freight booking, returns, invoice and proof-of-delivery documents, temperature views and alerts for cold-chain customers, and customer user management
- **Agent view**: the customer service agent view across business units
- **Identity and data**: one customer identity service and one authoritative customer record
- **Users**: consumers and business customers of Acme Parcel, Brabant Freight and Flanders Cold Chain
- **Integrations**: transport management systems, the ERP (invoice copies), the CRMs (read), the telematics feed, workforce identity and central security monitoring
- **Transition**: migration of users, accounts and history from Portals A, B and C, and switch-off of all three

**Out of Scope** [PM-C3]:

- Replacing the transport management systems, the ERP or the CRMs
- Changes to pricing or tariffs
- Driver apps
- Changes to invoice generation or Peppol e-invoicing; the portal shows invoice copies only [AIP-C11]
- Workforce identity redesign; the existing group service is reused [AIP-C5]

---

## Stakeholders

| Stakeholder | Role | Organization | Involvement Level |
|-------------|------|--------------|-------------------|
| Annelies Claes | COO, Programme Sponsor | Executive Committee | Decision maker; go/no-go per business unit [PM-C10] |
| Marc Dubois | CFO | Finance | Business case owner; funding gates |
| Sofie Peeters | CIO, chair of the Architecture Board | IT | Design authority; platform selection |
| Pieter Janssens | CISO | Security | Security review; risk acceptance |
| Isabelle Martin | DPO | Legal / Privacy | Regulatory compliance; DPIA advice |
| Nathalie Lambert | Head of Customer Service | Customer Service | Requirements for the agent view; owner of benefit measures |
| Koen De Smet | Portal A owner | Acme Parcel | Domain requirements and user acceptance (Wave 3) |
| Julie Leclercq | Portal B owner | Brabant Freight | Domain requirements and user acceptance (Wave 1) |
| Tom Wouters | Portal C owner | Flanders Cold Chain | Domain requirements and user acceptance (Wave 2) |
| Enterprise Architecture team | Enterprise Architect | Architecture | Technical oversight; author of this document |
| Programme Product Owner | Product Owner (not yet appointed) | Programme | Backlog and feature retain/drop decisions |

---

## Business Requirements

### BR-001: One Customer Portal Replaces Portals A, B and C

**Description**: Provide one customer portal, under one Acme brand, for consumers and business customers of all three business units. Migrate every active user to it and switch off Portals A, B and C [PM-C1].

**Rationale**: This is the core of the One Acme commitment [ACP-C5]. In the Sponsor's words, "Customers see three companies. By the end of 2028 they should see one Acme." [SI-C1] Three portals mean three run costs, three security postures and a split customer experience. Traces to STKE goal G-1, outcome O-1 and principle 1.

**Acceptance Criteria**:

- [ ] All active customers of Portals A, B and C use the new portal by 30 June 2028
- [ ] Portals A, B and C are switched off by 31 December 2028, with a target of 14 October 2028 (before the peak freeze)
- [ ] No new business-unit-specific customer portal has been created

**Priority**: MUST_HAVE

**Stakeholder**: Annelies Claes (COO)

---

### BR-002: Wave-Based Migration With a Go/No-Go per Business Unit

**Description**: Migrate customers in three waves, each with a formal go/no-go decision by the Sponsor [SI-C3]:

| Wave | Portal | Migrated by |
|------|--------|-------------|
| 1 | B | 30 June 2027 |
| 2 | C | 31 March 2028 |
| 3 | A | 30 June 2028 |

These dates come from the mandate [PM-C4].

**Rationale**: The dates are set by external contract ends (Portal B hosting, Portal C subscription) and by the end of life of Portal A's platform and the Ghent data centre [PI-C9] [AIP-C2]. A go/no-go per business unit keeps risk under control. Traces to G-1 and SD-2.

**Acceptance Criteria**:

- [ ] Each wave has documented go/no-go criteria, approved by the Sponsor at least 6 weeks before go-live
- [ ] Each wave completes on or before its mandated date
- [ ] Each go/no-go decision is recorded with the evidence reviewed

**Priority**: MUST_HAVE

**Stakeholder**: Annelies Claes (COO)

---

### BR-003: No Migrations or Go-Lives During the Peak Freeze

**Description**: No migration, go-live or legacy switch-off takes place between 15 October and 10 January [AIP-C14] [SI-C2].

**Rationale**: Parcel volumes rise 2.3 times in peak season [ACP-C2], and a failed change at peak would cause the greatest damage to customers and revenue. Traces to SD-2 and principle 24.

**Acceptance Criteria**:

- [ ] The programme plan contains no migration, go-live or switch-off dated between 15 October and 10 January
- [ ] Any emergency change during the freeze goes through group change management with Sponsor approval

**Priority**: MUST_HAVE

**Stakeholder**: Annelies Claes (COO)

---

### BR-004: Reduce Portal Run Cost by at Least 35%

**Description**: Reduce the annual run cost of the customer portal estate from EUR 1,310,000 to EUR 851,500 or less [PM-C5] [SI-C4].

**Rationale**: This contributes to the group target of a 20% cut in IT run cost by 2029. Traces to G-2, O-2 and principle 5.

**Acceptance Criteria**:

- [ ] Finance reports a portal run cost of EUR 851,500 or less for calendar year 2029
- [ ] Each legacy portal's run cost stops within 3 months of its wave completing

**Priority**: MUST_HAVE

**Stakeholder**: Marc Dubois (CFO)

---

### BR-005: Payback Within 4 Years Inside the Investment Envelope

**Description**: Deliver the programme within the indicative EUR 4–6M envelope, with payback within 4 years. Discovery must stay within the approved EUR 350,000 [SI-C5].

**Rationale**: This is the CFO's investment test. Run-cost savings alone (about EUR 458,500 a year) do not pay back the envelope within 4 years, so contact-centre and risk benefits must be measurable (see Conflict C-2). Traces to G-2 and SD-4.

**Acceptance Criteria**:

- [ ] At discovery close (31 March 2027), the business case shows payback within 4 years using baselines agreed with the CFO
- [ ] Discovery spend is EUR 350,000 or less
- [ ] Benefits are tracked against the business case after each wave

**Priority**: MUST_HAVE

**Stakeholder**: Marc Dubois (CFO)

---

### BR-006: Reduce "Where Is My Shipment?" Contacts by 40%

**Description**: Reduce "where is my shipment?" contacts from about 127,100 a year (31% of 410,000) to 76,260 or fewer [SI-C10] [PM-C6].

**Rationale**: This is the largest single contact reason. Self-service tracking and proactive notifications remove most of these calls. Traces to G-6, O-3 and principle 3.

**Acceptance Criteria**:

- [ ] The baseline is validated in both CRMs by 31 March 2027
- [ ] Annual "where is my shipment?" contacts are 76,260 or fewer by end 2029, normalised for shipment volume

**Priority**: MUST_HAVE

**Stakeholder**: Nathalie Lambert (Head of Customer Service)

---

### BR-007: Cut Handling Time by 25% and Raise First-Contact Resolution to 80%

**Description**: Reduce average handling time from 7 min 40 s to 5 min 45 s or less, and raise first-contact resolution from 64% to at least 80% [SI-C11] [PM-C7].

**Rationale**: Agents switching between five tools drives handling time up and resolution down. This is the main benefit stream behind payback. Traces to G-7 and O-3.

**Acceptance Criteria**:

- [ ] Average handling time is 345 s or less, measured monthly, by end 2029
- [ ] First-contact resolution is at least 80%, measured monthly, by end 2029

**Priority**: MUST_HAVE

**Stakeholder**: Nathalie Lambert (Head of Customer Service)

---

### BR-008: Keep Business-Critical Features of Each Portal

**Description**: The new portal must provide, at the latest by the go-live of the relevant wave, the features customers rely on [SI-C19]:

- **Returns flow** (Portal A)
- **EDI order upload** (Portal B)
- **Temperature alerts and compliance certificates** (Portal C), including audit-proof temperature records for pharma customers [SI-C20]

Other features are kept, changed or dropped based on usage data [SI-C21].

**Rationale**: Losing these features would drive customers away and break their own compliance obligations. The portal owners' support depends on them being kept. Traces to G-9, SD-11 and SD-12.

**Acceptance Criteria**:

- [ ] FR-015 (returns), FR-014 (EDI order upload), FR-019 (temperature alerts) and FR-020 (certificates) are accepted by the relevant portal owner before their wave's go/no-go
- [ ] A feature-parity register lists every feature of Portals A, B and C with a retain, change or drop decision based on usage data, signed off by its portal owner
- [ ] No feature marked critical is lost at any wave

**Priority**: MUST_HAVE

**Stakeholder**: Koen De Smet, Julie Leclercq, Tom Wouters (portal owners)

---

### BR-009: One Account per Customer Across Business Units

**Description**: Customers who use more than one business unit, about 1,800 business customers today [ACP-C1], have one Acme account that gives access to all their services, contracts and documents.

**Rationale**: "One login, one customer record" is a Strategy 2030 commitment [ACP-C5]. Traces to G-1, O-1 and principle 14.

**Acceptance Criteria**:

- [ ] 100% of the business customers who appear in more than one legacy portal are merged into one account by the end of Wave 3
- [ ] Each merge is traceable to its source records (see DR-004)

**Priority**: MUST_HAVE

**Stakeholder**: Annelies Claes (COO)

---

### BR-010: Compliance by Design

**Description**: The portal meets these obligations from its first release:

- **GDPR**: 100% of data subject requests answered within one month [PM-C8]
- **NIS2**: supports the CyberFundamentals level Important target by end 2027 [AIP-C9]
- **Accessibility**: WCAG 2.2 AA [AIP-C12]
- **Language**: full Dutch and French [PM-C1]
- **MFA**: offered to all users and mandatory for business administrators [PM-C9]

**Rationale**: These are legal obligations and part of Strategy 2030. They cost far less when designed in than when retrofitted. Traces to G-5, G-8, G-10, O-4 and principle 4.

**Acceptance Criteria**:

- [ ] Met through NFR-C-001 to NFR-C-005, NFR-U-002, NFR-U-003 and NFR-SEC-001, each tested before its wave's go-live

**Priority**: MUST_HAVE

**Stakeholder**: Isabelle Martin (DPO), Pieter Janssens (CISO)

---

### BR-011: Key Decisions Taken on Time

**Description**: Two decisions must be taken on time [PM-C4]:

- **By 31 December 2026**: agree a 12-month TrackBox extension instead of a 3-year renewal
- **By 31 March 2027**: choose the platform and customer identity service

Platform choice follows reuse, then buy (SaaS preferred), then build [AIP-C3] [SI-C8].

**Rationale**: Every later milestone depends on these decisions. Traces to G-3 and G-4.

**Acceptance Criteria**:

- [ ] The TrackBox extension decision is recorded by 31 December 2026
- [ ] The platform and identity ADRs are approved by the Architecture Board by 31 March 2027 [AIP-C13]

**Priority**: MUST_HAVE

**Stakeholder**: Sofie Peeters (CIO), Marc Dubois (CFO)

---

### BR-012: Digital Self-Service Is the Default Channel

**Description**: The portal contributes to the group target of 70% of service interactions through digital self-service [ACP-C3]. Every in-scope task can be completed without contacting staff.

**Rationale**: Self-service lowers cost to serve and is part of Strategy 2030. Traces to O-6 and principle 3.

**Acceptance Criteria**:

- [ ] The self-service baseline is measured by 31 March 2027
- [ ] All journeys in FR-007 to FR-021 can be completed without contacting staff
- [ ] Portal self-service rate is reported monthly

**Priority**: SHOULD_HAVE

**Stakeholder**: Nathalie Lambert (Head of Customer Service)

---

## Functional Requirements

### User Personas

#### Persona 1: Business Account Administrator

- **Role**: Logistics or office manager at a shipper with an Acme contract (parcel, freight or cold chain, often more than one)
- **Goals**: Manage colleagues' access, see all Acme services in one place, control spending and documents
- **Pain Points**: Separate accounts in up to three portals; three invoice layouts [SI-C12]; inconsistent MFA
- **Technical Proficiency**: Medium

#### Persona 2: Business Shipper Operator

- **Role**: Booking or dispatch clerk at a business customer
- **Goals**: Book pickups and pallets quickly, upload orders in bulk, track shipments, get proof of delivery
- **Pain Points**: Portal B is slow (6.8 s average page load) [PI-C10]; French is incomplete in Portal B and missing in Portal C [PI-C5]
- **Technical Proficiency**: Medium

#### Persona 3: Cold-Chain Quality Manager

- **Role**: Quality or compliance officer at a pharma or food customer
- **Goals**: Be alerted at once to temperature excursions; get audit-proof temperature records and GDP/HACCP certificates for audits
- **Pain Points**: Evidence must hold up in their own regulatory audits [SI-C20]; Portal C has no French interface [PI-C5]
- **Technical Proficiency**: Medium

#### Persona 4: Consumer

- **Role**: Private person sending or receiving parcels (about 150,000 registered users [PI-C1])
- **Goals**: Track a parcel and arrange a return quickly on a mobile phone
- **Pain Points**: Account compromised in the credential-stuffing incident (12,000 resets) [PI-C10]
- **Technical Proficiency**: Low to Medium

#### Persona 5: Customer Service Agent

- **Role**: Contact-centre agent handling calls and messages for all three business units
- **Goals**: Answer the customer in one contact from one screen
- **Pain Points**: Switching between three portals and two CRMs; handling time 7 min 40 s; first-contact resolution 64% [SI-C11]
- **Technical Proficiency**: Medium to High

#### Persona 6: Acme Privacy Officer

- **Role**: Member of the DPO's team handling data subject requests
- **Goals**: Find, export, correct or erase a person's data within the legal deadline
- **Pain Points**: Data spread over three portals and two CRMs; 41-day average [SI-C16]
- **Technical Proficiency**: Medium

---

### Use Cases

#### UC-1: First Login After Migration

**Actor**: Business Account Administrator (also Consumer)

**Preconditions**:

- The user's legacy account has been migrated to the customer record
- The user has received a migration notice in their language

**Main Flow**:

1. User opens the activation link from the migration notice
2. System verifies the link and identifies the migrated account
3. User sets new credentials and enrols in MFA (mandatory for administrators)
4. System links the identity to the merged customer account, including all business units and contracts
5. User sees one dashboard with shipments, documents and users from all business units

**Postconditions**:

- The user authenticates through the customer identity service only
- The legacy login is disabled for this user

**Alternative Flows**:

- **Alt 1a**: If the link has expired, the user requests a new link by email after verification
- **Alt 3a**: Consumers may skip MFA enrolment, but are prompted again at each login and when doing sensitive actions

**Exception Flows**:

- **Ex 1**: If the account matching was ambiguous, the user is told that customer service will contact them, and the case is queued for data stewards

**Business Rules**:

- Business administrators cannot complete activation without MFA [PM-C9]
- Legacy passwords are never migrated

**Priority**: CRITICAL

---

#### UC-2: Track a Shipment

**Actor**: Consumer, Business Shipper Operator

**Preconditions**:

- The shipment exists in a transport management system or in the cold-chain telematics data

**Main Flow**:

1. User enters a tracking number (consumers: number plus postcode, no login needed) or opens their shipment list
2. System retrieves status and events from the relevant transport management system
3. System shows status, expected delivery window and event history in the user's language
4. User subscribes to notifications for this shipment

**Postconditions**:

- Notification preference stored

**Alternative Flows**:

- **Alt 2a**: If the source system is unavailable, the system shows the last known status with a timestamp and a clear message

**Exception Flows**:

- **Ex 1**: Unknown number: a helpful error message with guidance, and no information about other shipments is disclosed

**Business Rules**:

- Anonymous tracking shows no personal data beyond what the number and postcode holder needs

**Priority**: CRITICAL

---

#### UC-3: Book a Parcel Pickup or Freight Shipment

**Actor**: Business Shipper Operator

**Preconditions**:

- Authenticated user with a booking role on a contract with the relevant business unit

**Main Flow**:

1. User selects service type (parcel pickup, or pallet and part-load freight)
2. System offers addresses from the address book and the contract's service options
3. User enters shipment details; for freight, the user can first request and accept a quote
4. System validates and submits the booking to the relevant transport management system
5. System confirms with a booking reference and adds it to the shipment list

**Postconditions**:

- Booking created in the transport management system; confirmation stored

**Alternative Flows**:

- **Alt 4a**: If the transport management system is unavailable, the booking is queued and confirmed when submitted, and the user is told

**Exception Flows**:

- **Ex 1**: If validation fails, field-level errors are shown in the user's language

**Business Rules**:

- Prices and tariffs come from existing pricing; the portal does not change pricing [PM-C3]

**Priority**: CRITICAL

---

#### UC-4: Create a Return

**Actor**: Consumer, Business Shipper Operator

**Preconditions**:

- An eligible delivered parcel, or an authorised business return

**Main Flow**:

1. User starts a return from the shipment or from a returns entry point
2. System checks eligibility and offers return options (drop-off point or pickup)
3. User selects an option and confirms
4. System creates the return in the parcel transport management system and issues a return label or code
5. User tracks the return like any other shipment

**Postconditions**:

- Return shipment registered and trackable

**Alternative Flows**:

- **Alt 1a**: A guest consumer starts a return with the tracking number and postcode

**Exception Flows**:

- **Ex 1**: If the parcel is not eligible, the system explains why and offers contact options

**Business Rules**:

- Return eligibility rules are those currently applied in Portal A, unless the Portal A owner agrees a change

**Priority**: CRITICAL

---

#### UC-5: Upload an EDI Order File

**Actor**: Business Shipper Operator (Brabant Freight customers)

**Preconditions**:

- Authenticated user with an order upload role; an EDI format agreed for the account

**Main Flow**:

1. User uploads an order file in an agreed format
2. System validates structure and content and shows a summary (orders accepted, rejected and why)
3. User confirms
4. System submits accepted orders to the freight transport management system
5. System shows booking references per order and keeps an upload history

**Postconditions**:

- Orders created; upload and result logged

**Alternative Flows**:

- **Alt 2a**: If some lines fail validation, the user can correct them and resubmit only the failed lines

**Exception Flows**:

- **Ex 1**: If the file format is unknown, the file is rejected with a clear error and no orders are created

**Business Rules**:

- Formats currently accepted by Portal B are accepted unchanged at migration

**Priority**: CRITICAL

---

#### UC-6: Handle a Temperature Excursion and Retrieve a Certificate

**Actor**: Cold-Chain Quality Manager

**Preconditions**:

- Cold-chain shipment with active temperature monitoring and alert thresholds

**Main Flow**:

1. System detects a reading outside the threshold from the telematics feed
2. System sends an alert through the user's chosen channels within the agreed time
3. User opens the alert and sees the temperature curve, location and time of the excursion
4. User acknowledges the alert and adds a note
5. After delivery, the user downloads the GDP/HACCP certificate with the full temperature record

**Postconditions**:

- Alert, acknowledgement and certificate stored as tamper-evident records

**Alternative Flows**:

- **Alt 2a**: If an alert is not acknowledged within the escalation time, it goes to the escalation contact

**Exception Flows**:

- **Ex 1**: Gap in telematics data: the gap is marked visibly on the record and certificate, never interpolated silently

**Business Rules**:

- Temperature records cannot be edited once stored

**Priority**: CRITICAL

---

#### UC-7: Agent Handles a "Where Is My Shipment?" Contact

**Actor**: Customer Service Agent

**Preconditions**:

- Agent authenticated through workforce identity with an agent role

**Main Flow**:

1. Agent searches by tracking number, customer name or account number
2. System shows the matching shipment and the minimum customer data needed for the contact
3. Agent sees status, events, documents and recent contact history from the relevant CRM
4. Agent resolves the query or takes an action on the customer's behalf (for example, resends a document)

**Postconditions**:

- Access logged; action recorded

**Alternative Flows**:

- **Alt 2a**: The agent records a reason to see more customer data; the system reveals it and logs the reason

**Exception Flows**:

- **Ex 1**: CRM unavailable: the shipment view still works and the CRM panel shows "unavailable"

**Business Rules**:

- Agents see only data needed for the contact [SI-C18]

**Priority**: HIGH

---

#### UC-8: Fulfil a Data Subject Request

**Actor**: Acme Privacy Officer

**Preconditions**:

- Verified data subject request logged

**Main Flow**:

1. Officer searches the customer record for the person
2. System lists all personal data held by the portal and the customer record, plus where else the person's data is held (CRMs, transport management systems)
3. Officer exports the data in a readable format, or carries out correction or erasure
4. System records the action and the date

**Postconditions**:

- Request fulfilled and logged with its date

**Alternative Flows**:

- **Alt 3a**: Erasure blocked by a legal retention obligation (for example, invoices); the system anonymises what it can and records the reason

**Exception Flows**:

- **Ex 1**: Person not found: the result is recorded

**Business Rules**:

- The answer is due within one month of receipt [PM-C8]

**Priority**: HIGH

---

### Functional Requirements Detail

#### Identity and Accounts

#### FR-001: Single Customer Login

**Description**: All customer users of all business units sign in through one customer identity service, which is shared by every customer channel [SI-C9].

**Relates To**: BR-001, BR-009, UC-1

**Rationale**: "One login" is a Strategy 2030 commitment. Today each portal has its own user store [AIP-C6]. Traces to principle 9.

**Acceptance Criteria**:

- [ ] Given a migrated user, when they sign in, then one credential gives access to all their business units and contracts
- [ ] Given any customer channel in scope, when authentication is needed, then the shared identity service is used and no local credential store exists
- [ ] Edge case: a user with both a consumer and a business role can switch context without signing in again

**Data Requirements**:

- **Inputs**: Credentials, MFA factor
- **Outputs**: Authenticated session with the user's account and roles
- **Validations**: Password policy and checks against known breached passwords

**Priority**: MUST_HAVE

**Complexity**: HIGH

**Dependencies**: BR-011 (identity selection), DR-001

**Assumptions**: Standard federation protocols are supported by the selected identity service

---

#### FR-002: Multi-Factor Authentication

**Description**: MFA is offered to all users and enforced for business account administrators [PM-C9]. Re-authentication with MFA (step-up) is required for sensitive actions: changing users or roles, changing bank or invoice details, and downloading certificates in bulk.

**Relates To**: BR-010, UC-1

**Rationale**: Portal A has no MFA and suffered credential stuffing [SI-C13]. The CISO wants one hardened login [SI-C15].

**Acceptance Criteria**:

- [ ] Given a business administrator, when they sign in, then MFA is required
- [ ] Given any user, when they open security settings, then they can enrol at least two MFA methods, including one that does not depend on SMS
- [ ] Given a sensitive action, when the session has no recent MFA, then step-up authentication is required

**Data Requirements**:

- **Inputs**: MFA enrolment data
- **Outputs**: MFA status per user
- **Validations**: Recovery codes issued at enrolment

**Priority**: MUST_HAVE

**Complexity**: MEDIUM

**Dependencies**: FR-001

**Assumptions**: Consumers accept optional MFA (see Conflict C-3)

---

#### FR-003: Self-Registration and Account Recovery

**Description**: New consumers and business users can register themselves. Business users join through an invitation from their administrator (FR-004). All users can recover access themselves, securely.

**Relates To**: BR-012, UC-1

**Rationale**: Recovering access is a common contact reason, and self-service recovery reduces calls.

**Acceptance Criteria**:

- [ ] Given a new consumer, when they register, then their email is verified before the account becomes active
- [ ] Given a forgotten password, when the user requests a reset, then the reset completes without contacting staff and the event is logged
- [ ] Edge case: repeated reset requests are rate-limited

**Data Requirements**:

- **Inputs**: Email, name, language
- **Outputs**: Verified account
- **Validations**: Email verification; bot protection

**Priority**: MUST_HAVE

**Complexity**: LOW

**Dependencies**: FR-001

**Assumptions**: None

---

#### FR-004: Business Accounts and Customer User Management

**Description**: A business account represents one customer organisation across all its Acme contracts and business units. Business administrators can invite, edit and deactivate users, and assign roles by business unit, contract and function (booking, tracking, invoices, EDI upload, temperature data, administration) [PM-C2].

**Relates To**: BR-009, UC-1

**Rationale**: Business customers need delegated access across services, and 1,800 customers use more than one business unit today [ACP-C1].

**Acceptance Criteria**:

- [ ] Given an administrator, when they invite a user and assign roles, then the user can access only those business units, contracts and functions
- [ ] Given a deactivated user, when they try to sign in, then access is refused immediately
- [ ] Every account always has at least one administrator

**Data Requirements**:

- **Inputs**: User details, roles, scopes
- **Outputs**: Role assignments
- **Validations**: Roles limited to the contracts the account holds

**Priority**: MUST_HAVE

**Complexity**: MEDIUM

**Dependencies**: FR-001, DR-001

**Assumptions**: Contract-to-business-unit relationships are available from the source systems

---

#### FR-005: Account Migration and Activation

**Description**: Users of Portals A, B and C are migrated without re-registering, by activating their existing account (UC-1). Their preferences, address books, saved settings and relevant history move with them.

**Relates To**: BR-001, BR-002, BR-009, UC-1

**Rationale**: Forcing users to re-register causes drop-out and contacts. The migration is the critical path for every wave.

**Acceptance Criteria**:

- [ ] Given a migrated user, when they activate, then their address book and preferences are present
- [ ] At least 90% of active users from each portal have activated within 8 weeks of their wave (proposed target, to be agreed per wave)
- [ ] Legacy passwords are never migrated

**Data Requirements**:

- **Inputs**: Legacy user and account data
- **Outputs**: Migrated accounts and activation status
- **Validations**: Match and merge rules (DR-004)

**Priority**: MUST_HAVE

**Complexity**: HIGH

**Dependencies**: DR-004, DR-005, INT-010

**Assumptions**: Data can be extracted from TrackBox (INT-010)

---

#### FR-006: Language Selection

**Description**: Users choose Dutch, French or English. The choice is stored in their profile and used for the portal, notifications and documents generated by the portal.

**Relates To**: BR-010, UC-1

**Rationale**: Dutch and French are legal and commercial requirements [ACP-C4]. Portal C has no French today [PI-C5].

**Acceptance Criteria**:

- [ ] Given a stored language, when the user receives a notification, then it is in that language
- [ ] Given a first visit, when the browser language is Dutch, French or English, then that language is preselected

**Data Requirements**:

- **Inputs**: Language choice
- **Outputs**: Profile language
- **Validations**: Only NL, FR or EN

**Priority**: MUST_HAVE

**Complexity**: LOW

**Dependencies**: NFR-U-003

**Assumptions**: None

---

#### Tracking

#### FR-007: Track and Trace Across Business Units

**Description**: One search finds parcel, freight and cold-chain shipments. Consumers can track without signing in using the tracking number and postcode. Signed-in users see their shipments across all business units (UC-2).

**Relates To**: BR-001, BR-006, UC-2

**Rationale**: "Where is my shipment?" is 31% of all contacts [SI-C10].

**Acceptance Criteria**:

- [ ] Given a valid tracking number and postcode, when a guest searches, then status, expected delivery window and event history are shown
- [ ] Given a business user, when they search, then results include shipments from every business unit they have access to
- [ ] Edge case: if the source system is unavailable, the last known status is shown with its timestamp

**Data Requirements**:

- **Inputs**: Tracking number, postcode or account context
- **Outputs**: Status and events
- **Validations**: Rate limiting for anonymous lookups

**Priority**: MUST_HAVE

**Complexity**: MEDIUM

**Dependencies**: INT-001, INT-002, INT-004

**Assumptions**: Both transport management systems expose tracking events

---

#### FR-008: Proactive Shipment Notifications

**Description**: Users can subscribe to status notifications (for example, out for delivery, delay, delivered or exception) by email, SMS or push, per shipment or as an account default.

**Relates To**: BR-006, BR-012, UC-2

**Rationale**: Telling customers before they ask is the most effective way to cut "where is my shipment?" calls.

**Acceptance Criteria**:

- [ ] Given a subscribed shipment, when its status changes to a notifiable event, then a notification is sent within 15 minutes of the event reaching the portal
- [ ] Given account defaults, when a new shipment is created for the account, then notifications follow the defaults
- [ ] Every notification includes an unsubscribe or manage-preferences link

**Data Requirements**:

- **Inputs**: Preferences, tracking events
- **Outputs**: Notifications
- **Validations**: Consent (FR-027)

**Priority**: MUST_HAVE

**Complexity**: MEDIUM

**Dependencies**: FR-027, INT-009

**Assumptions**: Tracking events are available close to real time

---

#### FR-009: Business Shipment Dashboard

**Description**: Business users see a filterable list of their shipments across business units, by status, date, reference, contract and business unit, and can export it.

**Relates To**: BR-001, BR-009

**Rationale**: Operators manage many shipments at once. One view replaces up to three portals.

**Acceptance Criteria**:

- [ ] Given a business user, when they filter by status and date, then results update for every business unit in scope
- [ ] Given a filtered list, when they export, then a CSV file with the visible columns is produced

**Data Requirements**:

- **Inputs**: Filters
- **Outputs**: Shipment list or export
- **Validations**: Role scope (FR-004)

**Priority**: MUST_HAVE

**Complexity**: MEDIUM

**Dependencies**: FR-004, FR-007

**Assumptions**: None

---

#### Booking

#### FR-010: Parcel Pickup Booking

**Description**: Business users book parcel pickups (Portal A feature) [PI-C6].

**Relates To**: BR-008, UC-3

**Rationale**: Core existing Acme Parcel feature in the mandate scope [PM-C2].

**Acceptance Criteria**:

- [ ] Given a valid pickup request, when submitted, then the parcel transport management system confirms it and a reference is shown
- [ ] Edge case: if the transport management system is unavailable, the booking is queued and the user is told

**Data Requirements**:

- **Inputs**: Address, date and time window, parcel details
- **Outputs**: Booking reference
- **Validations**: Service area and date rules from the transport management system

**Priority**: MUST_HAVE

**Complexity**: MEDIUM

**Dependencies**: INT-001

**Assumptions**: None

---

#### FR-011: Pallet and Part-Load Freight Booking

**Description**: Business users book pallet and part-load freight shipments (Portal B feature) [PI-C6].

**Relates To**: BR-008, UC-3

**Rationale**: Core Brabant Freight feature; needed for Wave 1.

**Acceptance Criteria**:

- [ ] Given a valid freight booking, when submitted, then the freight transport management system confirms it and a reference is shown
- [ ] All booking types used in Portal B in the last 12 months are supported, or have a documented, agreed alternative

**Data Requirements**:

- **Inputs**: Pallet count, dimensions, weights, addresses, dates
- **Outputs**: Booking reference
- **Validations**: Rules from the freight transport management system

**Priority**: MUST_HAVE

**Complexity**: MEDIUM

**Dependencies**: INT-002

**Assumptions**: None

---

#### FR-012: Freight Quotes

**Description**: Business users request a freight quote and turn an accepted quote into a booking (Portal B feature) [PI-C6].

**Relates To**: BR-008, UC-3

**Rationale**: Existing Portal B feature. Pricing logic stays in existing systems [PM-C3]. Its priority is confirmed by the usage review [SI-C21].

**Acceptance Criteria**:

- [ ] Given a quote request, when submitted, then a quote is returned from the existing pricing source and can be accepted within its validity period
- [ ] Given an accepted quote, when the user books, then the quote reference carries into the booking

**Data Requirements**:

- **Inputs**: Shipment details
- **Outputs**: Quote and validity
- **Validations**: No price calculation in the portal

**Priority**: SHOULD_HAVE

**Complexity**: MEDIUM

**Dependencies**: INT-002

**Assumptions**: The freight transport management system provides quotes

---

#### FR-013: Address Book

**Description**: Users keep an address book of senders and receivers, which is migrated from Portal A [PI-C6].

**Relates To**: BR-008, FR-005

**Rationale**: Saves re-entering addresses and reduces booking errors.

**Acceptance Criteria**:

- [ ] Given a migrated user, when they book, then their Portal A addresses are available
- [ ] Users can add, edit, delete and import addresses

**Data Requirements**:

- **Inputs**: Addresses
- **Outputs**: Address book
- **Validations**: Address format per country

**Priority**: SHOULD_HAVE

**Complexity**: LOW

**Dependencies**: FR-005

**Assumptions**: None

---

#### FR-014: EDI Order Upload (Must-Have Feature of Portal B)

**Description**: Brabant Freight business users upload order files in the EDI formats currently accepted by Portal B. The portal validates them, reports accepted and rejected lines with reasons, and submits accepted orders to the freight transport management system (UC-5) [SI-C19].

**Relates To**: BR-008, UC-5

**Rationale**: Business customers rely on this feature, and losing it would break their order processes and send work back to manual booking. The portal owner named it as a must-keep.

**Acceptance Criteria**:

- [ ] Given a file in any format accepted by Portal B today, when uploaded, then it is accepted unchanged, with no customer-side change needed at migration
- [ ] Given a file with invalid lines, when uploaded, then valid lines can be submitted and invalid lines are listed with reasons in the user's language
- [ ] Given a submitted upload, when processing completes, then booking references per order and the upload history are visible for at least 12 months
- [ ] A file with the largest order volume seen in Portal B over the last 12 months, plus 50%, is processed within 5 minutes
- [ ] Wave 1 cannot go live until the Portal B owner, Julie Leclercq, has accepted this requirement with real customer files

**Data Requirements**:

- **Inputs**: Order files
- **Outputs**: Orders, validation report, booking references
- **Validations**: Format and business rules from the freight transport management system

**Priority**: MUST_HAVE

**Complexity**: HIGH

**Dependencies**: INT-002

**Assumptions**: The list of formats and the volumes are documented from Portal B during discovery

---

#### Returns

#### FR-015: Returns Flow (Must-Have Feature of Portal A)

**Description**: Consumers and business users create a return for an eligible parcel, choose drop-off or pickup, receive a return label or code, and track the return (UC-4) [SI-C19].

**Relates To**: BR-008, BR-012, UC-4

**Rationale**: Portal A's returns flow is relied on by customers and named by the portal owner as a must-keep. Returns are a high-volume consumer journey on a portal with 41,000 monthly active users [PI-C2].

**Acceptance Criteria**:

- [ ] Given an eligible delivered parcel, when a consumer starts a return (signed in or as a guest), then a return is created in the parcel transport management system and a label or code is issued
- [ ] Given a business user, when they create returns for their customers, then the returns are linked to their account
- [ ] Eligibility rules match those of Portal A unless a change is agreed with the Portal A owner
- [ ] Returns are trackable like other shipments (FR-007)
- [ ] Wave 3 cannot go live until the Portal A owner, Koen De Smet, has accepted this requirement after consumer usability testing

**Data Requirements**:

- **Inputs**: Original shipment, return option
- **Outputs**: Return shipment and label or code
- **Validations**: Eligibility rules

**Priority**: MUST_HAVE

**Complexity**: MEDIUM

**Dependencies**: INT-001

**Assumptions**: The parcel transport management system supports return creation through an interface

---

#### Documents

#### FR-016: Invoice Copies Across Business Units

**Description**: Business users see one list of invoice copies from all business units and contracts, clearly labelled as copies of the official e-invoice, filterable and downloadable [AIP-C11].

**Relates To**: BR-007, BR-009

**Rationale**: Customers with several contracts receive three invoice layouts and call to ask which is right [SI-C12]. One labelled list with explanations reduces these calls. The ERP stays the source.

**Acceptance Criteria**:

- [ ] Given a business user with invoice rights, when they open invoices, then copies from every contract are listed, labelled with business unit and contract
- [ ] Each invoice copy matches the ERP document exactly
- [ ] An explanation page in Dutch, French and English shows how to read each business unit's invoice layout

**Data Requirements**:

- **Inputs**: Invoice documents from the ERP
- **Outputs**: Invoice list and PDF download
- **Validations**: Read-only

**Priority**: MUST_HAVE

**Complexity**: MEDIUM

**Dependencies**: INT-003

**Assumptions**: Invoice layout harmonisation is outside the programme

---

#### FR-017: Proof of Delivery Documents

**Description**: Users download proof of delivery for their shipments in all business units where it is available [PM-C2].

**Relates To**: BR-008

**Rationale**: Existing Portal B feature and a frequent reason for contacts.

**Acceptance Criteria**:

- [ ] Given a delivered shipment with proof of delivery, when the user opens it, then the document can be viewed and downloaded
- [ ] Business users can download proof of delivery in bulk for a filtered list

**Data Requirements**:

- **Inputs**: Proof-of-delivery documents
- **Outputs**: Download
- **Validations**: Role scope

**Priority**: MUST_HAVE

**Complexity**: LOW

**Dependencies**: INT-001, INT-002

**Assumptions**: None

---

#### Cold Chain

#### FR-018: Temperature Monitoring View

**Description**: Cold-chain customers see temperature data per shipment, as a curve over time with thresholds, location and excursions, close to real time from the telematics feed [PI-C6].

**Relates To**: BR-008, UC-6

**Rationale**: Core Flanders Cold Chain feature [PM-C2].

**Acceptance Criteria**:

- [ ] Given an active cold-chain shipment, when the user opens it, then readings no older than 5 minutes after their arrival from telematics are shown
- [ ] Gaps in data are visibly marked, never interpolated

**Data Requirements**:

- **Inputs**: Telematics readings
- **Outputs**: Temperature curve and excursions
- **Validations**: Units and sensor identification

**Priority**: MUST_HAVE

**Complexity**: MEDIUM

**Dependencies**: INT-004

**Assumptions**: The telematics feed can be connected to the new platform

---

#### FR-019: Temperature Alerts (Must-Have Feature of Portal C)

**Description**: Users set alert thresholds per shipment or product profile and receive alerts by their chosen channels when readings go outside them. They acknowledge alerts and add notes. Alerts that are not acknowledged escalate (UC-6) [SI-C19].

**Relates To**: BR-008, UC-6

**Rationale**: Pharma and food customers must act on excursions quickly to protect product and meet GDP and HACCP obligations. The portal owner named this feature as a must-keep.

**Acceptance Criteria**:

- [ ] Given a reading outside the threshold, when it reaches the platform, then an alert is sent within 5 minutes, measured end to end from the reading's arrival
- [ ] No alert is lost if a component fails; alerts are queued and delivered when service resumes (NFR-A-003)
- [ ] Given an alert, when the user acknowledges it, then the acknowledgement, user, time and note are stored and cannot be edited
- [ ] Given no acknowledgement within the configured time, when that time passes, then the alert goes to the escalation contact
- [ ] Wave 2 cannot go live until the Portal C owner, Tom Wouters, and the cold-chain customer advisory group have accepted this requirement

**Data Requirements**:

- **Inputs**: Thresholds, contacts, readings
- **Outputs**: Alerts, acknowledgements
- **Validations**: Thresholds within sensor range

**Priority**: MUST_HAVE

**Complexity**: HIGH

**Dependencies**: INT-004, INT-009, DR-006

**Assumptions**: The 5-minute target is checked with cold-chain customers during discovery

---

#### FR-020: Compliance Certificates (Must-Have Feature of Portal C)

**Description**: For each cold-chain shipment, the portal produces a compliance certificate (GDP or HACCP as applicable) with the complete, audit-proof temperature record, excursions, acknowledgements and data gaps. Users download it as a document they can check for tampering [SI-C20].

**Relates To**: BR-008, UC-6

**Rationale**: Pharma customers require audit-proof temperature records; this is non-negotiable. Certificates are the evidence customers present in their own audits.

**Acceptance Criteria**:

- [ ] Given a delivered cold-chain shipment, when the user requests the certificate, then it includes the full temperature record, thresholds, excursions, acknowledgements and marked gaps
- [ ] Each certificate carries an integrity check that can be verified (for example, a digital signature) so any change is detectable
- [ ] Certificates and their underlying records can be retrieved for the full retention period (DR-006), including those created in TrackBox before migration (FR-021)
- [ ] The cold-chain customer advisory group confirms that the certificate format meets their audit needs before Wave 2

**Data Requirements**:

- **Inputs**: Temperature records, alerts, shipment data
- **Outputs**: Signed certificate
- **Validations**: Completeness of the record

**Priority**: MUST_HAVE

**Complexity**: HIGH

**Dependencies**: DR-006, FR-021

**Assumptions**: Certificate content requirements are confirmed with pharma and food customers during discovery

---

#### FR-021: Historic Temperature Record Migration

**Description**: Historic temperature records, alerts and certificates from TrackBox are migrated, or kept retrievable through the new portal, for their full retention period, with integrity preserved.

**Relates To**: BR-008, FR-020

**Rationale**: Breaks in the evidence trail would expose pharma customers in audits.

**Acceptance Criteria**:

- [ ] A reconciliation report shows 100% of TrackBox records and certificates migrated with matching checksums
- [ ] Users retrieve pre-migration certificates from the new portal

**Data Requirements**:

- **Inputs**: TrackBox data export
- **Outputs**: Migrated records
- **Validations**: Checksums and record counts

**Priority**: MUST_HAVE

**Complexity**: HIGH

**Dependencies**: INT-010, DR-005, DR-006

**Assumptions**: The TrackBox contract allows a full data export (see Conflict C-5)

---

#### Customer Service

#### FR-022: Agent View Across Business Units

**Description**: Agents search by tracking number, customer, account or contract and see shipments, account status, documents and alerts across all business units in one view (UC-7) [PM-C2].

**Relates To**: BR-007, UC-7

**Rationale**: Agents switch between three portals and two CRMs today [SI-C11].

**Acceptance Criteria**:

- [ ] Given a tracking number, when the agent searches, then the shipment and its account context are shown in one screen for any business unit
- [ ] In a pilot, agents complete contacts without opening a legacy portal in at least 90% of "where is my shipment?" contacts

**Data Requirements**:

- **Inputs**: Search keys
- **Outputs**: Contact view
- **Validations**: Role scope

**Priority**: MUST_HAVE

**Complexity**: HIGH

**Dependencies**: FR-023, INT-005, INT-006, INT-007

**Assumptions**: None

---

#### FR-023: Contact-Scoped, Role-Based Data in the Agent View

**Description**: By default, the agent view shows only the data needed for the current contact. Agents can see more after recording a reason, and every access is logged [SI-C18].

**Relates To**: BR-010, UC-7

**Rationale**: The DPO requires that agents see no more personal data than the contact needs. Traces to principle 13.

**Acceptance Criteria**:

- [ ] Given a contact, when the agent opens a customer, then only the fields defined for that contact type are shown
- [ ] Given a reveal action, when the agent records a reason, then extra fields are shown and the access is logged
- [ ] The DPO approves the field set for each contact type before the first wave

**Data Requirements**:

- **Inputs**: Contact type, reason
- **Outputs**: Filtered view; access log
- **Validations**: Reason is mandatory

**Priority**: MUST_HAVE

**Complexity**: MEDIUM

**Dependencies**: NFR-C-002

**Assumptions**: None

---

#### FR-024: Assisted Actions on Behalf of the Customer

**Description**: Agents perform selected self-service actions on behalf of a customer (for example, resend a document, set up a return, update notification preferences). They use the same services as the portal, and every action is logged.

**Relates To**: BR-007, BR-012

**Rationale**: Customers get the same result in every channel, which raises first-contact resolution. Traces to principle 3.

**Acceptance Criteria**:

- [ ] Given an agent action, when it completes, then the customer sees the same result in the portal
- [ ] Each action records the agent, the customer, the time and the reason

**Data Requirements**:

- **Inputs**: Action parameters
- **Outputs**: Result; audit record
- **Validations**: Agent role permits the action

**Priority**: SHOULD_HAVE

**Complexity**: MEDIUM

**Dependencies**: FR-022

**Assumptions**: None

---

#### FR-025: CRM Contact History in the Agent View

**Description**: The agent view shows recent contact history for the customer from the relevant CRM (the Acme Parcel CRM or the Brabant Freight CRM), read-only [PI-C7].

**Relates To**: BR-007

**Rationale**: The CRMs stay out of scope [PM-C3], but agents need context to resolve contacts at the first attempt.

**Acceptance Criteria**:

- [ ] Given a customer with CRM history, when the agent opens the customer, then the last 10 contacts are shown with date, channel and summary
- [ ] If the CRM is unavailable, the rest of the view still works

**Data Requirements**:

- **Inputs**: CRM contact records
- **Outputs**: History panel
- **Validations**: Read-only

**Priority**: SHOULD_HAVE

**Complexity**: MEDIUM

**Dependencies**: INT-005, INT-006

**Assumptions**: Both CRMs offer a read interface

---

#### Privacy, Preferences and Operations

#### FR-026: Data Subject Request Support

**Description**: Privacy officers find all personal data for a person in the portal and customer record, and can export, correct, erase or anonymise it. A register shows where else the person's data is held (UC-8).

**Relates To**: BR-010, UC-8

**Rationale**: Requests take 41 days on average against a one-month limit, because the data is spread across systems [SI-C16].

**Acceptance Criteria**:

- [ ] Given a person's identifiers, when searched, then all their personal data in the portal and customer record is listed within 1 minute
- [ ] Export produces a readable, machine-readable file
- [ ] Erasure keeps data that must be kept by law (for example, invoice references) and records the reason
- [ ] 100% of requests in a 3-month trial are answered within one month

**Data Requirements**:

- **Inputs**: Identifiers
- **Outputs**: Export; erasure log
- **Validations**: Request verified

**Priority**: MUST_HAVE

**Complexity**: MEDIUM

**Dependencies**: DR-001, DR-003

**Assumptions**: None

---

#### FR-027: Consent and Communication Preferences

**Description**: Each user's consent and communication preferences are stored once and respected by all channels, including notifications and marketing.

**Relates To**: BR-010, FR-008

**Rationale**: Consent given in one business unit must not be assumed for others. Traces to principle 13.

**Acceptance Criteria**:

- [ ] Given a withdrawal of consent, when the user saves it, then all channels stop the relevant messages within 24 hours
- [ ] The consent history is kept with timestamps

**Data Requirements**:

- **Inputs**: Consent choices
- **Outputs**: Preference record
- **Validations**: Purpose-specific consent

**Priority**: MUST_HAVE

**Complexity**: LOW

**Dependencies**: DR-001

**Assumptions**: None

---

#### FR-028: Multilingual Content Management

**Description**: Acme staff manage help content, notices and labels in Dutch, French and English without developer involvement.

**Relates To**: BR-012, NFR-U-003

**Rationale**: Keeps content current and complete in all languages.

**Acceptance Criteria**:

- [ ] A content editor can publish a notice in all three languages without a code release
- [ ] Content cannot be published in one language while missing in Dutch or French

**Data Requirements**:

- **Inputs**: Content
- **Outputs**: Published content
- **Validations**: Translation completeness

**Priority**: SHOULD_HAVE

**Complexity**: LOW

**Dependencies**: None

**Assumptions**: None

---

#### FR-029: Usage Analytics

**Description**: Feature and journey usage, completion and drop-out are recorded per business unit in the new portal. The same measures are collected from Portals A, B and C during discovery.

**Relates To**: BR-008, BR-012, BR-006

**Rationale**: Portal owners want usage data before features are dropped [SI-C21], and benefits must be measured.

**Acceptance Criteria**:

- [ ] Usage reports for Portals A, B and C are available by 31 January 2027
- [ ] The new portal reports completion rate per journey and business unit monthly
- [ ] Analytics respects consent (FR-027)

**Data Requirements**:

- **Inputs**: Usage events
- **Outputs**: Reports
- **Validations**: No personal data beyond what consent allows

**Priority**: MUST_HAVE

**Complexity**: LOW

**Dependencies**: FR-027

**Assumptions**: Legacy portals can provide logs or analytics

---

#### FR-030: Legacy Redirects and Read-Only Transition

**Description**: After each wave, links to the legacy portal redirect to the new portal, and users are told about the move in their language. Where agreed, the legacy portal stays read-only for a short period before switch-off.

**Relates To**: BR-001, BR-002

**Rationale**: Avoids broken bookmarks, lost users and transition contacts.

**Acceptance Criteria**:

- [ ] Every known legacy URL pattern redirects to the matching page in the new portal
- [ ] Any read-only period is 3 months or less and ends before the peak freeze

**Data Requirements**:

- **Inputs**: URL map
- **Outputs**: Redirects
- **Validations**: None

**Priority**: SHOULD_HAVE

**Complexity**: LOW

**Dependencies**: BR-002

**Assumptions**: None

---

## Non-Functional Requirements (NFRs)

### Performance Requirements

#### NFR-P-001: Response Time

**Requirement**: Customer and agent journeys respond quickly at peak load. Today, Portal B averages 6.8 s per page [PI-C10].

- Page load: < 2 seconds (95th percentile)
- Tracking search result: < 1.5 seconds (95th percentile), excluding source system latency above 1 s, which must be reported separately
- Agent view search: < 2 seconds (95th percentile)

**Measurement Method**: Load testing before each wave; real-user monitoring in production

**Load Conditions**:

- **Peak load**: peak-hour volume of the December peak (2.3 times normal parcel volume [ACP-C2]) plus 20% margin, derived from the usage analytics in FR-029
- **User base**: about 45,500 monthly active users across the three portals today [PI-C2]
- **Data volume**: all migrated accounts plus 3 years of shipment and temperature history

**Rationale**: Slow pages push customers to the contact centre and work against the benefits in BR-006 and BR-007. Traces to principle 19.

**Acceptance Criteria**:

- [ ] A load test at peak load meets all three p95 targets
- [ ] Production monitoring reports the same percentiles monthly

**Priority**: MUST_HAVE

---

#### NFR-P-002: Throughput

**Requirement**: The system handles peak-season booking, tracking, EDI upload and telematics volumes without queuing that customers notice. The temperature data pipeline processes readings from all monitored vehicles without backlog.

**Scalability**: Scales with demand (NFR-S-001)

**Rationale**: Peak volumes are 2.3 times normal [ACP-C2].

**Acceptance Criteria**:

- [ ] A sustained 1-hour load test at peak load completes with an error rate below 0.1%
- [ ] Temperature pipeline latency stays within the FR-019 alert target at peak load

**Priority**: MUST_HAVE

---

### Availability and Resilience Requirements

#### NFR-A-001: Availability Target

**Requirement**: Customer portal and agent view availability is at least 99.9% a month (about 43.8 minutes of downtime). Temperature alerting availability is at least 99.95% a month.

- **Planned downtime**: none for customer journeys; maintenance must not interrupt service
- **Unplanned downtime**: within the targets above

**Maintenance Windows**: Only outside the peak freeze for major changes; routine changes without downtime

**Rationale**: Outages push customers to the contact centre. Missed temperature alerts put pharma products at risk. Traces to principle 20.

**Acceptance Criteria**:

- [ ] External synthetic monitoring shows monthly availability meets the targets
- [ ] No planned downtime affects customer journeys

**Priority**: MUST_HAVE

---

#### NFR-A-002: Disaster Recovery

**RPO (Recovery Point Objective)**: 15 minutes or less for portal and customer record data. No loss of temperature readings: readings are buffered and replayed.

**RTO (Recovery Time Objective)**: 4 hours or less for the full service; 1 hour or less for temperature alerting

**Backup Requirements**:

- **Frequency**: continuous or at least every 15 minutes
- **Retention**: in line with the retention schedule (DR-003)
- **Location**: EU/EEA only [AIP-C1]

**Failover Requirements**:

- Automatic failover across availability zones within EU/EEA regions
- Failover time: < 15 minutes for zone failure

**Rationale**: Customers depend on the portal for daily operations, and pharma customers on uninterrupted alerting.

**Acceptance Criteria**:

- [ ] A disaster recovery rehearsal before each wave and every year before the peak freeze meets the RTO and RPO
- [ ] All backups are confirmed to be in EU/EEA locations

**Priority**: MUST_HAVE

---

#### NFR-A-003: Fault Tolerance

**Requirement**: The portal degrades gracefully when a transport management system, the ERP, a CRM or the telematics feed is unavailable. Bookings and alerts are queued rather than lost.

**Resilience Patterns Required**:

- [ ] Circuit breaker for external dependencies
- [ ] Retry with exponential backoff
- [ ] Timeout on all network calls
- [ ] Bulkhead isolation for critical resources
- [ ] Graceful degradation with reduced functionality

**Rationale**: The portal depends on many back-end systems, and one failure must not take everything down. Traces to principle 7.

**Acceptance Criteria**:

- [ ] Fault-injection tests show the loss of any single back-end affects only the features that depend on it
- [ ] Queued bookings and alerts are delivered after recovery, with no loss

**Priority**: MUST_HAVE

---

### Scalability Requirements

#### NFR-S-001: Horizontal Scaling

**Requirement**: Capacity scales automatically for the peak and scales down afterwards, without code changes.

**Growth Projections**:

- **Year 1**: all Portal B users (3,100 business accounts) plus Wave 2 preparation
- **Year 2**: all users of the three portals (about 150,000 consumers and 9,500 business accounts [PI-C1])
- **Year 3**: user numbers stay flat; parcel volumes about 2.3 times normal at peak

**Scaling Triggers**: Demand metrics defined by the platform; capacity added within 5 minutes of the threshold

**Rationale**: Peak is seasonal, and paying for peak capacity all year conflicts with BR-004. Traces to principle 6.

**Acceptance Criteria**:

- [ ] A load test shows capacity grows near-linearly as instances are added
- [ ] Capacity returns to normal levels within 24 hours after demand falls

**Priority**: MUST_HAVE

---

#### NFR-S-002: Data Volume Scaling

**Requirement**: The system handles growth in temperature records, documents and shipment history over the retention periods without performance falling below NFR-P-001.

**Data Archival Strategy**: Hot data for active and recent shipments; cheaper storage for older records, which must stay retrievable (certificates in particular) within 1 minute

**Rationale**: Temperature records and certificates must be kept long-term (DR-006).

**Acceptance Criteria**:

- [ ] Performance tests at the projected 5-year data volume meet NFR-P-001
- [ ] An archived certificate is retrieved within 1 minute

**Priority**: SHOULD_HAVE

---

### Security Requirements

#### NFR-SEC-001: Authentication

**Requirement**: All customer users authenticate through the customer identity service using industry-standard protocols. All staff authenticate through the existing workforce identity service [AIP-C5].

**Multi-Factor Authentication (MFA)**:

- **Required for**: business administrators, all staff, and all users performing sensitive actions [PM-C9]
- **Offered to**: all users
- **Methods**: authenticator app, phishing-resistant keys or passkeys; SMS only as a fallback

**Protection against credential stuffing**: bot detection, rate limiting, checks against known breached passwords, and alerts on unusual sign-in patterns [SI-C13]

**Session Management**:

- **Inactivity timeout**: 30 minutes
- **Absolute timeout**: 12 hours
- **Re-authentication**: required for role changes, user management, bulk downloads and changes to contact details

**Rationale**: Portal A's credential-stuffing incident led to 12,000 password resets [PI-C10]. The CISO requires one hardened login [SI-C15]. Traces to principles 8 and 9.

**Acceptance Criteria**:

- [ ] 100% of business administrators and staff use MFA
- [ ] A penetration test, including a credential-stuffing simulation, finds no authentication bypass
- [ ] Session timeout and lockout behave as specified

**Priority**: MUST_HAVE

---

#### NFR-SEC-002: Authorization

**Requirement**: Role-based access control with least privilege. Customer roles are limited by account, business unit and contract (FR-004); agent roles by contact type (FR-023).

**Roles and Permissions**: Customer roles (administrator, booking, tracking, invoices, EDI upload, temperature data); staff roles (agent, team lead, privacy officer, content editor, support engineer)

**Privilege Elevation**: Time-limited, approved and logged; supplier support access only from the EU/EEA [AIP-C1]

**Rationale**: A compromised account must not expose other customers' data.

**Acceptance Criteria**:

- [ ] Access control tests show each role can do only what it is permitted to
- [ ] Privileged access is reviewed every quarter, and every privileged action is logged

**Priority**: MUST_HAVE

---

#### NFR-SEC-003: Data Encryption

**Requirement**:

- **Data in transit**: TLS 1.2 or higher (TLS 1.3 preferred) with strong cipher suites
- **Data at rest**: strong encryption (AES-256 or equivalent) for all data stores
- **Key management**: a managed key service in the EU/EEA, with Acme-controlled keys for Strictly Confidential data

**Encryption Scope**:

- [ ] Database encryption at rest
- [ ] Backup encryption
- [ ] File storage encryption, including documents and certificates
- [ ] Application-level field encryption for sensitive personal data where the platform supports it

**Rationale**: Customer personal data is Confidential; credentials and security logs are Strictly Confidential [AIP-C8].

**Acceptance Criteria**:

- [ ] A configuration scan confirms no unencrypted store or endpoint
- [ ] Key access is logged and restricted

**Priority**: MUST_HAVE

---

#### NFR-SEC-004: Secrets Management

**Requirement**: No secrets in code or configuration files. All secrets are held in a managed secrets store and rotated automatically, at least every 90 days for service credentials.

**Rationale**: Leaked credentials are a common route to compromise. Traces to principle 8.

**Acceptance Criteria**:

- [ ] Secret scanning in the pipeline finds no credentials
- [ ] Secret rotation runs automatically and is evidenced

**Priority**: MUST_HAVE

---

#### NFR-SEC-005: Vulnerability Management

**Requirement**:

- Dependency scanning in the delivery pipeline; critical findings block release
- Static and dynamic application security testing
- Independent penetration testing before each wave and at least once a year
- For SaaS components, vendor evidence of equivalent practice

**Remediation SLA**:

- **Critical**: 7 days
- **High**: 30 days
- **Medium**: 90 days

**Rationale**: The portal is internet-facing and holds Confidential data, and NIS2 requires managed vulnerabilities [AIP-C9].

**Acceptance Criteria**:

- [ ] Every release passes the scans
- [ ] Penetration test findings are fixed within the SLA and tracked to closure

**Priority**: MUST_HAVE

---

#### NFR-SEC-006: Central Security Logging

**Requirement**: All authentication, authorisation, administrative and security events from the portal, the identity service and the agent view go to central security monitoring within 5 minutes. They are handled as Strictly Confidential [AIP-C8] [SI-C15].

**Rationale**: The CISO requires central logging, and NIS2 incident detection depends on it.

**Acceptance Criteria**:

- [ ] 100% of the defined event types appear in central monitoring in tests
- [ ] Security logs are access-controlled as Strictly Confidential and stored in the EU/EEA

**Priority**: MUST_HAVE

---

#### NFR-SEC-007: Interim Protection for Portal A Until Migration

**Requirement**: By 31 December 2027, Portal A logins are protected against credential stuffing. This is done either by moving Portal A users to the new customer identity service early, or by adding interim controls in front of Portal A (bot protection, rate limiting, optional MFA). The CISO decides which during discovery (Conflict C-4).

**Rationale**: Portal A has no MFA [PI-C4] and will not be migrated until 30 June 2028, after the CyberFundamentals deadline at end 2027 [SI-C14].

**Acceptance Criteria**:

- [ ] The CISO has decided and recorded it in an ADR by 31 March 2027
- [ ] Protection is in place and tested by 31 December 2027

**Priority**: MUST_HAVE

---

### Compliance and Regulatory Requirements

#### NFR-C-001: Data Privacy Compliance

**Applicable Regulations**: GDPR, supervised by the Belgian Data Protection Authority (GBA/APD) [AIP-C10]

**Compliance Requirements**:

- [ ] Data subject rights (access, correction, erasure, portability) answered within one month (FR-026) [PM-C8]
- [ ] Consent management and audit trail (FR-027)
- [ ] Privacy by design and by default; minimum data in the agent view (FR-023)
- [ ] Personal data breach notification to the GBA/APD within 72 hours where required
- [ ] DPIA completed before live personal data is processed
- [ ] Every supplier processing customer data signs the Acme Data Processing Agreement [AIP-C4]

**Data Residency**: EU/EEA for all customer data, backups, logs and supplier support access (NFR-C-004)

**Data Retention**: According to the retention schedule (DR-003)

**Rationale**: Requests currently take 41 days on average, which is a breach of the deadline [SI-C16]. Traces to principle 13.

**Acceptance Criteria**:

- [ ] The DPIA is signed off before Wave 1 go-live
- [ ] 100% of data subject requests are answered within one month after Wave 3

**Priority**: MUST_HAVE

---

#### NFR-C-002: Audit Logging

**Requirement**: Comprehensive audit trail for compliance and forensics

**Audit Log Contents** (for sensitive operations, including agent access to customer data, role changes, data subject actions, and temperature record and certificate events):

- **Who**: user or service identity
- **What**: action performed
- **When**: timestamp (UTC, millisecond precision)
- **Where**: system component
- **Why**: context, such as request ID or the agent's recorded reason
- **Result**: success or failure

**Log Retention**: According to the retention schedule agreed by the CISO and DPO; in immutable storage in the EU/EEA

**Log Integrity**: Tamper-evident (cryptographic chaining or write-once storage)

**Rationale**: Audit trails are needed for accountability, NIS2 evidence and pharma audit support.

**Acceptance Criteria**:

- [ ] Every sensitive operation in the list above is logged with all six fields
- [ ] A tamper test detects any modification

**Priority**: MUST_HAVE

---

#### NFR-C-003: NIS2 and CyberFundamentals Evidence

**Requirement**: The portal estate provides evidence for the CyberFundamentals controls at assurance level Important, in time for the group target at end 2027 [AIP-C9]. This covers incident detection and reporting support, asset inventory, access control, logging, vulnerability management and supplier security.

**Rationale**: Acme is an important entity under the Belgian NIS2 law.

**Acceptance Criteria**:

- [ ] Portal controls are mapped to CyberFundamentals by 31 March 2027
- [ ] Evidence is accepted by the CISO by 31 December 2027

**Priority**: MUST_HAVE

---

#### NFR-C-004: EU/EEA Data Residency Including Support Access

**Requirement**: All customer data, backups, logs and supplier support access stay in the EU/EEA [AIP-C1]. This applies to the new platform, the identity service and any SaaS component. It also applies to TrackBox for the remainder of its contract (Conflict C-5).

**Rationale**: Group policy. TrackBox support access from outside the EU is an open finding [SI-C17].

**Acceptance Criteria**:

- [ ] Contracts for every supplier confirm the EU/EEA location of data, backups, logs and support
- [ ] There are no open findings on residency or support access by 31 March 2028

**Priority**: MUST_HAVE

---

#### NFR-C-005: Cold-Chain Evidence Integrity (GDP and HACCP)

**Requirement**: Temperature records, alerts, acknowledgements and certificates are complete, time-stamped, cannot be altered, and are retrievable for the retention period. This enables customers to rely on them under Good Distribution Practice (pharma) and HACCP (food) [SI-C20].

**Rationale**: Pharma customers' audits depend on this evidence.

**Acceptance Criteria**:

- [ ] Independent review (quality assurance or an external auditor) confirms the integrity controls before Wave 2
- [ ] The cold-chain customer advisory group accepts the evidence model

**Priority**: MUST_HAVE

---

### Usability Requirements

#### NFR-U-001: User Experience

**Requirement**: Customers complete core journeys unaided on desktop and mobile.

**UX Standards**:

- One Acme brand and design system across all journeys
- Accessibility: WCAG 2.2 Level AA (NFR-U-002)
- Mobile responsive design
- Browser support: the last 2 versions of the major browsers

**User Onboarding**: Contextual help and migration guidance in every language

**Rationale**: Self-service only works if it is easy. Traces to BR-012 and principle 3.

**Acceptance Criteria**:

- [ ] Usability testing with representative users from each business unit shows at least 90% complete each core journey unaided
- [ ] After each wave, satisfaction is at or above the pre-migration baseline

**Priority**: MUST_HAVE

---

#### NFR-U-002: Accessibility

**Requirement**: WCAG 2.2 Level AA compliance for all customer journeys and the agent view [AIP-C12]

**Accessibility Features**:

- [ ] Keyboard navigation for all functions
- [ ] Screen reader compatibility
- [ ] Sufficient contrast and support for high-contrast modes
- [ ] Text resizing without loss of content
- [ ] Alternative text for images and charts, including temperature curves
- [ ] Captions for video and audio

**Testing**: Automated accessibility testing in the delivery pipeline plus manual testing

**Rationale**: Group policy and legal requirement. Traces to principle 18.

**Acceptance Criteria**:

- [ ] An independent audit confirms WCAG 2.2 AA in Dutch and French before each wave
- [ ] Core journeys pass testing with assistive technology

**Priority**: MUST_HAVE

---

#### NFR-U-003: Localization and Internationalization

**Requirement**: Full Dutch and French for every journey, notification and document produced by the portal. English for international shippers [PM-C1] [ACP-C4].

**Localization Scope**:

- [ ] UI text translation
- [ ] Date and time formats per locale
- [ ] Currency formatting (EUR)
- [ ] Number formatting
- [ ] Right-to-left languages: not required

**Rationale**: Legal and commercial requirement. Portal B's French is incomplete and Portal C has none [PI-C5].

**Acceptance Criteria**:

- [ ] There are no untranslated strings in Dutch or French in production
- [ ] Dates, numbers and currency display in the user's locale

**Priority**: MUST_HAVE

---

### Maintainability and Supportability Requirements

#### NFR-M-001: Observability

**Requirement**: Comprehensive telemetry for monitoring and troubleshooting

**Telemetry Requirements**:

- **Logging**: structured logs, centralised, with no credentials or unnecessary personal data
- **Metrics**: request rate, errors and duration per journey and per business unit; business metrics (bookings, tracking lookups, self-service completion)
- **Tracing**: distributed tracing across portal, identity and integrations
- **Dashboards**: real-time operational and benefits dashboards
- **Alerts**: alerts based on SLOs, each with a runbook

**Log Levels**: DEBUG, INFO, WARN, ERROR, FATAL

**Rationale**: The service cannot be run at peak without visibility, and benefits must be measured. Traces to principle 10.

**Acceptance Criteria**:

- [ ] Correlation IDs flow across all components
- [ ] Every SLO has an alert linked to a runbook

**Priority**: MUST_HAVE

---

#### NFR-M-002: Documentation

**Requirement**: Comprehensive documentation for operators, developers and the Architecture Board

**Documentation Types**:

- [ ] Architecture documentation (C4 model) and ADRs [AIP-C13]
- [ ] API documentation (published, machine-readable specifications)
- [ ] Runbooks for operational procedures
- [ ] Troubleshooting guides
- [ ] User help in Dutch, French and English
- [ ] Administrator guides

**Documentation Format**: Version-controlled with the solution where possible

**Documentation Currency**: Updated within 10 working days of a change

**Rationale**: The platform will be run for many years and possibly by different suppliers.

**Acceptance Criteria**:

- [ ] Documentation is reviewed at each release
- [ ] Handover to IT Operations is accepted before Wave 1

**Priority**: MUST_HAVE

---

#### NFR-M-003: Operational Runbooks

**Requirement**: Runbooks for common operational tasks and incident response

**Runbook Coverage**:

- [ ] Deployment procedures
- [ ] Rollback procedures
- [ ] Backup and restore procedures
- [ ] Incident response, including NIS2 incident reporting steps
- [ ] Scaling procedures
- [ ] Disaster recovery procedures
- [ ] Wave cut-over and legacy switch-off procedures

**Rationale**: Consistent runbooks shorten incidents and reduce reliance on individuals.

**Acceptance Criteria**:

- [ ] A runbook exists for every alert
- [ ] A cut-over rehearsal is done for each wave

**Priority**: MUST_HAVE

---

#### NFR-M-004: Configuration Over Customisation

**Requirement**: Bought components are configured rather than customised. Custom extensions are limited to differentiating capabilities, such as the cold-chain evidence in FR-020 and the EDI upload in FR-014, and must not block upgrades [AIP-C3].

**Rationale**: Customisation raises run cost and blocks upgrades, which conflicts with BR-004. Traces to principle 2.

**Acceptance Criteria**:

- [ ] Every customisation is recorded in an ADR with its justification
- [ ] Vendor upgrades are applied within 6 months of release without rework

**Priority**: MUST_HAVE

---

### Portability and Interoperability Requirements

#### NFR-I-001: API Standards

**Requirement**: All interfaces the programme builds or exposes use open, versioned, documented standards, with published machine-readable specifications.

**API Design Principles**:

- Standard web protocols with standard methods
- Structured, documented payloads
- Explicit versioning with deprecation periods
- Consistent error response format
- Authentication through standard protocols

**Rationale**: Business units' back-ends must be replaceable without breaking the customer experience. Traces to principle 16.

**Acceptance Criteria**:

- [ ] Every interface has a published specification
- [ ] Breaking changes follow a versioning and deprecation process

**Priority**: MUST_HAVE

---

#### NFR-I-002: Integration Capabilities

**Requirement**: The system integrates with the systems listed under INT-001 to INT-010.

**Integration Patterns**:

- [ ] Request-response interfaces for queries and bookings
- [ ] Event-driven integration for tracking and temperature events
- [ ] File-based exchange where a legacy system offers nothing else (for example, migration extracts)
- [ ] Database replication across system boundaries is not allowed
- [ ] Webhooks or push notifications for real-time alerts

**Integration SLA**: At least 99.9% of messages processed successfully on the first attempt; the rest retried, and never lost

**Rationale**: Traces to principle 17.

**Acceptance Criteria**:

- [ ] Integration tests cover success and failure for every interface
- [ ] Failed exchanges are queued and alerted

**Priority**: MUST_HAVE

---

#### NFR-I-003: Data Portability and Exit

**Requirement**: All Acme data held by any supplier (accounts, preferences, documents, temperature records, audit logs) can be exported in documented open formats. The exit process is written into each contract.

**Export Formats**: CSV or JSON for structured data; PDF for documents, with integrity metadata

**Export Scope**: Complete export, plus filtered export for data subject requests

**Import Capability**: Bulk import for migration waves

**Rationale**: Avoids lock-in like the current TrackBox position [SI-C6].

**Acceptance Criteria**:

- [ ] A full export is tested before contract signature or during the first 6 months
- [ ] The export can be imported into a test environment without loss

**Priority**: MUST_HAVE

---

## Integration Requirements

### External System Integrations

#### INT-001: Integration with the Parcel Transport Management System (ParcelCore)

**Purpose**: Tracking events, pickup bookings, returns and proof of delivery for Acme Parcel [PI-C7]

**Integration Type**: Real-time interface plus event-driven updates

**Data Exchanged**:

- **From the portal to ParcelCore**: pickup bookings, return requests (on demand)
- **From ParcelCore to the portal**: tracking events (near real time), booking confirmations, proof-of-delivery references

**Integration Pattern**: Request-response for bookings; publish-subscribe for tracking events

**Authentication**: Service-to-service authentication with signed tokens or mutual certificates

**Error Handling**: Retry with backoff; queue bookings when the system is unavailable; dead-letter queue with alerting

**SLA**: Tracking events available in the portal within 5 minutes of creation

**Owner**: Acme Parcel IT / Koen De Smet (business owner)

**Rationale**: Supports FR-007, FR-010, FR-015 and FR-017.

**Acceptance Criteria**:

- [ ] End-to-end tests pass for tracking, booking and returns, in both success and failure cases
- [ ] No events are lost when the system is unavailable

**Priority**: MUST_HAVE

---

#### INT-002: Integration with the Freight Transport Management System (FreightMaster)

**Purpose**: Pallet bookings, quotes, EDI orders, tracking and proof of delivery for Brabant Freight [PI-C7]

**Integration Type**: Real-time interface plus event-driven updates

**Data Exchanged**:

- **From the portal to FreightMaster**: freight bookings, quote requests, orders from EDI upload
- **From FreightMaster to the portal**: quotes, confirmations, tracking events, proof of delivery

**Integration Pattern**: Request-response; publish-subscribe for events

**Authentication**: Service-to-service authentication

**Error Handling**: Retry and queue; per-line error reporting for EDI uploads

**SLA**: Booking confirmation within 30 seconds; EDI upload processing as in FR-014

**Owner**: Brabant Freight IT / Julie Leclercq (business owner)

**Rationale**: Supports FR-011, FR-012, FR-014 and FR-017. This is the critical path for Wave 1.

**Acceptance Criteria**:

- [ ] End-to-end tests pass with real customer EDI files
- [ ] Failure cases are queued and reported

**Priority**: MUST_HAVE

---

#### INT-003: Integration with the ERP (Invoice Copies)

**Purpose**: Provide invoice copies from the ERP, which remains the system of record and the source of Peppol e-invoices [AIP-C11]

**Integration Type**: Real-time query or batch document feed (read-only)

**Data Exchanged**:

- **From the portal to the ERP**: invoice queries by account and contract
- **From the ERP to the portal**: invoice metadata and documents

**Integration Pattern**: Request-response, or a daily batch with on-demand retrieval

**Authentication**: Service-to-service authentication

**Error Handling**: Show "temporarily unavailable" and retry

**SLA**: New invoices visible in the portal within 24 hours of issue

**Owner**: Finance / ERP team

**Rationale**: Supports FR-016.

**Acceptance Criteria**:

- [ ] Invoice copies match the ERP documents byte for byte
- [ ] The portal cannot change invoices

**Priority**: MUST_HAVE

---

#### INT-004: Integration with the Cold-Chain Telematics Feed

**Purpose**: Temperature readings and positions from trucks for monitoring, alerts and certificates [PI-C7]

**Integration Type**: Event streaming, near real time

**Data Exchanged**:

- **From the telematics feed to the portal**: temperature readings, sensor identifiers, timestamps, positions
- **From the portal to the telematics feed**: none

**Integration Pattern**: Publish-subscribe with buffering and replay

**Authentication**: Service-to-service authentication

**Error Handling**: Buffer and replay; gaps detected and marked (FR-018)

**SLA**: Readings available in the portal within 2 minutes of transmission, so that the 5-minute alert target in FR-019 can be met

**Owner**: Flanders Cold Chain operations / Tom Wouters (business owner)

**Rationale**: Supports FR-018 to FR-021.

**Acceptance Criteria**:

- [ ] A replay test after an outage shows no lost readings
- [ ] Gaps are detected and marked

**Priority**: MUST_HAVE

---

#### INT-005: Integration with the Acme Parcel CRM

**Purpose**: Read contact history for the agent view (the CRM stays out of scope for replacement) [PM-C3]

**Integration Type**: Real-time query (read-only)

**Data Exchanged**:

- **From the portal to the CRM**: query by customer
- **From the CRM to the portal**: recent contacts (date, channel, summary)

**Integration Pattern**: Request-response

**Authentication**: Service-to-service authentication

**Error Handling**: Panel shows "unavailable"; the rest of the view works

**SLA**: Response within 2 seconds at p95

**Owner**: Customer Service / CRM team

**Rationale**: Supports FR-025 and BR-007.

**Acceptance Criteria**:

- [ ] The agent view shows CRM history for test customers
- [ ] A CRM outage does not break the view

**Priority**: SHOULD_HAVE

---

#### INT-006: Integration with the Brabant Freight CRM

**Purpose**: Read contact history for the agent view [PI-C7]

**Integration Type**: Real-time query (read-only)

**Data Exchanged**:

- **From the portal to the CRM**: query by customer
- **From the CRM to the portal**: recent contacts

**Integration Pattern**: Request-response

**Authentication**: Service-to-service authentication

**Error Handling**: As INT-005

**SLA**: As INT-005

**Owner**: Customer Service / CRM team

**Rationale**: Supports FR-025 and BR-007.

**Acceptance Criteria**:

- [ ] As INT-005

**Priority**: SHOULD_HAVE

---

#### INT-007: Integration with Workforce Identity

**Purpose**: Staff sign-in for the agent view, administration and support, using the existing group workforce identity service [AIP-C5]

**Integration Type**: Identity federation

**Data Exchanged**:

- **From the portal to workforce identity**: authentication requests
- **From workforce identity to the portal**: identity, group and role claims

**Integration Pattern**: Standard federation protocol

**Authentication**: Federation trust

**Error Handling**: Staff access is unavailable during an outage; customer journeys are not affected

**SLA**: As provided by workforce identity

**Owner**: Group IT (Identity)

**Rationale**: Supports FR-022 and NFR-SEC-001. Traces to principle 9.

**Acceptance Criteria**:

- [ ] Staff use single sign-on with MFA
- [ ] Removing a person from a role in workforce identity removes their access within 1 hour

**Priority**: MUST_HAVE

---

#### INT-008: Integration with Central Security Monitoring

**Purpose**: Send security events to group security monitoring (NFR-SEC-006)

**Integration Type**: Log streaming

**Data Exchanged**:

- **From the portal to security monitoring**: authentication, authorisation, administrative and security events
- **From security monitoring to the portal**: none

**Integration Pattern**: Push or streaming

**Authentication**: Service-to-service authentication

**Error Handling**: Buffer locally, never drop events; alert if the delay exceeds 5 minutes

**SLA**: Events delivered within 5 minutes

**Owner**: CISO team

**Rationale**: NIS2 detection; the CISO's requirement for central logging [SI-C15].

**Acceptance Criteria**:

- [ ] All defined event types are visible in monitoring in tests

**Priority**: MUST_HAVE

---

#### INT-009: Integration with Notification Delivery Services

**Purpose**: Send email, SMS and push notifications for shipments and temperature alerts

**Integration Type**: Real-time interface

**Data Exchanged**:

- **From the portal to the notification service**: messages and recipients
- **From the notification service to the portal**: delivery status

**Integration Pattern**: Request-response with delivery callbacks

**Authentication**: Service-to-service authentication

**Error Handling**: Retry; fall back to another channel for temperature alerts

**SLA**: Sent within 1 minute of the trigger

**Owner**: Programme (supplier to be selected)

**Rationale**: Supports FR-008 and FR-019. Processing must stay in the EU/EEA [AIP-C1].

**Acceptance Criteria**:

- [ ] Delivery status is recorded for every message
- [ ] Failover between channels is tested for temperature alerts

**Priority**: MUST_HAVE

---

#### INT-010: Migration Extracts From Portals A, B and C

**Purpose**: Extract users, accounts, preferences, address books, documents, temperature records and certificates for migration [PI-C3]

**Integration Type**: Batch extract (one-off per wave, with delta runs)

**Data Exchanged**:

- **From the legacy portals to migration**: legacy data
- **From migration to the legacy portals**: none (switched off after the wave)

**Integration Pattern**: Extract, transform and load with reconciliation

**Authentication**: Restricted, logged access

**Error Handling**: Reconciliation reports; failed records corrected and re-run

**SLA**: Final delta within the wave's cut-over window

**Owner**: Portal owners and IT Operations

**Rationale**: Supports FR-005, FR-021 and DR-005. The TrackBox export is a contractual condition (Conflict C-5).

**Acceptance Criteria**:

- [ ] A full rehearsal extract for each portal reconciles at 100% of records before cut-over

**Priority**: MUST_HAVE

---

## Data Requirements

### Data Entities

All personal data below is **Confidential** under the Acme scheme. Credentials are **Strictly Confidential** [AIP-C8].

#### Entity 1: Customer (Party)

**Description**: The authoritative record of a person or organisation that is an Acme customer, across all business units

**Attributes**:

| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| customer_id | UUID | Yes | Unique identifier | Primary key |
| party_type | Enum | Yes | Person or organisation | ['person', 'organisation'] |
| legal_name | String(255) | Yes | Name | Not null |
| vat_number | String(20) | No | Organisation VAT number | Validated format; unique per organisation |
| preferred_language | Enum | Yes | Language | ['nl', 'fr', 'en'] |
| status | Enum | Yes | Lifecycle | ['active', 'inactive', 'merged', 'erased'] |
| source_refs | List | Yes | Links to legacy and source-system identifiers | For lineage |
| created_at / updated_at | Timestamp | Yes | Audit timestamps | Indexed |

**Relationships**:

- One-to-many with Business Account
- One-to-many with Consent

**Data Volume**: About 150,000 consumers and about 7,700–9,500 business organisations at migration (business accounts after merging duplicates)

**Access Patterns**: Lookup by ID, name, VAT number or email; data subject request search

**Data Classification**: CONFIDENTIAL (Acme scheme)

**Data Retention**: While the customer relationship lasts, plus the period in the retention schedule (DR-003)

---

#### Entity 2: Business Account and Contract Relationship

**Description**: A customer organisation's account and its contracts with each business unit

**Attributes**:

| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| account_id | UUID | Yes | Unique identifier | Primary key |
| customer_id | UUID | Yes | Owning customer | Foreign key |
| business_unit | Enum | Yes | Business unit | ['parcel', 'freight', 'cold_chain'] |
| contract_ref | String(50) | Yes | Contract reference in the source system | Unique per business unit |
| status | Enum | Yes | Contract status | ['active', 'suspended', 'ended'] |

**Relationships**:

- Many-to-one with Customer
- One-to-many with Portal User (through role assignments)

**Data Volume**: About 9,500 contract relationships at migration

**Access Patterns**: By customer; by contract reference

**Data Classification**: CONFIDENTIAL

**Data Retention**: As Customer

---

#### Entity 3: Portal User and Role Assignment

**Description**: A person who signs in, with roles scoped to accounts, business units and contracts. Credentials are held only in the identity service.

**Attributes**:

| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| user_id | UUID | Yes | Identifier linked to the identity service | Primary key |
| email | String(255) | Yes | Sign-in email | Unique |
| name | String(255) | Yes | Display name | Not null |
| roles | List | Yes | Role, account, business unit and contract scope | Validated against contracts |
| mfa_enrolled | Boolean | Yes | MFA status | Mandatory for administrators |
| status | Enum | Yes | Lifecycle | ['invited', 'active', 'deactivated'] |

**Relationships**:

- Many-to-many with Business Account through role assignments

**Data Volume**: About 160,000 users at migration

**Access Patterns**: By email; by account

**Data Classification**: CONFIDENTIAL; credentials STRICTLY CONFIDENTIAL (held in the identity service only)

**Data Retention**: Deactivated users are deleted or anonymised according to DR-003

---

#### Entity 4: Temperature Record

**Description**: Time-series temperature readings, excursions, alerts and acknowledgements for a cold-chain shipment

**Attributes**:

| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| record_id | UUID | Yes | Identifier | Primary key |
| shipment_ref | String(50) | Yes | Shipment reference | Indexed |
| sensor_id | String(50) | Yes | Sensor | Not null |
| reading_time | Timestamp | Yes | UTC time of the reading | Indexed |
| temperature_c | Decimal(5,2) | Yes | Reading | Within sensor range |
| integrity_hash | String | Yes | Tamper-evidence value | Chained |

**Relationships**:

- Many-to-one with Shipment (reference)
- One-to-many with Alert and Certificate

**Data Volume**: To be measured from TrackBox during discovery, together with the growth rate

**Access Patterns**: By shipment and time range

**Data Classification**: INTERNAL for readings; CONFIDENTIAL when linked to an identifiable customer's shipment

**Data Retention**: Set in the retention schedule, taking account of customers' GDP and HACCP obligations (DR-006)

---

#### Entity 5: Document (Invoice Copy, Proof of Delivery, Certificate)

**Description**: Documents shown to customers. Invoice copies are owned by the ERP; certificates are produced by the portal.

**Attributes**:

| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| document_id | UUID | Yes | Identifier | Primary key |
| type | Enum | Yes | Document type | ['invoice_copy', 'pod', 'certificate'] |
| source_system | String(50) | Yes | Owner system | Not null |
| account_id | UUID | Yes | Owning account | Foreign key |
| signature | String | Certificates only | Integrity value | Verifiable |

**Relationships**:

- Many-to-one with Business Account

**Data Volume**: To be measured during discovery

**Access Patterns**: By account, type and date

**Data Classification**: CONFIDENTIAL

**Data Retention**: Invoices according to legal retention for accounting records; certificates according to DR-006; proof of delivery according to DR-003

---

#### Entity 6: Consent and Preferences

**Description**: Consent and communication preferences per user and purpose

**Attributes**:

| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| consent_id | UUID | Yes | Identifier | Primary key |
| user_id | UUID | Yes | User | Foreign key |
| purpose | Enum | Yes | Purpose | Defined list |
| granted | Boolean | Yes | State | Not null |
| changed_at | Timestamp | Yes | Change time | History kept |

**Relationships**:

- Many-to-one with Portal User

**Data Volume**: A few records per user

**Access Patterns**: By user and purpose

**Data Classification**: CONFIDENTIAL

**Data Retention**: Kept with the user record, as evidence of consent

---

#### Entity 7: Audit and Access Log

**Description**: Records of sensitive operations and agent access (NFR-C-002)

**Attributes**:

| Attribute | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| event_id | UUID | Yes | Identifier | Primary key |
| actor | String | Yes | User or service | Not null |
| action | String | Yes | Action | Not null |
| target | String | Yes | Object affected | Not null |
| reason | String | Conditional | Recorded reason (agent reveal) | Required for reveal actions |
| timestamp | Timestamp | Yes | UTC, millisecond precision | Indexed |

**Relationships**: Links to users and targets by ID

**Data Volume**: High; partitioned by time

**Access Patterns**: Investigations, audits, data subject requests

**Data Classification**: STRICTLY CONFIDENTIAL for security logs [AIP-C8]

**Data Retention**: According to the retention schedule agreed by the CISO and DPO

---

### Data Requirements Detail

#### DR-001: One Authoritative Customer Record

**Description**: The customer record (Entities 1–3 and 6) is the single authoritative source for customer identity, accounts, contract relationships and preferences used by the portal and the agent view [PM-C1]. The transport management systems, ERP and CRMs remain authoritative for shipments, invoices and contacts.

**Rationale**: Traces to BR-009, principle 14 and STKE synergy 2 (data subject requests and the agent view).

**Acceptance Criteria**:

- [ ] A system-of-record register names the authoritative system for each data entity
- [ ] There is no two-way synchronisation without a documented conflict rule

**Priority**: MUST_HAVE

---

#### DR-002: Classification Using the Acme Scheme

**Description**: Every data store and data flow is classified using the Acme scheme before go-live. Customer personal data is at least Confidential; credentials and security logs are Strictly Confidential [AIP-C7] [AIP-C8].

**Rationale**: Group policy; traces to principle 12.

**Acceptance Criteria**:

- [ ] The data catalogue shows a classification and owner for 100% of stores before each wave

**Priority**: MUST_HAVE

---

#### DR-003: Retention and Deletion

**Description**: A retention schedule is agreed with the DPO for every data type: accounts, consent, documents, logs and temperature records. Deletion or anonymisation runs automatically, with legal holds where needed.

**Rationale**: GDPR storage limitation; supports data subject requests (FR-026).

**Acceptance Criteria**:

- [ ] The retention schedule is approved by the DPO before Wave 1
- [ ] Automated deletion is tested

**Priority**: MUST_HAVE

---

#### DR-004: Data Quality, Matching and Merging

**Description**: Duplicate customers across the three portals (including the 1,800 multi-portal business customers [ACP-C1]) are matched and merged using documented rules. Every merge keeps the source identifiers, and uncertain matches are reviewed by data stewards.

**Rationale**: BR-009; traces to principle 15.

**Acceptance Criteria**:

- [ ] The matching rules are approved by the portal owners and the DPO
- [ ] Every merged record traces to its source records
- [ ] Wrong merges found in testing are below 0.5% of a validated sample before go-live

**Priority**: MUST_HAVE

---

#### DR-005: Migration Completeness and Reconciliation

**Description**: Each wave's migration reconciles record counts and checksums for users, accounts, preferences, address books, documents and temperature records. Rollback is possible until the go/no-go after cut-over.

**Rationale**: BR-002; supports the go/no-go per business unit.

**Acceptance Criteria**:

- [ ] Reconciliation shows 100% of records accounted for (migrated, merged or excluded with a reason)
- [ ] The rollback procedure is rehearsed before each wave

**Priority**: MUST_HAVE

---

#### DR-006: Temperature Record Integrity and Retention

**Description**: Temperature records, alerts, acknowledgements and certificates are stored so that changes can be detected (Entity 4). They are retained for the period agreed with cold-chain customers and the DPO, and stay retrievable across platform changes, including TrackBox history (FR-021).

**Rationale**: Audit-proof evidence for pharma customers [SI-C20]; NFR-C-005.

**Acceptance Criteria**:

- [ ] Integrity checks detect any modification in testing
- [ ] Retention periods are confirmed with the customer advisory group and the DPO

**Priority**: MUST_HAVE

---

#### DR-007: EU/EEA Residency of Data

**Description**: All data in Entities 1–7, including backups and replicas, is stored and processed in the EU/EEA [AIP-C1].

**Rationale**: Group policy; NFR-C-004.

**Acceptance Criteria**:

- [ ] Hosting locations are confirmed by configuration evidence and contracts

**Priority**: MUST_HAVE

---

#### DR-008: No Live Personal Data in Non-Production

**Description**: Development and test environments use synthetic or anonymised data. Migration rehearsals with real data run only in controlled environments with production-level security.

**Rationale**: Principles 13 and 23.

**Acceptance Criteria**:

- [ ] Environment scans find no live personal data in non-production environments

**Priority**: MUST_HAVE

---

### Data Quality Requirements

**Data Accuracy**: Below 0.5% wrong customer merges in validated samples (DR-004). Email and VAT numbers are validated at entry.

**Data Completeness**: Mandatory fields as in the entity tables. Migrated records with missing mandatory data are queued for data steward correction, not loaded incomplete.

**Data Consistency**: Customer, account and contract data reconcile with the source systems at least daily.

**Data Timeliness**: Tracking events within 5 minutes; temperature readings within 2 minutes; invoices within 24 hours.

**Data Lineage**: Source identifiers kept on every migrated or merged record. Transformation rules are version-controlled.

---

### Data Migration Requirements

**Migration Scope**: Users, accounts, contract relationships, preferences, consent, address books, notification settings, upload history (Portal B), and temperature records, alerts and certificates (Portal C). Shipment history comes from the source systems rather than being migrated.

**Migration Strategy**: Phased by wave (B, then C, then A), each with rehearsals and a delta cut-over

**Data Transformation**: Mapping to the customer record model; matching and merging (DR-004); language defaults; role mapping

**Data Validation**: Reconciliation of counts and checksums (DR-005); test activation by sample users from each business unit

**Rollback Plan**: The legacy portal stays available (read-only or active) until the go/no-go after cut-over confirms success

**Migration Timeline**:

| Wave | Portal | Completed by |
|------|--------|--------------|
| 1 | B | 30 June 2027 |
| 2 | C | 31 March 2028 |
| 3 | A | 30 June 2028 |

No cut-over is allowed between 15 October and 10 January [PM-C4] [AIP-C14].

---

## Constraints and Assumptions

### Technical Constraints

**TC-1**: Hosting must be on the group's strategic cloud platform [AIP-C15], or on SaaS that meets EU/EEA residency for data, backups, logs and support access [AIP-C1].

**TC-2**: The transport management systems, ERP and CRMs are not replaced. They stay systems of record and are reached through interfaces [PM-C3].

**TC-3**: Staff authentication uses the existing workforce identity service [AIP-C5].

**TC-4**: The sourcing order is reuse, then buy (SaaS preferred), then build. Custom code is for differentiating capabilities only [AIP-C3].

**TC-5**: The portal shows invoice copies only. Invoices and Peppol e-invoicing stay in the ERP [AIP-C11].

---

### Business Constraints

**BC-1**: The mandate milestones are fixed [PM-C4]:

| Milestone | Date |
|-----------|------|
| TrackBox extension decision | 31 December 2026 |
| Platform chosen | 31 March 2027 |
| Portal B migrated | 30 June 2027 |
| Portal C migrated | 31 March 2028 |
| Portal A migrated | 30 June 2028 |
| All legacy portals switched off | 31 December 2028 |

**BC-2**: Discovery budget is EUR 350,000. The total envelope is EUR 4–6M (indicative). Payback must be within 4 years [SI-C5].

**BC-3**: No migrations or go-lives between 15 October and 10 January [AIP-C14].

**BC-4**: Pricing changes and driver apps are out of scope [PM-C3].

---

### Assumptions

**A-1**: The transport management systems, the ERP, the CRMs and the telematics feed can provide the interfaces in INT-001 to INT-006, or can be extended to within the envelope.

**A-2**: TrackBox data (including temperature history and certificates) can be fully exported under the current contract or the extension.

**A-3**: A market solution exists that meets the MUST_HAVE requirements for identity, portal, language and accessibility. Cold-chain evidence and EDI upload may need targeted extension.

**A-4**: Usage data can be collected from all three portals by 31 January 2027.

**A-5**: The contact-reason coding in both CRMs can be aligned to give a reliable baseline for BR-006 and BR-007.

**A-6**: The 5-minute temperature alert target (FR-019) matches what cold-chain customers need.

**Validation Plan**: Each assumption is checked during discovery and closed or turned into a risk by 31 March 2027. The Enterprise Architecture team reports on them to the steering committee every month.

---

## Success Criteria and KPIs

### Business Success Metrics

| Metric | Baseline | Target | Timeline | Measurement Method |
|--------|----------|--------|----------|-------------------|
| Legacy portals live | 3 | 0 | By 31 Dec 2028 (target 14 Oct 2028) | Decommissioning register |
| Customers on a single Acme account | 0% | 100% | 30 Jun 2028 | Identity service and customer record |
| Portal run cost | EUR 1,310,000 a year | EUR 851,500 a year or less | 2029 | Finance cost reports |
| "Where is my shipment?" contacts | About 127,100 a year | 76,260 a year or fewer | End 2029 | CRM contact reasons, normalised for volume |
| Average handling time | 460 s | 345 s or less | End 2029 | Contact-centre reporting |
| First-contact resolution | 64% | At least 80% | End 2029 | Contact-centre reporting |
| Data subject requests answered within one month | Average 41 days | 100% within one month | From 30 Jun 2028 | DPO request log |
| Critical features lost | Not applicable | 0 | Each wave | Feature-parity register |

---

### Technical Success Metrics

| Metric | Target | Measurement Method |
|--------|--------|-------------------|
| Portal availability | 99.9% a month or better | Synthetic monitoring |
| Temperature alerting availability | 99.95% a month or better | Synthetic monitoring |
| Page load (p95) | < 2 seconds at peak | Real-user monitoring |
| Temperature alert latency | 5 minutes or less end to end | Pipeline metrics |
| Business administrators with MFA | 100% | Identity service |
| Successful credential-stuffing takeovers | 0 | Security monitoring |
| Mean time to recovery | < 1 hour for alerting; < 4 hours for the full service | Incident tracking |

---

### User Adoption Metrics

| Metric | Target | Timeline | Measurement Method |
|--------|--------|----------|-------------------|
| Migrated users activated | At least 90% of active users | 8 weeks after each wave | Identity service |
| Notification opt-in (business accounts) | At least 50% (proposed) | 6 months after each wave | Preferences data |
| User satisfaction | At or above the pre-migration baseline | After each wave | Post-journey survey |

---

## Dependencies and Risks

### Dependencies

| Dependency | Description | Owner | Target Date | Status | Impact if Delayed |
|------------|-------------|-------|-------------|--------|-------------------|
| TrackBox extension | 12-month extension with EU-only support and a data export clause | CIO / CFO | 31 Dec 2026 | At Risk | HIGH |
| Usage analytics | Usage data from Portals A, B and C | Portal owners | 31 Jan 2027 | On Track | HIGH |
| Platform and identity selection | ADRs approved by the Architecture Board | CIO / Architecture Board | 31 Mar 2027 (Jan 2027 recommended) | At Risk | HIGH |
| Transport management system interfaces | Interfaces for INT-001 and INT-002 | Business unit IT | Before Wave 1 (INT-002) and Wave 3 (INT-001) | On Track | HIGH |
| Telematics interface | INT-004 | Flanders Cold Chain operations | Before Wave 2 | On Track | HIGH |
| Programme Product Owner | Appointment | Sponsor | 31 Dec 2026 | At Risk | MEDIUM |

---

### Risks

| Risk ID | Description | Probability | Impact | Mitigation Strategy | Owner |
|---------|-------------|-------------|--------|---------------------|-------|
| R-1 | Portal B deadline missed: only 3 months between platform choice and hosting end | HIGH | HIGH | Bring the decision forward to Jan 2027; minimum viable Wave 1 scope; 3-month hosting contingency | CIO |
| R-2 | Business case fails the 4-year payback test | MEDIUM | HIGH | Agree contact-centre benefit baselines; lower-cost buy option | CFO |
| R-3 | Portal A stays without MFA until mid-2028 | MEDIUM | HIGH | NFR-SEC-007 interim protection by end 2027 | CISO |
| R-4 | TrackBox refuses a short term, EU-only support or a data export | MEDIUM | HIGH | Negotiate from Oct 2026; compensating controls agreed with the DPO in advance | CIO / DPO |
| R-5 | Cold-chain evidence cannot be shown on a standard platform | MEDIUM | HIGH | Targeted extension under NFR-M-004; advisory group sign-off | Tom Wouters |
| R-6 | EDI formats more varied than expected | MEDIUM | MEDIUM | Inventory formats in discovery; test with real files | Julie Leclercq |
| R-7 | Agent-view gains limited because the CRMs are out of scope | MEDIUM | MEDIUM | INT-005 and INT-006 read interfaces; change request if needed | Head of Customer Service |

**Risk Scoring**: Probability × Impact = Risk Level

- **High risk (red)**: requires executive escalation
- **Medium risk (yellow)**: active monitoring and mitigation
- **Low risk (green)**: accepted

---

## Requirement Conflicts & Resolutions

> **Purpose**: This section records conflicting requirements that come from competing stakeholder drivers, and how each is resolved.
>
> **Source**: ARC-001-STKE-v1.0, Conflict Analysis.
>
> **Status**: Each resolution is **proposed** until the named decision authority confirms it. The decision authorities follow the RACI in ARC-001-STKE-v1.0.

### Conflict C-1: Portal B Deadline vs Full Wave 1 Scope

**Conflicting Requirements**:

- **Requirement A**: BR-002 (Portal B migrated by 30 June 2027) and BR-011 (platform chosen by 31 March 2027)
- **Requirement B**: BR-008 and FR-004 to FR-030 delivered with full quality at each wave

**Stakeholders Involved**:

- **Sofie Peeters (CIO)**: needs Portal B migrated before its hosting ends [SI-C7]
- **Julie Leclercq (Portal B owner)**: needs EDI upload and freight booking to work fully for her customers [SI-C19]
- **Annelies Claes (COO)**: wants a controlled go/no-go [SI-C3]

**Nature of Conflict**:

- Three months between platform choice and the hosting end are not enough to build, test and migrate the full functional scope for Brabant Freight customers

**Trade-off Analysis**:

| Option | Pros | Cons | Impact |
|--------|------|------|--------|
| **Option 1**: Full scope by 30 Jun 2027 | ✅ No second migration step | ❌ Very high delivery risk<br>❌ Quality pressure | CIO and portal owner exposed |
| **Option 2**: Extend Portal B hosting by 6–12 months | ✅ Time for full scope | ❌ Pays for an unsupported platform<br>❌ Delays benefits | CFO and CIO unhappy |
| **Option 3**: Minimum viable Wave 1 scope (login, booking, proof of delivery, invoices, EDI upload, tracking, user management) on time; other features (for example quotes) follow within 3 months | ✅ Meets the deadline<br>✅ Must-have EDI kept | ❌ Some features follow later | Portal B owner partly satisfied |
| **Option 4**: Option 3 plus an earlier platform decision (Jan 2027) and a 3-month hosting contingency | ✅ Deadline met with a safety net | ❌ Shorter discovery; contingency cost | All partly satisfied |

**Resolution Strategy**: PHASE

**Decision**: Proposed: Option 4

**Rationale**: It protects the must-have EDI upload and the deadline, and the hosting contingency limits the downside.

**Decision Authority**: Architecture Board (platform timing), Sponsor (Wave 1 scope), CFO (contingency cost)

**Impact on Requirements**:

- **Modified**: BR-011, with a recommended platform decision by 31 January 2027
- **Phased**: FR-012 (quotes) and FR-024 (assisted actions) may follow Wave 1 within 3 months for Brabant Freight
- **Unchanged**: FR-014 (EDI upload) stays mandatory for Wave 1

**Stakeholder Management**:

- **Julie Leclercq**: EDI upload protected; agreed date for any deferred feature; portal owner sign-off at go/no-go
- **Marc Dubois**: contingency used only if the go/no-go fails

**Future Consideration**:

- Review at the Wave 1 go/no-go (31 May 2027)

---

### Conflict C-2: Payback vs Feature Parity and Customisation

**Conflicting Requirements**:

- **Requirement A**: BR-004 and BR-005 (run cost at least 35% lower; payback within 4 years)
- **Requirement B**: BR-008 (keep features), including FR-014, FR-015, FR-019 and FR-020, which may need custom extension

**Stakeholders Involved**:

- **Marc Dubois (CFO)**: wants the lowest run cost and payback within 4 years [SI-C5]
- **Portal owners**: want features their customers rely on [SI-C19]

**Nature of Conflict**:

- Every custom extension adds build and run cost; dropping features risks losing customers

**Trade-off Analysis**:

| Option | Pros | Cons | Impact |
|--------|------|------|--------|
| **Option 1**: Standard product only; drop what it cannot do | ✅ Lowest cost | ❌ Risk of losing EDI or cold-chain evidence | Portal owners and customers lose |
| **Option 2**: Rebuild every legacy feature | ✅ No customer disruption | ❌ High cost; fails payback | CFO loses |
| **Option 3**: Keep the four named must-haves (with targeted extension if needed); decide other features by usage data | ✅ Protects critical customers<br>✅ Contains cost | ❌ Some low-use features dropped | Balanced |

**Resolution Strategy**: PRIORITIZE

**Decision**: Proposed: Option 3

**Rationale**: The user mandate and the stakeholder analysis both make returns, EDI upload, temperature alerts and certificates non-negotiable. Everything else follows usage data [SI-C21].

**Decision Authority**: Sponsor (feature retain or drop), with the CFO for business-case impact

**Impact on Requirements**:

- **Confirmed MUST_HAVE**: FR-014, FR-015, FR-019, FR-020, FR-021
- **Set to SHOULD_HAVE, pending usage data**: FR-012, FR-013
- **Added**: NFR-M-004 (configuration over customisation)

**Stakeholder Management**:

- **Portal owners**: their critical features are guaranteed; they sign the feature-parity register
- **CFO**: every customisation needs an ADR with its cost

**Future Consideration**:

- Re-check payback at discovery close using real usage data

---

### Conflict C-3: Strong Authentication vs Consumer Convenience

**Conflicting Requirements**:

- **Requirement A**: PM-C9 and NFR-SEC-001 ("MFA for all users")
- **Requirement B**: NFR-U-001 and FR-007 (easy consumer tracking and returns, high self-service)

**Stakeholders Involved**:

- **Pieter Janssens (CISO)**: wants one hardened login with MFA [SI-C15]
- **Nathalie Lambert / consumers**: want easy, fast journeys

**Nature of Conflict**:

- Forcing MFA on 150,000 occasional consumers adds friction and contacts. Not using MFA leaves accounts exposed to credential stuffing.

**Trade-off Analysis**:

| Option | Pros | Cons | Impact |
|--------|------|------|--------|
| **Option 1**: Mandatory MFA for every user | ✅ Strongest security | ❌ Consumer drop-out; more contacts | CISO wins, Customer Service loses |
| **Option 2**: MFA offered to all, mandatory for business administrators, step-up for sensitive actions, credential-stuffing protection for all, tracking and returns possible without login | ✅ Strong where risk is high<br>✅ Low friction | ❌ Consumer accounts without MFA remain | Both largely satisfied |

**Resolution Strategy**: COMPROMISE

**Decision**: Proposed: Option 2. We read the mandate's "MFA for all users" as "available to all users", with enforcement for business administrators and for sensitive actions.

**Rationale**: It meets the mandate's explicit mandatory scope (business administrators) and closes the credential-stuffing route through bot protection and checks against breached passwords.

**Decision Authority**: CISO (security risk acceptance), with the Sponsor confirming the reading of the mandate

**Impact on Requirements**:

- **Modified**: FR-002 and NFR-SEC-001 as written

**Stakeholder Management**:

- **CISO**: reviews the enrolment rate every quarter and may raise enforcement

**Future Consideration**:

- Consider enforcing passkeys for consumers once adoption is high

---

### Conflict C-4: Portal A Security Gap vs Wave Order and Cost

**Conflicting Requirements**:

- **Requirement A**: NFR-C-003 (CyberFundamentals by end 2027) and NFR-SEC-001
- **Requirement B**: BR-002 (Portal A migrated last, by 30 June 2028)

**Stakeholders Involved**:

- **Pieter Janssens (CISO)**: Portal A has no MFA [SI-C13] [SI-C14]
- **Annelies Claes / Marc Dubois**: wave order and cost

**Nature of Conflict**:

- Portal A would remain without MFA for 6 months after the NIS2 target date

**Trade-off Analysis**:

| Option | Pros | Cons | Impact |
|--------|------|------|--------|
| **Option 1**: Identity first: move Portal A users to the new identity service early | ✅ Brings the identity benefit forward | ❌ Changes legacy code; extra effort | CISO wins |
| **Option 2**: Interim controls in front of Portal A | ✅ Low change to legacy code | ❌ Cost of a temporary solution | Balanced |
| **Option 3**: Accept the risk until Jun 2028 | ✅ No cost | ❌ Non-compliance; exposure | CISO loses |

**Resolution Strategy**: INNOVATE (Option 1) or COMPROMISE (Option 2)

**Decision**: Proposed: NFR-SEC-007. The CISO chooses Option 1 or 2 by 31 March 2027; Option 3 is rejected.

**Rationale**: The risk and the regulatory deadline outweigh the cost of interim protection.

**Decision Authority**: CISO, with the CIO

**Impact on Requirements**:

- **Added**: NFR-SEC-007

**Stakeholder Management**:

- **CFO**: interim cost included in the business case

**Future Consideration**:

- None

---

### Conflict C-5: TrackBox Extension vs EU-Only Support Access

**Conflicting Requirements**:

- **Requirement A**: BR-011 (12-month TrackBox extension to avoid a 3-year renewal) [SI-C6]
- **Requirement B**: NFR-C-004 (EU/EEA-only support access) [SI-C17]

**Stakeholders Involved**:

- **Marc Dubois (CFO) and Sofie Peeters (CIO)**: want a short extension
- **Isabelle Martin (DPO)**: has an open finding on non-EU support access

**Nature of Conflict**:

- The vendor may refuse to change its support model for a short extension

**Trade-off Analysis**:

| Option | Pros | Cons | Impact |
|--------|------|------|--------|
| **Option 1**: Extension conditional on an EU-only support clause and a data export clause | ✅ Closes the finding | ❌ May cost more or be refused | Both satisfied if accepted |
| **Option 2**: Extension with compensating controls (access only on Acme approval, logged, time-limited) until 31 Mar 2028 | ✅ Achievable | ❌ Finding stays open but controlled | DPO partly satisfied |
| **Option 3**: 3-year renewal | ✅ Simple | ❌ Lock-in; finding open | CFO and DPO lose |

**Resolution Strategy**: PRIORITIZE (Option 1), with Option 2 as fallback

**Decision**: Proposed: Option 1; if refused, Option 2 with a closure date of 31 March 2028

**Rationale**: It protects both the cost objective and data protection compliance.

**Decision Authority**: CFO (Accountable) and CIO; the DPO is consulted on compensating controls

**Impact on Requirements**:

- **Added**: data export clause (INT-010, NFR-I-003)

**Stakeholder Management**:

- **DPO**: approves the compensating controls before signature

**Future Consideration**:

- A monthly roll-on option to cover a Wave 2 slip

---

### Conflict C-6: Single Agent View vs Minimum Data

**Conflicting Requirements**:

- **Requirement A**: FR-022 (one view across business units, to cut handling time)
- **Requirement B**: FR-023 and NFR-C-001 (agents see only the data the contact needs) [SI-C18]

**Stakeholders Involved**:

- **Nathalie Lambert**: lower handling time, higher first-contact resolution
- **Isabelle Martin (DPO)**: data minimisation

**Nature of Conflict**:

- A wider view helps agents but exposes more personal data

**Trade-off Analysis**:

| Option | Pros | Cons | Impact |
|--------|------|------|--------|
| **Option 1**: Full view | ✅ Fastest handling | ❌ GDPR minimisation breach | DPO loses |
| **Option 2**: Contact-scoped view with reveal-with-reason and logging | ✅ Fast for common contacts<br>✅ Compliant | ❌ Extra step for rare cases | Both satisfied |

**Resolution Strategy**: INNOVATE

**Decision**: Proposed: Option 2 (FR-023 as written)

**Rationale**: It meets both needs; the DPO co-designs the field sets.

**Decision Authority**: Architecture Board, with DPO consultation and DPIA approval by the COO

**Impact on Requirements**:

- **Confirmed**: FR-022 and FR-023

**Stakeholder Management**:

- **Agents**: pilot to tune the field sets

**Future Consideration**:

- Review the reveal frequency after 3 months; adjust the default fields if reveals are frequent

---

### Conflict C-7: Final Switch-Off Date vs Peak Freeze

**Conflicting Requirements**:

- **Requirement A**: BR-001, with switch-off by 31 December 2028 as in the mandate [PM-C4]
- **Requirement B**: BR-003 (no changes between 15 October and 10 January)

**Stakeholders Involved**:

- **Annelies Claes (COO)**: owns both the mandate and the peak protection

**Nature of Conflict**:

- Switching off on 31 December 2028 would fall inside the freeze

**Trade-off Analysis**:

| Option | Pros | Cons | Impact |
|--------|------|------|--------|
| **Option 1**: Switch off by 14 Oct 2028 | ✅ Respects the freeze<br>✅ Earlier savings | ❌ About 2.5 months less contingency | Positive overall |
| **Option 2**: Switch off after 10 Jan 2029 | ✅ More time | ❌ Breaks the mandate date and the Ghent data centre exit | Mandate missed |

**Resolution Strategy**: PRIORITIZE

**Decision**: Proposed: Option 1, keeping 31 December 2028 as the formal mandate date

**Rationale**: It meets both requirements with no extra cost.

**Decision Authority**: Sponsor

**Impact on Requirements**:

- **Modified**: BR-001 acceptance criteria (target date 14 October 2028)

**Stakeholder Management**:

- Not needed

**Future Consideration**:

- None

---

**Common Conflict Patterns** represented above: speed vs quality (C-1), cost vs features (C-2), security vs usability (C-3, C-6), flexibility vs standardisation (C-2), and global vs local (C-1, C-2).

---

## Timeline and Milestones

### High-Level Milestones

| Milestone | Description | Target Date | Dependencies |
|-----------|-------------|-------------|--------------|
| Requirements Approval | Architecture Board and Sponsor sign-off on this document | 2026-11-30 | This document |
| TrackBox decision | 12-month extension agreed | 2026-12-31 | Conflict C-5 |
| Platform and identity chosen | ADRs approved (Jan 2027 recommended) | 2027-03-31 | Requirements, usage data |
| Wave 1 go-live (Portal B) | Brabant Freight customers migrated | 2027-06-30 | Platform, INT-002, FR-014 |
| Portal A interim protection | NFR-SEC-007 in place | 2027-12-31 | CISO decision |
| Wave 2 go-live (Portal C) | Flanders Cold Chain customers migrated | 2028-03-31 (target end Feb 2028) | INT-004, FR-019 to FR-021 |
| Wave 3 go-live (Portal A) | Acme Parcel customers migrated | 2028-06-30 | INT-001, FR-015 |
| Legacy switch-off | All legacy portals off | 2028-10-14 target (mandate 2028-12-31) | Waves 1–3 |

---

## Budget

### Cost Estimate

| Category | Estimated Cost | Notes |
|----------|----------------|-------|
| Discovery | EUR 350,000 | Approved [SI-C5]; covers analysis, usage data and platform selection |
| Delivery and migration | Within the EUR 4–6M indicative envelope | Breakdown (development, licences, integration, testing, migration, training) to be produced in the business case at discovery close |
| Contingency | Included in the envelope | Includes a possible 3-month Portal B hosting contingency (Conflict C-1) and Portal A interim protection (C-4) |
| **Total** | **EUR 4–6M (indicative)** | Payback within 4 years (BR-005) |

### Ongoing Operational Costs

| Category | Annual Cost | Notes |
|----------|-------------|-------|
| Current baseline | EUR 1,310,000 a year | Portal A EUR 610,000; Portal B EUR 420,000; Portal C EUR 280,000 [PI-C8] |
| Target run cost | EUR 851,500 a year or less | From 2029 (BR-004); covers platform subscriptions, hosting, support and identity |
| **Target saving** | **At least EUR 458,500 a year** | |

---

## Approval

### Requirements Review

| Reviewer | Role | Status | Date | Comments |
|----------|------|--------|------|----------|
| Annelies Claes | Business Sponsor | [ ] Approved | PENDING | |
| Programme Product Owner (to be appointed) | Product Owner | [ ] Approved | PENDING | |
| Enterprise Architecture team | Enterprise Architect | [ ] Approved | PENDING | |
| Pieter Janssens | Security | [ ] Approved | PENDING | |
| Isabelle Martin | Compliance (DPO) | [ ] Approved | PENDING | |
| Nathalie Lambert | Customer Service | [ ] Approved | PENDING | |
| Koen De Smet, Julie Leclercq, Tom Wouters | Portal owners | [ ] Approved | PENDING | |

### Sign-Off

By signing below, stakeholders confirm that requirements are complete, understood, and approved to proceed to design phase.

| Stakeholder | Signature | Date |
|-------------|-----------|------|
| Annelies Claes, COO and Programme Sponsor | _________ | PENDING |
| Sofie Peeters, CIO and Chair of the Architecture Board | _________ | PENDING |

---

## Appendices

### Appendix A: Glossary

| Term | Definition |
|------|------------|
| AHT | Average handling time of a customer contact |
| CyberFundamentals (CyFun) | Belgian CCB cyber security framework used for NIS2; "Important" is the target assurance level |
| DPIA | Data Protection Impact Assessment |
| EDI | Electronic data interchange: structured order files uploaded by business customers |
| FCR | First-contact resolution: share of contacts resolved without follow-up |
| GDP | Good Distribution Practice, the quality standard for pharmaceutical distribution |
| HACCP | Hazard Analysis and Critical Control Points, the food safety system |
| MFA | Multi-factor authentication |
| PoD | Proof of delivery |
| TMS | Transport management system (ParcelCore for parcel, FreightMaster for freight) |
| Wave | A migration step for one legacy portal: B, then C, then A |
| WISMO | "Where is my shipment?" contact |

### Appendix B: Reference Documents

- ARC-000-PRIN-v1.0, Acme Logistics NV Enterprise Architecture Principles
- ARC-001-STKE-v1.0, Stakeholder Drivers and Goals Analysis
- ARC-001-ADMP-v1.0, Architecture Vision (TOGAF ADM Preliminary)
- Programme mandate, stakeholder interview notes and portal inventory (`001-customer-portal-consolidation/external/`)
- Acme company profile and IT policies (`000-global/policies/`)

### Appendix C: Wireframes and Mockups

None yet. Journey designs follow platform selection.

### Appendix D: Data Models

Run `/arckit:data-model` to produce the full data model from the entities and DR-001 to DR-008.

### Appendix E: Requirements Traceability Matrix

| Stakeholder Goal (ARC-001-STKE) | Vision Criterion (ARC-001-ADMP) | Requirements |
|----------------------------------|----------------------------------|--------------|
| G-1 Migrate and switch off A, B, C | 1, 2, 12 | BR-001, BR-002, BR-003, BR-009, FR-005, FR-030, DR-004, DR-005, INT-010 |
| G-2 Run cost at least 35% lower; payback within 4 years | 3, 4 | BR-004, BR-005, NFR-M-004, NFR-S-001 |
| G-3 TrackBox decision with EU-only support | 13 | BR-011, NFR-C-004, NFR-I-003 |
| G-4 Platform chosen by 31 Mar 2027 | — | BR-011, FR-029 |
| G-5 One hardened login with MFA | 9 | FR-001, FR-002, FR-003, NFR-SEC-001, NFR-SEC-006, NFR-SEC-007, INT-007, INT-008 |
| G-6 40% fewer "where is my shipment?" calls | 5 | BR-006, FR-007, FR-008, FR-009, INT-001, INT-002, INT-009 |
| G-7 Handling time and first-contact resolution | 6, 7 | BR-007, FR-016, FR-022, FR-023, FR-024, FR-025, INT-005, INT-006 |
| G-8 Data subject requests within one month | 8 | BR-010, FR-026, FR-027, NFR-C-001, DR-001, DR-003 |
| G-9 Keep critical features | 11 | BR-008, FR-010 to FR-021 (incl. FR-014 EDI, FR-015 returns, FR-019 alerts, FR-020 certificates), NFR-C-005, DR-006, INT-004 |
| G-10 NL/FR and WCAG 2.2 AA | 10 | BR-010, FR-006, FR-028, NFR-U-001, NFR-U-002, NFR-U-003 |

| Principle (ARC-000-PRIN) | Key Requirements |
|--------------------------|------------------|
| 1 One Acme Customer Experience | BR-001, BR-009, FR-001 |
| 2 Reuse, Then Buy, Then Build | BR-011, NFR-M-004 |
| 3 Digital Self-Service by Default | BR-012, FR-008, FR-024 |
| 4 Compliance by Design | BR-010, NFR-C-001 to NFR-C-005 |
| 5 Cost-Conscious Architecture | BR-004, BR-005 |
| 6 Scalability and Peak-Season Elasticity | NFR-P-002, NFR-S-001 |
| 7 Resilience | NFR-A-003 |
| 8 Security by Design | NFR-SEC-001 to NFR-SEC-007 |
| 9 Unified Identity and Access | FR-001, FR-002, INT-007 |
| 10 Observability | NFR-M-001 |
| 11 EU-Hosted, Cloud-First Platform | TC-1, NFR-C-004, DR-007 |
| 12 Data Classification and Sovereignty | DR-002 |
| 13 Privacy by Design | FR-023, FR-026, FR-027, DR-008 |
| 14 Single Source of Truth | DR-001, FR-016 |
| 15 Data Quality and Lineage | DR-004, DR-005 |
| 16 Standard Interfaces | NFR-I-001 |
| 17 Loose Coupling and Asynchronous Integration | NFR-I-002, INT-001 to INT-004 |
| 18 Accessible and Multilingual by Design | NFR-U-002, NFR-U-003, FR-006 |
| 19–21 Performance, Availability, Maintainability | NFR-P-001, NFR-A-001, NFR-A-002, NFR-M-002 |
| 22–24 IaC, Testing, CI/CD and Change Windows | BR-003, NFR-SEC-005, NFR-M-003 |

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
| PM-C4 | PM | Milestones | Business Requirement | Milestone list: discovery complete and platform chosen 31 March 2027; TrackBox decision 31 December 2026; Portal B migrated 30 June 2027; Portal C 31 March 2028; Portal A 30 June 2028; all legacy portals switched off 31 December 2028 |
| PM-C5 | PM | Targets | Business Requirement | "Portal run cost down at least 35% (baseline EUR 1.31M per year)" |
| PM-C6 | PM | Targets | Business Requirement | "\"Where is my shipment?\" calls down 40%" |
| PM-C7 | PM | Targets | Business Requirement | "Average handling time down 25%; first-contact resolution at least 80%" |
| PM-C8 | PM | Targets | Compliance Constraint | "100% of data subject requests answered within one month" |
| PM-C9 | PM | Targets | Security Requirement | "MFA for all users, mandatory for business administrators" |
| PM-C10 | PM | Governance | Stakeholder Need | "Sponsor: Annelies Claes (COO). Design authority: Architecture Board. Monthly steering committee." |
| SI-C1 | SI | Annelies Claes - COO | Stakeholder Need | "\"Customers see three companies. By the end of 2028 they should see one Acme.\"" |
| SI-C2 | SI | Annelies Claes - COO | Stakeholder Need | "No migrations during the peak season." |
| SI-C3 | SI | Annelies Claes - COO | Stakeholder Need | "Wants a clear go/no-go per business unit." |
| SI-C4 | SI | Marc Dubois - CFO | Stakeholder Need | "Run cost of the three portals (EUR 1.31M) must drop by at least 35%." |
| SI-C5 | SI | Marc Dubois - CFO | Business Requirement | "Payback within 4 years. Discovery budget EUR 350,000 approved; total envelope EUR 4-6M indicative." |
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
| SI-C19 | SI | Portal owners | Functional Requirement | "Fear losing features their customers rely on: A the returns flow, B the EDI order upload, C the temperature alerts and certificates." |
| SI-C20 | SI | Portal owners | Compliance Constraint | "Pharma customers require audit-proof temperature records: non-negotiable for Tom." |
| SI-C21 | SI | Portal owners | Stakeholder Need | "All three want usage data before deciding what can be dropped." |
| PI-C1 | PI | Registered users row | Business Requirement | Table row: 150,000 consumers + 4,200 business accounts (A); 3,100 business accounts (B); 2,200 business accounts (C) |
| PI-C2 | PI | Monthly active users row | Non-Functional Requirement | Table row: 41,000 (A); 2,600 (B); 1,900 (C) |
| PI-C3 | PI | Technology row | Risk Factor | Table row: .NET Framework 4.6, SQL Server, on-premises Ghent (A); Liferay 6.2 (out of support), Java, hosted by a German service provider (B); SaaS product "TrackBox", multi-tenant (C) |
| PI-C4 | PI | Login row | Security Requirement | Table row: own user database, no MFA (A); own user database, MFA optional (B); vendor login, MFA for admins only (C) |
| PI-C5 | PI | Languages row | Compliance Constraint | Table row: NL, FR, EN (A); NL, FR (French incomplete) (B); NL, EN (no French) (C) |
| PI-C6 | PI | Key features row | Functional Requirement | Table row: track and trace, pickup booking, returns, invoice PDFs, address book (A); pallet booking, quotes, proof of delivery, invoices, EDI order upload (B); temperature monitoring, alerts, compliance certificates (HACCP, GDP) (C) |
| PI-C7 | PI | Integrations row | Integration Requirement | Table row: TMS "ParcelCore", Dynamics 365 CRM, SAP S/4HANA (A); TMS "FreightMaster", Salesforce, SAP S/4HANA (B); telematics feed from trucks, SAP S/4HANA (C) |
| PI-C8 | PI | Annual run cost row | Business Requirement | Table row: EUR 610,000 (A); EUR 420,000 (B); EUR 280,000 (C). "Total run cost: EUR 1.31M per year." |
| PI-C9 | PI | Contract / end of life row | Procurement Constraint | Table row: in-house; .NET 4.6 out of support (A); hosting contract ends 30 June 2027 (B); subscription renews 31 March 2027 for 3 years (C) |
| PI-C10 | PI | Known issues row | Risk Factor | Table row: credential-stuffing attack Feb 2025, 12,000 password resets (A); slow (6.8 s average page load), no new features since 2022 (B); vendor support staff outside the EU can access data, DPA finding open (C) |
| ACP-C1 | ACP | At a glance | Stakeholder Need | "1,800 business customers use more than one portal (overlap analysis, Q2 2026)." |
| ACP-C2 | ACP | At a glance | Non-Functional Requirement | "Peak season: mid-October to early January, parcel volumes x2.3." |
| ACP-C3 | ACP | Strategy 2030 | Business Requirement | "Digital self-service as the default channel: 70% of service interactions." |
| ACP-C4 | ACP | At a glance | Compliance Constraint | "Dutch and French are required commercially and legally; English for international shippers." |
| ACP-C5 | ACP | Strategy 2030 | Business Requirement | "\"One Acme\" for customers: one brand, one login, one customer record." |
| AIP-C1 | AIP | Cloud and hosting | Data Requirement | "All customer data, backups, logs and vendor support access stay in the EU/EEA." |
| AIP-C2 | AIP | Cloud and hosting | Design Decision | "The on-premises data centre in Ghent closes by end 2028." |
| AIP-C3 | AIP | Sourcing | Procurement Constraint | "Reuse, then buy (SaaS preferred), then build. Custom code only for differentiating capabilities." |
| AIP-C4 | AIP | Sourcing | Procurement Constraint | "Every vendor processing customer data signs the Acme Data Processing Agreement and keeps data in the EU." |
| AIP-C5 | AIP | Identity | Design Decision | "Workforce identity: Microsoft Entra ID (in place)." |
| AIP-C6 | AIP | Identity | Risk Factor | "Customer identity: no group standard yet; each portal has its own user store." |
| AIP-C7 | AIP | Data classification | Data Requirement | "Public, Internal, Confidential, Strictly Confidential." |
| AIP-C8 | AIP | Data classification | Data Requirement | "Customer personal data is Confidential. Credentials and security logs are Strictly Confidential." |
| AIP-C9 | AIP | Security and compliance | Security Requirement | "Acme is registered as an \"important entity\" under the Belgian NIS2 law (postal and courier services). Target control set: CCB CyberFundamentals, assurance level Important, by end 2027." |
| AIP-C10 | AIP | Security and compliance | Compliance Constraint | "GDPR supervisory authority: Belgian Data Protection Authority (GBA/APD)." |
| AIP-C11 | AIP | Security and compliance | Integration Requirement | "Belgian B2B e-invoicing via Peppol is live since 1 January 2026 from SAP S/4HANA. Portals show invoice copies only." |
| AIP-C12 | AIP | Security and compliance | Compliance Constraint | "New customer-facing services meet WCAG 2.2 AA." |
| AIP-C13 | AIP | Governance | Design Decision | "The Architecture Board meets monthly (chair: CIO). Decisions are recorded as ADRs." |
| AIP-C14 | AIP | Governance | Business Requirement | "Peak freeze: no go-lives or migrations between 15 October and 10 January." |
| AIP-C15 | AIP | Cloud and hosting | Design Decision | "Microsoft Azure is the strategic platform (Enterprise Agreement until 2029)." |

### Unreferenced Documents

| Filename | Source Location | Reason |
|----------|-----------------|--------|
| — | — | All consulted documents were cited |

---

**Generated by**: ArcKit `/arckit:requirements` command
**Generated on**: 2026-10-08 GMT
**ArcKit Version**: 6.17.5
**Project**: One Acme Customer Portal (Project 001)
**AI Model**: Claude Opus 5.5 (claude-opus-5-5)
**Generation Context**: Derived from the programme mandate, stakeholder interview notes and portal inventory (project 001 external documents), the Acme company profile and IT policies, ARC-000-PRIN-v1.0, ARC-001-STKE-v1.0 and ARC-001-ADMP-v1.0

<!-- arckit-provenance:start -->

## Build Provenance

*Stamped automatically by the ArcKit plugin's `provenance-stamp.mjs` PostToolUse hook. Complements (does not replace) the human-authored footer above. Carries only fields the model can't authoritatively self-report: build context from `.arckit/state.json` and effort levels derived from command frontmatter + the silent-downgrade matrix.*

| Field | Value |
|-------|-------|
| Requested Effort | `high` |
| Effective Effort | _unknown — model not parsed from existing footer_ |
| Stamped at | 2026-10-08T06:28:30.923Z |

<!-- arckit-provenance:end -->
