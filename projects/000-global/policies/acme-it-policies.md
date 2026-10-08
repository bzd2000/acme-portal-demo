# Acme Logistics NV - IT and Architecture Policies (FICTIONAL)

## Cloud and hosting
- Microsoft Azure is the strategic platform (Enterprise Agreement until 2029).
- All customer data, backups, logs and vendor support access stay in the EU/EEA.
- The on-premises data centre in Ghent closes by end 2028.

## Sourcing
- Reuse, then buy (SaaS preferred), then build. Custom code only for differentiating capabilities.
- Every vendor processing customer data signs the Acme Data Processing Agreement and keeps data in the EU.

## Identity
- Workforce identity: Microsoft Entra ID (in place).
- Customer identity: no group standard yet; each portal has its own user store.

## Data classification (Acme scheme - use this instead of UK government markings)
- Public, Internal, Confidential, Strictly Confidential.
- Customer personal data is Confidential. Credentials and security logs are Strictly Confidential.

## Security and compliance
- Acme is registered as an "important entity" under the Belgian NIS2 law (postal and courier services). Target control set: CCB CyberFundamentals, assurance level Important, by end 2027.
- GDPR supervisory authority: Belgian Data Protection Authority (GBA/APD).
- Belgian B2B e-invoicing via Peppol is live since 1 January 2026 from SAP S/4HANA. Portals show invoice copies only.
- New customer-facing services meet WCAG 2.2 AA.

## Governance
- The Architecture Board meets monthly (chair: CIO). Decisions are recorded as ADRs.
- Peak freeze: no go-lives or migrations between 15 October and 10 January.
