# Current Portal Inventory (FICTIONAL - compiled by the EA team, August 2026)

| | Portal A "MyAcme" | Portal B "FreightView" | Portal C "ColdTrack" |
|---|---|---|---|
| Business unit | Acme Parcel | Brabant Freight | Flanders Cold Chain |
| Registered users | 150,000 consumers + 4,200 business accounts | 3,100 business accounts | 2,200 business accounts |
| Monthly active users | 41,000 | 2,600 | 1,900 |
| Technology | .NET Framework 4.6, SQL Server, on-premises Ghent | Liferay 6.2 (out of support), Java, hosted by a German service provider | SaaS product "TrackBox", multi-tenant |
| Live since | 2014, built in-house | 2016, built by an agency | 2019, subscription |
| Login | own user database, no MFA | own user database, MFA optional | vendor login, MFA for admins only |
| Languages | NL, FR, EN | NL, FR (French incomplete) | NL, EN (no French) |
| Key features | track and trace, pickup booking, returns, invoice PDFs, address book | pallet booking, quotes, proof of delivery, invoices, EDI order upload | temperature monitoring, alerts, compliance certificates (HACCP, GDP) |
| Integrations | TMS "ParcelCore", Dynamics 365 CRM, SAP S/4HANA | TMS "FreightMaster", Salesforce, SAP S/4HANA | telematics feed from trucks, SAP S/4HANA |
| Annual run cost | EUR 610,000 | EUR 420,000 | EUR 280,000 |
| Contract / end of life | in-house; .NET 4.6 out of support | hosting contract ends 30 June 2027 | subscription renews 31 March 2027 for 3 years |
| Known issues | credential-stuffing attack Feb 2025, 12,000 password resets | slow (6.8 s average page load), no new features since 2022 | vendor support staff outside the EU can access data (DPA finding open) |

Total run cost: EUR 1.31M per year.
