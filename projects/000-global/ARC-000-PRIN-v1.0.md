# Acme Logistics NV Enterprise Architecture Principles

> **Template Origin**: Official | **ArcKit Version**: 6.17.5 | **Command**: `/arckit:principles`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-000-PRIN-v1.0 |
| **Document Type** | Enterprise Architecture Principles |
| **Project** | Acme Logistics NV Global Architecture Governance (Project 000) |
| **Classification** | Internal |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-10-08 |
| **Last Modified** | 2026-10-08 |
| **Review Cycle** | Annual |
| **Next Review Date** | 2027-10-08 |
| **Owner** | Sofie Peeters, CIO (Chair, Architecture Board) |
| **Reviewed By** | [PENDING] |
| **Approved By** | [PENDING] |
| **Distribution** | Architecture Board; Executive Committee; CISO; DPO; Portal owners; IT delivery teams and suppliers working under the Acme Data Processing Agreement |

> **Classification note**: This document uses the Acme data classification scheme (Public / Internal / Confidential / Strictly Confidential) in place of UK government markings, as group IT policy requires [AIP-C8].

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-10-08 | ArcKit AI | Initial creation from `/arckit:principles` command | PENDING | PENDING |

---

## Executive Summary

This document sets out the principles that govern all technology architecture decisions at Acme Logistics NV. They turn Strategy 2030 and the group IT and architecture policies into decision criteria. Projects, design reviews and vendor evaluations are measured against them.

Acme grew by acquisition. Acme Parcel, Brabant Freight (acquired 2021) and Flanders Cold Chain (acquired 2023) each still run their own customer portal [ACP-C1], and 1,800 business customers use more than one of them [ACP-C2]. Strategy 2030 commits the group to four outcomes. These principles exist to deliver them:

1. **One Acme** for customers: one brand, one login, one customer record [ACP-C5]
2. **20% lower group IT run cost** by 2029 [ACP-C6]
3. **Digital self-service as the default channel** for 70% of service interactions [ACP-C7]
4. **Compliance by design**: GDPR, NIS2 and accessibility [ACP-C8]

**Scope**: All technology projects, systems, platforms and suppliers in all Acme Logistics NV business units
**Authority**: Acme Architecture Board (meets monthly, chaired by the CIO; decisions recorded as ADRs) [AIP-C14]
**Compliance**: Mandatory unless the Architecture Board approves an exception (see Section VII)

**Philosophy**: These principles are **technology-agnostic**. They describe WHAT qualities the architecture must have, not HOW to build them with specific products. Products are chosen during research and design, guided by these principles and by the group's existing platform commitments in the IT policies.

**Normative language**: **MUST** = mandatory; **SHOULD** = expected unless there is a documented reason not to; **MAY** = optional.

---

## I. Business Principles

### 1. One Acme Customer Experience

**Principle Statement**:
Every customer-facing capability MUST present one Acme brand, MUST be reachable with one customer login, and MUST read and write one shared customer record. New business-unit-specific customer channels MUST NOT be created.

**Rationale**:
Strategy 2030 sets "One Acme" as the first group objective [ACP-C5]. Today three separate portals [ACP-C1] force 1,800 business customers to juggle several accounts [ACP-C2], and each portal keeps its own user store [AIP-C7]. Every new silo makes consolidation harder and more expensive.

**Implications**:

- Customer-facing services are designed as group capabilities, not business-unit capabilities
- Parcel, freight and cold-chain services are presented as products within one experience, not as separate sites
- Business-unit differences (e.g. temperature monitoring for cold chain) are handled as features of a shared platform
- Legacy portals are only extended where needed to keep the service running until they are retired

**Validation Gates**:

- [ ] Design shows how the capability fits the single customer experience and brand
- [ ] Customer authentication uses the group customer identity service (Principle 9)
- [ ] Customer data is read from and written to the authoritative customer record (Principle 14)
- [ ] No new standalone customer portal, user store or customer database is introduced

**Example Scenarios**:

- ✅ **Good**: Cold-chain temperature reports are added as a feature that business customers see after signing in to the group portal.
- ❌ **Bad**: Brabant Freight launches a new booking site with its own login because "it is faster than waiting for the group platform".

**Common Violations**:

- Adding features to a legacy portal that is due for retirement instead of the target platform
- Building separate registration journeys per business unit
- Copying customer data into a local database "for performance"

---

### 2. Reuse, Then Buy, Then Build

**Principle Statement**:
When meeting a need, teams MUST first reuse an existing Acme capability, then buy a market solution (Software-as-a-Service preferred), and only build custom software for capabilities that set Acme apart from competitors.

**Rationale**:
This is group sourcing policy [AIP-C4]. Custom code is the most expensive option to run and maintain, which conflicts with the 20% run-cost reduction target [ACP-C6]. Commodity capabilities (identity, content management, notifications, payments) give Acme no competitive advantage.

**Implications**:

- Every options analysis evaluates reuse and buy before build, and records the result
- Bought solutions are configured, not customised; changes that lock Acme into an old version are avoided
- Build is limited to differentiating logistics capabilities (e.g. network-specific tracking, cold-chain compliance evidence)
- Every vendor processing customer data must sign the Acme Data Processing Agreement and keep data in the EU [AIP-C5]

**Validation Gates**:

- [ ] Options analysis covers reuse, buy and build, with reasons for the chosen option
- [ ] A build decision is justified as differentiating and recorded in an ADR
- [ ] Customisation of bought products is minimised and documented
- [ ] Vendor has accepted the Acme Data Processing Agreement and EU data location (if customer data is processed)

**Example Scenarios**:

- ✅ **Good**: The programme selects a SaaS customer identity service and configures it for the three brands' customers.
- ❌ **Bad**: A team builds its own password store and login pages because it has the skills in-house.

**Common Violations**:

- Treating "build" as the default because a team is already in place
- Heavily customising a SaaS product until it can no longer be upgraded
- Skipping the reuse check across business units

---

### 3. Digital Self-Service by Default

**Principle Statement**:
Customer services MUST be designed so that customers can complete the task end-to-end in digital channels without contacting staff. Assisted channels SHOULD use the same services and data as the digital channel.

**Rationale**:
Strategy 2030 targets 70% of service interactions through digital self-service [ACP-C7]. Self-service lowers cost-to-serve and supports the run-cost target [ACP-C6]. It only works if digital journeys are complete, reliable and easier than calling.

**Implications**:

- Journeys are designed around the top customer contact reasons, not around existing system screens
- Contact-centre staff use the same services, so customers get the same answer in every channel
- Each journey measures self-service completion and failure points
- Status, documents (e.g. invoice copies, proof of delivery) and changes are available digitally

**Validation Gates**:

- [ ] Top contact reasons covered by the design are listed
- [ ] Each journey can be completed without staff help
- [ ] Self-service completion and drop-out rates are instrumented (Principle 10)
- [ ] Assisted and digital channels use the same services and data

**Example Scenarios**:

- ✅ **Good**: A business customer reschedules a pallet delivery online and the change is visible to the contact centre straight away.
- ❌ **Bad**: The portal shows a "call us to change your delivery" message because the change process exists only in a back-office tool.

**Common Violations**:

- Journeys that end with "contact customer service" for common tasks
- Separate back-office tools with logic the digital channel cannot reach
- No measurement of self-service success

---

### 4. Compliance by Design

**Principle Statement**:
Regulatory obligations (GDPR, the Belgian NIS2 law, accessibility and e-invoicing rules) MUST be identified at the start of every initiative and built into requirements, design and testing. Compliance MUST NOT be left to a check before go-live.

**Rationale**:
Strategy 2030 makes compliance by design a group objective [ACP-C8]. Acme is registered as an "important entity" under the Belgian NIS2 law and must reach CCB CyberFundamentals at assurance level Important by end 2027 [AIP-C10]. The Belgian Data Protection Authority (GBA/APD) is the GDPR supervisory authority [AIP-C11]. New customer-facing services must meet WCAG 2.2 AA [AIP-C13]. Fixing compliance late costs far more and puts the timeline at risk.

**Implications**:

- Every initiative records its regulatory obligations in its requirements
- The DPO is involved where personal data is processed; the CISO is involved for all systems in NIS2 scope
- Compliance controls are traced to requirements and tested like other requirements
- Compliance evidence (DPIAs, control mappings, accessibility audits) is produced during delivery

**Validation Gates**:

- [ ] Regulatory obligations listed in requirements (GDPR, NIS2, accessibility, e-invoicing where relevant)
- [ ] DPIA screening completed where personal data is processed
- [ ] Mapping to CyberFundamentals controls completed for systems in NIS2 scope
- [ ] Accessibility testing planned against WCAG 2.2 AA for customer-facing services

**Example Scenarios**:

- ✅ **Good**: The portal programme does DPIA screening and CyberFundamentals mapping during discovery and turns them into requirements.
- ❌ **Bad**: An accessibility audit is ordered two weeks before launch and finds that core components fail WCAG 2.2 AA.

**Common Violations**:

- Treating the DPO and CISO as sign-off steps rather than design partners
- Assuming a SaaS vendor's certification covers Acme's own obligations
- No evidence trail for audits

---

### 5. Cost-Conscious Architecture and Rationalisation

**Principle Statement**:
Every initiative MUST show its effect on group IT run cost. It SHOULD retire or consolidate at least as many systems as it introduces. Duplicate capabilities across business units MUST have a retirement plan.

**Rationale**:
The group must cut IT run cost by 20% by 2029 [ACP-C6]. Running three portals, three user stores and three sets of integrations [ACP-C1] [AIP-C7] for overlapping customers is a major cost driver. The Ghent data centre closes by end 2028 [AIP-C3], so every workload needs a planned destination.

**Implications**:

- Business cases include total cost of ownership and the run-cost change, not just build cost
- Each replaced system has a dated decommissioning plan, funded within the initiative
- Shared platforms and capabilities are preferred over per-business-unit copies
- Resources are right-sized and costs are visible per service and per business unit

**Validation Gates**:

- [ ] Total cost of ownership and run-cost change are estimated
- [ ] Systems to be retired are named with target dates
- [ ] Hosting destination is defined for any workload currently in the Ghent data centre
- [ ] Cost is allocated and visible per service

**Example Scenarios**:

- ✅ **Good**: The consolidated portal business case includes switching off Portals A, B and C, with dates and run-cost savings.
- ❌ **Bad**: The new platform goes live but all three legacy portals stay running "just in case" with no switch-off date.

**Common Violations**:

- Business cases that count build cost but leave out run cost
- Leaving decommissioning out of scope or unfunded
- Over-provisioning capacity all year to cope with the seasonal peak

---

## II. Technology Principles

### 6. Scalability and Peak-Season Elasticity

**Principle Statement**:
All customer-facing and operational systems MUST scale horizontally to handle peak-season demand without changes to the architecture, and MUST scale down outside peak to control cost.

**Rationale**:
Parcel volumes rise 2.3 times between mid-October and early January [ACP-C4]. Systems sized for average load fail at peak; systems sized for peak all year waste money (Principle 5).

**Implications**:

- Components are stateless where possible so they can be replicated
- No hard-coded capacity limits
- Capacity scales automatically on demand metrics
- Load tests use peak volumes (at least 2.3 times normal parcel volume) plus a safety margin

**Validation Gates**:

- [ ] System can scale horizontally by adding instances
- [ ] Load test shows the system handles at least 2.3 times normal volume with margin
- [ ] Scaling triggers and limits are defined
- [ ] Cost model covers both peak and off-peak capacity

**Example Scenarios**:

- ✅ **Good**: Tracking services add capacity automatically during the December peak and shrink in January.
- ❌ **Bad**: A tracking page runs on fixed servers and slows down every December, so customers call the contact centre.

**Common Violations**:

- Load testing at average volumes only
- Session state held on a single server
- Shared components (e.g. a database) that cannot scale and become a bottleneck

---

### 7. Resilience and Fault Tolerance

**Principle Statement**:
All systems MUST degrade gracefully when a dependency fails and MUST recover automatically, without data loss or manual intervention.

**Rationale**:
Portals depend on many back-end systems (transport management, ERP, tracking feeds). One failing dependency must not take down the whole customer experience, especially during peak [ACP-C4]. The NIS2 obligations [AIP-C10] also require demonstrable service continuity.

**Implications**:

- Every network call has a timeout
- Calls to external dependencies are protected with circuit breakers, and transient failures are retried with backoff
- Non-critical features are switched off cleanly when their dependency fails
- Failure domains are isolated so a failure in one area does not cascade

**Validation Gates**:

- [ ] Failure modes identified and mitigated
- [ ] Fault injection or failover testing performed
- [ ] Recovery Time Objective (RTO) and Recovery Point Objective (RPO) defined
- [ ] Degraded-mode behaviour documented and tested

**Example Scenarios**:

- ✅ **Good**: If the invoice source is unavailable, the portal still shows tracking and bookings, with a message that invoices are temporarily unavailable.
- ❌ **Bad**: A slow tracking feed blocks every page in the portal.

**Common Violations**:

- Calls without timeouts
- Hidden synchronous dependencies chained together
- Failover that has never been tested

---

### 8. Security by Design (NON-NEGOTIABLE)

**Principle Statement**:
All architectures MUST apply defence-in-depth and zero-trust principles. Security MUST be designed in from the start, not added later.

**Rationale**:
As a NIS2 "important entity" in postal and courier services, Acme must reach CCB CyberFundamentals at assurance level Important by end 2027 [AIP-C10]. Credentials and security logs are Strictly Confidential [AIP-C9]. A breach of a consolidated portal would affect customers of all three business units at once.

**Implications**:

- Threat modelling happens during design, not after build
- Every request is authenticated and authorised, including service-to-service calls
- Security controls are traced to requirements and tested like any other requirement
- Security debt is tracked and prioritised alongside functional work

**Zero Trust Pillars**:

1. **Identity-Based Access**: No trust based on network location; every request is authenticated
2. **Least Privilege**: Minimum necessary permissions, time-limited where possible
3. **Encryption Everywhere**: Data encrypted in transit and at rest
4. **Continuous Verification**: Access is monitored, logged and analysed

**Mandatory Controls**:

- [ ] Multi-factor authentication for all workforce access and all privileged access
- [ ] Strong customer authentication options, with multi-factor authentication for business account administrators
- [ ] Service-to-service authentication (mutual certificate authentication, signed tokens or equivalent)
- [ ] Secrets kept in a managed secrets store, never in code or configuration files
- [ ] Network segmentation with minimal trust zones
- [ ] Encryption at rest for all data stores
- [ ] Encrypted transport for all network communication
- [ ] Structured logging of all authentication and authorisation events, handled as Strictly Confidential
- [ ] Regular security testing (penetration testing, vulnerability scanning)

**Compliance Frameworks**:

- Belgian NIS2 law; CCB CyberFundamentals, assurance level Important (target end 2027) [AIP-C10]
- GDPR security of processing (Article 32), supervised by GBA/APD [AIP-C11]

**Exceptions**:

- NONE. Security principles are non-negotiable.
- How a control is implemented may vary if compensating controls are approved by the CISO.

**Validation Gates**:

- [ ] Threat model completed and reviewed by the CISO's team
- [ ] Security controls mapped to requirements and to CyberFundamentals controls
- [ ] Security testing plan defined
- [ ] Incident response runbook created, including NIS2 incident notification steps

**Example Scenarios**:

- ✅ **Good**: Vendor support staff reach production only through just-in-time, logged access from within the EU.
- ❌ **Bad**: An integration uses a shared service account whose password is stored in a configuration file.

**Common Violations**:

- Trusting traffic because it comes from the internal network
- Long-lived standing admin rights
- Security logs kept at a lower classification than Strictly Confidential

---

### 9. Unified Identity and Access

**Principle Statement**:
Customers MUST authenticate through one group customer identity service shared by all customer-facing channels. Employees and supplier staff MUST authenticate through the existing group workforce identity service. Systems MUST NOT keep their own credential stores.

**Rationale**:
"One login" is a Strategy 2030 commitment [ACP-C5]. Today there is no group standard for customer identity and each portal has its own user store [AIP-C7], which causes duplicate accounts, inconsistent security and repeated cost. Workforce identity is already standardised [AIP-C6] and must be reused (Principle 2).

**Implications**:

- Customer identity is a shared group capability, selected once and reused by all channels
- Business accounts support several users with delegated roles across parcel, freight and cold-chain services
- Account migration from the legacy user stores is planned, including merging duplicate accounts
- Access decisions use standard identity federation and authorisation protocols

**Validation Gates**:

- [ ] Customer authentication goes through the group customer identity service
- [ ] Workforce and supplier access goes through the group workforce identity service
- [ ] No local credential stores in new systems
- [ ] Account migration and duplicate-merge approach defined for legacy users

**Example Scenarios**:

- ✅ **Good**: A shipper that uses both parcel and freight services signs in once and sees both under one business account.
- ❌ **Bad**: The cold-chain module keeps its own user table "temporarily" while the group service is selected.

**Common Violations**:

- Local admin accounts that bypass group identity
- Choosing a customer identity product separately for each project
- Customer roles hard-coded per business unit

---

### 10. Observability and Operational Excellence

**Principle Statement**:
All systems MUST emit structured telemetry (logs, metrics, traces) that supports real-time monitoring, troubleshooting, security detection and capacity planning.

**Rationale**:
We cannot run what we cannot see, especially at peak [ACP-C4]. NIS2 requires timely detection and reporting of significant incidents [AIP-C10]. Self-service targets [ACP-C7] can only be managed if journey success is measured.

**Implications**:

- Telemetry is designed alongside features, not added just before go-live
- Every service passes correlation and trace identifiers across calls
- Alerts are tied to Service Level Objectives and each alert has a runbook
- Telemetry is stored in the EU/EEA [AIP-C2]

**Telemetry Requirements**:

- **Logging**: Structured logs with correlation IDs; no credentials or unnecessary personal data in logs
- **Metrics**: Request volume, latency percentiles (p50, p95, p99), error rates
- **Tracing**: Distributed trace context across request flows
- **Alerting**: Alerts based on Service Level Objectives (SLOs), each with an actionable runbook

**Required Instrumentation**:

- Request volume, latency distribution and error rate
- Resource use (CPU, memory, I/O, network)
- Business metrics (bookings, tracking lookups, self-service completion rate)
- Security events (authentication failures, policy violations, suspicious patterns)

**Log Retention**:

- **Security and audit logs**: Strictly Confidential [AIP-C9]; kept for the period set by the CISO for NIS2 and CyberFundamentals evidence
- **Application logs**: Long enough for troubleshooting (typically 30 to 90 days), then deleted
- **Metrics**: Long-term trends, aggregated (typically one to two years, so peak seasons can be compared year on year)

**Validation Gates**:

- [ ] Logging, metrics and tracing instrumented
- [ ] Dashboards and alerts configured
- [ ] SLOs and Service Level Indicators (SLIs) defined
- [ ] Runbooks created for common failure scenarios
- [ ] Security events forwarded to group security monitoring

**Example Scenarios**:

- ✅ **Good**: A dashboard shows booking latency and self-service completion per business unit, with year-on-year peak comparison.
- ❌ **Bad**: An outage is first noticed when the contact centre reports a spike in calls.

**Common Violations**:

- Logging full customer records or authentication tokens
- Alerts with no owner or runbook
- Telemetry sent to a monitoring service hosted outside the EU/EEA

---

### 11. EU-Hosted, Cloud-First Platform

**Principle Statement**:
New and migrated workloads MUST be hosted on the group's designated strategic cloud platform, unless the Architecture Board approves an exception. All customer data, backups, logs and vendor support access MUST stay in the EU/EEA. No new workloads MAY be placed in the on-premises data centre.

**Rationale**:
Group policy names a single strategic cloud platform under an enterprise agreement running to 2029 [AIP-C1]. The Ghent data centre closes by end 2028 [AIP-C3]. EU/EEA residency applies to data, backups, logs and vendor support access [AIP-C2]. Concentrating on one platform cuts run cost and operational complexity [ACP-C6].

**Implications**:

- Platform-managed services are preferred over self-managed infrastructure
- SaaS products are acceptable (Principle 2) if they meet EU/EEA residency for data, backups, logs and support access
- Every workload in the Ghent data centre has a migration or retirement plan completed before end 2028
- Hosting regions are restricted to EU/EEA by policy, not by convention

**Validation Gates**:

- [ ] Hosting is on the strategic platform, or an approved SaaS, or an approved exception exists
- [ ] Data, backup, log and support-access locations are confirmed as EU/EEA
- [ ] Region restrictions are enforced by platform policy
- [ ] Workloads leaving the Ghent data centre have a migration plan and date

**Example Scenarios**:

- ✅ **Good**: A SaaS vendor confirms in contract that data, backups and follow-the-sun support all stay in EU/EEA.
- ❌ **Bad**: A new service is deployed on spare on-premises hardware in Ghent because it is "free".

**Common Violations**:

- Ignoring where vendor support staff access data from
- Backups or disaster recovery copies replicated outside the EU/EEA
- New dependencies on the Ghent data centre

---

## III. Data Principles

### 12. Data Classification and Sovereignty

**Principle Statement**:
All data MUST be classified using the Acme classification scheme before it is stored or processed. Residency, retention and access controls MUST match the classification.

**Rationale**:
Group policy sets the classification scheme and the minimum classification for key data types [AIP-C8] [AIP-C9]. Residency is set by policy [AIP-C2]. Data with no owner, no classification and no retention rule becomes a regulatory and security liability.

**Implications**:

- Every data store has a named owner and a classification before go-live
- Controls are applied according to classification
- Retention periods are set per data type and enforced automatically
- Access follows least privilege and is reviewed periodically

**Data Classification Tiers (Acme scheme)** [AIP-C8] [AIP-C9]:

1. **Public**: Approved for publication (e.g. service descriptions, public tariffs, help content)
2. **Internal**: Employees and contracted suppliers only (e.g. internal procedures, architecture documents, aggregated operational reports)
3. **Confidential**: Need-to-know access. **All customer personal data is Confidential.** Also covers commercial contracts, customer-specific pricing and shipment details linked to identifiable customers
4. **Strictly Confidential**: Highest controls. **All credentials and security logs are Strictly Confidential.** Also covers cryptographic keys and secrets

**Minimum controls by tier**:

| Tier | Encryption | Access | Location | Logging of access |
|------|-----------|--------|----------|-------------------|
| Public | In transit | Open | No restriction | Not required |
| Internal | In transit and at rest | Authenticated staff and suppliers | EU/EEA preferred | Recommended |
| Confidential | In transit and at rest | Role-based, need-to-know | EU/EEA required [AIP-C2] | Required |
| Strictly Confidential | In transit and at rest, keys managed by Acme | Named individuals, time-limited, multi-factor | EU/EEA required [AIP-C2] | Required and monitored |

**Data Residency**:

- Customer data, backups, logs and vendor support access stay in the EU/EEA [AIP-C2]
- Any transfer outside the EU/EEA needs a GDPR legal basis and Architecture Board and DPO approval
- Vendors processing customer data sign the Acme Data Processing Agreement [AIP-C5]

**Data Retention**:

- Data is deleted automatically after its retention period
- A legal-hold process is in place for litigation or investigation
- Backup retention matches compliance and recovery needs

**Validation Gates**:

- [ ] All data stores classified using the Acme scheme
- [ ] Controls match the classification table above
- [ ] Residency confirmed for data, backups, logs and support access
- [ ] Retention rules configured with automatic deletion

**Example Scenarios**:

- ✅ **Good**: A data catalogue entry shows the customer contact table as Confidential, owned by Customer Service, retained for a defined period after account closure.
- ❌ **Bad**: A test environment holds a copy of production customer data marked Internal.

**Common Violations**:

- Using UK or other external classification labels instead of the Acme scheme
- Classifying customer personal data below Confidential
- Treating security logs as ordinary application logs

---

### 13. Privacy by Design

**Principle Statement**:
Systems that process personal data MUST apply data minimisation, purpose limitation and privacy-protective defaults, and MUST support data subject rights through automated or documented processes.

**Rationale**:
The consolidated customer record will bring together personal data from three business units, which raises the privacy impact. The Belgian Data Protection Authority (GBA/APD) is Acme's supervisory authority [AIP-C11], and compliance by design is a strategy objective [ACP-C8].

**Implications**:

- Only personal data needed for a defined purpose is collected
- Every processing activity has a lawful basis and is in the record of processing
- Consent and communication preferences are held once and respected in every channel
- Data subject requests (access, correction, erasure, portability) can be met across all systems holding the person's data
- Non-production environments use synthetic or anonymised data

**Validation Gates**:

- [ ] DPIA screening done, and a full DPIA where required
- [ ] Lawful basis and purpose recorded for each personal data element
- [ ] Data subject requests can be fulfilled across all stores
- [ ] No live personal data in non-production environments

**Example Scenarios**:

- ✅ **Good**: Merging customer records across business units is assessed in a DPIA before it starts, and customers are told about it.
- ❌ **Bad**: Marketing consent from one business unit is assumed to cover all three.

**Common Violations**:

- Collecting data "in case it is useful later"
- Erasure processes that miss copies in reporting or archive stores
- Production extracts used for testing

---

### 14. Single Source of Truth

**Principle Statement**:
Every data domain MUST have one authoritative system of record. Derived copies MUST be read-only, clearly labelled and kept in sync from the authoritative source.

**Rationale**:
"One customer record" is a Strategy 2030 commitment [ACP-C5]. Three portals with their own user stores [AIP-C7] create conflicting customer data. Policy already sets the ERP as the source for invoices and limits portals to showing invoice copies [AIP-C12].

**Implications**:

- A system of record is named for each data domain (customer, account, shipment, invoice, pricing)
- The ERP stays the system of record for invoices and e-invoicing; portals display copies only [AIP-C12]
- Customer master data is held in one authoritative record, with business-unit relationships attached to it
- Two-way synchronisation is avoided; where it cannot be avoided, a conflict resolution rule is defined

**Validation Gates**:

- [ ] System of record identified for each data entity
- [ ] Derived copies documented with sync method and frequency
- [ ] No two-way sync without a conflict resolution strategy
- [ ] Master data management approach defined for customer and reference data

**Example Scenarios**:

- ✅ **Good**: The portal fetches invoice documents from the finance system and labels them "copy".
- ❌ **Bad**: The portal creates its own invoice PDFs from local data, and they differ from the official e-invoice.

**Common Violations**:

- Portals editing master data locally without writing it back to the source
- Several systems each claiming to own the customer address
- Reports built on stale copies with no freshness indicator

---

### 15. Data Quality and Lineage

**Principle Statement**:
Data flows MUST meet defined quality standards and provide end-to-end lineage for audit and troubleshooting.

**Rationale**:
Consolidating customer data from three acquired businesses [ACP-C1] will expose duplicates and conflicting records, including for the 1,800 shared business customers [ACP-C2]. Without quality rules and lineage, errors cannot be traced and merge decisions cannot be audited.

**Implications**:

- Quality rules are defined with data owners and checked automatically
- Producers and consumers agree data contracts before integrating
- Lineage is captured as data moves, not reconstructed afterwards
- Quality failures are visible to the data owner and block downstream use where the impact is material

**Quality Standards**:

- **Completeness**: No unexpected gaps in required fields
- **Consistency**: Data reconciles across systems
- **Accuracy**: Validation rules enforced at source
- **Timeliness**: Freshness targets defined and monitored

**Lineage Requirements**:

- Source-to-target mapping documented for every data flow
- Transformation and matching logic version-controlled and reviewable
- Quality metrics tracked per flow
- Impact of schema changes can be analysed

**Validation Gates**:

- [ ] Quality rules defined and automated
- [ ] Lineage captured and queryable
- [ ] Data contracts in place between producers and consumers
- [ ] Customer matching and merge rules documented and auditable

**Example Scenarios**:

- ✅ **Good**: Duplicate business accounts across portals are matched with documented rules, and every merge can be traced back to its source records.
- ❌ **Bad**: Accounts are merged with a one-off script that leaves no record of what was combined.

**Common Violations**:

- One-off migration scripts with no lineage
- Quality checks only in reporting, not at source
- Undocumented manual corrections

---

## IV. Application and Integration Principles

### 16. Interoperability Through Standard Interfaces

**Principle Statement**:
All systems MUST expose functionality through well-defined, versioned interfaces using open, industry-standard protocols and data formats. Direct database access across system boundaries is prohibited.

**Rationale**:
A single customer experience must draw on transport, tracking, cold-chain monitoring and finance systems from three business units. Standard interfaces let back-end systems change or be replaced without breaking the customer experience, and support open standards already in use, such as Peppol e-invoicing [AIP-C12].

**Implications**:

- Interfaces are designed contract-first and specifications are published
- Every interface is versioned with a backward compatibility policy
- Open standards are preferred where they exist (e.g. e-invoicing, logistics messaging)
- Business-unit back-end systems are hidden behind stable group interfaces

**Validation Gates**:

- [ ] Interface specifications published in a machine-readable format
- [ ] Versioning and deprecation policy defined
- [ ] Authentication and authorisation model documented
- [ ] Error handling and retry behaviour specified
- [ ] No direct database coupling across systems

**Example Scenarios**:

- ✅ **Good**: The portal calls one group shipment-status interface, which hides whether the shipment is parcel, freight or cold chain.
- ❌ **Bad**: The portal queries the freight transport management database directly.

**Common Violations**:

- Unversioned interfaces with breaking changes
- Exchanging files over shared folders with no defined contract
- Each consumer building its own adapter to the same back-end

---

### 17. Loose Coupling and Asynchronous Integration

**Principle Statement**:
Systems MUST be loosely coupled through published interfaces or events, with no shared databases, shared file systems or tight runtime dependencies. Systems SHOULD use asynchronous, event-driven communication for interactions that do not need an immediate answer.

**Rationale**:
Loose coupling lets each business-unit system, and each legacy portal being retired, change on its own schedule. Asynchronous integration absorbs peak load [ACP-C4] and isolates customer channels from slow or failing back-ends (Principle 7).

**Implications**:

- Each system owns its data and lifecycle
- Event and message schemas are versioned and published like interfaces
- Consumers are idempotent, because messages may be delivered more than once
- Delivery guarantees, ordering and dead-letter handling are decided per flow
- Customer journeys that span asynchronous steps show status rather than making the customer wait

**When to Use Asynchronous Integration**:

- Shipment status and tracking events
- Notifications to customers
- Long-running processes (bookings that need confirmation, claims, returns)
- Integration with slow or unreliable systems

**When Synchronous Is Acceptable**:

- Real-time user interactions that need an immediate answer
- Read-only queries
- Transactions that need immediate consistency (e.g. price quote confirmation)

**Validation Gates**:

- [ ] Systems communicate through interfaces or events, not shared databases
- [ ] Deploying one system does not require deploying another
- [ ] Asynchronous patterns used for non-real-time flows
- [ ] Delivery guarantees, dead-letter handling and replay defined

**Example Scenarios**:

- ✅ **Good**: Tracking events from all three networks are published once and used by the portal, notifications and reporting.
- ❌ **Bad**: The portal polls three back-end systems every few seconds for every open shipment.

**Common Violations**:

- Distributed transactions across systems
- Shared "integration databases"
- Non-idempotent event handlers

---

### 18. Accessible and Multilingual by Design

**Principle Statement**:
All customer-facing services MUST meet WCAG 2.2 level AA and MUST be fully available in Dutch and French, and SHOULD be available in English. Language and accessibility MUST be designed in from the start, not translated or fixed afterwards.

**Rationale**:
Group policy requires WCAG 2.2 AA for new customer-facing services [AIP-C13], and accessibility is part of the compliance-by-design objective [ACP-C8]. Dutch and French are required commercially and legally, and English is needed for international shippers [ACP-C3]. Self-service targets [ACP-C7] will not be met if some customers cannot use the service.

**Implications**:

- Design components are accessible by default and reused across all channels
- All customer-facing text, notifications and documents are managed as translatable content
- Language choice is stored in the customer profile and used in every channel
- Accessibility and language testing are part of the definition of done

**Validation Gates**:

- [ ] Automated and manual WCAG 2.2 AA testing in the delivery pipeline
- [ ] Independent accessibility audit before go-live
- [ ] All customer-facing content available in Dutch and French (and English where offered)
- [ ] Language preference applied consistently in portal, email and documents

**Example Scenarios**:

- ✅ **Good**: A new booking flow is tested with screen readers in Dutch and French before release.
- ❌ **Bad**: Error messages are hard-coded in Dutch, so French-speaking customers see them in Dutch.

**Common Violations**:

- Text built into images or code
- Adding translations after launch
- Accessibility checked only with automated tools

---

## V. Quality Attributes

### 19. Performance and Efficiency

**Principle Statement**:
All systems MUST meet defined performance targets under peak load and use computing resources efficiently.

**Rationale**:
Slow digital services push customers to the contact centre, which works against the 70% self-service target [ACP-C7] and the run-cost target [ACP-C6]. Performance that is not specified at the start is rarely achieved later.

**Performance Targets** (define for each system):

- **Response time**: p50, p95 and p99 latency targets for key journeys
- **Throughput**: Requests or transactions per second at peak
- **Concurrency**: Number of simultaneous users at peak
- **Resource efficiency**: Utilisation targets

**Implications**:

- Performance requirements are defined before implementation
- Load testing is done before production at peak volumes (Principle 6)
- Performance is monitored continuously in production
- Expensive operations are cached where data freshness allows

**Validation Gates**:

- [ ] Measurable performance targets defined
- [ ] Load testing performed at peak capacity
- [ ] Performance metrics monitored in production
- [ ] Capacity plan defined

**Example Scenarios**:

- ✅ **Good**: Tracking lookups have a p95 target that is load-tested at December volumes.
- ❌ **Bad**: Performance is first measured after customers complain.

**Common Violations**:

- No performance requirements
- Testing only in environments much smaller than production
- Caching data that must be current, such as delivery slot availability

---

### 20. Availability and Reliability

**Principle Statement**:
All systems MUST meet availability targets set according to business impact, with automated recovery and minimal data loss.

**Rationale**:
When digital services fail, customers are pushed to the contact centre, which costs most during peak season [ACP-C4]. Targets based on business impact let investment in resilience match what each service actually needs (Principle 5). NIS2 obligations require proven continuity [AIP-C10].

**Implications**:

- Availability, RTO and RPO targets are agreed with the service owner for each system
- Resilience patterns are chosen to meet those targets, not maximised by default
- Recovery procedures are automated where possible and rehearsed regularly
- Planned maintenance avoids customer-facing downtime, and major changes respect the peak freeze [AIP-C15]

**Availability Targets** (define for each system):

- **Uptime target**: e.g. 99.9% (about 43.8 minutes of downtime a month), higher for critical customer journeys
- **Recovery Time Objective (RTO)**: Maximum acceptable downtime
- **Recovery Point Objective (RPO)**: Maximum acceptable data loss

**High-Availability Patterns**:

- Redundancy across availability zones within EU/EEA regions [AIP-C2]
- Automated health checks and failover
- Active-active or active-passive configurations according to target
- Regular disaster recovery testing, finished before each peak season

**Validation Gates**:

- [ ] Availability target defined
- [ ] RTO and RPO documented
- [ ] Redundancy strategy implemented within EU/EEA
- [ ] Failover and restore tested before peak season

**Example Scenarios**:

- ✅ **Good**: A disaster recovery test in September confirms RTO and RPO before the peak freeze.
- ❌ **Bad**: Backups are taken but have never been restored.

**Common Violations**:

- The same "five nines" target for every system, with no business justification
- Recovery copies stored outside the EU/EEA
- Disaster recovery tests scheduled during peak

---

### 21. Maintainability and Evolvability

**Principle Statement**:
All systems MUST be designed for change, with clear separation of concerns, modular architecture and up-to-date documentation. Significant decisions MUST be recorded as Architecture Decision Records (ADRs).

**Rationale**:
Software spends most of its life being maintained. Recording decisions as ADRs is Architecture Board practice [AIP-C14] and keeps the reasons for decisions available long after delivery teams move on.

**Implications**:

- Modular architecture with clear boundaries
- Business logic, data access and presentation are kept separate
- ADRs for significant choices, reviewed by the Architecture Board
- Automated tests make refactoring safe

**Validation Gates**:

- [ ] Architecture documentation exists and is up to date
- [ ] Module boundaries and responsibilities are clear
- [ ] Automated test coverage supports safe refactoring
- [ ] ADRs record significant choices

**Example Scenarios**:

- ✅ **Good**: The choice of customer identity approach is recorded as an ADR with the options considered.
- ❌ **Bad**: Nobody remembers why a legacy integration exists, so nobody dares to switch it off.

**Common Violations**:

- Decisions made in meetings with no record
- Documentation written once and never updated
- Business rules duplicated across channels

---

## VI. Development and Operations Practices

### 22. Infrastructure as Code

**Principle Statement**:
All infrastructure and platform configuration MUST be defined as code, version-controlled and deployed through automated pipelines.

**Rationale**:
Manual changes cause drift and leave no record. Infrastructure as Code (IaC) supports repeatable migration out of the Ghent data centre [AIP-C3], enforces EU/EEA region policy [AIP-C2], and provides change evidence for CyberFundamentals [AIP-C10].

**Implications**:

- All infrastructure is defined in declarative code
- Infrastructure changes go through code review
- Environments can be rebuilt from code
- No manual changes to production infrastructure
- Policy-as-code enforces region, encryption and tagging rules

**Validation Gates**:

- [ ] Infrastructure defined as code and version-controlled
- [ ] Automated deployment pipeline for infrastructure
- [ ] Policy checks (region, encryption, tagging) automated
- [ ] No manual production changes outside emergency procedures

**Example Scenarios**:

- ✅ **Good**: A pipeline policy check blocks a deployment that tries to use a non-EU region.
- ❌ **Bad**: A firewall rule is changed by hand in production and never recorded.

**Common Violations**:

- "Click-ops" changes in production
- Infrastructure code kept apart from the application it supports
- Emergency changes never brought back into code

---

### 23. Automated Testing

**Principle Statement**:
All code and configuration changes MUST be validated by automated tests before deployment to production.

**Rationale**:
Manual testing cannot keep up with frequent change, and production defects cost far more to fix, especially at peak. Automated tests give the confidence to change systems safely.

**Implications**:

- Tests are written with the code they cover and run on every change
- A failing test blocks the merge
- Non-functional tests (performance, security, accessibility, resilience) are automated
- Test data is synthetic or anonymised, never live personal data (Principle 13)

**Test Pyramid**:

- **Unit tests**: Fast, isolated, high coverage (70 to 80% of tests)
- **Integration tests**: Component interactions (15 to 20% of tests)
- **End-to-end tests**: Critical customer journeys in each supported language (5 to 10% of tests)

**Required Test Types**:

- Functional (does it work?)
- Performance (is it fast enough at peak?)
- Security (is it secure?)
- Accessibility (does it meet WCAG 2.2 AA?)
- Resilience (does it cope with failures?)

**Validation Gates**:

- [ ] Automated tests exist and pass before merge
- [ ] Test coverage meets defined thresholds
- [ ] Critical journeys have end-to-end tests
- [ ] Performance and accessibility tests run regularly

**Example Scenarios**:

- ✅ **Good**: Every merge runs unit, interface-contract and automated accessibility tests.
- ❌ **Bad**: A release is tested by hand the night before go-live.

**Common Violations**:

- Tests switched off to "unblock" a release
- Test environments loaded with production customer data
- No tests for the French or English versions

---

### 24. Continuous Integration, Deployment and Change Windows

**Principle Statement**:
All changes MUST go through automated build, test, security-scan and deployment pipelines with quality gates. Go-lives and migrations MUST NOT take place during the peak freeze from 15 October to 10 January.

**Rationale**:
Automated pipelines make releases small, frequent and repeatable, lowering the risk of each change. The peak freeze protects operations during the highest-volume period [AIP-C15] [ACP-C4].

**Implications**:

- Every change reaches production through the pipeline; there are no manual deployments
- Quality and security gates are automated and cannot be skipped without a recorded exception
- Deployments can be reversed, and rollback or roll-forward is rehearsed
- Programme plans schedule go-lives and migrations outside the peak freeze window
- During the freeze, only emergency fixes approved through change management are deployed

**Pipeline Stages**:

1. **Source control**: All changes committed to version control
2. **Build**: Automated build and packaging
3. **Test**: Automated test execution
4. **Security scan**: Dependency and code vulnerability scanning
5. **Deployment**: Automated deployment to each environment

**Quality Gates**:

- All tests pass
- No critical security vulnerabilities
- Code review approved
- Production readiness checklist completed

**Validation Gates**:

- [ ] Automated CI/CD pipeline exists, including security scanning
- [ ] Deployment is automated and repeatable
- [ ] Rollback tested
- [ ] Go-live and migration dates fall outside 15 October to 10 January

**Example Scenarios**:

- ✅ **Good**: Portal migration waves are planned for February to September, with a rehearsal before each wave.
- ❌ **Bad**: A customer migration is scheduled for early November to "catch up" on a delayed plan.

**Common Violations**:

- Manual hotfixes that bypass the pipeline
- Programme plans that ignore the peak freeze
- Security scan findings waived without a record

---

## VII. Exception Process

### Requesting Architecture Exceptions

Principles are mandatory unless the Acme Architecture Board approves a documented exception. The Board meets monthly, is chaired by the CIO, and records decisions as ADRs [AIP-C14].

**Valid Exception Reasons**:

- Technical constraints that prevent compliance
- Regulatory or legal requirements
- A temporary state during migration (e.g. a legacy portal kept running until it is retired)
- A pilot or proof of concept with a fixed end date

**Exception Request Requirements**:

- [ ] Business or technical justification
- [ ] Alternative approach and compensating controls
- [ ] Risk assessment and mitigation plan
- [ ] Expiry date (exceptions are time-limited)
- [ ] Plan to reach compliance

**Approval Process**:

1. Submit the exception request to Enterprise Architecture
2. Architecture Board review at the next monthly meeting
3. CIO approval; CISO approval as well for exceptions involving security, and DPO approval for those involving personal data
4. Record the exception as an ADR and in the project's architecture documentation
5. Review open exceptions every quarter

**Non-Negotiable**: Principle 8 (Security by Design) allows no exceptions to the principle itself. Only how a control is implemented may vary, and only with compensating controls approved by the CISO. EU/EEA residency (Principles 11 and 12) cannot be waived through this process because it is a group policy requirement [AIP-C2].

---

## VIII. Governance and Compliance

### Architecture Review Gates

All projects must pass architecture reviews at key milestones:

**Discovery / Alpha**:

- [ ] Architecture principles understood by the delivery team
- [ ] High-level approach aligns with the principles, especially One Acme (1) and Reuse, Then Buy, Then Build (2)
- [ ] Regulatory obligations identified (Principle 4)
- [ ] No obvious principle violations

**Beta / Design**:

- [ ] Detailed architecture documented, with ADRs for significant decisions
- [ ] Compliance with each principle checked against its validation gates
- [ ] Exceptions requested and approved
- [ ] Security, data classification and privacy principles checked with the CISO and DPO

**Pre-Production**:

- [ ] Implementation matches the approved architecture
- [ ] All validation gates passed
- [ ] Operational readiness confirmed
- [ ] Go-live date is outside the peak freeze [AIP-C15]

### Enforcement

- Architecture reviews are **mandatory** for all projects
- Principle violations must be fixed before production deployment
- Approved exceptions are time-limited and reviewed every quarter
- Live systems are reviewed after the fact for compliance, with priority given to systems in NIS2 scope

---

## IX. Appendix

### Principle Summary Checklist

| # | Principle | Category | Criticality | Validation |
|---|-----------|----------|-------------|------------|
| 1 | One Acme Customer Experience | Business | CRITICAL | Single brand, login and customer record |
| 2 | Reuse, Then Buy, Then Build | Business | HIGH | Options analysis, ADR for build |
| 3 | Digital Self-Service by Default | Business | HIGH | Self-service completion metrics |
| 4 | Compliance by Design | Business | CRITICAL | DPIA, CyberFundamentals mapping, WCAG audit |
| 5 | Cost-Conscious Architecture and Rationalisation | Business | HIGH | TCO, decommissioning plan |
| 6 | Scalability and Peak-Season Elasticity | Technology | HIGH | Peak load testing (2.3 times volume) |
| 7 | Resilience and Fault Tolerance | Technology | CRITICAL | Failover testing, RTO/RPO |
| 8 | Security by Design | Technology | CRITICAL | Threat model, penetration testing |
| 9 | Unified Identity and Access | Application | CRITICAL | No local credential stores |
| 10 | Observability and Operational Excellence | Technology | HIGH | SLOs, dashboards, runbooks |
| 11 | EU-Hosted, Cloud-First Platform | Technology | CRITICAL | Hosting and residency checks |
| 12 | Data Classification and Sovereignty | Data | CRITICAL | Acme classification applied |
| 13 | Privacy by Design | Data | CRITICAL | DPIA, data subject request handling |
| 14 | Single Source of Truth | Data | HIGH | System of record register |
| 15 | Data Quality and Lineage | Data | MEDIUM | Quality metrics, lineage |
| 16 | Interoperability Through Standard Interfaces | Application | HIGH | Published, versioned interfaces |
| 17 | Loose Coupling and Asynchronous Integration | Application | HIGH | Independent deployment |
| 18 | Accessible and Multilingual by Design | Application | CRITICAL | WCAG 2.2 AA audit, NL/FR content |
| 19 | Performance and Efficiency | Technology | HIGH | Load testing |
| 20 | Availability and Reliability | Technology | CRITICAL | Availability monitoring, DR test before peak |
| 21 | Maintainability and Evolvability | Application | MEDIUM | Documentation, ADRs |
| 22 | Infrastructure as Code | Technology | HIGH | IaC coverage, policy-as-code |
| 23 | Automated Testing | Technology | HIGH | Test coverage |
| 24 | Continuous Integration, Deployment and Change Windows | Technology | HIGH | Pipeline exists, peak freeze respected |

### Strategy Traceability

| Strategy 2030 Objective | Supporting Principles |
|-------------------------|-----------------------|
| One Acme: one brand, one login, one customer record [ACP-C5] | 1, 9, 14, 15, 16 |
| Reduce group IT run cost by 20% by 2029 [ACP-C6] | 2, 5, 6, 11, 22 |
| Digital self-service for 70% of interactions [ACP-C7] | 3, 10, 18, 19, 20 |
| Compliance by design: GDPR, NIS2, accessibility [ACP-C8] | 4, 8, 12, 13, 18 |

### Resolved Tensions

| Tension | Resolution |
|---------|------------|
| Peak capacity (6) vs run-cost reduction (5) | Capacity scales with demand rather than being provisioned for peak all year |
| High availability (20) vs run-cost reduction (5) | Availability targets are set by business impact per system, not maximised everywhere |
| Buy/SaaS preference (2) vs EU-hosted platform (11) | SaaS is acceptable if it meets EU/EEA residency for data, backups, logs and support access |
| Loose coupling (17) vs single customer record (14) | The customer record is owned by one system and reached through published interfaces and events, never through a shared database |

---

## External References

> This section links content in this document back to its source documents, following the ArcKit citation instructions.

### Document Register

| Doc ID | Filename | Type | Source Location | Description |
|--------|----------|------|-----------------|-------------|
| ACP | acme-company-profile.md | Company Profile | 000-global/policies/ | Acme Logistics NV company profile: business units, customer base, Strategy 2030, key people |
| AIP | acme-it-policies.md | Policy | 000-global/policies/ | Acme IT and architecture policies: cloud and hosting, sourcing, identity, data classification, security and compliance, governance |

### Citations

| Citation ID | Doc ID | Page/Section | Category | Quoted Passage |
|-------------|--------|--------------|----------|----------------|
| ACP-C1 | ACP | At a glance | Business Requirement | "Built by acquisition: three business units, each still running its own customer portal." |
| ACP-C2 | ACP | At a glance | Stakeholder Need | "1,800 business customers use more than one portal (overlap analysis, Q2 2026)." |
| ACP-C3 | ACP | At a glance | Compliance Constraint | "Dutch and French are required commercially and legally; English for international shippers." |
| ACP-C4 | ACP | At a glance | Non-Functional Requirement | "Peak season: mid-October to early January, parcel volumes x2.3." |
| ACP-C5 | ACP | Strategy 2030 | Business Requirement | "\"One Acme\" for customers: one brand, one login, one customer record." |
| ACP-C6 | ACP | Strategy 2030 | Business Requirement | "Reduce group IT run cost by 20% by 2029." |
| ACP-C7 | ACP | Strategy 2030 | Business Requirement | "Digital self-service as the default channel: 70% of service interactions." |
| ACP-C8 | ACP | Strategy 2030 | Compliance Constraint | "Compliance by design: GDPR, NIS2, accessibility." |
| AIP-C1 | AIP | Cloud and hosting | Design Decision | "Microsoft Azure is the strategic platform (Enterprise Agreement until 2029)." |
| AIP-C2 | AIP | Cloud and hosting | Data Requirement | "All customer data, backups, logs and vendor support access stay in the EU/EEA." |
| AIP-C3 | AIP | Cloud and hosting | Design Decision | "The on-premises data centre in Ghent closes by end 2028." |
| AIP-C4 | AIP | Sourcing | Procurement Constraint | "Reuse, then buy (SaaS preferred), then build. Custom code only for differentiating capabilities." |
| AIP-C5 | AIP | Sourcing | Procurement Constraint | "Every vendor processing customer data signs the Acme Data Processing Agreement and keeps data in the EU." |
| AIP-C6 | AIP | Identity | Design Decision | "Workforce identity: Microsoft Entra ID (in place)." |
| AIP-C7 | AIP | Identity | Risk Factor | "Customer identity: no group standard yet; each portal has its own user store." |
| AIP-C8 | AIP | Data classification | Data Requirement | "Public, Internal, Confidential, Strictly Confidential." |
| AIP-C9 | AIP | Data classification | Data Requirement | "Customer personal data is Confidential. Credentials and security logs are Strictly Confidential." |
| AIP-C10 | AIP | Security and compliance | Security Requirement | "Acme is registered as an \"important entity\" under the Belgian NIS2 law (postal and courier services). Target control set: CCB CyberFundamentals, assurance level Important, by end 2027." |
| AIP-C11 | AIP | Security and compliance | Compliance Constraint | "GDPR supervisory authority: Belgian Data Protection Authority (GBA/APD)." |
| AIP-C12 | AIP | Security and compliance | Integration Requirement | "Belgian B2B e-invoicing via Peppol is live since 1 January 2026 from SAP S/4HANA. Portals show invoice copies only." |
| AIP-C13 | AIP | Security and compliance | Compliance Constraint | "New customer-facing services meet WCAG 2.2 AA." |
| AIP-C14 | AIP | Governance | Design Decision | "The Architecture Board meets monthly (chair: CIO). Decisions are recorded as ADRs." |
| AIP-C15 | AIP | Governance | Non-Functional Requirement | "Peak freeze: no go-lives or migrations between 15 October and 10 January." |

### Unreferenced Documents

| Filename | Source Location | Reason |
|----------|-----------------|--------|
| — | — | All consulted documents were cited |

---

**Generated by**: ArcKit `/arckit:principles` command
**Generated on**: 2026-10-08
**ArcKit Version**: 6.17.5
**Project**: Acme Logistics NV Global Architecture Governance (Project 000)
**AI Model**: Claude Opus 5.5 (claude-opus-5-5)

<!-- arckit-provenance:start -->

## Build Provenance

*Stamped automatically by the ArcKit plugin's `provenance-stamp.mjs` PostToolUse hook. Complements (does not replace) the human-authored footer above. Carries only fields the model can't authoritatively self-report: build context from `.arckit/state.json` and effort levels derived from command frontmatter + the silent-downgrade matrix.*

| Field | Value |
|-------|-------|
| Requested Effort | `high` |
| Effective Effort | _unknown — model not parsed from existing footer_ |
| Stamped at | 2026-10-08T06:05:49.909Z |

<!-- arckit-provenance:end -->
