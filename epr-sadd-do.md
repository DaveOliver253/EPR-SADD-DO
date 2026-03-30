
# 8. Department for Environment, Food and Rural Affairs
# Solution architecture definition document (SADD)
# EPR: RPD and PayCal
 
**Version: 1.1**  
**DDTS Delivery Architecture Team**  
**Date: 23/3/2026**

## Contents
1. [Introduction](#introduction)  
1.1 [Purpose](#11-purpose)  
1.2 [History](#12-history)  
1.3 [References to governance products](#13-references-to-governance-products)  

2. [Business context model](#2-business-context-model)  
2.1 [Background](#21-background)  
2.2 [Product vision](#22-product-vision)  
2.3 [Business model (actors, functions, products, goals)](#23-business-model-actors-functions-products-goals)  
2.4 [Business process (how, when, why, with what)](#24-business-process-how-when-why-with-what)  
2.5 [Business rules](#25-business-rules)  
2.6 [Timing view](#26-timing-view)  

3. [Solution landscape](#3-solution-landscape)  
3.1 [Solution landscape – overview](#31-solution-landscape--overview)  
3.2 [Solution landscape – business to information system](#32-solution-landscape--business-to-information-system)  
3.3 [Solution landscape – information system to technology](#33-solution-landscape--information-system-to-technology)  

4. [Change impacts](#4-change-impacts)  
4.1 [Non system IT service impacts](#41-non-system-it-service-impacts)  
4.2 [Application dimension](#42-application-dimension)  
4.3 [Data dimension](#43-data-dimension)  
4.4 [Technology dimension](#44-technology-dimension)  

5. [Information system view - apps](#5-information-system-view---apps)  
5.1 [System context](#51-system-context)  
5.2 [Application architecture – external cooperation view](#52-application-architecture--external-cooperation-view)  
5.3 [Application architecture – internal structure view](#53-application-architecture--internal-structure-view)  
5.4 [Application architecture – internal behavioural view](#54-application-architecture--internal-behavioural-view)  
5.5 [Application architecture – state model](#55-application-architecture--state-model)  
5.6 [Component classification table](#56-component-classification-table)  
5.7 [Application architecture – cloud native design approach](#57-application-architecture--cloud-native-design-approach)  

6. [Information system view – data](#6-information-system-view--data)  
6.1 [Data architecture – overview](#61-data-architecture--overview)  
6.2 [Data architecture – integrity and quality view](#62-data-architecture--integrity-and-quality-view)  
6.3 [Data architecture – data models](#63-data-architecture--data-models)  
6.4 [Data architecture – data model terminology--glossary](#64-data-architecture--data-model-terminology--glossary)  
6.5 [Data architecture – data dependency referential integrity view](#65-data-architecture--data-dependency-referential-integrity-view)  
6.6 [Data architecture – data stores](#66-data-architecture--data-stores)  
6.7 [Data architecture – data exchanges (flows)](#67-data-architecture--data-exchanges-flows)  
6.8 [Data architecture – synchronisation](#68-data-architecture--synchronisation)  
6.9 [Data architecture – data resilience and recovery](#69-data-architecture--data-resilience-and-recovery)  
6.10 [Data architecture – retention, archival and disposal](#610-data-architecture--retention-archival-and-disposal)  
6.11 [Data architecture – non-core (logging)](#611-data-architecture--non-core-logging)  
6.12 [Data architecture – mastership--ownership-view](#612-data-architecture--mastership--ownership-view)  
6.13 [Data architecture – business reporting--intelligence-and-analytics](#613-data-architecture--business-reporting--intelligence-and-analytics)  

7. [Integration architecture](#7-integration-architecture)  
7.1 [Interfaces overview](#71-interfaces-overview)  
7.2 [Interface catalogue](#72-interface-catalogue)  

8. [Software architecture](#8-software-architecture)  
8.1 [Component “micro designs”](#81-component-micro-designs)  
8.2 [Exception handling view / pattern](#82-exception-handling-view--pattern)  
8.3 [Component environment specific behaviours](#83-component-environment-specific-behaviours)  
8.4 [Component replacement or upgrade capability](#84-component-replacement-or-upgrade-capability)  
8.5 [Component behaviour tuning / adjustment](#85-component-behaviour-tuning--adjustment)  
8.6 [Component-specific “health warnings” / constraints](#86-component-specific-health-warnings--constraints)  
8.7 [Monitoring and logging hooks / facilities](#87-monitoring-and-logging-hooks--facilities)  

9. [Technology architecture](#9-technology-architecture)  
9.1 [Logical platform architecture](#91-logical-platform-architecture)  
[Logical](#logical)  
9.2 [Physical platform architecture](#92-physical-platform-architecture)  
[Data curation - silver layer](#data-curation---silver-layer)  
[Data consumption - gold layer](#data-consumption---gold-layer)  
[Synapse data pipelines](#synapse-data-pipelines)  
[Enrolment app](#enrolment-app)  
[Intro](#intro)  
[Process diagram](#process-diagram)  
[Configuration file](#configuration-file)  
[Process flow](#process-flow)  
[Pipeline](#pipeline)  
[Notebook](#notebook)  
[Trigger](#trigger)  
[Schedule](#schedule)  
9.3 [Performance / volumetrics / scaling capability](#93-performance--volumetrics--scaling-capability)  
9.4 [Localised availability and recoverability features](#94-localised-availability-and-recoverability-features)  
9.5 [Cross-system reliability or recovery considerations](#95-cross-system-reliability-or-recovery-considerations)  
9.6 [“Test in live” considerations](#96-test-in-live-considerations)  
9.7 [Serviceability features](#97-serviceability-features)  

10. [Security architecture](#10-security-architecture)  
10.1 [Security view](#101-security-view)  
10.2 [Security roles and responsibilities view](#102-security-roles-and-responsibilities-view)  
10.3 [Information handling / classification view](#103-information-handling--classification-view)  
10.4 [Role, actor and function matrix](#104-role-actor-and-function-matrix)  
10.5 [Leveraged security components](#105-leveraged-security-components)  
10.5.1 [Web application firewall](#1051-web-application-firewall)  
10.5.2 [Protective monitoring](#1052-protective-monitoring)  
10.6 [Bespoke security components](#106-bespoke-security-components)  
10.7 [Key management](#107-key-management)  
10.8 [Malware detection / prevention](#108-malware-detection--prevention)  
10.9 [Authentication / authorisation model – human actors](#109-authentication--authorisation-model--human-actors)  
10.10 [Authentication / authorisation model – system actors](#1010-authentication--authorisation-model--system-actors)  
10.11 [GitHub and CI/CD pipeline](#1011-github-and-cicd-pipeline)  

11. [Delivery architecture (or secondary architecture)](#11-delivery-architecture-or-secondary-architecture)  
11.1 [Development platform](#111-development-platform)  
11.2 [Testing solution](#112-testing-solution)  
11.3 [Route to live](#113-route-to-live)  
11.4 [Service monitoring solution](#114-service-monitoring-solution)  
[Monitoring processes](#monitoring-processes)  
[Diagnosis features](#diagnosis-features)  

12. [Operational architecture](#12-operational-architecture)  
12.1 [Initialising, controlling, stopping](#121-initialising-controlling-stopping)  
12.2 [Monitoring processes](#122-monitoring-processes)  
12.3 [Diagnosis features](#123-diagnosis-features)  
12.4 [Capacity reporting](#124-capacity-reporting)  
12.5 [Rebuild, recovery and reinstatement](#125-rebuild-recovery-and-reinstatement)  
12.6 [Scheduled capabilities](#126-scheduled-capabilities)  
12.7 [Calendar constraints](#127-calendar-constraints)  
12.8 [Required cyclic activities (required forward schedule of changes)](#128-required-cyclic-activities-required-forward-schedule-of-changes)  
12.9 [Incident or problem management](#129-incident-or-problem-management)  

13. [Commercial perspectives](#13-commercial-perspectives)  
13.1 [Licencing](#131-licencing)  
13.2 [Recurring costs](#132-recurring-costs)  
13.3 [Costs to scale](#133-costs-to-scale)  
13.4 [Current information](#134-current-information)  

14. [Inventory view](#14-inventory-view)  
14.1 [Databases / stores / storage services](#141-databases--stores--storage-services)  
14.2 [Servers / hardware](#142-servers--hardware)  
14.3 [Services (PaaS etc)](#143-services-paas-etc)  
14.4 [Keys](#144-keys)  
14.5 [Built software components](#145-built-software-components)  
14.6 [Non-built software / cots](#146-non-built-software--cots)  
14.7 [Licences](#147-licences)  
14.8 [Scripts](#148-scripts)  
14.9 [Locations of documentation](#149-locations-of-documentation)  
14.10 [Current information](#1410-current-information)  

15. [Appendices](#15-appendices)  
15.1 [Glossary](#151-glossary)  
15.2 [Index of diagrams](#152-index-of-diagrams)  
15.3 [Index of tables](#153-index-of-tables)  
15.4 [Architectural RAID-D](#154-architectural-raid-d)  
15.5 [Architectural questions / answers](#155-architectural-questions--answers)  
15.6 [Architectural standards and patterns used](#156-architectural-standards-and-patterns-used)  
15.7 [References: ADR](#157-references-adr)  
15.8 [References: Input products](#158-references-input-products)  
15.9 [References: Derived products](#159-references-derived-products)  
15.10 [References: Related products](#1510-references-related-products)  
15.11 [Governance: Approval process](#1511-governance-approval-process)  
15.12 [Governance: Quality success criteria](#1512-governance-quality-success-criteria)


<br> 

# 1. Introduction

### Purpose
The Extended Producer Responsibility (EPR) system, implemented by the UK Department for Environment, Food & Rural Affairs (DEFRA), forms a cornerstone of sustainable waste management. It introduces a technical framework designed to transfer the costs and responsibilities of managing packaging waste across its full lifecycle – from production to disposal – directly to producers. This system aligns with the requirements of the Environment Act 2021 and seeks to streamline waste collection and recycling infrastructure while promoting accountability.

This architecture defines the roles and interactions of the key stakeholders:
- Producers are the primary participants, making periodic declarations of waste tonnage used.
- Compliance schemes are third-party mediators that support producers by handling reporting, payments, and regulatory adherence.
- Local authorities manage the operational aspects of waste collection and recycling.
- Regulatory bodies from the four nations in the UK provide governance, enforcement and ongoing system optimisation.

The EPR's modular design framework facilitates the transition toward a circular economy, emphasising sustainability and resource efficiency. 

This document reflects the system as it is at Release 16 for the RPD, PayCal and data platform components. Details of other components of the EPR service, including RE/EX (Reprocessors and Exporters) and LAPS (Local Authority Packaging Service) are out of scope for this document. 

Please note that the SADD is a high-level document bringing together everything related to the design of RPD and PayCal. For lower-level detail, this document signposts via links (URL) to Confluence and Defra SharePoint.

### History
*Summarise the major changes to the system implemented by successive projects.*

| Version | Date | Description | Author |
| :--- | :--- | :--- | :--- |
| 0.1 | 09/04/2025 | Initial draft | Tim Robinson |
| 0.2 | 31/07/2025 | Updated draft, to reflect release 12, with additional information on PayCal and FSS | David Thompson |
| 1.0 | 26/11/2025 | Updates to reflect R16 | Saunder Narayan (et al) |
| 1.1 | 23/03/2026 | Updates to reflect ADRs up to 143 | Dave Oliver (et al) |
| 1.2 | 30/03/2026 | Updates to reflect ADR-141 (PRN & Waste Balance Immutability — For Review) and ADR-146 (Certificates and Statements of Compliance — In Review) | Dave Oliver |

> **[v1.2 change]** Version 1.2 adds coverage of two ADRs currently under review: ADR-141 governing PRN and waste balance immutability in the RE/EX service, and ADR-146 introducing Certificates and Statements of Compliance (CSoC) as a new business function. Neither ADR has a formal signed-off decision at the time of writing — sections updated below are marked accordingly.

### References to governance products
*Project Management Quality products.* 

The EPR programme aligns with UK Government functional standards and governance frameworks to ensure transparency, accountability and effective decision-making. Key governance products include:. 

These products are developed in line with the Cabinet Office’s [Guide to Governance and Management Frameworks](https://www.gov.uk/guidance/guide-to-governance-and-management-frameworks) and the principles outlined in the [Teal Book – Chapter 13](https://projectdelivery.gov.uk/teal-book/home/part-d-managing-programmes-and-projects/chapter-13-the-governance-and-management-of-programmes-and-projects/).

<br> 

# 2. Business context model
*The intention should be to reuse existing information and place the solution architecture within a context. It should help the reader understand “Why” the system exists without needing to read another document. Most context information should be reused from prior discovery work with of course a brief health check that it is still relevant.*

### 2.1 Background
*Clearly state what the rationale for change is with some context as to the history of the initiative.* 

The Extended Producer Responsibility (EPR) initiative was introduced by Defra in response to the **Environment Act 2021**, which mandates that producers bear the full net cost of managing packaging waste. Historically, the UK’s packaging waste system relied on the National Packaging Waste Database (NPWD) and a series of fragmented processes across regulators and schemes. This resulted in limited transparency, manual effort and inconsistent recovery of costs from producers.

The rationale for change stems from:
- The need to modernise and digitise waste reporting and compliance.
- A policy shift toward full-cost recovery from producers.
- The ambition to improve data quality, transparency and accountability across the packaging lifecycle.

The programme developed into two core product-aligned workstreams:
- **Report Packaging Data (RPD)** – The producer-facing digital service and APIs used to register producers, capture and validate POM data and provide Regulators with accurate reporting.
- **PayCal** – The digital service used by the Scheme Administrators to calculate disposal fees for liable Producers based on POM (placed-on-market) data, LAPCAP (Local Authority Packaging Capacity)-derived local authority cost data and modulated fee parameters.

Together, RPD and PayCal provide the core digital capability to:
- Capture and maintain high-quality producer registration and POM data.
- Apply legislative fee structures and cost recovery policy to calculate producer obligations.
- Produce billing outputs that enable FSS (Financial Services Supplier) to issue invoices of liability to producers.

This modular approach enables incremental delivery, clear separation of responsibilities and a scalable foundation for future EPR enhancements.

### 2.2 Product vision
*Identifies the external customers of the system (e.g. Traders, Competent authorities, other government depts. etc.) and key internal stakeholders, and explains the value each gets from the solution.* 

The product vision is to deliver a scalable, resilient, and user-centred platform that:
- Enables accurate, timely, and secure data exchange.
- Supports policy evolution and behavioural change.
- Facilitates the UK’s transition to a circular economy by embedding sustainability into packaging design and disposal.
- Calculates producer liabilities using their market data and local authority costs to generate the billing data to issue invoices and collect payments.

The EPR digital service is designed to serve a diverse ecosystem of external and internal stakeholders. Within this document, we focus on how RPD and PayCal deliver value to:

**External customers**
- **Packaging producers (direct and via compliance schemes):** They can register, submit placed-on-market (PoM) data, view their obligations and historic submissions and manage account details. They benefit from clearer visibility of how their packaging choices drive costs and incentives to reduce environmental impact.
- **Compliance schemes:** Act on behalf of producers to manage submissions, payments, and regulatory adherence. Use RPD outputs to understand member obligations, support their account management and reporting.
- **Local authorities:** Submit data and receive payments for household packaging waste collection.
- **Reprocessors and exporters:** Gain accreditation and register PRNs/PERNs (Packaging Recovery Notes / Packaging Export Recovery Notes ) exchanged on the external market.
- **Regulators:** Environment Agency (EA), Scottish Environment Protection Agency (SEPA), National Resources Wales (NRW), The Northern Ireland Environment Agency (NIEA). These organisations use RPD regulatory views and reports to monitor compliance and enforce regulations. They also manage public registers and policy evaluation using data sourced from RPD.

**Internal stakeholders**
- **Defra digital delivery teams:** Design, build and maintain the platform using cloud-native architecture.
- **Scheme administrator (PackUK):** Operates PayCal to calculate producer disposal fees using RPD POM data, LAPCAP cost data and fee parameters. Reviews and classifies calculator runs and approves outputs for downstream invoicing and reconciliation.
- **Policy and legal teams:** Ensure the service aligns with legislative intent and regulatory frameworks.



### 2.3 Business model (actors, functions, products, goals)
*Identifies the functional goals of the system and which actor (groups) require these.* 

This section outlines the key actors involved in the Extended Producer Responsibility (EPR) system, the core functions they perform, the digital products that support them, and the overarching goals of the service. 

RPD and PayCal are comprised of a range of services and components supported by Azure technology services.

| Actor group | Service description | Functions | Goals |
| :--- | :--- | :--- | :--- |
| Producers | Businesses placing packaging on the UK market. | Submit packaging data, pay fees, ensure compliance. | Fund waste management, improve packaging sustainability, meet legal obligations. |
| Compliance schemes | Third-party organisations acting on behalf of producers. | Manage data submissions, handle payments, ensure producer compliance. | Simplify compliance for producers, ensure accurate reporting and timely payments. |
| Reprocessors and exporters | Accredited entities that recycle or export packaging waste. | Process packaging waste, issue PRNs/PERNs, report recycling/export data. | Support circular economy, ensure traceability of recycled/exported materials. |
| Local authorities | Manage household waste collection and submit data. | Collect packaging waste, report collection data, receive payments. | Improve local recycling rates, ensure accurate data for funding allocation. |
| Regulators (EA, SEPA, NRW, NIEA) | Oversee registration, compliance, enforcement and public registers. | Monitor compliance, enforce regulations, maintain public registers. | Ensure legal compliance, maintain transparency and accountability. |
| Scheme administrator (PackUK) | Manage financial flows, data validation, and operational oversight. | Validate data, manage payments, oversee scheme operations. | Ensure financial integrity, operational efficiency and data accuracy. |
| FSS | Manage the issuing and payment of producer invoices. | Send invoices, cancel invoices, support payment queries and maintain ledger. | Ensure bills are paid. |
| LAPCAP | Determine local authority household waste management cost. | Collate local authority household waste processing cost by material and country and provide to PayCal. | Provide accurate data. |
| Defra digital delivery teams | Design, build and maintain the digital infrastructure and services. | Dvelop and maintain digital services, ensure system scalability and security. | Deliver robust digital infrastructure to support EPR operations. |
| CCOE operations | Platform governance and compliance. | Enforce platform standards, monitor compliance, support governance. | Maintain platform integrity, ensure compliance with architectural and operational standards. |
| Platform/DevOps | Infrastructure as code, pipelines. | Automate deployments, manage environments, ensure CI/CD practices. | Enable efficient, reliable and scalable infrastructure delivery. |
| Service team | Day-to-day operation, support, and maintenance of EPR services. | Monitor services, resolve incidents, manage service performance. | Ensure high availability, reliability, and user satisfaction of EPR digital services. |

## 2.4 Business process (how, when, why, with what)
*Lists the main business processes affected, the teams / Business Units involved (internal). If prior to implementation, then there is value in showing the current state and envisaged state; whilst the process flows may essentially be the same it is likely the tools used to perform activities changes.*

The Extended Producer Responsibility (EPR) system introduces a set of interdependent business processes that support the UK’s transition to a circular economy. The RPD and PayCal services support a sub-set of interdependent business processes that implement the EPR policy intent ensuring that producers bear the full cost of managing packaging waste, while enabling regulators, local authorities, and compliance schemes to operate efficiently and transparently.

| Process | Description | When | Tools / Systems |
| :--- | :--- | :--- | :--- |
| Producer registration | Producers register and declare their packaging activity. | Annually, with updates as needed | pEPR (packaging EPR) web portal, Submission API |
| Packaging data submission | Producers and compliance schemes submit placed-on-market (PoM) data. | Biannually | Submission API, validation engine |
| PRN/PERN management | Reprocessors/exporters issue evidence of recycling and producers (direct/compliance schemes) buy these notes to offset their annual recycling obligations. | Ongoing throughout compliance year | RE/EX (or legacy NPWD), RPD |
| Disposal cost calculation | Scheme administrator calculates fees based on recyclability and volume. | Quarterly | Fee calculator, PayCal, Azure SQL DB |
| Local authority payments | Local authorities submit data and receive payments. | Quarterly | Scheme admin interface |
| Regulatory oversight | Regulators review submissions, manage public registers and enforce compliance. | Continuous | Regulator dashboard, public register |
| Reporting and analytics | Dashboards and reports support transparency and policy evaluation. | Monthly / Ad hoc | Power BI, Azure Monitor |
| CSoC submission *(pending ADR-146)* | Direct-registrant large producers and compliance schemes submit a Certificate of Compliance (producers) or Statement of Compliance (schemes) confirming whether they have met their recycling obligations for the preceding compliance year. Regulators review and accept, reject or cancel submissions. Accepted submissions are published to the public register. | Annually by 31 January | New CDP Obligations FE, new CDP Regulator FE, new CDP CSoC API (pending ADR-146 decision) |

> **[v1.2 change — ADR-146]** CSoC row added. This is a new business process not previously covered in the SADD. ADR-146 is currently In Review; the recommended option is to build all components on CDP. No formal decision has been signed off at the time of writing.
| Obligation calculation | PayCal calculates disposal cost fees per producer per material including adjustments and generates result file for review. | Half-yearly for large producers and annually for small producers. | PayCal application associated with RPD. |
| Review, classification and approval | Scheme administrator reviews result file, runs QA checks and classifies the run. Approved runs are signed off and billing file is produced for downstream system. | Half-yearly for large producers and annually for small producers. | PayCal application associated with RPD. |
| Invoicing and NoL generation | FSS receives billing and payment files from PayCal, generates invoices and Notice of Liabilities while producers access invoice details via appropriate service and payment management is handled by FSS (details are out of scope for this SADD). | Half-yearly for large producers and annually for small producers. | FSS system is software as a service (SaaS) from ServiceNow. |


![Figure 1.0 (E2E RPD flow)](./epr-sadd-images/01/figure-1.0-e2e-rpd-flow.png)
Figure 1.0 E2E RPD flow - business process - [original illo file](./illos)

<br>

![Figure 2.0 (Calculator Journey)](./epr-sadd-images/01/figure-2.0-calculator-journey.png)
Figure 2.0 PayCal - payment calculator process - [original illo file](./illos)

<br>

The end-to-end business journey for the Extended Producer Responsibility (EPR) service, within the scope of this SADD, focuses on RPD (Report Packaging Data) and PayCal (Payment Calculator). Together, these systems support producers in registering, submitting data, and receiving accurate disposal fee calculations, while enabling regulators and scheme administrators to perform validation and financial settlement.

In essence, the end-to-end RPD and PayCal process ensures that:
- Producers submit accurate packaging data.
- Regulators validate submissions.
- PayCal calculates disposal fees using RPD data, LAPCAP inputs, and scheme parameters.
- Outputs are issued to FSS for invoice generation and liability notices.

## 2.5 Business rules
*Should ideally reference out to existing policy or regulatory frameworks but also capture any key rules that constrain or drive the solution and are implemented in system logic – for example a Rule that credit card information must never be displayed (a rule is a form of mandatory requirement that must be adhered to regardless of timing, scope, deferral etc.). A rule that a certain task must be concluded within a certain time frame etc. (KPI or perhaps a prior steps output “times out” of not processed within a certain period. Particular care must be taken in establishing these where automating existing manual processes. It may be that a specific rules engine product is used, and this is managed by the business.*

The Extended Producer Responsibility (EPR) system is governed by a set of mandatory business rules derived from legislation, regulatory frameworks and operational policy. These rules are implemented directly in system logic and must be always adhered to, regardless of timing, scope, or deferral. These are now specific for RPD and PayCal.

**Regulatory and policy foundations**

The business rules are aligned with:
- The Environment Act 2021
- Defra’s statutory guidance on packaging waste
- Four-nation regulatory requirements (EA, SEPA, NRW, NIEA)
- Data protection and security standards (e.g. GDPR, ISO/IEC 27001)

**Key business rules implemented in system logic**

| Rule category | Description |
| :--- | :--- |
| Data integrity | All packaging data submissions must pass schema validation and business rule checks before acceptance. |
| Time-bound submissions | Producers must submit placed-on-market (POM) data biannually. Submissions outside the defined windows are rejected unless explicitly authorised. |
| Accreditation validity | Reprocessors and exporters must hold valid accreditation before issuing PRNs/PERNs. Accreditation is time-limited and must be renewed annually. |
| Fee calculation | Disposal cost fees are calculated using modulated rates based on recyclability and packaging type. These rates are centrally maintained and version-controlled. |
| Data retention | All submitted data must be retained for a minimum of 6 years for audit and regulatory purposes. In practice for RPD due to regulations related to PayCal data needs be retained for a longer period of 11 years. |
| Access control | Role-based access control (RBAC) is enforced across all portals and APIs. Sensitive data (e.g. financials, personal identifiers) is masked or restricted based on user role. |
| Timeouts and escalations | Tasks such as registration approval or data validation must be completed within defined SLAs (e.g. 10 working days). Unresolved tasks trigger automated escalations. |
| Public register publication | Producer and reprocessor details are published to the public register only after successful validation and approval. |
| Error handling | All user-facing forms and APIs include real-time validation and user-friendly error messages to prevent invalid submissions. |
| CSoC submission authority *(pending ADR-146)* | Only the Approved Person for a producer or compliance scheme may submit a Certificate or Statement of Compliance. Delegated users may not submit on their behalf. |
| CSoC versioning *(pending ADR-146)* | Multiple CSoC submissions for the same compliance year are permitted, but only following the cancellation or rejection of the previously submitted CSoC. A history of all submissions for a given year must be retained. |
| CSoC deadline *(pending ADR-146)* | Certificates and Statements of Compliance must be submitted by 31 January each year, covering the preceding compliance year. |
| PRN immutability *(pending ADR-141)* | Once a PRN or PERN has been issued, its core fields (tonnage, accreditation reference, issuedToOrganisation) are immutable. Only status and metadata fields may be updated. Every status change is recorded in an append-only status history. |
| Waste balance integrity *(pending ADR-141)* | All changes to the waste balance are recorded as append-only transactions including opening and closing balances, transaction type (DEBIT/CREDIT), entity reference and the identity of the user making the change. No transaction may be deleted or updated. |

> **[v1.2 change — ADR-141 and ADR-146]** Five new business rules added: two for CSoC (ADR-146) covering submission authority, versioning and deadline; two for PRN/waste balance immutability (ADR-141). Both ADRs are pending formal decision.

## 2.6 Timing view
*Describes e.g. any cyclic activity or business events that need to be aligned to or avoided (essential the business calendar).*

| Period | Key activities | Notes |
| :--- | :--- | :--- |
| January – March | Finalisation of previous year’s data; compliance reporting including CSoC submission deadline (31 January); PRN/PERN reconciliation; initial PayCal runs for the previous compliance year. | Producers and compliance schemes submit final data for the previous compliance year. Direct-registrant large producers and compliance schemes must submit their Certificate or Statement of Compliance by 31 January. Regulators review and action CSoC submissions. PackUK runs PayCal using finalised data; preliminary billing files are generated for review. |

> **[v1.2 change — ADR-146]** January–March timing row updated to include the CSoC submission deadline of 31 January and regulator review activity.
| April – June | System enhancements; onboarding of new users; regulator workflow updates | Often includes releases and updates to accreditation workflows. |
| July – September | Packaging data submission (POM); fee calculation and invoicing | Includes modulation updates, any mid-year recalculations agreed with policy and finance teams. |
| October – December | Registration window opens in RPD for the next compliance year. | Producers and compliance schemes begin submitting registration data for the upcoming year and concurrent planning for the next cycle of PayCal runs and parameter updates. |

**Cyclic activities**
- **Biannual POM submissions:** Producers submit placed-on-market data twice per year.
- **Quarterly fee calculations:** Disposal cost calculations and invoicing are performed quarterly.
- **Annual registration:** Producers, reprocessors and exporters must register each year, typically starting in October.
- **PayCal run cycle:** PackUK runs PayCal at defined points (e.g. provisional, final reconciliation runs), each producing result files for review and when billing.
- **Accreditation reviews:** Reprocessors and exporters undergo annual accreditation and fee payment cycles.

**Events to align With or avoid**
- **Release windows:** Major platform updates are scheduled to avoid peak submission periods.
- **Regulatory deadlines:** Submission and payment deadlines are fixed and must be supported by system availability and user readiness.
- **Public register updates:** Occur in tandem with submission cycles and must be synchronised with data validation processes.

<br> 

# 3. Solution landscape
## 3.1 Solution landscape – overview
*Rich picture “helicopter view” of the system within the wider domain landscape. E.g. in the “international trade” domain there are some 15+ systems some of which are DEFRA, some not. Some affected directly by this system, some not. It is simply the systems landscape of the functional domain in question. In ArchiMate an application cooperation view is applicable but with a wider scope than the later system context diagram.*

The RPD and PayCal system is a connected set of digital tools that help companies report their packaging data and work out the fees they need to pay. It links producers’ own systems with central government systems so reporting is easier and more accurate, with APIs that allow information to move smoothly between producers, compliance schemes and regulators. Dashboards and analysis tools give clear insights to help improve performance and increase transparency. 

Altogether, this set-up ensures efficient implementation of EPR/RPD regulations and provides a scalable, accountable way to manage packaging waste across the whole system.

![Figure 3.0 Application cooperation view](./epr-sadd-images/01/figure-3.0-application-cooperation-view.png)

Figure 3.0 Application cooperation view - [original illo file](./illos)


The main components are:

#### 1. RPD front end
The RPD front end is the user interface for the Report Packaging Data (RPD) service. It allows producers and compliance schemes to:
- Register and submit packaging data.
- View calculated recycling obligations.
- Track compliance with Extended Producer Responsibility (EPR) regulations.
- Access PRNs (Packaging Recovery Notes) and PERNs (Packaging Export Recovery Notes) for evidence of recycling.

#### 2. Regulator front end
This interface is used by environmental regulators (Environment Agency, SEPA, NRW, NIEA) to:
- Monitor producer compliance.
- Review submitted data and evidence.
- Manage accreditations for reprocessors and exporters.
- Enforce regulations under the producer responsibility obligations.

#### 3. PRN front end – live, PRN obligations to go live in release 13
The PRN (Packaging Recovery Note) front end is used by:
- Accredited reprocessors and exporters to issue PRNs and PERNs from RE/EX that is outside RPD.
- Producers and compliance schemes to acquire and manage these notes as proof of recycling.
- Regulators to track the flow and validity of issued notes.

#### 4. LAPS (local authority packaging service – outside RPD and PayCal) - to go live in a future release
- Supports local authorities in managing packaging waste data.
- LAPCAP interfaces with national systems like RPD or RE/EX.
- May be involved in reporting or validating local recycling efforts.

#### 5. RE/EX (reprocessors and exporters platform – RREPW) – from February 2026
From February 2026, the RE/EX platform (RREPW – Reprocessors, Recyclers, Exporters and Producers of Waste) on the Core Delivery Platform (CDP) became the official system for all PRNs and PERNs issued on or after 1 February 2026. It replaces NPWD for the 2026 compliance year onwards.

NPWD still holds all PRNs and PERNs issued up to 31 January 2026 (the 2025 compliance year). NPWD-facing functions continue to operate in parallel for 2025-year obligations.

Key architectural features of RE/EX:
- **Organisation API:** A CDP-hosted REST API that returns producer and compliance-scheme organisation data (Example: `GET /organisations?registrations=LARGE-PRODUCER,COMPLIANCE-SCHEME`). It's secured via CDP API Gateway using AWS Cognito with client-credentials authentication.
- **PRN/PERN API:** RE/EX provides APIs for querying newly-issued PRNs/PERNs and for receiving accept/reject status updates from RPD.
- **Three new Azure functions** (timer-triggered, based on existing NPWD function patterns): (1) Organisation sync: RPD → RE/EX; (2) PRN/PERN retrieval: RE/EX → RPD PRN database; (3) Accept/reject status updates: RPD PRN database → RE/EX.

#### 5a. NPWD (national packaging waste database – outside RPD and PayCal) - legacy
- Registered producers and compliance schemes.
- Submitted packaging data.
- Issued and tracked PRNs and PERNs.
- Managed accreditations for reprocessors and exporters.

#### 6. FSS (financial services supplier – outside RPD and PayCal) – to go live in a future release
- Handles financial transactions related to PRNs, PERNs, and registration fees.
- Supports reconciliation and auditing of payments.
- Ensures accurate settlement between producers, schemes, and regulators.


Additional information:
- [Extended producer responsibility for packaging: recycling ... - GOV.UK](https://www.gov.uk/guidance/extended-producer-responsibility-for-packaging-recycling-obligations-and-waste-disposal-fees)
- [National Packaging Waste Database - Environment Agency](https://npwd.environment-agency.gov.uk/Public/PackagingHome.aspx)
 
 
#### Data flow and interaction
- Producers register and submit packaging data via the RPD front end.
- Data is validated and stored in the central Azure-hosted system.
- Regulators access this data through their dedicated front end to monitor compliance.
- PRNs/PERNs are fetched by RE/EX API and accepted/rejected by direct registrants (producers) and compliance schemes through the PRN front end.
- Notifications and reports are sent via Gov.Notify email.
- Power BI dashboards provide insights for regulators.
- External services like Companies House are used to verify identities and legal status.



## 3.2 Solution landscape – business to information system
*Rich picture/diagram, narrated, that illustrates the aspects of the business model that the solution supports/enhances/changes. In ArchiMate is the application usage viewpoint.*

This diagram focues on RPD and PayCal from an application viewpoint (technology elements obscured).

<br>

![Figure 4.0 RPD and PayCal applications](./epr-sadd-images/01/figure-4.0-rpd-and-paycal-applications.png)
Figure 4.0 RPD and PayCal applications - [original illo file](./illos)

<br>

The diagram outlines the workflow and system interactions between key stakeholders in the RPD and PayCal process, including producers, regulators, compliance schemes and the scheme administrator. It also shows how the various front-end systems support these business interactions.

**Key entities and their interactions**

**Producer**
- **Check obligation:** Anonymously. If obligated, then:
- **Enroll organisation:** Initiates registration via the RPD front end.
- **Upload submission data:** Periodically submits registration and packaging data through the RPD front end, which also connects to the regulator front end.
- **Compliance scheme:** Producer works with a specialist third party that aggregates obligations.
- **Regulator:** Verifies submitted data and interacts for compliance and fee payment.

**Compliance scheme**
- Interfaces with both the producer and the Financial Services Supplier (FSS) and accepts or rejects the Packaging Recovery Note / Packaging Export Recovery Note (PRN/PERN) on their behalf.

**Regulator**
- **Approve/reject submission:** Reviews data via the regulator front end and visualises outcomes as data via Power BI.
- **Pay fee:** Manages payments by producer through the payment front end.
- **Upload submission data:** Receives data submitted by producer.

**Front-end systems**
- **RPD front end:** Used by producers to enrol and submit data.
- **Regulator front end:** Used by regulators to review and manage submissions.
- **Power BI:** Used for data visualisation (e.g. graphs) and decision support.
- **Payment front end:** Handles fee transactions.
- **PRN front end:** Supports the acceptance/rejection by producer from within RPD of PRNs interfaced from RE/EX (outside RPD) where they were created.

## 3.3 Solution landscape – information system to technology
*Rich picture/diagram, narrated, that illustrates the technology services used and how they support the information system view. In ArchiMate is the technology usage viewpoint.*

This diagram focuses on RPD and PayCal from a technology viewpoint (application elements obscured).

<br>

![Figure 4.1 RPD and PayCal technology](./epr-sadd-images/01/figure-4.1-rpd-and-paycal-technology.png)
Figure 4.1 RPD and PayCal technology - [original illo file](./illos)

<br>

The information system (blue boxes in the diagram) is supported by the technology (green boxes), like this:

- RPD front end for producers and compliance schemes is supported by the **Accounts database** during enrolment.
- The **Anti-virus** service verifies submissions that, if successful, then go on to the **BLOb storage**. Metadata in those submission files changes their status from uploaded, to submitted, to approved/rejected etc and is also recorded on the **Cosmos NoSQL** database.
- Fee payables and payments are captured in the **Fee Payments** database.
- Finally, the RPD front end gives the window to direct registrant producers and compliance schemes to receive and accept or reject PRNs/PERNs via the **PRN database**. 

- **Regulator front end** is also supported by the **Accounts database**, where regulators approve or reject a producer enrolment. Again, it is supported by **Cosmos NoSQL** database for status updates made on submissions of producers. Finally, the **Synapse data warehouse** approves or rejects producer submissions.
- **Reporting front end** is again supported by **Synapse** for data analytics purposes.
- **PayCal** is supported by its own database technology service.

<br>

# 4. Change impacts

## 4.1 Non-system IT service impacts
*Should also identify key requirements for IT process changes (e.g. service/support impacts), to allow service design/transition planning.*

Non-system IT service impacts to EPR are changes that affect the supporting IT services and operational processes, rather than the core system functionalities. These include:
- Service desk operations and escalation paths
- Environment provisioning and migration
- Data platform integration with third-party services
- Release management and sprint planning
- Stakeholder communication and governance

### Key requirements for IT process changes

#### 4.1.1. Environment readiness and migration
EPR environment readiness includes:
- A tracker for each dev environment (e.g. PRN, PayPal) with a goal of achieving “dark green” status, indicating full service readiness.
- A standardised environment migration tracker reviewed every two sprints.
- Non-functional testing (e.g. accessibility) and automated regression testing to ensure stability.

These elements are critical for service transition planning, ensuring that environments are production-ready and support teams are aligned with deployment timelines.

#### 4.1.2. Release planning and support implications
The EPR Release Plan provides a granular view of upcoming releases and their associated capabilities. It highlights:
- Persona-based capabilities (e.g. producer, PackUK) that will be impacted by new features.
- Support implications such as billing file generation, invoicing and customer support integration with FSS.
- Dependencies on external systems like PayCal and the need for clear rejection handling and support escalation

This release cadence demands proactive service desk training, updated knowledge bases and revised SLAs.

#### 4.1.3. Data platform integration and event-driven architecture
As the EPR data platform has feeds from a rangew of parties including the FSS, local authorities and Defra, there's a shift to a multi-supplier model and the need for:
- Event-based data ingestion using Azure Event Grid, Event Hub, or ServiceBus.
- Real-time integration with SaaS platforms like ServiceNow (FSS) and CDP-hosted services (LAPS, RE/EX).
- Storage and access control strategies for raw data from third-party systems.

This architectural evolution requires changes to data governance, monitoring and support processes.

#### 4.1.4. Non-functional requirements (NFRs)
The Non Functional Requirements contains detailed specifications for performance, availability, and supportability.

## 4.2 Application changes
*Application components including integration aspects: New, Amend, Reuse, Replace, Remove together with Notes, Warnings and Guidance.*

This section outlines the application components and integration aspects impacted by the EPR programme with warnings and guidance to support service design and transition planning.

| Component | Impact | Notes | Warnings | Guidance |
| :--- | :--- | :--- | :--- | :--- |
| **Producer registration portal** | New | A new digital platform for producers to register and submit compliance data. | Ensure data security and GDPR compliance. | Provide user-friendly interfaces and multilingual support. |
| **Packaging data submission system** | Amend | Updated to capture more granular data on packaging types, weights and recyclability. | Risk of non-compliance if data is incomplete or inaccurate. | Offer clear data templates and validation tools. |
| **Waste management reporting interface** | Reuse | Existing interface reused for reporting collection and recycling data. | May require updates to align with new EPR categories. | Ensure consistent data formats across systems. |
| **Legacy compliance database** | Replace | Replaced by a centralised EPR compliance system. | Data migration risks and potential loss of historical records. | Archive legacy data and ensure audit trails are preserved. |
| **Fee calculation engine** | New | Introduced to automate eco-modulated fee calculations based on recyclability and material impact. | Complex fee structures may lead to miscalculations. | Regularly update algorithms in line with regulatory changes. |
| **Producer responsibility organisation (PRO) integration APIs** | New | APIs to enable data exchange between producers and PROs. | Inconsistent API standards may hinder interoperability. | Adopt open standards and provide sandbox environments for testing. |
| **Consumer education portal** | Amend | Enhanced to include EPR-related content and producer obligations. | Outdated or unclear information may mislead users. | Regularly review content and include feedback mechanisms. |
| **Data analytics and compliance dashboard** | New | Provides real-time insights into producer compliance and material flows. | Risk of misinterpretation without proper training. | Include training modules and contextual help within the dashboard. |
| **Manual submission channels (e.g. email, spreadsheets)** | Remove | Phased out in favour of automated digital submissions. | Resistance from smaller producers or those with limited digital access. | Provide transitional support and training for affected users. |


## 4.3 Data changes
*Data store or flow impacts including database, file, streaming: New, Amend, Reuse, Replace, Remove together with Notes, Warnings and Guidance.*

This section outlines the impacts on data stores and flows – including databases, files, and streaming pipelines – within the EPR programme, with warnings and guidance to support service design and transition planning. 

| Component | Impact | Notes | Warnings | Guidance |
| ------ | ------ | ------ | ------ | ------ |
| **Analytics (Azure Synapse)** | Amend | Ongoing improvements to address high-priority issues. | Current reliability concerns; requires front-door approval for changes. | Prioritise short-term fixes while planning long-term architectural refactoring. |
| **EPR test data framework** | New | Introduced to validate end-to-end scenarios across environments (e.g. tst1, dev8, pre1). Tracks step-level outcomes for registration, POM and compliance | High failure rates in early test runs; environment readiness is inconsistent. | Use structured test data to validate integration and regression scenarios before release. |
| **Billing file generation (PayCal)** | New | Enables generation, download and submission of billing files with accept/reject logic. Integrated with FSS for invoicing and customer support | Rejection handling must be robust to avoid billing delays. | Ensure clear mapping between producer data and billing logic. Validate with FSS before go-live. |
| **Modulation audit data** | Amend | Enhanced to support RAM rating breakdowns and fee modulation in PoM reports. | Data accuracy is critical for compliance reporting. | Align modulation logic with regulatory guidance and ensure auditability. |
| **Producer public register** | New | Allows public access to producer registration data | Must comply with data protection and publication standards. | Implement access controls and audit logging for public queries. |
| **Legacy CSV imports** | Reuse | Still used for some third-party data ingestion (e.g. LAPS, PRN) | Risk of inconsistent formatting and schema drift. | Transition to structured APIs or event-based ingestion where possible. |

## 4.4 Technology changes
*Technology service/platform impacts meaning moth physical assets as well as cloud, and noting that a technology service include PaaS, Networking, Encryption, Malware etc.: New, Amend, Reuse, Replace, Remove together with Notes, Warnings and Guidance.*

This section outlines the technology service and platform impacts across both physical and cloud assets. It includes platform-as-a-service (PaaS), networking, encryption, malware protection and other infrastructure components, with warnings and guidance to support service design and transition planning.

| Service | Impact | Notes | Warnings | Guidance |
| ------ | ------ | ------ | ------ | ------ |
| **Azure PaaS (Event Grid, Service Bus, Event Hub)** | New | Introduced to support event-driven architecture for multi-supplier integration (FSS, LAPS, PRN). Enables real-time data ingestion and decoupled service orchestration. | Requires robust monitoring and retry logic to handle transient failures. | Ensure all services are registered with appropriate topics and subscriptions. Use managed identities for secure access. |
| **Networking (hybrid connectivity)** | Amend | Existing VPN and Azure ExpressRoute configurations extended to support new cloud-hosted services and third-party SaaS platforms. | Latency and throughput must be validated for new endpoints. | Update network diagrams and firewall rules. Conduct performance testing post-deployment. |
| **Encryption (data at rest and in transit)** | Reuse | Existing Azure Key Vault and TLS configurations reused across new services. | Key rotation policies must be enforced. | Validate encryption compliance against Defra security standards. Document key usage and access controls. |
| **Malware protection (endpoint and cloud)** | Replace | Legacy endpoint protection replaced with Microsoft Defender for Cloud and Defender for Endpoint across all environments. | Ensure Defender policies are correctly scoped to avoid false positives. | Integrate alerts with SIEM and SOC workflows. Conduct regular threat modelling. |
| **Monitoring and logging (Azure Monitor, log analytics)** | New | Implemented to support observability across distributed services. | High ingestion volumes may incur cost spikes. | Use diagnostic settings to filter logs. Set up alerts for key metrics and anomalies. |

<br>

# 5. Information system view – apps
*Contains comprehensive description of the “non infrastructural” aspects of the system – data and application. Should relate the application services to the business context.*

## 5.1 System context
*More formal system view showing the system as a “black box” exposing interfaces and services, its external actors (other systems, teams, organisations) and showing the purpose of the relationship to the actors. Forms the basis of external dependency management so should not be artificially limited to 1st level removed actors. Should consider ALL information exchanges/flows not just system to system ones.*

<br>

![Figure 5.0 System context](./epr-sadd-images/01/figure-5.0-system-context.png)
Figure 5.0 System context

<br>

This system context diagram illustrates the data flow from source. The beige-coloured area is RPD, surrounded by external human and system actors. This is how RPD interacts with its external actors.

### Human users
People access RPD through the EPR web front-end:

- **Producers** check whether they are legally obligated to register (based on turnover and tonnage),
  then enrol, register periodically, and submit packaging tonnage data (Packaging on Market / PoM
  files). Once approved, they pay the relevant fees. A Compliance Scheme (CS) may act on behalf of
  one or more producers.
- **Regulators** review, approve, or reject producer and CS submissions, and view data reports.
- **Defra Core users** access England-specific RPD data for policy purposes.
- **The general public** can download the public list of producers via the web front-end.
- **Scheme Administrators (PackUK) and Financial Service Supplier (FSS) staff** are authenticated
  through the web front-end and then directed to the FSS application. Producers are similarly
  redirected to FSS to pay fees against their invoices.

### System integrations
System integrations use APIs or other interfaces:

- **Companies House** and **Postcode validation** services verify company and address details at
  enrolment, accessed securely via Azure API Management (APIM).
- **FSS (ServiceNow SaaS)** receives producer master data daily and invoice files periodically from
  RPD, sent via APIM.
- **LAP CAP** (another Defra application) supplies RPD's PayCal with local authority collection and
  disposal cost rates.
- **NPWD** (legacy) and **RE/EX** (its replacement) both receive daily producer registration
  data from RPD, and send back Packaging Recovery Notes (PRNs/PERNs) addressed to producers.
  Producers accept or reject these, and RPD sends the outcome back to both systems.


## 5.2 Application architecture – external cooperation view
(Conversation /Collaboration) Develops the system context view to describe processing flow triggers/sequence/responses – only normally focusses on the system-to-system flows. HOWEVER, if a system-to-system flow is handled manually/semi-manually via a human actor (“swivel chair ware”) then this should be shown. ArchiMate application cooperation view could be used – but use line numbering/naming scheme to show order/sequence. Should this be complex then a forward reference to the Integration Architecture should be provided where one or more sequence diagrams maybe used, and a sketch/overview provided here.

Using the same diagram from the previous section, here is how RPD and its external systems work together to deliver the EPR journey:

1. A potential producer checks with RPD to find out whether they have a legal obligation to report. If they don’t, their journey ends here.
2. If they are obligated, they register with RPD as either a small or large producer. They can also indicate if they belong to a compliance scheme (CS) that will manage reporting on their behalf.
3. During registration, RPD checks their address using the Postcodes service.
4. If the producer is a company, RPD also verifies their company details with Companies House.
5. Both of these external checks are made securely through the Azure API Manager (APIM).
6. A regulator reviews the registration in RPD and either approves or rejects it.
7. The producer is notified of the outcome by email via GOV.UK Notify. If rejected, the regulator provides reasons and the producer can try again.
8. Once approved, a user account is created in Azure AD B2C so the producer can log in to RPD going forward.
9. The producer (or their CS) submits a Company Details File (CSV) to RPD. The file is held in Blob Storage and its details are recorded in the Cosmos DB database.
10. The regulator uses RPD to tell the producer or CS what registration fee they owe.
11. The producer or CS pays the fee through GOV.UK Pay, accessed via the RPD Fees and Payments database.
12. The regulator reviews and approves or rejects the registration in RPD.
13. The producer is notified of the outcome by email. If rejected, reasons are given and they can resubmit.
14. A public list of registered producers is updated daily and available to download as a CSV file by anyone accessing RPD without logging in.
15. A daily extract of producer registration data is sent from RPD to both the legacy NPWD system and its replacement, RE/EX.
16. A separate daily extract of producer registration data is sent from RPD to the FSS system via APIM.
17. The producer (or their CS) submits a Packaging Details File (PoM CSV) to RPD. As with the company details file, it is stored in Blob Storage with metadata recorded in Cosmos DB.
18. The regulator uses RPD to tell the producer or CS what fee is owed for their packaging submission.
19. The producer or CS pays this fee through GOV.UK Pay.
20. The regulator reviews and approves or rejects the packaging submission.
21. Regulators can also view reports within RPD.
22. The producer is notified of the outcome by email. If rejected, reasons are given and they can resubmit.
23. The PayCal database periodically receives waste collection and disposal cost data from local authorities (via LAPCAP), broken down by nation and packaging material type. These are used as inputs to the fee calculation.
24. The PRN database receives Packaging Recovery Notes (PRNs) or Packaging Export Recovery Notes (PERNs) from NPWD (or RE/EX for 2026 onwards), addressed to specific producers or compliance schemes.
25. The producer or CS accepts or rejects each PRN/PERN in RPD, and the decision is sent back to NPWD or RE/EX.
26. Accepted PRNs/PERNs reduce the producer’s reported packaging tonnage, lowering their fee liability.
27. PayCal applies the relevant cost rates to the producer’s adjusted tonnage to calculate what they owe. The resulting billing file is sent periodically via APIM to the FSS system (ServiceNow).
28. Producers making a payment against their invoice are redirected from AD B2C to the FSS system to complete payment.
29. FSS call centre staff and PackUK scheme administrator staff are also directed to the FSS system after logging in through AD B2C.

This completes the RPD journey within EPR.

## 5.3 Application architecture – internal structure view
*Opens up the “black box” from the system context to describe the internal architecture of the system and internal model/patterns utilised.  Subsystems, and subcomponents should be shown and component dependencies captured. Identifies in principle those things for which a low-level design or build document should also exist and for which an “assembly” is required either at run time or before.  It is important that this model differentiates “owned” functional components that map to functions of this system, from those that map to functions of other systems (use those other systems).  Options to visualise this could be C4 Model L3, or ArchiMate Component Model. Annotate line with useful labels to make sure the reason for the structural relationship is evident.*

The internal structure of the pEPR application is straightforward. It provides a shared platform for hosting web portals, each backed by APIs that handle data exchange with four backend data services: Azure Blob Storage, Azure SQL Server, Cosmos DB, and Redis cache. Each portal follows the same three-tier architecture pattern. Data from the backend services is periodically extracted into Azure Synapse, which powers the reporting dashboards. This consistent pattern is reused across all parts of the RPD system.

<br>

![Figure 6.0 Internal structure PEPR](./epr-sadd-images/01/figure-6.0-internal-structure-pepr.png)
Figure 6.0 Internal structure PEPR

<br>

Payments

## 5.4 Application architecture – internal behavioural view
Illustrates the different triggers for system activity and any chaining/fundamental logic that is required (e.g. if a user creates an account, this triggers x and y, then if successful z). Ideally is a view for each use case variant/scenario/event type – of the journey a request takes through the components of the system, and allows an understanding of how a systems components co-operate to deliver a service, process a request etc. C4 Model L4 diagram or UML sequence may be appropriate for this (or potential BPMN using system service tasks as this conveys timing and events also).

### Context diagram
This diagram shows a high-level view of the EPR system together with the associated EPR reporting system, along with the relevant actors and dependant external systems.

<br>

![Figure 7.0 Context diagram](./epr-sadd-images/01/figure-7.0-context-diagram.png)

Figure 7.0 Context diagram

<br>


### Container diagram

<br>

![Figure 8.0 Container diagram](./epr-sadd-images/01/figure-8.0-container-diagram.png)
Figure 8.0 Container diagram

<br>

PayCal is covered in ADR-100.

Two pipelines are configured in Synapse to retrieve POM data and organisational data from the Synapse analytical database. Subsequently, the data will be loaded into the PayCal database for further processing in the calculator run process.

<br>

![Figure 9.0 Synapse pipelines](./epr-sadd-images/01/figure-9.0-synapse-pipelines.png)
Figure 9.0 Synapse pipelines

<br>

## 5.5 Application architecture – state model
Identifies which software components (if any) require state to be managed/manage state (control the state of data objects being persisted or exchanged), which are idempotent, which control sequence/order, which co-operate as part of a transaction (potentially long running/paused), which are truly atomic/stateless/scalable, which are essentially “helpers” or facades. This could be identified don the internal behaviour view if space allows.

### Deployment diagram
The following diagram illustrates the RPD components as deployed to Azure

The two major areas of functionality that we currently have in RPD are the account management and registration/PoM data upload. The following diagrams provide a more detailed view of those areas:

<br>

![Figure 10.0 RPD Azure deployment](./epr-sadd-images/01/figure-10.0-rpd-azure-deployment.png)
Figure 10.0 RPD Azure deployment

<br>


### User authentication and management
User authentication and authorisation approach is summarised in ADR-039: Authentication and Authorization consolidation

<br>

![Figure 11.0 RPD user authentication](./epr-sadd-images/01/figure-11.0-rpd-user-authentication.png)
Figure 11.0 RPD user authentication

<br>

### File upload detail

<br>

![Figure 12.0 File upload detail](./epr-sadd-images/01/figure-12.0-file-upload-detail.png)
Figure 12.0 File upload detail

<br>

ADR-043: PoM file upload performance remediation. Primary change is the addition of a back end Redis cache to coordinate error rate tracking across validation functions. Redis cache in the back end is available for other use cases as required.

### 5.6 Component classification table
| Component | State Management | Idempotent | Sequence Control | Transactional | Atomic/Stateless | Helper/Facade | Notes |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| Submission Split Checker (Function App) | Stateless | ✅ | ❌ | ❌ | ✅ | ❌ | Processes POM data into logical units. Highly scalable |
| Producer Content Validator (Function App) | Stateless | ✅ | ✅ | ❌ | ✅ | ❌ | Validates producer data. Idempotent and parallelisable |
| RWD Web API Gateway | Stateless | ✅ | ✅ | ❌ | ✅ | ✅ | Acts as facade. Routes requests and enforces API contracts |
| RWD Submission Status API | Stateful | ✅ | ✅ (long-running) | ❌ | ❌ | ❌ | Maintains lifecycle state. Supports retries and rollback |
| RWD Obligation Checker | Stateful | ❌ | ✅ | ❌ | ❌ | ❌ | Evaluates obligations using historical data. Requires persistence |
| Public Register API | Stateless | ✅ | ❌ | ❌ | ✅ | ✅ | Read-only API. Highly scalable and cacheable |
| Account Change Microservice | Stateful | ❌ | ✅ | ❌ | ❌ | ❌ | Manages user and organisation updates |

## 5.7 Application architecture – cloud native design approach
Identifies the elements of the overall solution design, and the implementation of individual subcomponents, or the patterns of cooperation with other components of the System, which align to “cloud first” reliability principles in how they handle errors gracefully, scale predictably etc. (see also Software Architecture exception handling patterns).

All components of RPD and PayCal are hosted in the UK South Region of the DEFRA Azure estate. All container-based components (web apps and APIs) are deployed to a minimum of two availability zones. All persistent portal data services are configured to be geo-resilient with the primary region being UK South and the secondary region being UK West. All infrastructure components are provisioned using CCoE standard templates via Azure DevOps pipelines. This delivers a solution that is resilient to the loss of one availability zone with the container-based services being arbitrarily scalable horizontally.

Diagrams in Sections 5.5 and 5.4 above amply demonstrate the complete harnessing of the Microsoft Azure cloud at function and component level.



# 6. Information system view – data
Note that if true microservices are being used and these have private data objects, then these topics should form subheadings (or be explored) in the respective microservice “component” designs. However, the general patterns to adopt (and principles used to maintain data integrity) should still be described here.

## 6.1 Data architecture – overview
Explains the key information concepts being processed by the system; their information classification, what datasets will be managed or integrated to. Should also note any data being exchanged via memoranda of understanding with other departments.

The key information concepts processed by the system are the following:
- Producers start by accessing the obligation checker to verify as to whether they are obliged or not. Access is anonymous and no data persisted at this step.
- If obliged, they are then expected to enrol as a Producer with the EPR service.
- The information that they provide at the first instance includes Organisation details, Producer-Compliance Scheme relationships and their authorised EPR user details. This is stored in the Accounts DB.
- They then submit periodic Registration and Packaging files.
- Organisation details (Registration) is an update, whereas packaging details list the quantity and type of packaging placed on market.
- Related to their above submissions, a calculation is performed to determine their share of collection costs that a producer is liable for with overhead uplifts. This is sent to the financial services supplier (FSS).
- Adjacent to the system, FSS using their own system produce an invoice (notice of liability called NoL) and send to the Producer who must pay for the packaging waste that they create).
- Using funds collected from Producers, the EPR scheme administrator (SA) then reimburses local authorities (LA) for their disposal costs incurred. This completes the periodic cycle.

This is illustrated by the below system context data diagram (SCDD):

<br>

![Figure 13.0 System context data](./epr-sadd-images/01/figure-13.0-system-context-data.png)
Figure 13.0 System context data

<br>


### Information classification
EPR information could be classified as follows:

#### Secret information
- Authentication credentials are securely held in active directory business to customer (AD B2C).
- Once authenticated, AD B2C passes an authentication token to prove the user’s identity that is then used by applications to show only relevant data, e.g. Producer users see only their own records. Regulator users see records pertaining only to their own UK Nation.
- In the online payment journey, Producer users provide their organisation credit/debit card details to the GOV.PAY payment handler. No card details are held by EPR.

#### Confidential information
Personally identifiable information (PII)
- Company officer information during enrolment and registration contains personally identifiable information (PII) of name and contact details. The company officers are Approved users, Delegated users, Basic users and Admin users.
- Packaging recycling notes and packaging export recycling notes (PRN/PERN) as well as notice of liability (NoL) from the financial services supplier (FSS) system have company officer details.
- We have identified in the context of the logical data model (LDM) the PII entities and attributes within the entities and listed these on Confluence at: https://eaflood.atlassian.net/wiki/x/TgCUdQE
- Please note that this list done by a data architect is not as definitive as one done by a Defra data steward.
- Additionally the raw Registration submission files referred to above as well as the Company Details, User, Person, Organisation, Audit log tables at least in Synapse and the Accounts DB have PII data and need to be appropriately protected.

#### Commercially sensitive information
- Packaging information is commercially sensitive, because sales and market share could be derived from packaging waste.

#### Nation information
- All the above information is related to a single UK Nation. In the spirit of UK devolution, such information is only for that Nation’s regulator and not shared even with Defra. Only two parties can see all information as part of their duties. These are the scheme administrator (SA) and the FSS.

#### Internal information
- Most other information within pEPR would be classified as Internal.

#### Public information
- The public list of producers is available to all members of the UK public from the GOV.UK website.

### Datasets managed and integrated
- Enrolment information includes Organisation details, Producer-Compliance Scheme relationships and their authorised EPR user details. This is stored in the Accounts DB.
- Updates to organisation data (registration submission) including changes to company and/or trading names or address or company offer details. From a legal regulation perspective, registration superseded enrolment. Submitted by producers via file upload called organisation_details_table.csv stored on Azure BLOb.
- Periodic packaging submissions. Submitted by producers via CSV file upload stored on Azure BLOb. The last submission for a period supersedes earlier ones.
- Submission & events data and file metadata are created in the Cosmos No-SQL DB.

### Data stores and entities
As in Section 9.2.3 further down this document
- **Azure SQL RDBMS Database:** Stores structured data such as enrolment, payment, PayCal and package recycling note (PRN).
- **Azure Blob Storage:** Stores unstructured data like packaging documentation, images, and audit files, as well as structured data related to organisation registration and packaging submission files.
- **Azure Cosmos DB:** Manages globally distributed, schema-less data such as real-time submissions, file meta data or IoT packaging data.
- **Azure Redis Cache:** Provides fast access to frequently used data, improving performance.
- **Azure Synapse Analytics:** Enables large-scale data analysis, reporting, and integration with Power BI for dashboards that acts as the repository for enrolment, organisation registration, packaging data now and more in the future.

### Integration
The journey of data is sequentially integrated from the upstream front-end creation through the mid-stream data warehouse to reports as well as input to downstream systems
- The front-end information is brought into the Azure Synapse data warehouse via Apache Pyspark that is an implementation of the Azure Data Factory (ADF). Accounts DB tables retain the same names.
- Exceptions in naming are that Registration is called as Company Details and packaging is called PoM that is the acronym for placed on the market.
- At the first instance the tables are copied into what one may consider the bronze layer of the medallion data layer architecture pattern with the prefix of app, that is the truncation of front-end application where they originate.
- Then, they are presently again copied into the silver layer with the prefix of rpd, that is the acronym of report packaging data.
- Finally, they are transformed to user requests of regulator reports or downstream application input extracts with the prefix of dbo, that is the acronym of data base object.
- From the Azure Synapse data warehouse, the downstream integration is with:
  - National packaging waste database (NPWD) for exchange of PRN/PERN via the PRN database.
  - FSS system for sending billing data via PayCal.
  - Power BI to produce Regulator reports.
  - Via APIs for standard services including Companies House, postal address verifications and GOV.PAY for application fee payments.
  - Common Data API for data exchange with the RPD front ends.
- Departmental exchange and memoranda of understanding MoUs.
- This is captured via the business context data diagram (BCDD) in Section Data Architecture – data models.

### Data architecture concepts
#### Data storage
- Azure SQL RDBMS is used to capture immutable Producer enrolment data, PayCal billing outputs, Fee payment rates, and PRN/PERNs.
- Azure Synapse data warehouse is used for reporting to Regulators and for extracting input data to downstream applications PayCal, and Direct Registrant and Compliance Scheme data, even to NPWD.
- Cosmos No-SQL database to capture metadata and file data related to Producer submissions.
- Azure BLOb storage to hold submission files
- Redis cache for front-end interaction with users.

#### Data management
- Data governance, data quality, MDM, Data standards – consistent formats – e.g. ISO for Nation, text length, Data format etc.
- Metadata – Cosmos DB.
- Data integration – using REST APIs. Detailed in other sections. Within Azure, we use ADF as the technology solution.

## 6.2 Data architecture – integrity and quality view
The organisation must be able to trust the accuracy and validity of data. This section should explain how data quality, accuracy and trust is maintained by the system – but also explain how “fuzzy” data is accounted for – i.e data whose reliability may be low but nevertheless it must be processed. Should include any caveats or warnings relating to non-owned data from other systems.

The EPR system holds high quality data. We aim to build data quality from capture at source.
During enrolment, all UK addresses are checked with the postcodes system as well as all limited companies are checked with Companies House database. Person contact details are e-mail verified.
Organisation registration as well as packaging submission CSV templates have user guidelines to help populate and build in quality data. Where these could fail due to user error, there are high level validation rules, for example, packaging files are accepted only if the corresponding organisation file precedes it. There are Cosmos File Metadata, Submissions and Submissions Events tables that keep track of submissions so that pre-submission mentioned re-submissions are tracked. Validation rules are being improved and tightened up as a continuous improvement process.
Enrolments and submission contents are manually, and human judgementally verified by Regulators who accept or reject these inputs. Prior to which they also check that the necessary fees have been paid.
In turn when PRNs and PERNs from the national packaging waste database (NPWD) are presented by Defra to Producers and Compliance Schemes, they examine these documents and can accept or reject this obligation offset document.
Producer obligation calculation outputs from PayCal are checked for organisation existence as well as packaging data content accuracy by the scheme administrator (SA) on the one hand.
To counter on the other hand, SAs also manually verify collection cost figures from local authorities (LAs) for accuracy.
In the future, we expect that there are plans to introduce trend analysis of packaging tonnage and disposal cost figures to pick up anomalies for further investigation by the Regulators or the SA.
Only authorised persons can create, change, or even read data.

## 6.3 Data architecture – data models
Relevant data model(s) showing which elements are involved in the solution in question – but the solutions own internal data model – but also relevant subsets of other system data models. Should differentiate transactional data which is subject to regular change and forms the system of record, from relatively static configuration or reference data.

### Business context data diagram
The BCDD illustrates the organisational actors and illustrates the desired information flows between them, once EPR is in its target end state.
The appropriate level of data-sharing agreement is determined by the group(s) that an organisation falls into. This is one of the purposes of the BCDD. The further one is from Core Defra as in another environment agency, or another government department, or a private company, the more formal and explicit are the data sharing arrangements.
Details of the groups and the type of agreements between them are detailed in the lower part of the diagram in green.

<br>

![Figure 14.0 Group differences](./epr-sadd-images/01/figure-14.0-group-differences.png)
Figure 14.0 Group differences

<br>

The full model is available on SharePoint at Business Context Data Diagram - EPR.docx

### System context data diagram (SCDD)
This diagram shows the application components and application data components of the extended data responsibility for packaging (EPR) with the information flows between them. As necessary, the diagram also shows some external applications and actors to contextualise data flows.

<br>

![Figure 13.0 System context data](./epr-sadd-images/01/figure-13.0-system-context-data.png)
Figure 13.0 System context data

<br>

The full model is available for reference or study on SharePoint at this location System Context Data Diagram - EPR.docx

### Conceptual data model
A Conceptual Data Model (CDM) is a collection of diagrams displaying Conceptual Data Entities and their relationships followed by a description for each of the data entities used in the diagrams. The key purpose of a Conceptual Data Model is to depict the relationships between critical data entities within an enterprise. Conceptual data models are the most abstract data model, they are developed to address the concerns of key business stakeholders and should be used to communicate with them because of their simplicity.
The below diagram is one of the views of the CDM on Finance and Documentation. There are two more views, one on Party and the other on Packaging Waste.
The full model is available for reference or study on SharePoint at this location Conceptual Data Model - EPR.docx

<br>

![Figure 15.0 Conceptual data model](./epr-sadd-images/01/figure-15.0-conceptual-data-model.png)
Figure 15.0 Conceptual data model

<br>

### Logical data model
The Logical Data Model (LDM) acts as the bridge between the conceptual and physical data models. This is in the third normal form (3NF) that shows the entire data of EPR in the minimum number of tables. This is the ideal representation of data. Normally adopted in the silver layer of data architecture.
The EPR LDM is shown below. This diagram like the all the other models (except the SCDD) is crosscutting across all EPR.

<br>

![Figure 16.0 Logical data model](./epr-sadd-images/01/figure-16.0-logical-data-model.png)
Figure 16.0 Logical data model

<br>

Please open and enlarge the embedded diagram to view the detail.
The full model is available for study or reference at Logical Data Model - EPR.docx
We have identified in the context of the logical data model (LDM) the PII entities and attributes within the entities and listed these on Confluence at: https://eaflood.atlassian.net/wiki/x/TgCUdQE
Please note that this list done by a data architect is not as definitive as one done by a Defra data steward.

### Subject area model
A Subject Area Model consists of ‘Subject Area’ elements nested into various levels of abstraction. Each level of abstraction is aligned to the activities conducted by the Organisational Data Actors e.g. Defra Core, Rural Payment Agency, Environment Agency etc.
A Subject Area Model partitions the data landscape of an Organisational Data Actor into various groups of activity related data entities with a manageable scope that can be prioritised and tackled independently, but in a coordinated way.
Comparable to the CDM there are the subject areas of Packaging Waste, Party & Identity and Finance.

<br>

![Figure 17.0 Subject area model](./epr-sadd-images/01/figure-17.0-subject-area-model.png)
Figure 17.0 Subject area model

<br>

The full model is available for reference or study on SharePoint at this location Subject Area Model - EPR.docx

## 6.4 Data architecture – data model terminology / glossary
For each data entity/concept/key attributes, provided a consistent useable definition of the term – noting that a one-word term (e.g. Applicant) is ambiguous and a term should always consist of 2 or more words. Optimally, this term list would form the common language of all other views (Business, Application).

The below table gives the list of all the entities across EPR in the conceptual data model (CDM). The same entities are mapped across the other models too. Some observations:
- The subject area model (SAM) has in common with the CDM those entities that are to do with subject (things) of interest to EPR including Waste, Finance and their sub-entities.
- The business context data diagram (BCDD) deals with organisation actors and how they need to handle data with the appropriate agreements in place.
- The system context data diagram shows all the EPR systems and the handling of data within them and without.
- The above three models appear to complement each other as in topic, actor and system all of which are captured in the CDM.
- LDM (yet to be created-waiting the CDM approval just obtained unofficially on 20 June 2025) is expected to have all the CDM entities with more details.
- Definitions for all the entities are in section 6.5 Conceptual Data Entities of the CDM lined in Section 6.3 above.

| Entity | SAM | BCDD | SCDD | CDM | LDM |
| ------ | ------ | ------ | ------ | ------ | ------ |
| Account | X | | X | X | X |
| Activity | | | | X | X |
| Application | X | | X | X | X |
| Calendar Period | X | | | X | X |
| Certificate | | | X | X | X |
| Communication | | | X | X | X |
| Document | | | X | X | X |
| Email | | | X | X | X |
| EPR Document | | | X | X | X |
| EPR Enrolment Application | X | | X | X | X |
| EPR Financial Services Supplier | | X | | X | X |
| EPR Report | | | X | X | X |
| External Organisation | | X | | X | X |
| Finance | X | | X | X | X |
| Financial Transaction | X | | X | X | X |
| Invoice | X | | X | X | X |
| Local Authority | | X | | X | X |
| Message | | | X | X | X |
| Obligated Packaging Producer | | X | | X | X |
| Organisation | | X | | X | X |
| Packaging Export Recycling Note | | | X | X | X |
| Packaging Recycling Note | | | X | X | X |
| Packaging Waste | X | | | X | X |
| Packaging Waste Compliance Scheme | | | X | X | X |
| Party | | X | | X | X |
| Party In Role | | X | | X | X |
| Party Role | | X | | X | X |
| Payment | X | | X | X | X |
| Person | | | X | X | X |
| Physical Address | | | X | X | X |
| Placed on the Market Submission | | | X | X | X |
| Postal Address | | | X | X | X |
| Regulator | | X | | X | X |
| Request | | | X | X | X |
| Scheme Administrator | | X | | X | X |
| Service | | | X | X | X |
| Submission | X | | X | X | X |
| Territory | | X | | X | X |
| User | | | | X | X |
| Waste | X | | | X | X |
| Waste Business Registration | X | | X | X | X |
| Waste Exporter | | X | | X | X |
| Waste Reprocessor | | X | | X | X |

## 6.5 Data architecture – data dependency referential integrity view
A sub-form of data dictionary that identifies “binding” data attributes that form intersystem keys (eg a transaction id, or a customer reference, or a classification code) and attributes that are key to creating facts and dimensional views that would be required by any MI/analytics capabilities, as well as maintaining cross system data integrity.

Entity identifiers that are cross-system within EPR are the six-digit Reference Number that is the natural key for Organisation and Packaging Material that is the natural key for packaging. Other natural packaging keys are Packaging Type and Packaging Class. These are different packaging analysis dimensions.
Reference Number is used as the natural key in the periodic organisation registration submission.
Packaging also has the organisation Reference Number (Organisation Id). This is cross validated against the registration submission in reporting and in PayCal for data integrity purposes
A data dictionary is available and maintained on the content repository Confluence at Data Dictionary - Report Packaging Data (RPD) - Data Warehouse - Collections & Packaging Reforms - Confluence.
An abstracted version of the key relationships between tables is available within the logical data model (LDM) in Section Data Architecture – data models data models which marks the primary key as the Business Identifier attribute of an entity, and the elsewhere used same attribute in another entity as the Business Key n. Both attributes are connected by a relationship line with cardinality. Such representation is following the Defra data architecture framework (DAF) guidelines. The LDM is an appropriate candidate for creating a silver layer and transform this to a reporting dimensional data model also in the silver layer. The gold layer downstream will have aggregated metrics for specific applications needed by the customer.
In current RPD Data Platform architecture we do not have clearly defined dimensions and fact tables for Silver Layer, All entities in Silver Layer are logical objects(Views/nested views) created for a specific report or a use-case, these views significantly complex with redundant business transformations and always process entire source data with all the columns.

## 6.6 Data architecture – data stores
Identifies the characteristics required of data stores, their capacity and growth forecasts, including persistent stores and transit ones. Covers the qualities of service required of each data store (performance, durability) and any approaches to caching that may be required. Don’t forget “external data which occur naturally such as feeds from google analytics.

The pEPR system contains five data stores
- Azure Blob Storage
- SQL Server RDBMS
- Cosmos DB NoSQL
- Redis cache
- Azure Synapse (SQL Server)

### Characteristics
All data store types are secure and have data integrity. All persistent portal data services are configured to be geo-resilient with the primary region being UK South and the secondary region being UK West.
Azure BLOb is used to store registration and packaging files. This is inexpensive storage used to store files for a long time. This is cold storage. It may take some time to retrieve.
SQL RDBMS is used to capture data populated by users using the front-end screens. Being an RDBMS, the table enforces relationships giving referential integrity.
Cosmos DB is NoSQL which holds file meta data, submission event and submission data using key value pairs. It is highly flexible in its schema, highly scalable and highly available.
The Redis cache is transitory and non-persistent used primarily for user-session data.
Azure Synapse is the powerful data warehouse used for big data analytics. It has a SQL tabular structure, but no relationships between the tables. It is fed by Spark ETL and is also well integrated with Power BI for reporting.

### Capacity, growth and quality of service (QoS)
The information in the below table has been collected from the respective architects of each of the data stores.

| Data store name | Size (MB) | Annual growth (approx. %) | Acceptable unplanned downtime | Acceptable data loss in time | (if primary capture DB) |
| ------ | ------ | ------ | ------ | ------ | ------ |
| Accounts DB (RDBMS) | 258MB for PRD; Other environments 2.5GB | 15-20%pa. Growth expected due to MYC PRN Obligation updates, Public Register RE/EX and obligation logic. Availability and data integrity are critical as it feeds regulatory data/logic. | <=1 hour/month. | Zero data loss. | This is primary capture that cannot be re-run if lost. |
| PayCal DB RDBMS | 120 MB For PRD; Other environments 240 MB | Y1 - 50% onetime due to inclusion of small producers; Y2 onwards – less than 5%pa | May not be an issue because the system is not transactional. | May not be an issue because there is no primary data capture. | |
| Payments DB (RDBMS) | | | Could be critical because it is customer facing. | No data loss acceptable because of primary data capture of invoices and payments. | |
| PRN DB (RDBMS) | 33 MB for PRD; Other environments 100 MB | Y1 – 300% if RE/EX journey is implemented. Y2 onwards – less than 5%pa | Customer facing, but less critical. | Some data loss could be accommodated because we could refresh from NPWD and request re-entry by DR and CS. | |
| Redis cache | | | Could be critical because it is customer facing. | Some inconvenience, but customer could be requested to re-create the session. Transient DB. | |
| Cosmos NoSQL DB | | | Critical because it is recording events. | No data loss acceptable because of primary data capture. | |
| Azure Synapse Data warehouse | 225,000 MB For PRD; Other environments 450,000 MB. Ref: SN presentation. | Y1 - 100% due to inclusion of small producers. Y2 onwards – less than 5%pa | Possibly less critical. | May not be an issue because there is no primary data capture. | |
| Azure BLOb storage | 210,000 MB For PRD | Y1 - 100% due to inclusion of small producers. Y2 onwards – less than 5%pa | Could be critical because it is customer facing. | No data loss is acceptable, because of primary data capture. | |



## 6.7 Data architecture – data exchanges (flows)
Show from a data perspective, data objects being exchanged by the application (as differentiated from data sync which is done by the platform or human actors). Can be a reuse of the component collaboration diagram if this conveys enough information about what is being exchanged, when, in what form, using what method (file message etc).

Enrolment information is held in the Accounts DB.
Registration and Packaging file submissions are held in BLOb storage. Information about these and the statuses through all the way from Uploaded to Accepted are captured in the Cosmos DB.
There is an hourly Spark pipeline run that copies across the incremental transactions from the Accounts and Cosmos DBs and the submitted files from BLOb into the Azure Synapse data warehouse.
These objects are in the silver layer of Synapse (if one were to use the medallion structure).

### Datasets managed and integrated
Enrolment information includes Organisation details, Producer-Compliance Scheme relationships and their authorised EPR user details. This is stored in the Accounts DB.
Updates to organisation data (registration submission) including changes to company and/or trading names or address or company offer details. From a legal regulation perspective, registration superseded enrolment. Submitted by producers via file upload called organisation_details_table.csv stored on Azure BLOb.
Periodic packaging submissions. Submitted by producers via CSV file upload stored on Azure BLOb. The last submission for a period supersedes earlier ones.
Submission data and metadata are created in the Cosmos No-SQL DB.

### Integration
The journey of data is sequentially integrated from the upstream front-end creation through the mid-stream data warehouse to reports as well as input to downstream systems
The front-end information is brought into the Azure Synapse data warehouse via Apache Pyspark that is an implementation of the Azure Data Factory (ADF). Accounts DB tables retain the same names.
Exceptions are Registration is called as Company Details and packaging is called PoM that is the acronym for placed on the market.
At the first instance the tables are copied into what one may consider the bronze layer of the medallion data layer architecture pattern with the prefix of app, that is the truncation of front-end application where they originate.
Then, they are presently again copied into the silver layer with the prefix of rpd, that is the acronym of report packaging data.
Finally, they are transformed to user requests of regulator reports or downstream application input extracts with the prefix of dbo, that is the acronym of data base object.
From the Azure Synapse data warehouse, the downstream integration is with:
- National packaging waste database (NPWD) for exchange of PRN/PERN.
- FSS system for sending billing data (PayCal).
- Power BI to produce Regulator reports.
Details of integrations are given in the next level of detail in the dedicated next Section Integration Architecture – Integration Architecture.
The architecture decision records (ADRs) in Confluence also describe data exchanges https://eaflood.atlassian.net/wiki/x/sIAr8g
At a higher level the data flows are shown in the system context data diagram (SCDD) in Section Data Architecture – data models Data Models.
An exercise was done during H2 of 2025 to detail data flows and integrations. The findings of this exercise are in Defra SharePoint at DataFlowsandIntegrations.xlsx

<br>

![Figure 18.0 Data flows and integrations](./epr-sadd-images/01/figure-18.0-data-flows-and-integrations.png)
Figure 18.0 Data flows and integrations

<br>


## 6.8 Data architecture – synchronisation
Explains any requirements to maintain data “in sync” with other systems and allowed/desired latency. For example there may be a master “list of allowed values” that needs to be synchronised manually thru change control. At the other extreme there may be distributed data stores that need to be aligned automatically by the platform within seconds.

The following are the instances where data needs to be in sync across the EPR systems:
As we have seen the upstream of data capture in the Accounts DB RDBMS, Azure BLOb storage and Cosmos NoSQL DB on the one hand, and its transfer to the mid-stream Azure Synapse data warehouse takes up to one hour. This is dependent on the Spark pipeline running once an hour on a temporal trigger. This one-hour time lag is acceptable. This is delta data sync normally. The only exception to delta is during pre-release when there is a schema change, where there is a full refresh sync.
In the context of PRN Management, there is a delta data sync of direct registrant (DR) and compliance scheme (CS) master data from EPR to NPWD every day outside working hours. The DR and CS in turn trigger a daily transfer of newly created PRN/PERN from NPWD to EPR to specific DR or CS parties. After acceptance or rejection by that DR/CS, the PRN/PERN is synced at day’s end from EPR to their natural home in NPWD.

**ADR-137 Update (from 1 February 2026):** The same organisation-data sync and PRN/PERN exchange pattern now also applies to **RE/EX (RREPW)** on CDP for the 2026 compliance year. Three new timer-triggered Azure Functions handle: (1) daily DR/CS organisation data sync from EPR to RE/EX; (2) daily retrieval of newly-issued 2026 PRNs/PERNs from RE/EX into the RPD PRN DB; and (3) real-time return of accept/reject decisions from RPD to RE/EX. The existing NPWD sync runs continue in parallel for 2025-year PRNs/PERNs.

In the context of PayCal, upon a run event trigger, the latest Producer master data and current period Packaging data is extracted by PayCal from Azure Synapse. The payment calculation is made for all Producers validating against their synced master and this output as a billing file is sent to the financial services supplier (FSS) system SNow for them to create a notice of liability (NoL) on a Producer.
There is another daily after-hours delta run of organisation details from Synapse via PayCal to FSS. This is for the contact centre staff to be current on Producer details when they call them up with queries on their accounts.
Since recently there has come about another need to actively sync across systems. Subsidiaries are subject to mid-year changes whereby typically parent 1 sells subsidiary 1 to parent 2. Such movement is immediately recognised in the Accounts DB via the Organisation Relationships table. However, that relationship is can only be manually updated to the Producer master in the rpd.CompanyDetails.sql table within a few weeks as required by regulation for both parents to submit respective registration files. Failing this, only when they submit their half yearly return. There is a small data quality (DQ) risk that for downstream applications that transfer obligations or liability such as PRN obligation (based on packaging or PoM file), or PayCal invoice (based on the registration file), the latest Parent-Subsidiary relationship is unavailable.

## 6.9 Data architecture – data resilience and recovery
Explains how data is protected from loss whether by system failure or otherwise, and how data can be restored (and with what impacts) in the event of actual data loss.

As stated in section Localised Availability and Recoverability Features further down this document and at the time of writing (July 2025), the pEPR solution is only resilient to the failure of a single availability zone in the UK South region. No OAT has currently been conducted so empirical validation has not yet been proven. The current proposal for a DR strategy is to provision all the infrastructure components to the UK West region via Azure DevOps pipelines, similarly the containerised web apps and APIs will be provisioned to the UK West region via Azure DevOps pipelines. All persistent data stored will be restored from geo-resilient backups to the UK West Region, but this has not yet happened. The second availability zone in UK West is yet to be implemented.
The table in Section 6.6 above details the real organisational requirements to downtime (RTO) and data loss (RPO) for each of the data stores. The stringent ones are the Account DB, BLOb storage and Cosmos NoSQL for RPO because these are primary capture stores, and again for RTO the Account DB, Payment DB, BLOb storage, Cosmos No SQL and PRN DB because these are customer facing.

### RTO
From a data perspective as a Platform-as-a-service (PaaS), the Azure SQL Database service provides availability as an off-the-shelf feature with an industry-leading availability SLA of 99.99%. The Azure SQL RDBMS has an even higher SLA.

### RPO
Azure SQL RDBMS’ have always on availability groups (AOAG) that provide synchronous replication of the data layer that eliminates data loss of committed transactions due to unforeseen circumstances.
In addition to the above, all data stores described in Section 6.6 above as non-primary capture can have data restored from their upstream system via a re-run, e.g. full restore to Azure Synapse data warehouse etc.

## 6.10 Data architecture – retention, archival and disposal
Defines the business rules that have been (will be) implemented and connects to the mechanisms used to effect retention, archive and disposal.

### Retention
The UK statute of limitations requires most records to be held for 6 years. This is effectively 6 years + 1 years to have 6 full financial years’ worth of records at any point in time during the year.
Having said the above, we have a more stringent requirement in the PayCal area of 10+1 years’ retention due to the regulations. This translates to holding PayCal billing output, their input the Azure Synapse packaging and registration tables (rpd.CompanyDetails.sql and rpd.PoM.sql) and their respective primary capture files in BLOb, all of these for 10+1 years. Good work in this regard has been done by the PayCal architect documented at: ADR-100.B: Fees & Payment Calculator - Calculator Data Storage - Collections & Packaging Reforms - Confluence. Analysis : Fees & Payment Calculator - Calculator Data Storage - Collections & Packaging Reforms - Confluence

### Archival
Because EPR is still evolving and less than 3 years old (at the time of writing in July 2025), we have not yet implemented an archival solution. When that happens, there will be considerations of using Azure native archiving functionality like Azure Archive Storage, retrieval to online or offline etc. Please note that no decisions have been made on these aspects yet. The only decision made is that we will hold data for as long as legally required. It is possible that we may need to act sooner on archiving because of online datastore performance reasons. Too much data online results in slower performance. It is also likely that we will implement archival for PayCal first, then use that approach and roll out for other EPR data.

### Disposal
Finally, to conclude the information lifecycle, in line with good information management practice we will eventually have automation to safely destroy stored data that is older than the retention period to prevent this falling into wrong hands and being misused.

## 6.11 Data architecture – non-core (logging)
Log files form part of the data and operational architectures. They can often contain useful or sensitive data. Ensure any beneficial usage of e.g. PaaS log files or IAM logs is described here especially for things like audit logging or “accidental analytics”.

There are a few types of logs that RPD and PayCal has:
- There is the standard system log for RDBMS databases that records who altered records and when. Probably used for roll-back and roll-forward with reference to a clean moment in time to recover should there be any unfortunate DB accidents.
- In the Accounts DB there is another Audit Log table that records what, when, who and before & after was changed. This is a simple long table to store. Requires some programming effort to re-construct records as at an earlier moment should the need arise. This was used once in 2024 to report on acceptances of submissions by regulators.
- Cosmos logs via its Submission Events table the progress of registration or packaging file submissions through their various statuses.
- The below Confluence link used by regulators to carry out their data auditing: Power BI Reporting - Collections & Packaging Reforms - Confluence.
- More recently in July 2025 we are starting to introduce extension fields to RDBMS tables in the PRN DB to capture in table itself the changed record now marked latest with timestamp, superseding the earlier records also timestamped.

> **[v1.2 change — ADR-141]** ADR-141 (currently For Review) formalises how PRNs/PERNs and the waste balance are kept accurate and tamper-evident in the RE/EX service:
>
> **PRNs:** Once a PRN or PERN has been issued, the key details — the tonnage, the accreditation it was issued under, and the organisation it was issued to — cannot be changed. Only the status of the PRN can be updated as it moves through its lifecycle (from created through to accepted or cancelled). Every status change is saved as a new record in a history table, so there is always a full trail of what happened and when.
>
> **Waste balance:** Every time the waste balance changes, a new entry is added to a running transaction log. That log is never edited or deleted. Each entry records whether tonnes were added or removed, how many, who made the change, and what the balance was before and after. This gives a complete, auditable record of all movements.
>
> **How the balance works:** The waste balance tracks two figures: the total amount available, and the amount currently free to allocate. When a PRN is created, some tonnes are ring-fenced (reserved) against the free amount. When the PRN is actually issued, those tonnes are deducted from the total. If a PRN is cancelled at any point, the relevant amounts are restored. This two-figure approach means the system can hold tonnes in reserve for pending PRNs without permanently removing them until the PRN is confirmed.
>
> **Audit trail:** The transaction log is read-only within the system and is also sent to the CDP security audit service, consistent with how RE/EX handles other audit records.
>
> **Reconciliation:** A check between PRNs/PERNs recorded in RE/EX and those held in RPD will be introduced as part of implementing ADR-141.
>
> A more technically robust approach using cryptographic linking between records (hash chaining) was considered but set aside for now. It would only be revisited if there is a serious legal challenge to the records, or if regulators require a higher standard of proof.

## 6.12 Data architecture – mastership / ownership view
Shows in matrix form the role the application plays in relation to each entity. Identifies 3 typical modes: Master, Multi-master and Dependent. For multi-master and dependent, the other actors (systems, people) who have CRUD roles on the entity should be identified.

**Keys for table:**
- **Systems:** RPD, PayCal, PRN, Payments – fee; FSS – financial service; LAPS – payment to LA; LAPCAP – LA payment calculation; PRN/CDP
- **System role:** M – master; MM – multi master; D – dependent
- **Actors:** PR – producer; CS – compliance scheme; RE – reprocessor; EX – exporter; RG – regulator; LA – local authority; SA – scheme administrator
- **Operations:** C – create; R – read; U – update; D – delete

**Notes:**
The table below shows the entities, systems and actors.
The systems within the scope of this RPD SADD are the first four RPD, PayCal, PRN and Payment (fee) columns on the left.
The columns on the right are shown for completeness and to illustrate multi-master (MM) across the EPR systems, for example (financial) Account is there as master in the RPD Payment system for paying submission fees, as well as master in FSS for paying obligated packaging costs. Same entity mastered in different systems for different purposes.
References to PRN and RE, EX on the left columns is now greyed out because of a decision on 11 July 2025 to de-scope RE and EX registrations and accreditations from RPD.
The editable table is in the embedded MS-Excel sheet just below.
The tabular form presentation (non-editable) is on the next page.

## 6.13 Data architecture – business reporting / intelligence and analytics
Explains how the data (will) support ongoing business management and analytics i.e what Events/Facts are (will be) captured in the data layer, propagated to where, transformed how etc. Should itemise the key business facts (process events) recorded and the additional classification information that is recorded directly or may be derived to allow dimensions to be analysed (likely source from the existing DWH models – eg geography, product type, business policy/rule applied). These facts should by default be assumed to need to be fed to the enterprises DWH or Analytics “hub” and the dimensions may need to be aligned to these as part of the systems core data model. However, if a COTS solution is in use, explain how the COTS solutions own MI and that of the enterprise solution are used together (if this is the case). Include reference to any overviews of the DWH solution/pattern.

The initial ADRs for the Data Platform identified the Medallion Pattern as the basis for the data processing functions. This is a common pattern in modern data warehouses and is considered good practice. The Medallion Pattern defines a sequence of phases or domains, labelled bronze, silver and gold.

The Bronze Layer is a basic data ingestion and integration layer where all source data is initially collected. The Silver Layer implements data transformations such as filtering, cleansing, validation and augmentation (e.g. with reference data). The Gold Layer is the source for all data requests by client applications such as interfaces and reports, in this layer the data is commonly de-normalised and aggregated for query performance.

<br>

![Figure 19.0 Medallion pattern](./epr-sadd-images/01/figure-19.0-medallion-pattern.png)
Figure 19.0 Medallion pattern

<br>



Source code for above high-level architecture diagram:

### Raw layer
The Raw Layer serves as a permanent data repository for source data received.
This layer preserves all data from source files exactly as received, without modifications, overwrites, or deletions. It forms the foundation for all source data on the platform and allows for reprocessing and audit checks. Files within this location are immutable, meaning they cannot be changed or deleted once placed. This is achieved by partitioning received data into structured and incremental folders aligned with the order of receipt.
This layer acts as a historical record, crucially retaining data according to EPR data retention policies. Data from the source systems is ingested into Raw Layer using hourly micro batches.

**Gaps in Current Architecture:**
- Raw Layer is not fully implemented for all the source systems e.g. Fee Payments DB, it is implemented only for file uploads, Accounts DB and PRN DB as at December 2025.
- Partitioning strategy is not as per industry best practices, all the files are ingested into a single folder rather partitioning by /source/entity/yyyy/mm/dd/hh.
- Lack of data retention policies set at storage account level.

### Bronze layer
The Bronze Layer is the staging area for the Medallion Architecture, storing data in a relational format.
Data in this layer remains in its original form, maintaining the integrity of the source data. The Bronze Layer can also include logs and records from various sources. Data here is stored in optimised formats like Parquet.
This layer serves as a historical record and, more importantly, the source for further data processing stages. This layer contains limited history comparing to Raw Layer. Data from the Raw Layer/source systems is ingested into Bronze Layer in hourly batch jobs.

**Gaps in Current Architecture:**
- Bronze Layer does not keep history for any records, it always Upsert, if you want to rebuild dimensions and fact tables in Silver Layer historical data needs to be sourced from actual source systems.
- It requires rebuilding of entire table with full data when new metadata introduced in source system e.g. new columns or renaming columns.
- No schema evaluation.
- No DQ rules applied during data ingestion.

### Silver layer - refined and conformed data
The Silver Layer should contain conformed and cleansed data extracted from the Bronze Layer.
Data in this stage undergoes cleansing, transformation, enrichment, and deduplication. The Silver Layer is where the platform's fundamental data model is constructed ideally as the LDM described in section Data Architecture – data models, typically organised in dimensions and fact tables. Data in this layer is maintained at the lowest granularity to support various aggregations in the Gold Layer.
This layer provides the foundation for further analysis and can be referenced for more detailed queries and reports requiring custom joins.

**Gaps in Current Architecture:**
- Bronze Layer (Delta Live Tables) are replicated into separate Schema called “rpd” in Synapse Dedicated SQL Pool.
- Data cleansing, transformations are performed using complex nested views.
- Pipelines process the data in full (complete history) always as no CDC implemented in views.
- Most of the views under “dbo” schema considered as Silver Layer object however there is no clear distinction.
- ETL processes are implemented using T-SQL instead Spark SQL pool.

### Gold layer - Business-Aggregated data
The Gold Layer contains the enriched and business-level aggregates of data from the Silver Layer.
This layer features the most refined data, often structured in a way that directly supports decision-making and automated PowerBI reporting.
Data in the Gold Layer is ready for use in business analytics, ad-hoc reporting, and regular dashboards.
Data in this layer is processed using T-SQL/nested views and final curated data is stored in “dbo.t_*” tables and “apps” schemas.
Dbo.t_tables are used primarity by PwerBI reporting and “apps” schema is used by regulatory front-end and other consumers.

**Gaps in Current Architecture:**
- dbo.t_* tables are fully refreshed on an hourly basis, which is a resource-intensive and costly operation.
- We have implemented cache tables to improve front-end workloads as an interim solution. The long-term solution should include properly pre-curated tables in the Silver Layer with Change Data Capture (CDC) enabled, along with an event-based or streaming platform to support real-time use cases, such as regulatory front-end applications.

### Data analytics & reporting:
Power BI is the standard reporting and analytics tool used by regulators. The reports and dashboards are designed to provide insights from curated data in the Gold Layer, supporting business decision-making, regulatory compliance, and operational monitoring.
To provide a high-level view of how the architecture supports key reports and their source data, underlying datasets, and refresh mechanisms are summarised below.
For detailed documentation about PowerBI reporting please refer to Power BI Reporting - Collections & Packaging Reforms - Confluence.
For RPD Data Platform and PowerBI Report entity level mapping please refer to Synapse Tables and PowerBI Report Mapping - Collections & Packaging Reforms - Confluence, PowerBI consumes data from Gold Layer t_tables under “dbo” schema.
For PowerBI source table metadata please refer to Reporting Table Metadata - Collections & Packaging Reforms - Confluence.



# 7. Integration architecture
This section provides the high-level design explain how end to end system integrations are implemented – be they with other system actors or with human actors (i.e. must not exclude extracts taken off the system).

## 7.1 Interfaces overview
Develops the system context diagram to visualise the method, frequency and exchange pattern for each outward facing interface. Developed application usage view, or C4model can be used for this. Interface timings that are not “adhoc” (triggered on demand) should be identified as such – e.g. “polls every 10 minutes”.

### PRN interfaces
Reprocessors and exporters use NPWD to record packaging waste and issue PRNs/PERNs, which producers and compliance schemes rely on to meet recycling obligations. Since January 2025, PRNs and PERNs will continue to be issued via NPWD, their acceptance by producers and compliance schemes will occur exclusively through the RPD platform which will integrate assigned PRN/PERN data from NPWD, calculate producers’ obligations, and update balances upon acceptance of notes. Regulators will maintain visibility of PRN details throughout this process.

To ensure data can flow accurately from NPWD to RPD and vice versa will allow both systems to work in unison, so that updates to PRN records are accurate and timely. As a result, producers will be able to correctly manage their obligations and regulators will be able to achieve the necessary regulatory oversight. To deliver this, the integration work needs to ensure three main objectives are met:
- RPD can send data to NPWD
- RPD can retrieve data from NPWD
- Both systems can share producer / compliance scheme organisation details

**Component Diagram**

<br>

![Figure 20.0 Component diagram](./epr-sadd-images/01/figure-20.0-component-diagram.png)
Figure 20.0 Component diagram

<br>

Azure Function – Daily/Weekly Reconciliation Emails: This function is designed to automate reconciliation reporting between the PRN system and NPWD. It runs on a scheduled basis (daily or weekly) and generates email notifications that include a summary of PRNs received, processed, and sent back to NPWD. The email provides key metrics such as transaction counts, status updates, and any discrepancies identified during reconciliation. This ensures stakeholders have timely visibility into data exchange activities, supports compliance monitoring, and helps maintain data integrity across integrated systems.

### RE/EX integration from 1 February 2026 (ADR-137, implemented)

From 1 February 2026, all new PRNs and PERNs for the 2026 compliance year are issued via the **RE/EX (RREPW)** platform on CDP, not NPWD. NPWD remains operational only for PRNs/PERNs from the 2025 compliance year (issued up to 31 January 2026). This change was implemented in RPD Release 17 (15 January 2026) under ADR-137.

The RE/EX integration uses three new timer-triggered Azure Functions modelled on the existing NPWD-facing functions:

1. **Organisation Sync (RPD → RE/EX):** When a DR or CS is registered or updated in RPD, this function sends the organisation record to the RE/EX Organisation API (`POST /organisations`). Secured via CDP API Gateway (AWS Cognito, `client_credentials` grant). This is structurally equivalent to the existing NPWD organisation sync function.
2. **PRN/PERN Retrieval (RE/EX → RPD PRN DB):** A timed Azure Function calls the RE/EX PRN API to pull newly-issued 2026 PRNs/PERNs assigned to specific DRs or CSs and stores them in the RPD PRN DB, making them visible in the RPD portal for acceptance or rejection.
3. **Accept/Reject Status Return (RPD PRN DB → RE/EX):** After a DR or CS accepts or rejects a 2026 PRN/PERN in the RPD portal, this function sends the updated status back to RE/EX via the PRN API in real time, equivalent to the existing NPWD status-return function.

The three objectives for the NPWD integration (RPD can send data to NPWD; RPD can retrieve data from NPWD; both systems can share organisation details) apply equally to the RE/EX integration. Existing NPWD interfaces (processes 1–4 in the Interface Catalogue below) continue to operate in parallel for 2025-year obligations.

> **[v1.2 change — ADR-141]** ADR-141 (currently For Review) governs how PRN/PERN records and the waste balance within RE/EX are kept accurate and auditable. The key rules are that core PRN fields cannot be changed once a PRN is issued, every status change is saved in a history table, and every movement of the waste balance is written to an append-only transaction log. See section 6.11 for the full detail of this pattern.

### PayCal interfaces
The PayCal interfaces are:
- Input parameters from LAP CAP to PayCal that is collection & disposal cost per tonne per Packaging Material per Nation.
- Producer master data daily from RPD Synapse via PayCal to the FSS system.
- Periodic billing data from PayCal to the FSS system via APIM.

The calculator run is initiated by Scheme Administrator (SA) internal users from Defra, after which the PayCal calculator is executed using key inputs – latest RPD data, LAPCAP data, and scheme parameter configurations – to generate the required calculation outputs, triggering the Billing File Process Workflow to produce the billing file. Once the billing file becomes available, the FSS system invokes the billingDetails APIM endpoint, which forwards the request, including the mandatory calculatorRunId, to the billingDetail EPR Web API. The API retrieves the corresponding JSON billing data stored in Blob Storage and returns the response to FSS through APIM. FSS then acquires organisation details from RPD via APIM and, upon receiving both the billing information and the associated organisation data, completes the processing of producer invoices.

**High Level Overview:**

<br>

![Figure 21.0 High-level overview](./epr-sadd-images/01/figure-21.0-high-level-overview.png)
Figure 21.0 High-level overview

<br>

**Component Diagram**

<br>

![Figure 22.0 Component diagram](./epr-sadd-images/01/figure-22.0-component-diagram.png)
Figure 22.0 Component diagram

<br>

### FSS authentication
**RPD User Journey with Azure B2C SSO Overview**
The RPD user journey leverages Azure B2C for Single Sign-On (SSO). Once a user is authenticated, the system enables account creation and enrolment for the RPD service. To provide a seamless experience, the same Azure B2C SSO integration has been extended to the FSS platform. Currently, the supported account types include Direct Producers, Compliance Schema Users, Regulators, and FFS Users.

During the account creation and enrolment process, the system captures both user and organization details. The individual enrolling an organization becomes the Administrator. Administrators can then invite additional roles such as Approved, Delegate, and Read-Only users. All provided information is validated and securely stored in the SQL Accounts Database.

### Regulator enrolment
There is an internal process for creating regulator accounts using a SQL script. The detailed procedure is documented in the Defra Confluence at this URL Reference.

The integration architecture leverages Azure B2C Single Sign-On (SSO) as the central authentication layer for RPD, FSS, and regulator platforms, delivering a unified and secure login experience. RPD enables account creation and enrolment for producers, compliance users, and regulators, while FSS uses the same SSO for seamless cross-platform access. Regulator accounts are provisioned internally via SQL scripts documented in Defra Confluence. All systems implement robust security controls, including multi-factor authentication (MFA), conditional access, GDPR compliance, encrypted data storage, and comprehensive audit logging. The enrolment workflow covers authentication, detail capture, administrator assignment, role management with notifications via Gov.Notify, and secure storage in an SQL database with RBAC enforcement. Additionally, the system validates organization details through Companies House API and Postcode API to ensure data accuracy during enrolment.

**Component Diagram**
- RPD Users

<br>

![Figure 23.0 Component diagram - RPD users](./epr-sadd-images/01/figure-23.0-component-diagram-rpd-users.png)
Figure 23.0 Component diagram - RPD users

<br>

- FSS

<br>

![Figure 24.0 Component diagram - FSS](./epr-sadd-images/01/figure-24.0-component-diagram-fss.png)
Figure 24.0 Component diagram - FSS

<br>

- Regulator Enrolment

<br>

![Figure 25.0 Component diagram - regulator enrolment](./epr-sadd-images/01/figure-25.0-component-diagram-regulator-enrolment.png)
Figure 25.0 Component diagram - regulator enrolment

<br>


### PRN
CS and DP users authenticate via Azure SSO using a single set of credentials to access the RPD portal and view PRNs. All PRN-related data is extracted from POM files, processed, and stored in Synapse DB, while compliance data from NPWD is maintained in the PRN SQL Database. The system consolidates this information and retrieves it from the PRN Database to display on the frontend, ensuring accurate and seamless user access to obligations and reporting.

Once CS and DP users register with the RPD system, they will have the option to submit their registration details, upload the POM file, and manage their organization. On the PRD portal, users can manage their PRN by navigating to the PRN Obligation tab, where they can review and update their obligations.

**PRN - Accept or Reject Workflow**
**Organisation Data Sync (Separate Function)** A separate Azure Function sends organisation data to NPWD when a new organisation is registered or an existing one is updated. NPWD uses this to maintain a mapping between internal orgIds and NPWD orgIds (different format). This function is unchanged by PRN update changes.

**Data Sync** NPWD system provides PRN data via API. Azure Function (triggered by a Timer) pulls PRN data and stores it in PRN-DB.

**Customer Interaction** PRNs in PRN-DB are displayed to customers for review. Customers Accept or Reject PRNs based on recycling material.

**Update NPWD System** Accept/Reject decisions, along with the obligation year, are sent back to NPWD via API. NPWD reflects updated PRN status and obligation details.

**Obligation Calculation** Accept/Reject decisions do not directly update compliance obligations. Tonnage and expected values are calculated dynamically when the screen loads. Main obligation calculation data is retrieved from the database, pre-computed by separate functions.

**Component Diagram**

<br>

![Figure 26.0 Component diagram](./epr-sadd-images/01/figure-26.0-component-diagram.png)
Figure 26.0 Component diagram

<br>

The integration architecture defines how the PRD portal, Azure SSO, PRN SQL Database, NPWD, and POM files interact to enable seamless user registration, authentication, and PRN management for CS (Compliance Scheme) and DP (Direct Producer) users.

The objective is to provide secure, unified access to the RPD portal via Azure SSO and ensure accurate synchronization of PRN data from POM files and NPWD into the PRN SQL Database. Users register and submit POM files through the RPD portal, while the PRD portal enables CS and DP users to manage obligations. Data from POM files and NPWD is processed and stored in the PRN SQL Database for compliance reporting. Azure SSO ensures authentication and identity management across platforms. This integration delivers streamlined registration, data handling, and obligation management for compliance.

### Fees and payments:
The Fees & Payments service makes a call to the GOV.UK Pay payment handler service via the payment façade. Upon receiving a payment request, GOV.UK Pay creates a payment session and returns the Next URL to the front end. Payment status updates are then retrieved by the Fees & Payments service and written back to the Fees & Payments DB.

**Component Diagram**

<br>

![Figure 27.0 Component diagram](./epr-sadd-images/01/figure-27.0-component-diagram.png)
Figure 27.0 Component diagram

<br>


## 7.2 Interface catalogue
Names and tabulates each interface purpose verbally including its behaviour and any n-level-removed dependencies (to protect from unintended cascade of changes); also contains links to any specific schema documents (with a clearly stated example in the appendix if the schemas are not available online). Should correlate to the data architecture section (e.g. an attribute name should have the same meaning as a minimum) if used in the interface catalogue.

### External interfaces
**PRN DB and NPWD**
All transactions between the RPD PRN database and NPWD occur via APIs, as defined in the API contract below, covering full loads and delta updates for Direct Registrants and Compliance Schemes using the Upsert Producer functionality. The API interfaces manage PRN/PERN document exchanges, with NPWD sending newly created documents to RPD and RPD returning accepted or rejected statuses back to NPWD. Periodic reconciliation emails are triggered using the Gov.Notify and NuGet package by calling the SendEmail method, based on API-driven confirmations of PRN documents received or sent between the two systems.

The data contracts detail the schema of the data exchange. The Method name in the contract forms part of the process in the table below.

| Process | Direction | Frequency | Description |
| :--- | :--- | :--- | :--- |
| DR and CS full loads & delta updates (Upsert Producer) | RPD PRN DB → NPWD | Daily around midnight. | Handles Upsert Producer functionality for Direct Registrant and Compliance Scheme data. |
| Newly created PRN/PERN document interface (GET PRNs) | NPWD → RPD PRN DB | Daily around midnight. | Transfers newly created PRN/PERN documents from NPWD to RPD PRN database. |
| Accepted or rejected PRN/PERN document interface (PRN Update) | RPD PRN DB → NPWD | Returned in real time. | Sends status updates (accepted/rejected) for PRN/PERN documents back to NPWD. |
| Reconciliation Emails (PRN received/sent) | NPWD ↔ RPD PRN DB | Periodically. | Email notifications for reconciliation of PRN documents between NPWD and RPD PRN database. |

### PayCal
- PayCal Organisation Data ICD: This is the data contract file that got agreed with FSS to fetch the organisation details
- PayCal Billing File ICD: This is the data contract file that got agreed with FSS to fetch the Billing file details

### Internal interfaces
Detailed internal APIs within RPD & PayCal are detailed in the below table as well as recorded on SharePoint at EPR API Catalogue.xlsx.

| Interface ref | Generic API Name | API Endpoint Name | Description |
| :--- | :--- | :--- | :--- |
| | EPR LoggingMicroservice.API (epr-logging-api) | | Logging API |
| IF-001 | | /api/v{version}/log-events | LoggingEvent |
| | epr-facade-account-microservice (FacadeAccountCreation.API) | | Persists and retrieves user and organisation account information. This is a common service shared by all EPR workstreams. |
| IF-002 | | /api/producer-accounts | Accounts |
| IF-003 | | /api/producer-accounts/ApprovedUser | Accounts |
| IF-004 | | /api/accounts-management/invite-user | AccountsManagement |
| IF-005 | | /api/accounts-management/enrol-invited-user | AccountsManagement |
| IF-006 | | /api/address-lookup | Address Lookup |
| IF-007 | | /api/enrolments/{enrolmentId}/approved-person-acceptance | Approved Person Enrolments |
| IF-008 | | /api/companies-house | Companies House |
| IF-010 | | /api/compliance-schemes/{organisationId}/schemes/{complianceSchemeId}/scheme-members | Compliance Schemes |
| IF-011 | | /api/compliance-schemes | Compliance Schemes |
| IF-012 | | /api/compliance-schemes/get-for-operator | Compliance Schemes |
| IF-013 | | /api/compliance-schemes/get-for-producer | Compliance Schemes |
| IF-014 | | /api/compliance-schemes/{complianceSchemeId}/summary | Compliance Schemes/{Complianceschemeid}/Summary |
| IF-015 | | /api/compliance-schemes/member-removal-reasons | Compliance Schemes |
| IF-016 | | /api/compliance-schemes/remove | Compliance Schemes/Remove |
| IF-017 | | /api/compliance-schemes/select | Compliance Schemes/Select |
| IF-018 | | /api/compliance-schemes/update | Compliance Schemes/Update |
| IF-019 | | /api/compliance-schemes/{organisationId}/scheme-members/{selectedSchemeId} | Organisationid Compliance-Schemes/{Organisationid} |
| IF-020 | | /api/compliance-schemes/{organisationId}/scheme-members/{selectedSchemeId}/removed | Organisationid Compliance-Schemes/{Organisationid}/Scheme-Members |
| IF-021 | | /api/compliance-schemes/{organisationId}/schemes/{complianceSchemeId}/export-subsidiaries | Organisationid Compliance-Schemes/{Organisationid}/Schemes |
| IF-023 | | /api/connections/{connectionId}/person | Connections |
| IF-024 | | /api/connections/{connectionId}/roles | Connections |
| IF-025 | | /api/connections/{connectionId}/roles | Connections |
| IF-026 | | /api/connections/{connectionId}/delegated-person-nomination | Delegated Person Connections |
| IF-028 | | /api/enrolments/{enrolmentId}/delegated-person-acceptance | Delegated Person Enrolments |
| IF-029 | | /api/enrolments/{enrolmentId}/delegated-person-nominator | Delegated Person Enrolments |
| IF-031 | | /api/enrolments/{personExternalId} | Enrolments |
| IF-032 | | /api/enrolments/v1/{personExternalId} | Enrolments |
| IF-033 | | /api/notifications | Notifications |
| IF-034 | | /api/organisations/users | Organisations |
| IF-035 | | /api/organisations/all-users | Organisations |
| IF-036 | | /api/organisations/team-members | Organisations |
| IF-037 | | /api/organisations/organisation-nation | Organisations |
| IF-038 | | /api/organisations/regulator-nation | Organisations |
| IF-039 | | /api/organisations/organisation-name | Organisations |
| IF-040 | | /api/organisations/organisation-by-reference-number/{referenceNumber} | Organisations |
| IF-041 | | /api/organisations/organisation-by-company-house-number/{companyHouseNumber} | Organisations |
| IF-042 | | /api/organisations/create-and-add-subsidiary | Organisations |
| IF-043 | | /api/organisations/add-subsidiary | Organisations |
| IF-044 | | /api/organisations/terminate-subsidiary | Organisations |
| IF-045 | | /api/organisations/{organisationId}/organisationRelationships | Organisations |
| IF-046 | | /api/organisations/organisationRelationships | Organisations |
| IF-047 | | /api/organisations/organisationRelationshipsWithoutPaging | Organisations |
| IF-048 | | /api/organisations/{organisationId}/export-subsidiaries | Organisations |
| IF-049 | | /api/organisations/organisation/{id} | Organisations |
| IF-050 | | /api/persons/current | Persons |
| IF-051 | | /api/persons | Persons |
| IF-052 | | /api/persons/all-persons | Persons |
| IF-053 | | /api/persons/person-by-externalId | Persons |
| IF-054 | | /api/persons/person-by-invite-token | Persons |
| IF-055 | | /api/regulators/resubmission-notify | Regulator resubmission notify |
| IF-056 | | /api/roles | Roles |
| IF-057 | | /api/user-accounts | User Accounts |
| IF-058 | | /api/user-accounts | User-accounts (v1) |
| IF-059 | | /api/user-accounts/personal-details | User - personal details |
| | PR.RegulatorService.Facade.API | | |
| IF-060 | | PR.RegulatorService.Facade.API | get accreditation data for the given registration |
| IF-061 | | /api/v1/accreditations/{id}/samplingPlan | get sampling data for a given accreditation |
| IF-062 | | /api/v1/accreditations/{id}/paymentFees | Get accreditation fee details by registered material id |
| IF-063 | | /api/v1/accreditations/{id}/paymentFees | Mark a accreditation as duly made |
| IF-064 | | /api/v1/regulatorAccreditationTaskStatus | Updates a accreditation task status |
| IF-065 | | /api/v1/accreditations/offlinePayment | Saves a new offline payment |
| IF-066 | | /api/v1/accreditations/{id}/businessPlan | get business plan for a given accreditation |
| IF-067 | | /api/v1/accreditations/file-download | Downloads a file from Azure blob storage |
| IF-068 | | /api/regulators/accounts/govNotification | |
| IF-069 | | /api/downloads/file-download | File Download |
| IF-070 | | /api/accounts-management/invite-regulator-user | invite-regulator-user |
| IF-071 | | /api/accounts-management/enrol-invited-user | enrol-invited-user |
| IF-072 | | /api/accounts-management/invited-regulator-user | invited-regulator-user |
| | | organisation-registration-submission-decision | |
| | | /api/organisation-registration-fee-payment | |
| | | /api/organisation-packaging-data-resubmission-fee-payment | |
| | | /api/organisation-registration-submissions | |
| | | /api/organisation-registration-submission-details/{submissionId} | |
| | | /api/organisations/search-organisations | |
| | | backend-account-microservice | |
| | | epr-pom-api-submission-status | |
| | | epr-pom-api-web | |
| | | epr-common-data-api | |
| | | backend-account-microservice (validation api) | |
| | | epr-calculator-api (PayCal) | Producer team calls PayCal API to get the total fees that the producer needs to pay for their registration |
| | | epr-payment-frontend | |
| | | epr-payment-facade | |
| | | epr-payment-service | |
| | | /api/organisations/v1/child-organisation-external-ids?organisationId={organisationId}&complianceSchemeId={complianceSchemeId} | facade/backend endpoint that will return a list of GUIDs (ExternalIds) for logged in Organisation (DirectProducer or ComplianceScheme) |
| | | v1/prn/obligationcalculation/{year}/ | This call will return the obligation calculation for a material, for an organisation and for a passed year. We will pass the organisation GUID as a http header variable called “X-EPR-ORGANISATION“ |
| | | /api/regulator-organisation | This endpoint allows you to check if a regulator account exists. It will search organisations by type of Regulator and nation name. |
| | | /api/regulator-accounts/invite-user | This endpoint allows you to create a new enrollment for a regulator with an ‘Invited’ status. The Enrolment will include the creation of a PersonOrganisationConnection, Person, and User resources. |
| | | /api/accounts-management/invite-regulator-user | This endpoint allows you to create a new enrollment for a regulator with an ‘Invited’ status. The Enrolment will include the creation of a PersonOrganisationConnection, Person, and User resources. |
| | | /prn/prns | Fetch PRN records from NPWD system |
| | | /submissions/v1/pom/approved/{approvedAfterDateString} | This call will return all approved submission data after the given date. TBC: The request body will send in a list of periods as well. |
| | | /v1/prn/organisation/{organisationId}/calculate | This call will trigger a calculation for this submission of which the result will be stored. |
| | | v1/prn/{id} | It fetch the data related external PRN id/ this API will be also used for Download PRN flow. |
| | | v1/prn/organisation/ | Get all the PRN's issued to organisation, we would be fetching OrganisationID from header X-EPR-ORGANISATION |
| | | v1/prn/search/{page}/{search}/{filterBy}/{sortBy} | Get Count of PRN’s waiting for acceptance - we would be fetching OrganisationID from header X-EPR-ORGANISATION |
| | | v1/prn/status | Update PRN Status (Accept/Reject) single or multiple and get the updated obligation values.Post data in body in JSON array |
| | | v1/prn/updatesyncstatus | Update the table pEPR_NPWD_Sync after pushing data into NPWD |
| | | v1/prn/syncstatus | Get the details of the Sync data |
| | | v1/prn/obligation/{id} | Get POM data from Azure Synapse by OrganisationId unique reference(externalid) |
| | | v1/prn/events/{id} | Get approval events from Cosmos DB by OrganisationId |
| | | producer/registration-fee | This API is called by RPD when a producer registers to get their registration fees, including any payments that have been made, and the delta between the fee amount and the registration fees. This API is also called by the regulator service to get the producers fees, payments made, and the delta between the fee amount and the previous payments. |
| | | Compliance-scheme/registration-fee | This API is called by RPD when a compliance scheme registers to get their registration fees, including any payments that have been made, and the delta between the fee amount and the registration fees. This API is also called by the regulator service to get the compliance scheme fees, payments made, and the delta between the fee amount and the previous payments. |
| | | producer/resubmission-fee | This API is called by RPD when a producer resubmits POM data to get their resubmission fee, including any payments that have been made, and the delta between the fee amount and the resubmission fee. This API is also called by the regulator service to get the producers fees, payments made, and the delta between the fee amount and the previous payments. |
| | | compliance-scheme/resubmission-fee | This API is called by RPD when a compliance scheme resubmits POM data to get their resubmission fee, including any payments that have been made, and the delta between the fee amount and the resubmission fee. This API is also called by the regulator service to get the compliance scheme fees, payments made, and the delta between the fee amount and the previous payments. |
| | | /defaultparameters | This end point is to upload the scheme parameters |
| | | /defaultparameters/{parameterYear} | This end point is to get the scheme parameters by parameterYear |
| | | /lapcapData | This end point is to upload the Lapcap Data |
| | | /lapcapData/{parameterYear} | This end point is to get the Lapcap data by parameterYear |
| | | /v1/calculatorRun | This end point to run the calculator and return |
| | | /v1/calculatorRuns | This end point is to return the calculator runs for the given financial year |
| | | /v1/loadrpdData | This end point load data from staging RPD tables to calculator run RPD tables |
| | | /v1/loadresultData | This end point store the required data to result tables, generate result file and update the status to Unclassified. |
| | | /v1/downloadResultFile | Download CSV file for requested run id |
| | | /v1/organisations-details | API to retrieve organization contact details based on a date parameter. When the FSS client requests compressed content, it must send the Accept-Encoding header with the request. The EPR API provider will send the compressed content accordingly and include information in the Content-Encoding header on how the compressed response is encoded. Request Header: Accept-Encoding: gzip. Response Header: Content-Encoding: gzip |
| | | /v1/billingdetails | API to retrieve billing details based on a calculatorrunid parameter. When the FSS client requests compressed content, it must send the Accept-Encoding header with the request. The EPR API provider will send the compressed content accordingly and include information in the Content-Encoding header on how the compressed response is encoded. Request Header: Accept-Encoding: gzip. Response Header: Content-Encoding: gzip |

## 7.3 Orchestration view
If for example activity across multiple interfaces needs to be co-ordinated, explains how this happens, how order is maintained, correlation of responses etc. Also explains any long running processes that require state to be maintained (e.g. saving of draft applications) and how the paused system process is restarted. It is probable that a UML sequence diagram is best for this but only for interfaces where complex behaviour is evident.

This sub-section is about the correct sequence of running the interfaces.

As a pre-requisite to all the below, the data warehouse Azure Synapse from where RPD originating data is sourced is no more than 1 hour behind front end capture.

All the below sequences are manually spaced apart in time. There is no event-triggered automated scheduler of interfaces.

### PayCal
- Producer master data interface must run daily.
- Input parameters must first be received from LAP CAP to PayCal.
- Only then would it be correct to run PayCal and then transfer the billing data from PayCal to the FSS system.

### RPD PRN
- Firstly, the DR/CS update from RPD to NPWD runs daily.
- PRN/PERN created by Reprocessors/Exporters respectively run daily from NPWD to RPD. These are in the specific name of a direct registrant producer (DR) or a compliance scheme (CS).
- After the DR or CS accept/reject their assigned PRN/PERN, the return interface runs from RPD to NPWD carrying the accepted or rejected PRN/PERN.

## 7.4 Reliability / recovery view
Explains any “cross system” referential integrity approaches, in support of understanding approaches to recovery if there is a system-to-system dependency at the data tier. [Cannot assume every interface is RESTful/stateless, cannot assume system to system interfaces are all within DEFRA etc.] Explores options for recovery if systems need to be brought “back in sync”.

Both the external applications NWPD and FSS leverage REST-based APIs for data exchange with RPD and PayCal respectively. The two endpoints provided for FSS are simple fetch ‘GET’ calls from FSS to PayCal, in the event of any recovery or re-synchronisation, FSS may call either endpoint (for billing data or organisational data) at any time.

Notwithstanding the above, if a sequential running of interfaces is necessary, then the sequence sets in the previous sub-section could be used.

## 7.5 Service consumption view
Explains which “enterprise” common application services and technical services are consumed, and the “contract” their exposed services provide (e.g. anti-virus). Whilst these will be listed in the interface catalogue, a description and a reference to their design patterns should be covered here.

This section outlines the enterprise-level common application and technical services consumed by the solution, along with the contracts and design patterns that govern their use. These services are typically shared across multiple systems and are essential for ensuring consistency, security, and operational efficiency.

### Enterprise common services consumed
| Service Name | Description | Contract / SLA | Design Pattern Reference | Service usage |
| :--- | :--- | :--- | :--- | :--- |
| Authentication Service | Provides user identity verification via Azure Active Directory. | OAuth 2.0 / OpenID Connect; 99.9% availability SLA. | Identity Federation Pattern | RPD and PayCal, FSS |
| Anti-Virus Scanning | Scans uploaded files for malware using Microsoft Defender for Cloud. | Files scanned within 5 seconds; alerts on detection. | Security Gateway Pattern | Submission |
| Logging and Monitoring | Centralized logging via Azure Monitor and Log Analytics. | Logs retained for 90 days; real-time alerting. | Observability Pattern | RPD and PayCal |
| Email Notification Service | Sends transactional and alert emails using SendGrid or Microsoft Graph. | Delivery within 1 minute; retry on failure. | Event-Driven Notification Pattern | RPD and PayCal |
| API Gateway | Manages and secures access to backend APIs. | Rate limiting, authentication, and logging enforced. | API Gateway Pattern | RPD and PayCal |
| Data Encryption Service | Encrypts data at rest and in transit using Azure Key Vault. | AES-256 encryption; key rotation every 90 days. | Data Protection Pattern | RPD and PayCal |

### Technical services consumed
| Service Name | Description | Contract / SLA | Design Pattern Reference | Service usage |
| :--- | :--- | :--- | :--- | :--- |
| DNS Resolution | Resolves internal and external domain names. | 100% uptime via Azure DNS. | Infrastructure Service Pattern | User interface, External API |
| Time Synchronization | Ensures consistent system time across services. | NTP-based; drift < 1 second. | System Clock Synchronization Pattern | RPD and PayCal |
| Backup and Recovery | Provides automated backups and disaster recovery. | Daily backups; 30-day retention. | Backup and Restore Pattern | RPD and PayCal |
| APIM | some of the external interfaces as referred to in Section 7.1 above use the Azure API Management (APIM) service. | Standard with the only specific requirement being that the payload shall not be more than 30MB (uncompressed or compressed file) in the case of the two interfaces from PayCal to the FSS system. | | Enrolment, PayCal |



# 8. Software architecture
Whether contained in a solution design document or externally stored, the software components of the solution must be documented, dependencies understood, implementation approach captured etc. For a relatively simple system, this section could be merged into the apps architecture section.

## 8.1 Component “micro designs”
Unless the apps architecture is relatively simple, it is usually required to provide an internal view of how each component of the architecture is implemented, its dependencies, the data it “owns” and shares, how it can be configured, the patterns it implements, frameworks (to be) used, logging/monitoring hooks etc. This could be a readme, a class diagram etc. So long as it “answers the question”. In general, should be considered a “one page summary” for each software component – with the components themselves having been itemised in the application architecture structural view (in s/w arch the component is the artefact that is assembled to create the working system).

The RPD software architecture is essentially simple, following a 3-tier architecture with a frontend web tier, a facade layer and backing API services. The software components are hosted in either Azure web apps or Azure function apps. Although not specifically named, the same pattern is applicable to RPD PRN, Payments as well as PayCal.

<br>

![Figure 28.0 Component micro designs](./epr-sadd-images/01/figure-28.0-component-micro-designs.png)
Figure 28.0 Component micro designs

<br>


## 8.2 Exception handling view / pattern
Should describe how the components in the software architecture respond to unexpected events ranging from timeouts, to overload, to unexpected restart etc. This section allows an understanding of how “brittle” the software architecture is and how much the design can be considered fault tolerant. Concepts such as tiering timeout settings and synchronising retry approaches should be described.

Exception handling is a critical aspect of system reliability, especially in distributed and cloud-native environments.

### General strategy
The architecture adopts a fault-tolerant design that emphasizes automatic recovery, graceful degradation, and consistent retry logic. Web applications and serverless functions are configured to restart automatically on failure, leveraging platform-level features such as Azure App Service auto-healing and Azure Functions runtime resilience. These are the Azure native patterns consumed.

### Monitoring and alerting
All exceptions are logged centrally using Azure Monitor and Application Insights. Alerts are configured for critical failure patterns, enabling rapid response and root cause analysis.

## 8.3 Component Environment specific behaviours
Software components may have in their design the ability to behave differently in different scenarios – for example they may be “aware” that they are in production and thus implement different behaviours than if they were in a development environment.

The software components have corresponding configuration parameters to manage differences between environments. Environments are initially built using a standard template via IaC ARM/Bicep pipelines. Differences between environments, particularly system behaviour, is minimised so that pre-Prod environments behave ‘as live’ where possible. The key exception to this approach is the use of mock services in Development to minimise impact due to outage or update for external dependent services such as the Trade Antivirus API.

## 8.4 Component replacement or upgrade capability
Any specific issues with “swapping” out a component with a new version should be noted. For example, is there a need to disable something whilst this happens or is there an external dependency that means that component must not be changed without wider consultation or is this component dependent on vary specific underlying software versions.

The RPD and PayCal application components are provisioned as containers hosted in either Azure Web Apps or Azure Function Apps. This implementation of the microservices pattern allows for simple scaling and replacement/upgrade with a new component. The web portal layer is protected from changes to either APIs or backend data sources by the façade layer.

## 8.5 Component behaviour tuning / adjustment
Are there any facilities for the component(s) that allow their performance characteristics to be adjusted or the level of activity beyond which the component can issue “too busy” responses?

### Performance tuning capabilities
Most RPD and PayCal components in the architecture are designed with configurable parameters that allow for dynamic adjustment of their behaviour based on workload and performance requirements. These include:
- **Concurrency Limits:** Web applications and serverless functions (e.g., Azure Functions) support configuration of maximum concurrent executions. This helps prevent resource exhaustion and ensures predictable performance under load.
- **Throttling and Rate Limiting:** API endpoints are protected by rate limiting policies at the API Gateway level. These policies can be adjusted to control the number of requests per second per client, and issue HTTP 429 “Too Many Requests” responses when thresholds are exceeded.
- **Queue Depth Monitoring:** Background processing components (e.g., Azure Service Bus consumers) monitor queue depth and can scale out or delay processing based on backlog size.
- **Timeout Settings:** Timeout values are tiered across components to ensure that upstream services fail fast and downstream services have sufficient time to respond. These settings are adjustable to balance responsiveness and reliability.
- **Autoscaling Rules:** Components deployed in Azure App Service or Kubernetes can be configured with autoscaling rules based on CPU usage, memory consumption, or custom metrics. This allows the system to adapt to varying loads without manual intervention.

### “Too busy” response mechanisms
Components issue “too busy” responses under the following conditions:
- **API Gateway:** Returns HTTP 429 when rate limits are exceeded.
- **Azure Functions:** May return 503 if concurrency limits are reached and no additional instances can be provisioned.
- **Database Services:** May throttle requests if resource limits are approached, especially in shared or provisioned throughput models.

These mechanisms are designed to protect the system from overload and maintain service availability, while providing feedback to clients for retry logic.

## 8.6 Component specific “health warnings” / constraints
Are there any inherited or known “gotchas” with the component?

### Azure component constraints and health warnings

| Component | Constraint / Gotcha | Impact | Mitigation / Guidance |
| :--- | :--- | :--- | :--- |
| Azure Functions (Consumption Plan) | Cold start latency during idle periods | Increased response time for first request | Use Premium Plan or pre-warmed instances for latency-sensitive workloads |
| Azure App Service | Limited visibility into underlying infrastructure | Difficult to diagnose low-level performance issues | Use Application Insights and App Service Diagnostics for observability |
| Azure SQL Database | Throttling under high DTU or vCore usage | Query timeouts or degraded performance | Monitor with Query Performance Insight; scale up or optimize queries |
| Azure Cosmos DB | RU/s limits can cause 429 errors under load | Request throttling and potential data loss if not handled | Implement retry logic with exponential backoff; enable autoscale |
| Azure API Management | Policy complexity can degrade performance | Latency or unexpected behavior in API responses | Keep policies simple; test thoroughly in staging environments |
| Azure Service Bus | Lock duration may expire during long processing | Message loss or duplication | Use lock renewal or defer messages; monitor dead-letter queues |
| Azure Blob Storage | Eventual consistency for overwrite operations | Clients may read stale data | Use versioning or ETags for consistency control |
| Azure Key Vault | Throttling under high request volume | Secrets/certificates may be temporarily inaccessible | Cache secrets locally where appropriate; monitor usage limits |
| Azure Monitor / Application Insights | Sampling may omit telemetry under high load | Incomplete diagnostics or alerting gaps | Adjust sampling settings; use dedicated ingestion for critical paths |

### General RPD and PayCal considerations
- **Platform Quotas:** Azure enforces service-specific quotas (e.g., storage limits, concurrent executions). These must be reviewed during design and monitored in production.
- **Multi-Region Deployments:** Some services (e.g., Cosmos DB, Key Vault) have region-specific behaviours or replication delays.
- **Configuration Drift:** Manual changes can introduce inconsistencies. Use Infrastructure as Code (e.g., Bicep, ARM, Terraform) to enforce consistency.
- **Dependency Failures:** External APIs or services may introduce instability. Use circuit breakers, retries, and fallback logic.

## 8.7 Monitoring and logging hooks / facilities
How is the component instrumented? Is it just basic audit trail or is it signalling e.g. process state changes? Do logged events correlate? Where are these events flowing to? What happens if the logging itself fails?

### Instrumentation approach
All RPD and PayCal components are instrumented using Azure-native observability tooling to ensure consistent, scalable, and secure monitoring across the platform. Instrumentation is applied at both the platform layer (infrastructure, services) and the application layer (business logic, APIs, workflows).
- **Azure Monitor:** Captures metrics and logs from infrastructure and services.
- **Application Insights:** Provides deep telemetry for custom applications and APIs.
- **Log Analytics:** Centralizes log data for querying, correlation, and alerting.
- **Diagnostic Settings:** Enable forwarding of platform logs (e.g., Key Vault, App Gateway, SQL) to Log Analytics or Event Hubs.

### Types of telemetry captured
- **Audit Trails:** User actions, configuration changes, and access logs (e.g., via Microsoft Entra ID).
- **Process State Changes:** Workflow transitions, job status updates, and deployment events.
- **Performance Metrics:** CPU, memory, latency, throughput, and error rates.
- **Custom Events:** Business-specific checkpoints and telemetry emitted by EPR services.
- **Exceptions and Failures:** Captured with full stack traces and contextual metadata.

### Event correlation
- Correlation IDs are propagated across services and APIs to enable end-to-end tracing.
- Distributed tracing is implemented using Application Insights to link user actions to backend processes.
- Log enrichment ensures that telemetry includes contextual metadata (e.g., tenant ID, environment, module name).

### Telemetry flow
- Application telemetry is sent to Application Insights.
- Platform logs and metrics are routed to Log Analytics via Diagnostic Settings.
- Security and compliance logs are retained in Microsoft Entra ID and optionally exported to SIEM tools.
- Alerts and dashboards are configured in Azure Monitor and Workbooks for real-time visibility.

### Failure handling
- **Buffered Logging:** SDKs buffer telemetry locally if ingestion endpoints are temporarily unavailable.
- **Sampling:** Adaptive sampling is used to manage telemetry volume; critical events are excluded from sampling.
- **Fallback Mechanisms:** In case of persistent failures, logs can be redirected to blob storage or Event Hubs.
- **Monitoring Logging Health:** Alerts are configured to detect drops in telemetry volume or ingestion anomalies.

# 9. Technology architecture
Should answer the question “what runs on what, and where”. It is expected this would be split into 3 aspects:
- **Logical view** – showing the classes of infrastructure/platform service being consumed and by what application facets
- **Physical view** – showing how many/much of each platform service is being consumed (or if elastic the bounds)
- Various views covering the qualities of service of the technical architecture which wraps application qualities of service and technology qualities of service into one area.

## 9.1 Logical platform architecture
For Prod and Pre-Prod describes how the application architecture and data architecture is mapped to logical platform services (be they servers, storage, SaaS, PaaS etc.).

The EPR system is composed of a number of logical layers:

### 1. Data ingestion layer
- **Sources:** Stakeholder portals, producer file submissions.
- **Data Types:** Packaging materials, organisational registrations.
- **Mechanisms:** Manual entry interfaces and file uploads.

### 2. Data processing & integration layer
- **Functions:** 
    - Standardizes and validates incoming data.
    - Integrates data from multiple sources into a unified format.
    - Prepares data for compliance evaluation and reporting.

### 3. Reporting & analytics layer
- **Dashboards:** Visualize compliance status, material usage, and environmental impact.
- **Reports:** Generate submission-ready reports for national authorities and producer responsibility organizations.

### 4. User interface layer
- **Portals:** 
    - For producers to manage packaging data and monitor compliance.
    - For regulators to review submissions and audit data.
- **Features:** Role-based access control; Workflow tools for approvals, corrections, and audits.

### Supporting capabilities
- **Cloud Infrastructure:** Scalable and secure hosting environment.
- **Security & Compliance:** Data encryption, access control, audit trails, and compliance with data protection laws.

<br>

![Figure 29.0 Supporting capabilities](./epr-sadd-images/01/figure-29.0-supporting-capabilities.png)
Figure 29.0 Supporting capabilities

<br>

The architecture pattern has been designed on the principles of **Data lake house**. Data lake house is a modern data architecture that combines the concepts of data lakes and data warehouses. It aims to address the limitations and challenges associated with both approaches by integrating them into a unified system.

**Data lake house**, data is ingested in its raw format into the data lake, just like in a traditional cloud file storage. However, the data lake house also incorporates a mechanism to apply schema enforcement, data governance, and indexing, time travel, versioning, which are common in data warehouses. This allows for faster query performance, easier data discovery, enhanced data quality and keeping a master copy of data.

**Data warehouse** to store structured and processed data for analytics and reporting purposes. Data warehouses are designed with a predefined schema, optimized for query performance.

**Data lakes** emerged as a solution to store large volumes of raw and unprocessed data in its native format. Data lakes provide a centralized repository for storing structured, semi-structured, and unstructured data, allows to perform advanced analytics, data exploration, and machine learning on diverse data sources.


### Logical
Logical data platform is the high-level representation and organization of data assets within Defra EPR Project, independent of any specific technology or implementation details. It focuses on the structure, relationships, and flow of data across different systems and applications. It is providing a logical framework that enables effective data management, integration, and analysis.
 
<br>

![Figure 30.0 Logical data platform](./epr-sadd-images/01/figure-30.0-logical-data-platform.png)
Figure 30.0 Logical data platform

<br>

<Current env landscape, replace w ArchiMate model mapping app to infra>

<br>

![Figure 31.0 Logical data platform - archimate](./epr-sadd-images/01/figure-31.0-logical-data-platform-archimate.png)
Figure 31.0 Logical data platform - archimate

<br>

## 9.2 Physical platform architecture
One per environment as this reflects “what must be provisioned”. Develops the logical platform architecture to show how physically the application and data architecture components are distributed onto the physical architecture (in this context a PaaS service represents a logical and physical concept, and the physical view should be used to reflect specific configurations e.g. to show that a PaaS service is distributed across multiple AZs, and how much “capacity” or “reliability” has been specified for the PaaS service and whether it is replicated and with what latency etc.). For non-cloud aspects or IaaS then the physical views will reflect a more traditional network-oriented diagram. For PaaS, SaaS or *potentially IaaS, any known constraints of the platform should be noted as such and considered as potential debt. For example, if the use of Azure SQL means a certain approach to replication could not be employed this should be noted.

### Core design principles
At the centre of the architecture is Network Segmentation & Security Layers, which include:
- **Azure Virtual Networks (VNets)**
- **Network Security Groups (NSGs)**
- **Azure Firewall / Application Gateway** These components ensure secure communication between services and enforce access control policies.

### Key Azure components
#### 1. Application layer
- **Azure App Services:** Hosts web portals for producers, regulators, and administrators.
- **Azure API Management:** Manages and secures APIs used for data submission, validation, and reporting.

#### 2. Compute & integration
- **Azure Functions:** Handles event-driven tasks like data validation, transformation, and notifications.
- **Azure Logic Apps (optional):** For orchestrating workflows between services.

#### 3. Data storage & processing
- **Azure SQL Database:** Stores structured data such as producer registrations, packaging data, and compliance reports.
- **Azure Blob Storage:** Stores unstructured data like packaging documentation, images, and audit files.
- **Azure Cosmos DB:** Manages globally distributed, schema-less data such as real-time submissions or IoT packaging data.
- **Azure Redis Cache:** Provides fast access to frequently used data, improving performance.
- **Azure Synapse Analytics:** Enables large-scale data analysis, reporting, and integration with Power BI for dashboards.

#### Azure infrastructure cost optimisation – ADR-142 and ADR-143 (approved)

**ADR-142 – Azure Environment Reservations and Autoscaling:**

- **Synapse Dedicated SQL Pool (1-year Reserved Instance, DWU3000):** A 1-year Azure Reserved Instance has been purchased for the Synapse Dedicated SQL Pool at DWU3000. This reduces the effective cost from approximately £43k/month (PAYG) to approximately £27k/month, with Synapse representing approximately 65% of total EPR infrastructure spend.
- **Azure Cosmos DB (Autoscaling):** CosmosDB has been switched from fixed provisioned throughput to autoscaling mode, which allows the provisioned RU/s to scale automatically between 10% and 100% of the configured maximum. This delivers approximately £12k annual savings by aligning consumed throughput to actual demand.
- **Azure SQL Elastic Pool (Development environments):** The 64 individual S0 Azure SQL database instances in development environments have been consolidated into an Azure SQL Elastic Pool. This provides 40–50% reduction in SQL costs and improved burst-capacity management for development workloads.

**ADR-143 – Synapse Dedicated SQL Pool Rightsizing:**

- **Production Pool:** Upsized from DWU1000 to DWU2000. Benchmarking showed near-linear improvement in data pipeline processing times at DWU2000, reducing end-to-end pipeline run times and improving data freshness for regulatory reporting.
- **TST Pool:** Decommissioned. The TST Dedicated SQL Pool (previously DWU1000) was switched off after analysis showed near-zero activity. Test workloads are now served from the Synapse Serverless SQL pool.
- **Lower Environments (DEV, PRE):** Scheduled automated downsizing to DWU200 on weekend nights, restoring to working-week levels on Monday mornings. This reduces idle costs in environments that have no weekend workloads.

Following RPD Data Platform technical architecture describes how EPR source systems data is ingested, transformed and made it available for the consumption by the downstream applications such as PowerBI dashboards and regulatory front-end applications.

<br>

![Figure 32.0 RPD technical architecture](./epr-sadd-images/01/figure-32.0-rpd-technical-architecture.png)
Figure 32.0 RPD technical architecture

<br>

Source code for above technical architecture diagram:

### Data ingestion strategy
This section describes data ingestion requirements and how data from source system are ingested into the RPD Data Platform in hourly basis using micro batch processing:
- configuration-driven data ingestion approach used when a large number of source tables need to be ingested regularly, the ingestion process is Spark-based via Synapse Notebooks, this helps minimise development and testing efforts. Additionally, maintaining future changes will be much easier, as there will be no need to develop new data pipelines. To support configuration-driven data ingestion from source systems, the solution requires a configuration data store(Blob Storage) that can hold the data mappings between Source, Raw Layer and the Bronze Layer for each source system and entity.

### Data curation - silver layer
The Silver Layer is responsible for transforming ingested source raw data into business-aligned, curated datasets that support regulatory reporting and data analytics. The source data from Bronze Layer is de-normalised into fewer number of tables to improve reporting and data query performance
- Data is modelled to align with data analytics and reporting requirements.
- Multiple Bronze Layer tables joined, aggregated, or enriched into a single conformed Silver Layer table.
- Partitioning and distribution strategies are determined based on data access patterns and performance expectations.

However, in current solution data is curated/transformed using views, nested views and the Stored procedures which lead to lot of redundant data transformations, objects and inefficient use of Synapse resources.

### Data consumption - gold layer
The Gold Layer provides cleaned, enriched, and business-ready data for reporting and analytics.
- Power BI Reporting connects to Gold Layer views to generate dashboards and reports.
- Views in the Gold Layer are designed to:
    - Include only the required columns and data for reporting and analysis.
    - Present data in a business-friendly format (use business glossary).
    - Ensure data accuracy and consistency across all reports.

These views act as the single source of truth for business users, reducing the need to query raw or intermediate data directly.

### Synapse data pipelines
The following two pipelines are used to copy data . The environment name starts with first 3 letter of connected recourse as per environment.

#### Enrolment app
##### Intro
This pipeline will process data from apps team SQL database , it connect to following instance ({dev1}_accounts) , as per environment prefix.

##### Process diagram
The application flow retrieves credentials from keyvault for two databases (appsdb and datadb) using the functions get_credentials_appsdb() and get_credentials_datadb(). The values are assigned to specific variables.
The required paths and URLs are constructed based on the obtained credentials. For example, delta_path is a file path for a Delta Lake, ctrl_table_path points to a CSV file, and appsdb_jdbc_url is a connection string for the apps database. The ODBC driver and constructs the URL for the data database.

The CSV file (ctrl_table.csv) contains the list of the tables to be loaded as a spark Dataframe. It prints the first two rows and logs a success message. If an error occurs, it logs an error message and raises the error.
If Delta Lake path for 'etl_run_ts' not exists, it sets intial_load to True, gets the timestamp (etl_run_ts), and updates the Delta Lake. Otherwise, it loads etl_run_ts from the Delta Lake.

The loop processes each table in ctrl_table_df one by one, extracting data, performing checks, and logging information. At the end of the loop, it logs statistics about the operations performed. If the table counts from source and target does not matched it will do a full load from source to keep it in sync. Finally, it checks if all tables were loaded successfully. If so, it updates etl_run_ts and logs a success message.

##### Configuration file
It is Mandatory to have ctrl_table.csv in conf directory of storage account ending 1401 in all environments. This is a configurable table list containing information about the table , primary key and load type (FULL/INCR).

##### Process flow
Here's a textual representation of the application's flow:

###### Initialization and configuration
- Import necessary libraries and modules.
- Set up logging.
- Configure Spark and Delta Lake settings.
- Define and load functions from the functions_lib.

###### Data loading and processing
- Read control table information from a CSV file located in the conf container of a storage account.
- Determine if it's an initial load or not based on the current day of the week (weekend loads are considered full loads).
- Load ETL run timestamps from Delta Lake or generate a new one.

###### Loop over control table
For each table defined in the control table:
- Fetch details such as schema, table name, load type, and primary key.
- Construct a SQL query based on load type and watermark column.
- Load data from the source SQL Server database using the constructed query.
- Add a load_ts column to the DataFrame.
- Write data to a Delta Lake table.
- Create or update an external Hive table pointing to the Delta Lake table.

###### Schema comparison
- Compare the schema of the data loaded from SQL Server with the schema in the destination SQL pool.
- Determine if schema transformation is required based on the comparison result. If Schema is not matched than It will perform full load as mentioned in next step by dropping the existing table.

###### Data loading into SQL pool
- If a full load is required or determined by schema comparison:
    - Fetch data from the Delta Lake table.
    - Load data into the destination SQL pool.
- If an incremental load is required:
    - Delete existing records in the destination SQL pool based on the Business key i:e (ExternalId).
    - Fetch data from the Delta Lake table based on the load timestamp.
    - Load new data into the destination SQL pool.

###### Logging and monitoring
- Log information and errors during the execution of each step.
- Track the count of tables processed and loaded successfully.

###### ETL_RUN_TS update
- Update the ETL_RUN_TS timestamp in the Delta Lake for the next run.

###### Exit and error handling
- Stop the Spark session and report any errors.

##### Pipeline
The pipeline ‘pip enrolment’ run from synapse pipeline namely 'pip_rpd_apps'

##### Notebook
The pipeline execute the notebook ‘enrolment’.

##### Trigger
The pipeline executed by 'trg_rpd_apps' trigger.

##### Schedule
It is running every 1 hour between 9:00 till 17:00 during weekdays and On Saturday.

#### 4. Identity & access management
- **Azure Active Directory (AAD):** Manages user authentication, role-based access control (RBAC), and single sign-on (SSO).

#### 5. Monitoring & observability
- **Azure Monitor:** Tracks system health, performance metrics, and logs.
- **Azure Log Analytics:** Provides deep insights into system behavior and security events.

### Data flow and integration
- All services communicate through secure, segmented networks.
- APIs expose data endpoints for internal and external use.
- Data flows from ingestion (via APIs or portals) to processing (Functions, Logic Apps), then to storage and analytics.

<br>

![Figure 33.0 Data flow and integration](./epr-sadd-images/01/figure-33.0-data-flow-and-integration.png)
Figure 33.0 Data flow and integration

<br>

## 9.3 Performance / volumetrics / scaling capability
Explains how the physical platform area provides for these services. After performance testing/implementation this section should contain summaries of test results and any known “pinch points” plus any required narrative on underlying platform limitations (for example use of PaaS may lead to non-deterministic behaviours or variances in latency).

Non-functional requirements are defined and maintained by the architecture team. These include performance benchmarks, availability targets, and scalability expectations. The NFRs are reviewed and updated as the system evolves. The current NFRs are stored here: **RPD NFRs.xlsx**.

## 9.4 Localised availability and recoverability features
Describes how the system “in itself” delivery high availability and in the circumstances of an unplanned outage how the system supports rapid recovery – or if required because it causes further problems – how the system can be prevented from auto recovering. After OAT or failure testing should capture any observed issues that cannot be resolved.

At the time of writing (July 2025), the pEPR solution is only resilient to the failure of a single availability zone in the UK South region [2, 3]. No OAT has currently been conducted so empirical validation of the possible failure modes is not possible [2, 3]. The current proposal for a DR strategy is to provision all the infrastructure components to the UK West region via Azure DevOps pipelines; similarly, the containerised web apps and APIs will be provisioned to the UK West region via Azure DevOps pipelines [2, 3]. All persistent data stored will be restored from geo-resilient backups to the UK West Region [2, 3].

## 9.5 Cross system reliability or recovery considerations
Explores whether there are there any aspects of the solution which if “stopped” or “failed” would lead to wider problems. An example could be where equivalent data is written to multiple interfaces and one of the writes fails but the target systems are not idempotent. Another example could be where there are transaction sequence numbers in use between systems and on system experiences an outage leading to data loss [6, 203].

Information is principally taken from EPR Report Packaging Data: High level solution architecture - Collections & Packaging Reforms - Confluence [203].

- Data uploads are based on a stream-based architecture; individual component failure will not cause issues with other components [204].
- The architecture uses Redis caching; if the cache is stale or unavailable, services may fall back to slower or inconsistent data sources [204].

### Component isolation and resilience
The EPR platform is built on a stream-based, loosely coupled architecture, which ensures that the failure of an individual component does not cascade to others. Services are designed to be independently deployable and recoverable, supporting high availability and fault tolerance [204].

### Caching and data consistency
The architecture leverages Redis caching to improve performance. In the event of cache unavailability or staleness:
- Services may fall back to slower or less consistent data sources.
- This can introduce latency or temporary inconsistencies [205].

## 9.6 “Test in live” considerations
Explains how the system can be tested whilst live (if at all) in order to investigate / diagnose issues 0- for example does it support synthetic “test” transactions.

The current RPD and PayCal system does not support ‘test’ transactions and the regulator stakeholders refuse the creations of any test users or dummy customers to support live testing. Live issues are either reproduced in PRE, possibly using a copy of PRD data, or testing is done via some ‘friendly’ end users [205].

## 9.7 Serviceability features
Explains to what extent the solution components can be “hot swapped” or otherwise changed. Does the solution offer the ability to change with zero outage, or if short outages are needed (often nearer the data services) then how does the solution allow for this in a controlled fashion? Which services can be disabled, and which can be left operational because for example they use cached data?

Below is a breakdown of how each component supports hot-swapping or controlled change [206]:

### 1. Azure web apps
Azure Web Apps support zero-downtime deployments through deployment slots. This allows new versions to be staged and tested before being swapped into production. Traffic redirection can be gradual or instant, and rollback is straightforward if issues arise [207].
- **Hot-swappable:** Yes, via deployment slots [207].
- **Controlled change:** Slot swap with warm-up ensures seamless transitions [207].

### 2. Azure functions (serverless)
Azure Functions support versioned deployments and can be updated with minimal disruption. Functions can be deployed in isolated plans or consumption plans, and traffic can be routed using Azure Front Door or API Management [207].
- **Hot-swappable:** Yes, especially when using deployment slots or blue-green strategies [208].
- **Controlled change:** Functions can be disabled individually without affecting others [208].

### 3. Azure Synapse analytics
Synapse is less amenable to hot-swapping due to its data warehousing nature. However, Synapse Pipelines and SQL Pools can be updated in a controlled fashion using CI/CD pipelines. Serverless SQL pools allow querying without impacting the underlying data [208].
- **Hot-swappable:** Limited; short outages may be required for pipeline changes [208].
- **Controlled change:** Use of staging environments and CI/CD mitigates risk [209].

### 4. Azure Cosmos DB
Cosmos DB supports multi-region writes and automatic failover, enabling high availability and minimal downtime during changes. It also supports live indexing and schema-agnostic updates, which reduces the need for downtime during data model changes [209].
- **Hot-swappable:** Yes, with multi-region and live indexing [209].
- **Controlled change:** Failover priorities and consistency levels can be configured [209].

### 5. Azure storage accounts
Storage Accounts configured with Geo-Redundant Storage (GRS) or Zone-Redundant Storage (ZRS) allow for high availability and replication. Updates to blob containers or file shares can be done without service interruption [209].
- **Hot-swappable:** Yes, for most operations [210].
- **Controlled change:** Replication and versioning support safe updates [210].

### 6. Azure SQL database
Azure SQL supports online schema changes, read replicas, and geo-replication, allowing for updates with minimal impact. Features like Query Store, Intelligent Query Processing, and Accelerated Database Recovery enhance resilience during changes [210].
- **Hot-swappable:** Yes, with online operations and replicas [211].
- **Controlled change:** Use of staging databases and failover groups [211].

### Service interdependencies and caching
- **Services that can be disabled:** Individual Azure Functions or Web Apps can be disabled without affecting the rest of the system [211].
- **Services that remain operational:** Components like Web Apps and APIs can continue to serve cached or static content via Azure Front Door or CDN while backend services are updated [211].

# 10. Security architecture

## 10.1 Security view
The Extended Producer Responsibility service is hosted in a Defra Azure tenant. A number of existing security controls provided by CCOE and other platformed services are in place with EPR utilising existing anti-virus solution from the Defra Trade service and adhering to architectural patterns for API Gateway management and API Management (APIM) [6, 211].

The diagram with accompanying descriptions below provides an overview of the layered security approach which has been embedded into the design of the overall EPR solution [212].

<br>

![Figure 34.0 Solution security overview](./epr-sadd-images/01/figure-34.0-solution-security-overview.png)
Figure 34.0 Solution security overview

<br>

For ease of viewing the above diagram and descriptions, the following embedded html view has also been included [212]:

## 10.2 Security roles and responsibilities view
The security roles and responsibilities have been defined in the following, through project into live, table below in the form of a Secure by Design RACI matrix. The matrix is based on the HMG’s secure by design roles and responsibilities matrix [6, 212].

<br>

![Figure 35.0 Secure by design RACI](./epr-sadd-images/01/figure-35.0-secure-by-design-raci.png)
Figure 35.0 EPR RACI Matrix

<br>

For ease of viewing the above table and descriptions, the following embedded excel spreadsheet view has also been included [213]:

## 10.3 Information handling / classification view
The classification view is OFFICIAL with handling instructions up to OFFICIAL-SENSITIVE. Further details in relation to the data types are provided in the Data Privacy Impact Assessment (DPIA) and the Data Sharing Agreement (DSA). Documentation relating the DSA located here: **2024_Data Sharing Agreement** [6, 213].

## 10.4 Role, actor and function matrix
The current view in relation to Role Based Access Control (RBAC) is shown in the table below. This is the current ‘As-Is’ view and further details describing the account management process are located here: [Reference URL] [6, 214].

| Capability | Admin user permissions | Approved | user permissions | Delegated user permissions | Basic user permissions | Regulator permissions |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| Invite new basic users to join existing organisation | Y | Y | Y |  |  |  |
| Invite new admin users to join existing organisation | Y | Y | Y |  |  |  |
| Invite a new approved user for a new organisation (Scenario 2) |  |  |  | Y (Regulator approval needed) |  |  |
| Invite a new admin user for a new organisation | Scenario 2 approval |  | Y |  |  |  |
| Invite a new delegated user to join existing organisation |  | Y (Regulator approval needed) |  |  |  |  |
| Nominate a new delegated user for existing organisation |  | Y (Regulator approval needed) |  |  |  |  |
| Approve or reject an Approved user to represent an organisation |  |  |  |  | Y |  |
| Approve or reject a Delegated user to represent an organisation |  |  |  |  | Y |  |
| Withdraw an existing delegated user |  | Y (Regulator to be informed) |  |  | Y (AP to be informed) |  |
| Remove a basic user | Y | Y | Y |  |  |  |
| Select or de-select a Compliance Scheme |  | Y | Y |  |  |  |
| Change of approved user | Y (Regulator approval needed) | Y (Regulator approval needed) |  |  | Y |  |
| Remove admin user | Y (Other than self) | Y | Y |  |  |  |
| Manage organisation account(s) for user | Y | Y | Y |  |  |  |
| Upload data for registering producer/CS | Y | Y | Y | Y |  |  |
| Submit data for registering producers/CS |  | Y | Y |  |  |  |
| Upload PoM data | Y | Y | Y | Y |  |  |
| Submit PoM data |  | Y | Y |  |  |  |
| Forgot own username / password | Y | Y | Y | Y | Y |  |
| Reset other users password (for the same organisation) | Y |  |  |  |  |  |


## 10.5 Leveraged security components
Azure firewall, as part of the standard CCOE architectural patterns, is deployed across Defra Azure tenants. Further details are shown here: AZR Cloud Service Azure Firewall - Overview. The design follows core design principles, as shown in section 9.2 of this document, including architecture in relation to network segmentation and security layers.

### 10.5.1 Web application firewall
WAF is deployed as part of the application gateway, which sits behind the Azure tenant firewall. This is depicted in 10.1 (item 3) above in this section.

### 10.5.2 Protective monitoring
Protective monitoring is in place for this service. Defra’s SOC monitoring team receive logs into the central SIEM tool (Sentinel). Further details are shown in the following ADR: ADR-028: Protective Monitoring Logging - Collections & Packaging Reforms - Confluence.

## 10.6 Bespoke security components
Security headers have been defined using OWASP best practice to ensure limitations in cross-site scripting attacks as described in the following ADR. ADR-008: Security Headers - Collections & Packaging Reforms - Confluence.

## 10.7 Key management
All keys are stored within Azure key vault (see section 14.4).

## 10.8 Malware detection / prevention
Files uploaded to the EPR service require anti-virus scanning to ensure that no infected files are stored within the system which could (as part of future themes) be downloaded. The EPR service is using the existing DEFRA Trade Anti-Virus Solution and further detail is shown in the following ADR: ADR-023: Anti-Virus Service - Collections & Packaging Reforms - Confluence.

## 10.9 Authentication / authorisation model – human actors
To access the service users need to authenticate to Azure AD B2C. When users access this application for the first time they are redirected to Azure AD B2C using the OpenId Connect protocol. After successful authentication, they are redirected back to the application together with an authorisation code, which is then used to acquire their ID, access and refresh tokens by standard OpenId Connect authorisation code flow.

Their identity information is then extracted from the ID token and a user session is established by creation of standard ASP.NET Core authentication cookie. Access and refresh tokens are stored for later use in the token cache (Azure Cache for Redis). Stored access tokens are then used to call backend APIs on behalf of the user. Stored refresh tokens are used to refresh access tokens when they expire.

Applications will use the user information retrieved from the account service (either directly or via a facade) to ensure that authenticated users have:
• restricted access to data, e.g., their access is limited to their own organisations.
• restricted access to functionality, e.g. only approved or delegated people can submit placed on the market data for a specific organisation.
ADR-015: Account Creation - Collections & Packaging Reforms - Confluence.

## 10.10 Authentication / authorisation model – system actors
An API endpoint in the account service will provide user information in a timely manner, containing:
• their enrolment data (enrolment status),
• their roles within the organisation (account and connection).
The API will be on Account Façade, which will call to Account Service to get the user information.
Further details are shown in the following ADRs: ADR-018: Account Service - Collections & Packaging Reforms - Confluence, ADR-022: User Authorisation - Collections & Packaging Reforms - Confluence.

## 10.11 GitHub and CI/CD pipeline
Details in relation to GitHub, account set-up and security authentication, using 2FA are shown in the following: GitHub Setup - Collections & Packaging Reforms - Confluence.

# 11. Delivery architecture (or secondary architecture)
This section should describe how the solution has been developed/configured, tooling used. A useful way to look at would be to consider the standard tools, setups, standards, frameworks, repos etc. that should be in place if we were to set up another dev shop. The RPD application part of EPR is primarily developed code. Development platforms include MS-Visual Studio Professional and Azure Synapse notebooks. Programming languages include C#, SQL, R and Python.

## 11.1 Development platform
Repos and repo management; Tooling; Version control; Branching; CD/CI method/guide; Pipeline flow/execute and config guide; s/w tech stack per service/component (frameworks, widgets, JVM etc.); Runbooks (deployment scripts); Coding standards.

### Repositories
Written code on developer workstations is uploaded by synchronisation, for example, from the workstation or Azure development environments to the GitHub repository listed here: DEFRA repositories. Up until the end of 2023, repos were maintained in Azure DevOps (ADO). During early 2024, almost all the repositories excepting EPR-Data were successfully migrated from ADO to GitHub. The reason that this was not migrated was because there had to be a period of absolute quiet (no changes in any branch) for these to be migrated, which given the busy activity over the 2024-2025 period has not lent itself to such a quiet time window. All code is public-readable, following GDS guidelines.

### Tooling
The following is the tooling set used for RPD:

| Tool | Vendor | Purpose | Comment |
| ------ | ------ | ------ | ------ |
| Azure Data Factory | Microsoft | For operational data pipelines. | |
| Azure DevOps | Microsoft | SaaS platform supporting DevOps | Code pipelines and just one code repository (EPR-Data). |
| BrowserStack | BrowserStack | Browser/Mobile App test tool. | |
| Confluence | Jira/Confluence | Documentation/content repository. | |
| Dependency-Check | OWASP | Dependency checker. | |
| draw.io | Drawio | Used for representing physical data model etc. | Open-source diagramming tool. |
| Figma | Figma | Collaboration tool for interface design. | |
| GitHub | Microsoft | Code repositories. | |
| JMeter | Apache | Load testing tool. | |
| Mural | Mural | Visual collaboration tool. | Internet SaaS whiteboard for process drawings, workshops, brainstorming etc. |
| OpenVPN Connect | OpenVPN | To securely access the Defra network. | In the context of SonarQube etc. |
| OWASP ZAP | OWASP | Security testing tool. | Open Worldwide Application Security Project. |
| Power BI | Microsoft | Data visualisation. | |
| SonarQube | SonarSource | Code quality analysis tool. | |
| SharePoint | Microsoft | Documentation/content repository. | |
| SSIS/SSMS | Microsoft | Data tools in a Microsoft environment. | |
| Visual Studio Professional | Microsoft | Development environment for C#. | Support is provided as part of the Microsoft Enterprise Agreement. |

### DevOps
Branching strategy is outlined in this document: Consolidated Release / Branching Strategy - Collections & Packaging Reforms - Confluence. A more specific and detailed version of the above strategy for the more recent (end 2025) releases associated with PayCal are detailed in this document: EPR Branching Strategy - Collections & Packaging Reforms - Confluence. These show the flexible approach to parallel development by teams and even emergency deployment but always maintaining the purity and integrity of the deployed code through strict version control. Additionally, the use of feature flags or toggles is done to enable controlled activation of deployed code. There are DevOps code pipelines that are used as technology to promote successfully tested code from the lower (DEV, TST) to the higher environments (PRE, PRD).

### Runbook
Every step of every code promotion into the TST, PRE and PRD environments is thought through and documented in the Run Book, located on Confluence at: Release Runbooks & Release Notes - Collections & Packaging Reforms - Confluence. The Runbook is created by the release and goes through review before being executed. The release team is always responsible for the Runbook, although it is executed by the cloud centre of excellence (CCoE) for promoting to the higher environments.

The Runbook includes pre-requisites, the implementation steps and fall back, should the implementation fail. The fall back will take us to a no-worse position should the promotion have not taken place at all, especially into the production environment (PRD). This is assuming that failure is detected during implementation. If a production failure is identified long after implementation (rare and probability likely to be small that errors escape detection), then those needs be managed by fixing forward. There are no known examples of fix-forward yet. All runbooks are available in Confluence at https://eaflood.atlassian.net/wiki/x/J4FqAwE.

### Coding standards
There are UK Government requirements about producing high quality code. These are maintained by running all written code through an approved open-source code quality tool called SonarQube.

## 11.2 Testing solution
It is expected that the solution for testing has its own specialist work product, therefore the list to the right represents a checklist of items that should be summarised here but referenced for the detail: Test Approach (strategy, plan, general method); Tooling; Environment; Plan/Characteristics/Capabilities; Regression approach; Functional approach; Performance approach; Integration test approach – internal; Integration test approach – external.

The testing strategy is described via the EPR Test Approach document page on Confluence located at: EPR Test Approach - Collections & Packaging Reforms - Confluence. The EPR approach is based on the Defra DDTS Test strategy. Functional testing is done in all environments by the appropriate and authorised persons for each environment. Functional testing includes Regression testing to ensure that nothing from the past (baseline) is broken because of the new development (increment). Functional testing progress through the environments is elaborated in the next section Route to Live.

Integration testing as with FSS (not deployed till late 2025) was managed simulated via using a RPD invoice file output comparing with the data contract for accuracy of matching the real with the expected result. Real-time integrations with Companies House or Postcodes could occur from the DEV4 integration testing environment via API Manager (APIM) to those respective web services.

The environments being on MS-Azure, rebuild of any of them could be done by restoring an appropriate pre-captured image of the environment. 

Currently test data is created manually via pre-requisite processes e.g. create master data like a producer Organisation prior to performing a transaction using that master data. From a process perspective, this is the purest approach. However, this is time consuming and not scalable to create large volumes of data that may be required. To overcome, we have informally explored AI based techniques to generate meaningful test data in large quantities that is also anonymised. This is possible as tried in a test bed, but EPR has not yet come around to implementing test data generation automation. 

<br>

![Figure 36.0 Testing](./epr-sadd-images/01/figure-36.0-testing.png)
Figure 36.0 Testing

<br>

**Performance testing** is carried out by the Defra DDTS testing team using the Apache JMeter tool. 

**Security testing** as in external IT Health Check or an internal security review is performed in the pre-production environment (PRE) by another partner service vendor or Defra security team as appropriate.

## 11.3 Route to live
Summarise tools used to promote aspects of the solution through environment to live.
Inter environment delivery (particularly into pre-prod).
Staging for release (in Prod – default activated or “waits for activation”).
Activation (of staged).
Reversion / redeployment of prior versions / fix forward capabilities.
The below figure also shows the route to Production.
The repository technology used is GitHub to store code and pipelines to transport code from store to the environment.
Please note that yet (end of 2025) functional testing itself is still manual and does not use automation technologies.

Individual teams do unit, system and integration tests within their sub-environments in DEV, except for DEV4 and DEV8 that are managed by the testing team.
Please note that there is only one common Synapse analytics as well as Cosmos NoSQL DB data layer in DEV that all the teams share.

Once the release management is happy with DEV, then the code is promoted to TST where functional testing is performed by Defra domain experts.

Upon successful TST, code is promoted to PRE where user acceptance testing (UAT) is done again by Defra experts.
This environment may also be used for performance testing by the Defra DDTS team using the automated JMeter tool, as mentioned earlier.

There is a parallel environment here called PRE-2.
Reason for this is to properly test data reports against all the rich variations that occur in records, we have not yet been able to manually or synthetically generate that large body of data.
Therefore, we use a tightly access controlled copy of production data in the PRE-2 data layer.
Incidentally, this data is only available to actual Defra users limited to their actual roles or to UK vetting service security cleared (SC) persons for data reports testing.
Ideally this environment should be created only if a release contains data reports and should be retired upon successful completion of that release.
In practice, the same PRE-2 has needed to be there for multiple releases, although strictly access controlled.
As it is only for data reports testing, PRE-2 is like a railway siding and not a path to production that PRE is.

Upon successful PRE testing, the code is finally promoted to production (PRD) with the accompanying Go Live and early life support.

<br>

![Figure 31.0 Logical data platform - archimate](./epr-sadd-images/01/figure-31.0-logical-data-platform-archimate.png)
Figure 31.0 Logical data platform - archimate

<br>



## 11.4 Service monitoring solution
Documents the solution for day to day monitoring the system at each tier including the end user experience.
Defines the use cases the monitoring solution supports, and the actors involved.
Describes any instrumentation “hooks”.
Needs to cover how “end to end” monitoring works not just “tin and wires”/platform.
As we are hosting RPD on MS-Azure, this comes with good native monitoring and management tools.
In lower environments, these are controlled by the development and testing teams respectively.
In the higher environments, by the dedicated CCoE team.
The monitoring and tooling are described in good detail in the dedicated next sections 12.2 and 12.3.

### Monitoring processes
Refers to monitoring solution but expands on who does what in response to et.
Might indicate behavioural aspect to watch for / alert on.
Monitoring is implemented using a layered approach, combining Azure-native observability tools with operational responsibilities.
Monitoring Stack:
- Azure Monitor and Log Analytics for telemetry ingestion.
- Application Insights for distributed tracing and performance metrics.
- AppInsights Alerting to SMTP distribution Groups for HealthCheckStatus and serverSideErrorAlerts for EPR key resources.
- Synapse Pipeline Alerts are set up for a PipelineAlertGroup which triggers to SMTP messages to key individuals.
Operational Responsibilities: [8, 9]
- First-line monitoring is handled by the Live Service team, who receive alerts via Azure Monitor Action Groups [8, 9].
- The Live Service Team log key information in SNOW or ADO and then perform an initial triage.
- Depending on the triage outcome incidents are either resolved by Live Service Team, passed to CCoE Team or escalated to expert areas within the wider EPR Programme Team.
- Second-line support (e.g. DevOps and platform teams) respond to escalated alerts and perform root cause analysis.
- 3LS/4LS support for alerts is provided by the wider EPR Programme Team such as the DG6 Data Team, DG5 Platforms Team or Lead Developer’s area.
- These areas contain SMEs with areas of specialisation who can perform deeper dives into the product then diagnose and provide resolution recommendations.
- As the Teams providing 3LS/4LS do not have direct production access, then any alert resolutions are passed to CCoE for completion (Depending on the required action an approved Defra Change Control may be necessary to complete any resolution work).
- Additional Security monitoring is provided by the Defra SOC who utilise the Defra adopted SIEM product suite to monitor EPR network data for suspicious traffic patterns or known threat sources.
- Any alerted activity auto-creates incidents in the Defra Service Now and assigns them to the EPR Live Service Team for initial triage.

### Diagnosis features
Which components support diagnosis, how can events be correlated to assist, who has access to what to assist with diagnosis [9, 11].
The EPR solution includes several built-in diagnostic capabilities to support rapid fault isolation and resolution: [9, 11]
- Application Insights: Enables distributed tracing across microservices, capturing request-response flows, dependency calls, and exception telemetry [12, 13].
- Custom Health Probes: Implemented in Function Apps and APIs to expose readiness and liveness endpoints [12, 13].
- Diagnostic Logs: Captured via Azure Monitor and routed to Log Analytics for querying and alerting [12, 13].

# 12. Operational architecture
It would be expected that this section generally links off to the “SKMS” or equivalent for the service and that this information is written by ops based on understanding / explanations of the design.
Sometimes called the “service wrap”.
This list therefore serves as a prompt for the form of questions that may be asked by service transition and an opportunity to provide some brief descriptions.
It is *not* intended to be ops procedure manual.

## 12.1 Initialising, controlling, stopping
How to activate, control usage – blunt instrument or designed in graceful capability.
Initialisation: Services are deployed via Azure DevOps pipelines using infrastructure-as-code (ARM/Bicep templates).
Initialisation includes environment-specific configuration, secure key injection via Azure Key Vault, and registration of event-driven components (e.g. Event Grid, Service Bus).
Control: Runtime control is achieved through Azure-native capabilities such as:
- Feature flags (via Azure App Configuration) to enable/disable capabilities without redeployment.
- Role-based access control (RBAC) to restrict administrative operations.
- API Management policies to throttle or block traffic if needed.
Stopping: Services can be paused or gracefully shut down using:
- Azure Function App stop/start controls.
- Scaling to zero for stateless components.
- Queue draining and message deferral for in-flight operations.
Note: All critical services are designed to support graceful degradation and controlled failover, ensuring minimal disruption during planned or unplanned shutdowns.


## 12.2 Monitoring processes
Monitoring is implemented using a layered approach, combining Azure-native observability tools with operational responsibilities:
**Monitoring Stack:**
- **Azure Monitor** and **Log Analytics** for telemetry ingestion.
- **Application Insights** for distributed tracing and performance metrics.
- **AppInsights Alerting** to SMTP distribution Groups for HealthCheckStatus and serverSideErrorAlerts for EPR key resources.
- **Synapse Pipeline Alerts** are set up for a PipelineAlertGroup which triggers to SMTP messages to key individuals.

**Operational Responsibilities:**
- **First-line monitoring** is handled by the Live Service team, who receive alerts via Azure Monitor Action Groups.
- The Live Service Team log key information in SNOW or ADO and then perform an initial triage.
- Depending on the triage outcome incidents are either resolved by Live Service Team, passed to CCoE Team or escalated to expert areas within the wider EPR Programme Team.
- **Second-line support** (e.g. DevOps and platform teams) respond to escalated alerts and perform root cause analysis.
- **3LS/4LS support** for alerts is provided by the wider EPR Programme Team such as the DG6 Data Team, DG5 Platforms Team or Lead Developer’s area.
- These areas contain SMEs with areas of specialisation who can perform deeper dives into the product then diagnose and provide resolution recommendations.
- As the Teams providing 3LS/4LS do not have direct production access, then any alert resolutions are passed to CCoE for completion (Depending on the required action an approved Defra Change Control may be necessary to complete any resolution work).
- **Additional Security monitoring** is provided by the Defra SOC who utilise the Defra adopted SIEM product suite to monitor EPR network data for suspicious traffic patterns or known threat sources.
- Any alerted activity auto-creates incidents in the Defra Service Now and assigns them to the EPR Live Service Team for initial triage.

## 12.3 Diagnosis features
Which components support diagnosis, how can events be correlated to assist, who has access to what to assist with diagnosis.
The EPR solution includes several built-in diagnostic capabilities to support rapid fault isolation and resolution:
- **Application Insights:** Enables distributed tracing across microservices, capturing request-response flows, dependency calls, and exception telemetry.
- **Custom Health Probes:** Implemented in Function Apps and APIs to expose readiness and liveness endpoints.
- **Diagnostic Logs:** Captured via Azure Monitor and routed to Log Analytics for querying and alerting.

## 12.4 Capacity reporting
What are the general maximum capacity thresholds of the system (as experienced during performance testing), how are we doing etc.
Capacity planning and utilisation monitoring are handled through a combination of Azure-native tools and operational dashboards:
- **Azure Metrics Explorer:** Tracks CPU, memory, and throughput for compute resources (Function Apps, App Services, Event Hub).
- **Log Analytics Dashboards:** Visualise ingestion rates, queue lengths, and storage consumption.
- **Scaling Rules:** Defined for auto scale-enabled services based on message volume and latency thresholds.
- CCoE has done the above during 2025 in the context of problem resolution, Azure Synapse Health Check etc.
- These are currently not done as BAU activity. It would be a good thing to start doing after configuring the tooling to do so on a regular basis.

## 12.5 Rebuild, recovery and reinstatement
Scenario based “how to” guide – not just the “tech stack” ensure understanding in particular of any cross-system RI issues - link to DR approach, Hours of Operation.
The EPR architecture supports resilience and recovery through a combination of platform features and operational procedures:
- **Infrastructure-as-Code:** All environments can be rebuilt using version-controlled ARM/Bicep templates.
- **Geo-Redundant Storage:** Used for critical data assets to support regional failover.
- **Backup Policies:** Applied to databases and configuration stores (e.g. Key Vault, App Configuration).

When Transitioned into a Defra Support Application, EPR will be a Tier 3 System and the underpinning design and infrastructure of EPR has been built to support the capability required to meet that.
The key parameters of a Defra Tier 3 Service are:
- Service hours of Mon-Fri 08:00-18:00 (excl Statutory Holidays).
- An Availability Target of >=98.50%.
- 3 hours of permitted unscheduled unavailability in a 28-day period.
- Recovery time objective (following complete service outage): 4 - 48 hours.
- Recovery point objective (extent of data loss): 8 - 48 hours.
- May have single Points of failure.
- Should be locally resilient and may be globally resilient.

When considering the above requirements of a Tier 3 Service, then the underlying design and infrastructure of EPR with its Azure geo-redundant replication means that EPR can more than satisfy them as its data is synchronously replicated in the primary region across the three Azure Southern UK datacentres.
In the highly unlikely event of the entire Azure Southern region becoming unavailable, it would be possible to recreate and reinstate EPR for Azure backups in a different Azure region.
Queries regarding the availability and DR approaches of other services providing interfaces to EPR such as PRN, FSS and core APIs such as Postcode Checker, Companies House, Antivirus, Gov Notify should be addressed to the relevant Service Providers.
As of December 2025, periodic DR testing is not done on a regular basis. It would be a good thing to start doing so.
Again, we do not have a Playbook as of December 2025 that could re-create environments, re-route data pipelines and restore data from geo resilient backups. A start was made during June 2025, but paused soon after probably because of the anticipated exit of the Atos Group.

## 12.6 Scheduled capabilities
What batch processes run, when (calendar view of the solution) – daily, hourly, yearly etc.
Operational support is integrated with the enterprise ITSM platform (e.g. ServiceNow):
- **Incident Routing:** Alerts from Azure Monitor are routed to the appropriate resolver groups based on severity and service tags.
- **Knowledge Articles:** Linked to common issues and recovery steps, maintained in the SKMS.
- **Change Management:** All deployments and configuration changes are logged and approved via CAB processes.

## 12.7 Calendar constraints
What periods of the year for example must the system operation be protected (e.g. via change freezes)?
The EPR platform operates under defined calendar constraints to ensure service continuity and minimise risk during critical operational periods. These constraints are particularly relevant for planning change windows, deployments, and maintenance activities.

### Change freeze periods
To protect system stability and ensure uninterrupted service during high-risk or high-demand periods, the following **change freeze windows** are enforced:
- **Financial Year-End (March–April):** No non-essential changes are permitted during the final two weeks of March and the first week of April. This aligns with statutory reporting deadlines and peak producer activity.
- **Holiday Periods (Mid-December to Early January):** A freeze is typically enforced from the second week of December through the first week of January to accommodate reduced staffing and ensure operational stability during the holiday season.

### Key submission periods
System stability is essential in the periods running up the deadlines for EPR Customer POM submissions which is normally around the start of April and the start of October.

### Additional considerations
- **Emergency Changes:** May be permitted during freeze periods but require elevated approval via the GIO Change Management process.
- **Scheduled Capabilities:** Batch processes and data synchronisation jobs are scheduled to avoid peak periods and freeze windows. These are documented in the SKMS and reviewed quarterly.
- Business define the change freeze timings for things like year-end, holiday periods and key submission deadlines.

## 12.8 Required cyclic activities (required forward schedule of changes)
For example, of crypto keys require to be change annually in co-ordination with other parties this would be covered here.
This section outlines recurring operational activities that must be scheduled and coordinated across the EPR platform to ensure compliance, security, and service continuity. These activities are typically included in the Forward Schedule of Changes (FSC) and reviewed during CAB meetings.

### Key cyclic activities
| Activity | Frequency | Description | Coordination Required |
| :--- | :--- | :--- | :--- |
| Cryptographic Key Rotation | Annually | All encryption keys stored in Azure Key Vault must be rotated annually in line with DEFRA security policy. | Yes – with third-party data providers and internal security teams. |
| Certificate Renewal | 90 days (Let’s Encrypt) or Annually (CA-issued) | SSL/TLS certificates for public-facing APIs and internal services must be renewed before expiry. | Yes – especially for services integrated with GOV.UK Notify, FSS, and LAPS. |
| RBAC and Access Review | Quarterly | Role-based access control (RBAC) assignments are reviewed to ensure least-privilege access. | Yes – with platform owners and security operations. |
| Backup and Restore Testing | Biannually | DR playbooks and backup integrity are tested to validate recovery objectives. | Yes – with Live Service and platform teams. |
| Environment Readiness Reviews | Every 2 sprints | Environment status (e.g. DEV, TST, PRE, PRD) is reviewed and updated in the EPR Environments Tracker. | Yes – with delivery teams and release managers. |
| Change Freeze Planning | Quarterly | Change freeze windows are aligned with statutory reporting and submission deadlines. | Yes – with CAB and business stakeholders. |

All of the above are set Defra requirements which EPR adheres to.

## 12.9 Incident or problem management
This section outlines how the EPR platform supports incident and problem management, with a focus on identifying self-healing behaviours and potential masking patterns that may obscure underlying issues.

### Incident management
- **Emergency Change Handling:** Emergency changes are governed by strict protocols. A P1 or P2 incident must be logged and accepted in ServiceNow before an emergency change can be initiated. The EPR Runbook provides detailed steps for executing emergency changes, including rollback procedures and verification steps. [16, 17]
- **Escalation and Communication:** Escalation contacts and duty managers are clearly defined for each environment (DEV, TST, PRE, PRD). All emergency changes are logged with references to the initiating incident and are subject to post-implementation review.
- **Monitoring Integration:** Alerts from Azure Monitor and Defender for Cloud are routed to the ITSM platform and trigger incident workflows. These alerts may include performance degradation, failed deployments, or security anomalies.

The EPR Live Support Teams use the Defra processes for Incident, Major Incident, Problem and Change Management which are detailed at the links below:
- Incident Management
- Major Incident Management
- Problem Management
- Change Management



# 13. Commercial perspectives *
The architect may have some understanding of the initial licencing model etc. (particularly if cots is used) and summarise here. All info needs to be caveated as being “point in time”. Only summaries: capture any information that emerged during delivery, but caveat as a “point in time” view.

## 13.1 Licencing
What aspects of the solution require licence management? What are the models in use (user, volume etc.)? What are the “tipping” or “break” points?

## 13.2 Recurring costs
Are there known future cyclical costs? Do these link to volume, time or a combination?

## 13.3 Costs to scale
Roughly what would the impact be of scaling either elastically or traditionally? A key consideration is the “tipping” point – is their tiering to be concerned about for example? Cap / collar regimes?

## 13.4 Current information
The information above should be taken over by service transition; link to the location of their information – or link in the Solution Architecture Definition Document page.

# 14. Inventory view *
Data required for loading into CMDB or service desk tools (aka bill of materials). Each of the headings should have been covered in the SA elsewhere so it should be that this is really an Index with hyperlinks. If the solution was being “bid” it would also represent the shopping list of solution components to be procured/licenced/built. The information above should be taken over by service transition; link to the location of their information – or link in the Solution Architecture Definition Document page.

For this section, we use two sources for complete coverage of the inventory in a complementary manner. The first source is a Confluence page at List of components in RPD - Collections & Packaging Reforms - Confluence. The second source is a spreadsheet extract from MS-Azure of components from the environments themselves that have identifiers and service level for each component. The spreadsheet is embedded here for complete reference. We shall see below a breakdown sub-list from the spreadsheet, categorised by type.

## 14.1 Data bases / stores / storage services
The below is an extract from the spreadsheet. 

<br>

![Figure 37.0 Database spreadsheet](./epr-sadd-images/01/figure-37.0-database-spreadsheet.png)
Figure 37.0 Database spreadsheet

<br>

Also the Confluence page at List of components in RPD - Collections & Packaging Reforms - Confluence that lists out this category of components as follows:
- Block/table 1 – SQL databases. Includes pricing tier information that is also an indicator of service level.
- Block/table 2 – Cosmos databases.
- Block/table 3 – Synapse databases.
- Block/table 4 – Storage Accounts.

## 14.2 Servers / hardware
The below is an extract from the spreadsheet. 

<br>

![Figure 38.0 Server spreadsheet](./epr-sadd-images/01/figure-38.0-server-spreadsheet.png)
Figure 38.0 Server spreadsheet

<br>

Also the Confluence page at List of components in RPD - Collections & Packaging Reforms - Confluence.

## 14.3 Services (PaaS etc.)
The Confluence link in Block/table 5 has a very large number of entries that in this case also includes pricing tier that is an indication of service level. https://eaflood.atlassian.net/wiki/spaces/MWR/pages/5816713361/List+of+components+in+RPD.

## 14.4 Keys
The below is an extract from the spreadsheet. 

<br>

![Figure 39.0 Key spreadsheet](./epr-sadd-images/01/figure-39.0-key-spreadsheet.png)
Figure 39.0 Key spreadsheet

<br>

All keys are located within Azure Key Vault. The CCoE pattern is to have all secrets with expiry dates that are rotated on a regular basis. Currently we use key vault to also store app configuration settings some which are not secrets and ideally should not be stored in key vault.

Incidentally there are no secrets in GitHub as ascertained from the environment and code quality specialists in the context of public readability of code in Section Delivery Architecture (or Secondary Architecture).

## 14.5 Built software components
All the built software components are held in the GitHub repository at DEFRA repositories. In addition, there is one more repository called EPR-Data within ADO in Defra.

## 14.6 Non “built” software / COTS
The only closest to COTS in RPD and PayCal is Power BI used for reports and data visualisation. Please note that COTS like ServiceNow, Stripe, Amazon Connect, Sequence Shift etc while being part EPR in FSS are outside of RPD and PayCal.

## 14.7 Licences
Almost all the components are running on the Azure subscription and are paid for through that mechanism. The one notable exception is Power BI that requires licensing for power users in the Defra data strategy team and data analysts from the supplier developer data team. The Microsoft 365 Admin Center shows all licenses available in the tenant including the number assigned and lets you drill into details for individual products. --> https://admin.microsoft.com/Adminportal/Home#/licenses.

## 14.8 Scripts
N/A

## 14.9 Locations of documentation
Documentation is stored in:
- **Confluence:** Extended Producer Responsibility for Packaging - Collections & Packaging Reforms - Confluence
- **Sharepoint:** Defra Architecture - Home

## 14.10 Current information
The information above should be taken over by service transition; link to the location of their information – or link in the Solution Architecture Definition Document page.

# 15. Appendices
Not possible to be too prescriptive with these but some typical ones are shown.

## 15.1 Glossary
Not just an acronym buster but an explanation.

## 15.2 Index of diagrams
Use Captions in word – this is then built automatically.

## 15.3 Index of tables
Use Captions in word – this is then built automatically.

## 15.4 Architectural RAID-D
This of course should be part of the overall project approach but often it is required to record these and the resolutions/outcomes separately. Show dates, status, names as appropriate.
- **Risks** – e.g. “lack of xxx means that yyy”.
- **Assumptions** - ensure sensitivity/impact if false noted – all assumptions are risks and assumptions of convenience need to be robustly managed out.
- **Issues** – something that blocks progress/blocked progress.
- **Dependencies** – external activity that needs to be coordinated.
- **Decisions** – with rationale/choices explored – “key design” decisions, potential project / scope decisions that influenced the architecture etc.

## 15.5 Architectural questions / answers
During delivery various questions will arise (e.g. choice of PaaS options etc.). Most of these should have been converted into decisions. However, there may still be open questions that were never resolved, and it is useful to reflect those here as they may represent a future risk or aspect that a future project may benefit from awareness of. Make sure the question itself is explained – i.e. why the question is important.

## 15.6 Architectural standards and patterns used
List those strategic components or approaches that have been used to deliver this system. The decision log should record any not used and why.

## 15.7 References: ADR

### Solution design and security

- **ADR-003:** Cosmos DB auditing – audit history tracking implemented via CosmosDB Submission Events table.
- **ADR-008 / ADR-008.A:** Security Headers – security header implementation across all RPD frontends and APIs.
- **ADR-016 / ADR-017:** Solution Design – core architectural decisions governing the overall RPD solution design.
- **ADR-020.A:** Solution Design update.
- **ADR-023:** Security – additional security design decisions (related to ADR-063.A anti-virus).
- **ADR-028:** Solution Design.
- **ADR-039:** Authentication / Authorisation – establishes the 1 user / 1 organisation / 1 role constraint; core auth pattern for RPD.
- **ADR-042:** RPD Business Intelligence – decisions governing Synapse-based BI and reporting architecture.
- **ADR-051:** Solution Design – deployed in release 2.6.
- **ADR-053 / ADR-053.1:** CI/CD pipeline design – GitHub Actions CI/CD patterns for all RPD services.
- **ADR-067 / ADR-067.1:** GitHub migration – ADO to GitHub repository migration.
- **ADR-068:** SonarQube security scanning integration into CI/CD.
- **ADR-070:** Shutter page – controlled service shutdown capability.
- **ADR-088:** Power BI access – Power BI licensing and access pattern for regulators and analysts.

### Producer registration and enrolment

- **ADR-002:** Producer – creation of the EPR provider task list and privacy declaration.
- **ADR-015:** User Account – core user account management design.
- **ADR-018 / ADR-018.A:** User Account – related to ADR-015; user account enhancements.
- **ADR-019 / ADR-021:** Producer – producer-facing design decisions.
- **ADR-040:** Compliance Schemes – CS enrolment and management design.
- **ADR-054:** Compliance Schemes – further CS design decisions.
- **ADR-055:** Org Data Validation.
- **ADR-055.A / ADR-055.B:** Organisation Registration Data – extensions to ADR-055.
- **ADR-056:** Linking reported data to Compliance Schemes.
- **ADR-064:** User Account.
- **ADR-071:** Organisations Self-Service – implemented in release 10.
- **ADR-073.2 / ADR-073.3 / ADR-073.4 / ADR-073.5:** User Account Self-Service – supersede ADR-073/073.1.
- **ADR-074.A:** RPD Public Register – large producers; implemented (ADR-074.B covers all producers, not yet implemented).
- **ADR-099 / ADR-099.1:** Subsidiaries – parent/subsidiary organisation relationships.
- **ADR-104.2:** Subsidiaries – bulk upload (supersedes ADR-104/104.1).
- **ADR-106:** Producer Registration and Fee Payment Journey.
- **ADR-106.A:** Producer Registration and Fee Payment Journey – Regulator view.
- **ADR-108:** Subsidiaries – one-off migration to fix subsidiary IDs.
- **ADR-113:** Subsidiaries – DB changes for looser parent/child coupling; deployed in releases 9/10.

### POM file submission

- **ADR-043:** POM File.
- **ADR-049:** POM File – parent of ADR-049.A.
- **ADR-049A:** Updates to submitted Packaging Data.
- **ADR-060 / ADR-060.A / ADR-060.B:** POM File Validation.
- **ADR-069 / ADR-069.D:** POM File Resubmission (069.D covers 2025 resubmission).

### Regulators

- **ADR-031:** Regulator – Approved and Delegated user management.
- **ADR-041:** Regulator Enrolment – internal SQL-script-based regulator account provisioning.
- **ADR-044:** Regulators Landing Page and Account Management.
- **ADR-052:** Regulators POM Approvals.
- **ADR-061:** Regulators – deployed in release 2.8.
- **ADR-063:** Regulator Organisation Data File Approval Journey.
- **ADR-063.A:** Regulator Organisation Data File Approval – Anti-virus integration (related to ADR-023).
- **ADR-066:** Registration Comparison Report.
- **ADR-072:** Registration File Resubmission.
- **ADR-094:** Producer Obligation Checker – separate portal.

### PRN / NPWD interface

- **ADR-109:** NPWD PRN Interface – defines the Fetch Issued PRNs, Update PRN Status, and Upsert Producer API contracts between RPD and NPWD. Direct predecessor to ADR-137.
- **ADR-098 / ADR-098.A / ADR-098.B / ADR-098.C:** Producer PRN Journey – producer-facing PRN acceptance/rejection journey; 098.C covers mid-year changes (MYC) obligation updates.
- **ADR-141:** RE/EX PRN & Waste Balance Immutability. **For Review — no formal decision at time of writing.** Recommended decision: Audit History Log approach. Core PRN fields (tonnage, accreditation, issuedToOrganisation) are immutable once issued; status changes are recorded in an append-only history table. All waste balance movements are written to an append-only transaction ledger recording type (DEBIT/CREDIT), amount, user, timestamp, and opening/closing balances. Logs are read-only in-system and sent to the CDP security audit service. Reconciliation of PRNs/PERNs between RE/EX and RPD to be introduced. Cryptographic hash chaining was considered but deferred pending any litigation risk or specific regulatory requirement.

> **[v1.2 change — ADR-141]** ADR-141 entry added.

### Payments

- **ADR-093 / ADR-093.1:** Gov.UK Pay Payment Journey – payment integration including API reference.
- **ADR-102:** Fees and Payments Calculator – late fees.
- **ADR-103:** Gov.UK Pay – mop-up payment journey.
- **ADR-111:** Offline Payments – regulator journey for recording BACS payments received directly.

### PayCal

- **ADR-091:** POM File Processing for PayCal – parent of ADR-091.A and ADR-091.B.
- **ADR-091.A:** Common Solution Design Component for Calculator.
- **ADR-091.B:** RPD Data Upload Process to the FPC.
- **ADR-092:** Parameter Maintenance for the FPC.
- **ADR-092.1:** Scheme Parameters API Reference.
- **ADR-100:** Calculator Result for the FPC.
- **ADR-100.A:** Calculator Result Output Database & API Reference.
- **ADR-100.B:** PayCal – previous year data retention (10+1 year retention policy).
- **ADR-101:** LAPCAP Data Upload Process to the FPC.
- **ADR-101.1:** LAPCAP Data Upload API Reference.
- **ADR-102:** Late Fees calculation.
- **ADR-110:** PayCal Resubmission Fees Lookup/Calculation.
- **ADR-120:** PayCal Billing File Generation Process.

### Infrastructure and integration

- **ADR-137:** RE/EX 2026 PRN and Producer Integration. Approved 28 October 2025. Implemented in RPD Release 17 (15 January 2026). Decision: Option 6 – three new timer-triggered Azure Functions interfacing with the RE/EX (RREPW) Organisation API and PRN/PERN API on CDP. Security via CDP API Gateway (AWS Cognito client-credentials). NPWD continues for 2025-year PRNs; RE/EX handles all 2026-year PRNs and PERNs from 1 February 2026.
- **ADR-142:** Azure Environment Reservations and Autoscaling. Approved. 1-year Azure Reserved Instance for Synapse Dedicated SQL Pool (DWU3000), reducing cost from ~£43k/month PAYG to ~£27k/month; CosmosDB switched to autoscaling (10%–100% of max RU/s), saving ~£12k/year; Azure SQL development instances consolidated into Elastic Pool, achieving 40–50% SQL cost reduction.
- **ADR-143:** Synapse Dedicated SQL Pool Rightsizing. Approved. Production pool upsized DWU1000 → DWU2000 (near-linear pipeline performance improvement); TST pool decommissioned (was DWU1000, zero activity); scheduled weekend downsizing to DWU200 in lower environments (DEV, PRE).

### Obligations / CSoC

- **ADR-146:** Certificates and Statements of Compliance (CSoC). **In Review — no formal decision at time of writing.** Recommended decision: Option 3 (CDP) — build all components on the Core Delivery Platform. This introduces two new frontend applications (an Obligations frontend for producers and compliance schemes, and a Regulator frontend) and a new CSoC API, all on CDP. Authentication continues via Azure B2C, with users redirected between the existing Azure portal and the new CDP components. New CSoC data is stored in the CDP API; a new Synapse pipeline extracts it to the Data Lake to support the public register. Concerns raised at the 26 March 2026 Architect Roundtable include: absence of formal Service Owner sign-off on CDP as the 3R analysis outcome; lack of objective cost/complexity comparison between Option 1 (Azure-only, quickest) and Option 3; and the risk that building in CDP now may not align with the staged migration pattern proposed by the 3R workstream.

> **[v1.2 change — ADR-146]** New Obligations/CSoC subsection added.

## 15.8 References: input products
Provide references to products used to inform this Solution Architecture Definition Document (NB these should in principle also be baselined).

## 15.9 References: derived products
Provide references to products derived wholly or partly from the solution design part of this Solution Architecture Definition Document [13, 14].

## 15.10 References: related products
Names/location of peer products that may be informed or influenced or be otherwise “useful” – e.g. test data pack, external documents, also links to “supplier” HLDs etc.

## 15.11 Governance: approval process
The associated Artefact(s) may need to be:
- Reviewed and endorsed by key stakeholders and/or the Solution Design Authority - SDA.
- (SDA is scheduled weekly for online approvals. All artefacts must be supplied 5 working days before the scheduled SDA session, so that they can be socialised for review. We can if required, also support ad hoc offline SDA approvals, if requested).

<br>

![Figure 40.0 Governance approval](./epr-sadd-images/01/figure-40.0-governance-approval.png)
Figure 40.0 Governance approval

<br>



## 15.12 Governance: quality success criteria
- **Clear, Concise and Unambiguous:** (It should go without saying that it needs to be in a language that the reader understands).
- **Accurate and Comprehensive:** (Must represent the system that has been delivered. If the information is correct, but parts of the product are not covered, the reader will not be able to achieve their goal).
- **Findable and Accessible:** (An often-overlooked aspect of quality is its usability in the context of the product. If a user can’t find the information, then it doesn’t matter how well it is constructed or how accurate it is, the objective will not be met).

Test Edit - Ignore.

[End of Document]
