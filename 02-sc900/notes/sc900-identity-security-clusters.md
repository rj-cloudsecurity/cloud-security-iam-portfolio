# SC-900: Identity & Security Clusters

Dit document bundelt de belangrijkste Microsoft securityproducten en Entra-functies in duidelijke clusters. Veel diensten hebben overlappende namen en vergelijkbare rollen, waardoor ze lastig te onderscheiden zijn. Door ze te groeperen op functie binnen identity, access, governance en threat protection ontstaat een helder en snel te onthouden overzicht dat helpt bij het herkennen van examenvragen.

Deze clusters sluiten goed aan bij een manier van leren die draait om verbanden leggen in plaats van losse definities onthouden, waardoor de structuur van Microsoft-securitydiensten veel sneller blijft hangen.

---

## Identity & Access

### Identity Protection
- Detecteert risky sign-ins en risky users
- Gebruikt risk signals zoals leaked credentials, unfamiliar sign-ins en malware-linked IPs
- Kan automatisch risk-based policies activeren (bijv. require MFA, block access)

### Conditional Access
- Voert policies uit op basis van signalen
- Werkt volgens het principe If this → then that
- Gebruikt signalen zoals user, device, location, app en risk
- Kan legacy authentication blokkeren
- Vormt de policy-engine van Microsoft Entra ID

### Privileged Identity Management (PIM)
- Biedt tijdelijke adminrechten (Just-in-Time)
- Ondersteunt approval workflows
- Houdt audit logs bij voor privileged access
- Voorkomt permanente adminrollen

### Access Reviews
- Controleert periodiek of toegang nog nodig is
- Gericht op guest users, groepen en applicaties
- Onderdeel van Identity Governance

### Access Packages
- Bundelen toegang voor onboarding
- Combineren apps, groepen en rollen
- Onderdeel van Entitlement Management

### Identity Models
- **Password Hash Sync (PHS)** — synchroniseert wachtwoordhash naar Entra ID
- **Pass-Through Authentication (PTA)** — on-premises AD valideert wachtwoorden
- **Federation (ADFS)** — externe identity provider verzorgt authenticatie

---

## Network Security (Azure Infrastructure)

### Azure DDoS Protection
- Beschermt op **layer 3 & 4** tegen volumetric, protocol en resource layer aanvallen
- Always-on monitoring en adaptive tuning
- Twee tiers: **DDoS Network Protection** (uitgebreid) en **DDoS IP Protection** (pay-per-IP)
- Standaard Azure infrastructuurbescherming biedt geen telemetry of alerting

### Azure Firewall
- Centralized, stateful **firewall-as-a-service**
- Filtering op netwerk- én applicatieniveau via FQDNs
- Threat intelligence feed, SNAT/DNAT, logging via Azure Monitor
- Drie SKUs: Standard, Premium en Basic

### Web Application Firewall (WAF)
- Beschermt web applicaties op **layer 7** (application layer)
- Beschermt tegen HTTP Floods en andere application-layer DDoS aanvallen
- Gecentraliseerde patching in plaats van per applicatie

### Network Security Groups (NSGs)
- Filterregels op subnet- en VM-niveau op basis van prioriteit
- Regels geëvalueerd op source, source port, destination, destination port en protocol
- Standaard regels kunnen niet verwijderd worden, wel overschreven
- Complementair aan Azure Firewall

| | **NSG** | **Azure Firewall** |
|---|---|---|
| Type | Distributed filtering | Centralized firewall-as-a-service |
| Scope | Binnen één subscription/VNet | Meerdere subscriptions en VNets |
| Bescherming | Network layer | Network én application level |

### Azure Virtual Network (VNet) & Network Segmentation
- Fundamentele bouwsteen voor privénetwerken in Azure
- Ondersteunt **Zero Trust** via subnets en isolatie
- Standaard geen verkeer tussen VNets; communicatie moet expliciet worden ingesteld

### Azure Bastion
- Veilige **RDP (Remote Desktop Protocol)** en **SSH (Secure Shell)** toegang tot VMs via de Azure portal
- Geen public IP, geen open poorten, geen NSG beheer nodig
- Deployment per virtual network; werkt ook voor peered VNets
- Verbinding via **TLS (Transport Layer Security)**

### Azure Key Vault
- Centraal beheer van secrets, encryptiesleutels en SSL/TLS certificaten
- Twee tiers: **Standard** (software encryptie) en **Premium** (HSM-beschermd)
- Toegangscontrole via Microsoft Entra en Azure RBAC
- Microsoft heeft zelf geen toegang tot jouw data

---

## Cloud Security

### Microsoft Defender for Cloud (CNAPP)
- **Cloud Security Posture Management (CSPM)** — zichtbaarheid, hardening en secure score
- **Cloud Workload Protection (CWPP)** — threat protection voor servers, containers, databases
- **DevSecOps** — security integreren in development pipelines via Defender for DevOps
- Aanbevelingen gebaseerd op **MCSB (Microsoft Cloud Security Benchmark)**
- Foundational CSPM is gratis; Defender CSPM plan is betaald

### Microsoft Security Exposure Management
- Unified view van security posture via de **Enterprise Exposure Graph**
- Genereert automatisch **attack paths** en identificeert **choke points**
- Classificeert **critical assets** zoals domain controllers en privileged accounts
- Drie Secure Scores naast elkaar: **Microsoft Secure Score**, **Cloud Secure Score** en domain-specific scores

---

## Threat Detection & Response

### Microsoft Sentinel (SIEM/SOAR)
- **SIEM** — verzamelen, detecteren en analyseren van security data
- **SOAR** — automatisch reageren via playbooks (Azure Logic Apps)
- Detectie via Analytics, MITRE ATT&CK coverage, watchlists en workbooks
- Onderzoek via incidents, hunts en Jupyter notebooks
- Genormaliseerde data via **ASIM**

### Microsoft Defender XDR
- Enterprise defense suite die threat signals centraliseert vanuit endpoints, email, identiteiten en cloud apps
- Alles zichtbaar in het **Microsoft Defender portal**

| **Product** | **Beschermt** |
|---|---|
| Defender for Endpoint | Laptops, telefoons, tablets, PCs (EDR, AIR, Attack Surface Reduction) |
| Defender for Office 365 | Email, links, bijlagen, SharePoint, Teams (Safe Attachments, Safe Links, ZAP) |
| Defender for Identity | On-premises Active Directory (lateral movement, privilege escalation) |
| Defender for Cloud Apps | SaaS applicaties als CASB (shadow IT, SSPM, OAuth governance) |
| Defender Vulnerability Management | CVEs, misconfigurations, software inventory op endpoints |
| Defender Threat Intelligence (TI) | Threat actors, IOCs, CVEs via Intel Profiles en Intel Explorer |

### Microsoft Security Copilot
- AI-powered security tool gebouwd op Azure OpenAI Service
- Beschikbaar als **standalone** en **embedded** in Defender XDR, Sentinel, Defender for Cloud
- Verwerkt prompts via de **orchestrator**; capacity gemeten in **SCUs**
- Effectieve prompt: **Goal, Context, Expectations, Source**
- Copilot gaat nooit verder dan de toegangsrechten van de gebruiker

---

## Governance & Compliance

### Secure Score
- Numerieke meting van security posture
- Hogere score = betere bescherming
- Verbetert alleen als alle aanbevelingen binnen één security control zijn opgelost

### Compliance Manager
- Assessments, regulatory compliance en verbeteracties

### Data Concepts
- **Data Minimization** — alleen data verzamelen die noodzakelijk is
- **Data Residency / Sovereignty** — waar data staat en wie erover mag beslissen

---

## Data Security & Compliance (Microsoft Purview)

### Microsoft Priva
- **Privacy Risk Management** — detecteert en remedieert data overexposure, data transfers en data minimization risico's
- **Subject Rights Requests (DSR/DSAR)** — beheert verzoeken van individuen om hun persoonlijke data in te zien of te beheren

### Data Classification
- **SITs (Sensitive Information Types)** — patroonherkenning voor gevoelige data zoals creditcardnummers en BSN
- **Trainable Classifiers** — AI/ML classificatie op basis van wat content is; pre-trained of custom via seeding
- Inzichten via **Content Explorer** (snapshot) en **Activity Explorer** (gebruikersacties)

### Sensitivity Labels
- Customizable, persistent labels die meereizen met content
- Kunnen encryptie, content markings en auto-labeling toepassen
- Gepubliceerd via **label policies**; gerespecteerd door Microsoft 365 Copilot
- Vier scopes: Files, Emails, Meetings en Groups & Sites

### Data Loss Prevention (DLP)
- Beschermt gevoelige data via deep content analysis across Microsoft 365, endpoints en AI interacties
- Protective actions: policy tip, block met/zonder override, quarantine
- **Endpoint DLP** — monitort activiteiten op Windows en macOS
- **Alert Triage Agent** via Security Copilot

### Adaptive Protection
- Koppelt insider risk levels aan DLP, Data Lifecycle Management en Conditional Access
- Drie niveaus: **Elevated** (sterkste controls), **Moderate** en **Minor** (policy tips)
- Controls worden automatisch aangepast op basis van gedrag

### Insider Risk Management
- Detecteert interne risico's zoals data theft, leaks en security policy violations
- Workflow: Policies → Alerts → Triage → Investigate → Action
- Integreert met **Adaptive Protection**, **Communication Compliance** en **eDiscovery**

### Data Security Posture Management (DSPM)
- Unified view van data security landscape; beantwoordt wie, wat, waar en hoe
- **AI observability** — monitort AI apps en agents op oversharing en exfiltration
- One-click policies via **Objectives**; integreert met DLP en Insider Risk Management

### Data Security Investigations
- AI-powered onderzoeksoplossing voor data breaches en insider leaks
- Drie AI capabilities: **vector search**, **categorization** en **examination**
- Pay-as-you-go billing

---

## Compliance & Governance (Microsoft Purview)

### Compliance Manager
- Beoordeelt compliance via **controls**, **assessments**, **regulations** (360+ templates) en **improvement actions**
- **Compliance score** = your points + Microsoft-managed points

### Communication Compliance
- Detecteert ongepaste berichten in Teams, Outlook, WhatsApp en AI interacties
- Workflow: Configure → Investigate → Remediate → Maintain

### eDiscovery
- Identificeert en levert elektronisch bewijs voor juridische zaken
- Premium features: review sets, OCR, conversation threading en decryption
- Integreert met Insider Risk Management en Security Copilot

### Audit
- **Standard** — 180 dagen retentie, duizenden doorzoekbare events
- **Premium** — tot 10 jaar retentie, intelligent insights, higher bandwidth

### Data Lifecycle Management
- **Retention policies** — site/mailbox niveau; instellingen reizen niet mee buiten container
- **Retention labels** — item niveau; reizen wel mee binnen Microsoft 365 tenant
- Ondersteunt **Adaptive Protection** en retentie van AI interacties

### Records Management
- High-value items beheren als **records** of **regulatory records**
- **Regulatory records** kunnen niet verwijderd worden, zelfs niet door Global Admin
- Ondersteunt **event-based retention**, **disposition reviews** en **file plan**

---

## Data Governance (Microsoft Purview Data Catalog)

### Data Catalog Kernconcepten
- **Governance domains** — organiseren data estate via business concepten zoals Finance of HR
- **Data products** — bundelen gerelateerde data assets met context en use cases
- **Glossary terms** — business begrippen met policies per governance domain
- **CDEs (Critical Data Elements)** — groeperen belangrijke data-elementen voor standaardisatie
- **OKRs** — koppelen data products aan zakelijke doelstellingen

### Data Governance Rollen
- **Data consumers** — vinden en gebruiken data
- **Data owners** — beheren kwaliteit en toegang
- **Data stewards** — borgen governance en vindbaarheid
- **Central data office** — stellen policies vast
