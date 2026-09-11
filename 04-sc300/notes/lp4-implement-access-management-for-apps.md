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

- Filters voor Discovered Apps (examen kernstof)
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
  - Uitdaging: bepalen welke apps compatilbe zijn en wat de migratiestappen zijn kost tijd
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

---

### Configure connectors to apps

- Wat app connectors doen
  - Gebruiken de APIs van app providers, voor meer zichtbaarheid en controle door MDCA over de gekoppelde apps
  - Alle communicatie tussen MDCA en connected apps is versleuteld via HTTPS
  - Elke service heeft eigen API beperkingen: throttling, API limits, dynamische time shifting windows
  - MDCA optimaliseert API gebruik binnen de toegestane capaciteit van elke service
  - Sommige operaties (bv. scannen van alle files in de tenant) vereisen veel API calls, worden dus over langere tijd gespreid. Policies kunnen dus uren of dagen duren om te draaien

- Multi instance support
  - Meerdere instances van dezelfde app connectbaar tegelijk, bv. 2 losse Salesforce instances (sales en marketing)
  - Beide beheerbaar vanuit dezelfde console, voor granulaire policies en dieper onderzoek
  - Geldt alleen voor API connected apps, niet voor Cloud Discovered apps of Proxy connected apps

- Hoe het werkt
  - MDCA draait met system admin privileges, voor volledige toegang tot alle objecten in de omgeving
  - App Connector flow:
    1. MDCA scant en bewaart authentication permissions
    2. MDCA vraagt de user list op; eerste keer kan dit even duren
    3. Na afronding: periodiek scannen van users, groups, activities, en files. Alle activiteiten pas volledig beschikbaar na de eerste volledige scan
  - Duur van connecties hangt af van tenant grootte, aantal users, en omvang/aantal files om te scannen

- Wat een API connectie mogelijk maakt (afhankelijk van de app, examen kernstof)
  - Account information; zichtbaarheid in users, accounts, profile info, status (suspended/active/disabled), groups, privileges
  - Audit trail; zichtbaarheid in user activities, admin activities, sign in activities
  - Account governance; users suspenden, passwords revoken, etc.
  - App permissions; zichtbaarheid in uitgegeven tokens en hun permissions
  - App permission governance; tokens verwijderen
  - Data scan; scannen van unstructured data, periodiek (elke 12 uur) en real time (getriggerd bij elke gedetecteerde wijziging)
  - Data governance; files quarantainen (incl. in trash), files overwriten

- Onthouden voor examen
  - Multi instance support werkt alleen bij API connected apps, niet bij Cloud Discovery of Proxy connected apps
  - Data scan gebeurt op 2 manieren: elke 12 uur periodiek, en real time bij gedetecteerde wijzigingen
  - MDCA gebruikt system admin privileges voor volledige zichtbaarheid, geen losse permissions per functie

---

### Exercise: Implement Access Management for Apps
  - [04-sc300/labs/20-implement-access-management-for-apps](../../04-sc300/labs/20-implement-access-management-for-apps.md)

---

### Design and implement app management roles

- 4 manieren om app creation/management te delegeren
  - Beperken wie apps mag maken/beheren
  - Owner(s) toewijzen aan een applicatie
  - Built-in admin role toewijzen die toegang geeft over alle applicaties
  - Custom role maken met specifieke permissions, toewijsbaar op single app scope (limited owner) of directory scope (limited administrator)

- Waarom delegeren
  - Vermindert de overhead voor Global Administrators
  - Least privilege verbetert security posture, minder kans op unauthorized access

- Wie mag apps aanmaken beperken
  - Default: alle users mogen application registrations aanmaken/beheren, en mogen consent geven voor apps die company data benaderen namens hen
  - Instelbaar via Global Administrator:
    - User settings; "Users can register applications" op No
    - Enterprise applications user settings; Gallery Apps toevoegen aan My App, Office 365 apps in het Office portal
    - Consent and Permissions settings; "Users can consent to applications accessing company data on their behalf" op No

- Individuele permissions teruggeven als default is uitgeschakeld
  - Application Developer role toewijzen; geeft het recht om application registrations aan te maken en eigen consent te geven
  - Zodra iemand een nieuwe app registration aanmaakt, wordt die persoon automatisch de eerste owner

- Application owners toewijzen
  - Simpele manier om iemand volledige controle te geven over een specifieke app registration/enterprise application
  - Automatisch: eerste maker = eerste owner
  - Originele owner kan verwijderd worden, extra owners toevoegbaar

- Enterprise application owners specifiek
  - Kan organisatie specifieke configuratie beheren: SSO config, provisioning, user assignments
  - Kan andere owners toevoegen/verwijderen
  - Anders dan Global Administrator: owner kan alleen de apps beheren die hij zelf bezit
  - Bij gallery apps met zowel enterprise app als app registration: owner toevoegen aan de enterprise app voegt automatisch ook owner toe aan de bijbehorende app registration

- Owner toewijzen aan een enterprise app (stappen)
  1. Application Administrator of Cloud Application Administrator
  2. App registrations pagina, app selecteren, Overview
  3. Owners > lijst bekijken
  4. Add, 1 of meer owners toevoegen

- Belangrijk over owners (examen kernstof)
  - Users en service principals kunnen owner zijn van app registrations
  - Alleen users kunnen owner zijn van enterprise applications
  - Groups kunnen nooit als owner toegewezen worden, bij geen van beide
  - Risico: owner kan credentials toevoegen aan de app en die gebruiken om de app's identity te impersoneren. De app kan meer permissions hebben dan de owner zelf, dus dit is een vorm van elevation of privilege

- Built-in application admin rollen (examen kernstof)
  - Application Administrator; volledig beheer van enterprise apps, app registrations, en application proxy settings. Kan consent geven voor delegated en application permissions, behalve Microsoft Graph. Wordt niet automatisch owner bij het aanmaken van nieuwe apps
  - Cloud Application Administrator; zelfde als Application Administrator, behalve geen application proxy beheer. Ook geen automatische owner status
  - Belangrijk: beide rollen kunnen credentials toevoegen en de app impersoneren, wat een elevation of privilege risico geeft. Geen van beide rollen geeft toegang om Conditional Access te beheren

- Custom role aanmaken en toewijzen, 2 losse stappen
  1. Custom role definition aanmaken, permissions toevoegen uit een preset lijst (dezelfde permissions als in built-in roles)
  2. Role assignment aanmaken om de custom role toe te wijzen
  - Voordeel van deze scheiding: 1 role definition kan meerdere keren op verschillende scopes toegewezen worden (bv. organization wide voor persoon A, en slechts 1 specifieke app voor persoon B)

- Tips bij custom roles voor app management (examen kernstof)
  - Werken alleen in het huidige app registration scherm van het Entra admin center, niet in het legacy scherm
  - Geven geen toegang tot het Entra ID portal als "Restrict access to Microsoft Entra ID administration portal" op Yes staat
  - Role assignments voor apps waar de user toegang tot heeft verschijnen alleen onder de All applications tab, niet onder Owned applications

- Onthouden voor examen
  - Owner ≠ built-in admin role: owner beheert alleen eigen apps, Application/Cloud Application Administrator beheert alle apps in de tenant
  - Groups kunnen nooit owner zijn, alleen users (en bij app registrations ook service principals)
  - Owners en de 2 built-in app admin rollen kunnen allebei de app impersoneren via credentials, wat een bekend elevation of privilege risico is
  - Custom roles werken alleen in de moderne app registration UI, niet legacy

---

### Exercise: Implement Access Management for Apps
  - [04-sc300/labs/21-exercise-create-a-custom-role-to-manage-app-registration](../../04-sc300/labs/21-exercise-create-a-custom-role-to-manage-app-registration.md)

---

### Configure preintegrated gallery SaaS apps

- Wat de gallery is
  - Entra ID heeft een gallery met duizenden pre integrated applicaties
  - Veel apps die een organisatie gebruikt staan waarschijnlijk al in de gallery
  - Eenmaal toegevoegd: properties configureerbaar, user access beheerbaar, SSO instelbaar zodat users inloggen met hun Entra credentials

- App properties configureren (stappen)
  1. Identity > Enterprise applications, gewenste app zoeken/selecteren
  2. Manage > Properties
  3. Beschikbare opties bekijken, hangt af van hoe de app is geintegreerd
     - SAML based SSO app; heeft velden zoals User access URL
     - OIDC based SSO app; heeft dit veld niet
     - Apps toegevoegd via App registrations; standaard OIDC based
     - Apps toegevoegd via Enterprise applications; kunnen elke SSO standaard gebruiken
  4. Save

- 3 velden die altijd beschikbaar zijn (examen kernstof)
  - Enabled for users to sign in?; bepaalt of toegewezen users kunnen inloggen
  - User assignment required?; bepaalt of ook niet toegewezen users kunnen inloggen
  - Visible to users?; bepaalt of toegewezen users de app zien in My Apps en de M365 app launcher (waffle menu)

- Custom logo instellen (stappen)
  1. Logo maken van 215 bij 215 pixels, .png formaat
  2. Enterprise applications > app selecteren > Manage > Properties
  3. Icoon selecteren om logo te uploaden
  4. Save

- Notes toevoegen
  - Notes veld gebruiken voor relevante management informatie over de app
  - Enterprise applications > app selecteren > Manage > Properties > Notes veld bijwerken > Save

- Onthouden voor examen
  - Enabled for users to sign in, User assignment required, en Visible to users zijn de 3 kernvelden die op elke app van toepassing zijn, ongeacht SSO type
  - App registrations = default OIDC, Enterprise applications = elke SSO standaard mogelijk
  - Logo formaat vereiste: 215x215 pixels, .png

---

### Implement and manage policies for OAuth apps

- Wat het is
  - Naast handmatig onderzoeken van gekoppelde OAuth apps, kun je permission policies instellen voor automatische notificaties
  - Voorbeeld trigger: apps die een hoge permission level vereisen en door meer dan 50 users geautoriseerd zijn
  - OAuth app policies laten je zien welke permissions elke app heeft aangevraagd, en welke users die hebben geautoriseerd voor Office 365 en andere OAuth apps
  - Permissions kunnen gemarkeerd worden als approved of banned; banned schakelt de bijbehorende Enterprise Application uit

- Nieuwe OAuth app policy aanmaken (stappen)
  1. Microsoft Defender for Cloud Apps openen (security.microsoft.com)
  2. Menu links > Cloud apps sectie > OAuth apps
  3. Apps filteren naar behoefte, bv. alle apps die permission vragen om calendars in je mailbox aan te passen
  4. New policy from search button selecteren

- Extra filter opties
  - Community use filter; laat zien of een bepaalde app-permission gangbaar, ongebruikelijk, of zeldzaam is onder andere organisaties. Handig bij een zeldzame app die hoge severity permissions vraagt of van veel users toestemming vraagt
  - Policy instellen op basis van group membership van de users die de app hebben geautoriseerd; bv. alleen uncommon apps met high permissions intrekken als de autoriserende user in de Administrators group zit

- Alternatieve manier om de policy aan te maken
  - Control > Policies > Create policy > OAuth app policy

- Onthouden voor examen
  - Banned permission = de gekoppelde Enterprise Application wordt uitgeschakeld, niet alleen de specifieke permission
  - Community use filter is bedoeld om zeldzame, risicovolle app permission combinaties op te sporen
  - Policies kunnen gescoped worden op basis van group membership van de autoriserende user, niet alleen op de app zelf
 
---

## Module Assessment — Module 1 (Plan and design the integration of enterprise apps for SSO)

**Score:** 100%

### Vraag 1
What is Microsoft's Cloud Access Security Broker solution?

- Microsoft Cloud Computing Services
- ✅ Microsoft Defender for Cloud Apps
- Microsoft Security Center

### Vraag 2
By default, who has the ability to create application registrations or consent to applications in Microsoft Entra ID?

- ✅ All Microsoft Entra Users
- All Microsoft Entra and Guest users
- Only users assigned the Global Administrator role

### Vraag 3
Which statement best describes the Cloud Application Administrator role?

- Users in this role have the same permissions as the Application Management role, excluding the ability to manage application proxy. Users assigned to this role are not added as owners when creating new application registrations or enterprise applications.
- Users in this role have the same permissions as the Site Administrator role, including the ability to manage application proxy.
- ✅ Users in this role have the same permissions as the Application Administrator role, excluding the ability to manage application proxy. Users assigned to this role are not added as owners when creating new application registrations or enterprise applications.

---





















  
