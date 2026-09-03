# SC-300: Microsoft Identity and Access Administrator
## Learning Path 4: Implement access management for apps
### Module 1: Plan and design the integration of enterprise apps for SSO
### Introduction

- Wat deze module behandelt
  - Apps ontdekken binnen je omgeving
  - Access management en app management rollen ontwerpen en implementeren
  - Preintegrated (gallery) SaaS apps configureren

- Learning objectives
  - Discover apps by using Defender for Cloud Apps app discovery
  - Design and implement access management for apps
  - Design and implement app management roles
  - Configure preintegrated (gallery) SaaS apps
  - Explore application connectors and OAuth apps

- Prerequisites
  - Solide ervaring met admin centers binnen de Microsoft Cloud
  - Ervaring met het gebruik van cloud applicaties

---

### Discover apps by using Microsoft Defender for Cloud Apps and Active Directory Federation Services app report

- Basisbegrippen
  - CASB (Cloud Access Security Broker); on premises of cloud based security policy enforcement point tussen cloud consumers en cloud providers, past enterprise security polices toe bij toegang tot cloud resources
  - MDCA (Microsoft Defender for Cloud Apps); Microsoft's CASB implementatie, beschermt data/services/apps met enterprise policies, biedt aanvullende reporting en analytics

- Wat MDCA doet
  - Balans vinden tussen toegang toestaan en controle behouden bij cloud gebruik
  - Ondersteunt meerdere deployment modes: log collection, API connectors, reverse proxy
  - Rijke zichtbaarheid, controle over data travel, geavanceerde analytics tegen cyberthreats, over Microsoft en third party cloud services
  - Native integratie met Microsoft oplossingen, centraal beheer, automation
  - Cloud Discovery feature; zichtbaarheid in Shadow IT door cloud apps te ontdekken die in gebruik zijn

- Architectuur (5 onderdelen)
  - Cloud Discovery; brengt cloud omgeving en gebruikte apps in kaart
  - Sanctioning/de-authorizing van apps
  - App connectors; gebruiken provider APIs voor zichtbaarheid en governance van gekoppelde apps
  - Conditional Access App Control; real time zichtbaarheid en controle binnen cloud apps
  - Continue policy fine tuning

- Cloud Discovery
  - Gebruikt traffic logs om dynamisch cloud apps te ontdekken en analyseren
  - Snapshot report; handmatig logs van firewalls/proxies uploaden
  - Continue reports; MDCA log collectors periodiek logs laten doorsturen

- Cloud Discovery Dashboard reviewen (volgorde van aanpak)
  1. High level usage overview; algemeen beeld van cloud app gebruik
  2. Top categorieen per gebruiksparameter, incl. hoeveel daarvan sanctioned apps zijn
  3. Discovered apps tab; alle apps binnen een specifieke categorie
  4. Top users en source IP addresses; wie gebruikt cloud apps het meest
  5. App Headquarters map; geografische spreiding van discovered apps (op basis van HQ locatie)
  6. App risk overview; risk score van discovered apps, plus discovery alerts status

- Filters voor Discovered Apps (examen kernstof, herkennen niet uit hoofd leren)
  - App tag; sanctioned/unsanctioned/geen tag, custom tags mogelijk
  - Apps and domains; zoeken op specifieke app of domein
  - Categories; bv. social network, cloud storage, hosting services
  - Compliance risk factor; standaarden zoals HIPAA, ISO 27001, SOC 2, PCI-DSS
  - General risk factor; consumer popularity, datacenter locatie, etc.
  - Risk score; filteren op risico niveau, override mogelijk
  - Security risk factor; bv. encryption at rest, MFA
  - Usage; op basis van uploads/aantal users
  - Legal risk factor; regelgeving/beleid rond databescherming en privacy

- Apps sanctionen/unsanctionen
  - Via de Cloud app catalog
  - Microsoft's analisten onderhouden een catalogus van 16.000+ cloud apps, gerankt/gescoord volgens industriestandaarden
  - Scores/gewichten aanpasbaar naar eigen organisatie behoeften
  - Risk scoring gebaseerd op 80+ risk factors

- Active Directory Federation Services (AD FS)
  - Standards based on premises identity service
  - Breidt SSO uit tussen trusted business partners zonder los in te loggen per app (federation)
  - Veel organisaties hebben SaaS/custom LOB apps direct gefedereerd met AD FS, naast M365/Entra ID apps
  - Doel: 1 set access controls en policies over on premises en cloud heen

- Waarom AD FS apps migreren naar Entra ID
  - Voordelen op gebied van cost management, risk management, productivity, compliance, en governance
  - Uitdaging: bepalen welke apps compatible zijn en wat de migratiestappen zijn kost tijd
  - Sommige organisaties gebruiken alternatieve IdPs zoals SiteMinder, Oracle Access Manager, PingFederate (meestal on premises), of Okta/OneLogin (cloud)

- AD FS application activity report
  - Helpt bepalen welke apps migeerbaar zijn naar Entra ID
  - Checkt compatibiliteit, issues, en geeft guidance voor migratievoorbereiding
  - Toont AD FS apps met een actieve user login in de laatste 30 dagen
  - Toegankelijk voor: global reader/administrator, report reader, security reader, application administrator, of cloud application administrator

- 2 types apps om te migreren
  - SaaS applications; ingekocht door de organisatie
  - Line of business (LOB) applications; zelf ontwikkeld, niet bedoeld voor andere bedrijven
  - Apps met moderne protocollen (SAML, OpenID Connect) eerst migreren; via App Gallery connector of eigen app registration
  - Apps met oudere protocollen; via Application Proxy en/of Entra Domain Services

- AD FS apps ontdekken voor migratie (stappen)
  1. Azure portal, met de juiste admin rol (administrator, report reader, security reader, application administrator, of cloud application administrator)
  2. Microsoft Entra ID > Enterprise applications
  3. Activity > Usage and insights > AD FS application activity
  4. Migration status per app bekijken

- Migration status opties (examen kernstof)
  - Ready to migrate; configuratie volledig ondersteund, migreerbaar zoals hij is
  - Needs review; deels migreerbaar, sommige settings moeten gereviewd worden
  - Additional steps required; Entra ID ondersteunt bepaalde settings niet, app kan in huidige staat niet gemigreerd worden

- Onthouden voor examen
  - MDCA = Microsoft's CASB implementatie, Cloud Discovery is de kernfeature voor Shadow IT detectie
  - AD FS application activity report kijkt naar de laatste 30 dagen actieve logins
  - 3 migration statuses: Ready to migrate, Needs review, Additional steps required
  - Modern authentication apps (SAML/OIDC) migreren eerst, legacy apps via Application Proxy/Domain Services
