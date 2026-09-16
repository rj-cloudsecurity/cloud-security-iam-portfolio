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

## Learning Path 4: Implement access management for apps
### Module 2: Implement and monitor the integration of enterprise apps for SSO

### Introduction

- Wat deze module behandelt
  - Token customizations implementeren
  - Consent settings configureren
  - On premises apps integreren via Microsoft Entra application proxy
  - Custom SaaS apps integreren voor SSO
  - Application user provisioning implementeren
  - Application collections aanmaken en beheren
  - Access naar Entra ID integrated enterprise applications monitoren en auditen

- Learning objectives
  - Implement token customizations
  - Implement and configure consent settings
  - Integrate on-premises apps by using Microsoft Entra application proxy
  - Integrate custom SaaS apps for SSO
  - Implement application user provisioning
  - Create and manage application collections
  - Monitor and audit acess to Microsoft Entra ID integrated enterprise applications

- Prerequisites
  - Ervaring met het beheren van users en administrators in Entra ID
  - Ervaring met het opzetten van Conditional Access

---

### Implement token customizations

- Wat je kunt instellen
  - Lifetime van tokens uitgegeven door het Microsoft identity platform
  - Instelbaar voor: alle apps in de organisatie, een multitenant applicatie, of een specifieke service principal
  - Policy object; representeert een set regels, afgedwongen op individuele apps of alle apps in de organisatie
  - Policy kan als default voor de hele organisatie ingesteld worden, of aan specifieke apps toegewezen worden
  - Default policy geldt overal, tenzij overschreven door een policy met hogere prioriteit

- Authentication session management via Conditional Access (herhaling)
  - Relevant bij: unmanaged/shared device toegang, gevoelige info vanaf extern netwerk, high impact users, kritieke business apps
  - Conditional Access controls laten policies maken voor specifieke use cases zonder alle users te raken

- Token customization opties (examen kernstof)

| Instelling | Wat het doet |
|---|---|
| Access and ID token lifetime | Levensduur van de OAuth 2.0 bearer token en ID token |
| Refresh token lifetime (days) | Maximale periode voordat een refresh token gebruikt kan worden om een nieuwe access token te krijgen |
| Refresh token sliding window lifetime | Het type sliding window voor de refresh token |
| Lifetime length (days) | Na deze periode moet de user opnieuw authenticaten |

- Optional claims configureren
  - Developers kunnen optional claims gebruiken om te bepalen welke claims ze in tokens voor hun app willen
  - Gebruik: andere claims toevoegen, gedrag van bestaande claims aanpassen, custom claims toevoegen
  - Werkt bij v1.0, v2.0, en SAML tokens, maar levert de meeste waarde bij de overstap van v1.0 naar v2.0
  - Reden: v2.0 tokens zijn bewust kleiner voor betere performance, dus sommige claims die vroeger standaard in v1.0 tokens zaten moeten nu per applicatie specifiek aangevraagd worden

- Onthouden voor examen
  - Token lifetime policies kunnen op 3 niveaus toegepast worden: alle apps, multitenant app, of specifieke service principal
  - Default policy geldt overal tenzij een specifiekere, hoger geprioriteerde policy die overschrijft
  - v2.0 tokens zijn kleiner dan v1.0, optional claims zijn nodig om ontbrekende claims alsnog toe te voegen

---

### Implement and configure consent settings

- Context
  - Apps integreren met het Microsoft identity platform, zodat users met werk/school account inloggen en de app organisatiedata kan gebruiken
  - Voordat een app data mag benaderen, moet een user consent geven
  - Default: users kunnen consent geven voor permissions die geen admin consent vereisen (bv. toegang tot eigen mailbox), maar niet voor permissios met breed bereik (bv. alle files in de organisatie lezen/schrijven)
  - Risico: als dit niet gemonitord/gecontroleerd wordt, kunnen users misleid worden om kwaadaardige apps toegang te geven
  - Aanbevolen: user consent alleen toestaan voor apps van een verified publisher

- User consent settings, 4 opties (examen kernstof)
  - Disable user consent; users kunnen geen nieuwe permissions/apps consenten. Bestaande consents blijven werken. Alleen users met een directory role die consent-permission bevat kunnen nog nieuwe apps consenten
  - Users can consent to apps from verified publishers or your organization, but only for permissions you choose; alleen apps van verified publisher of uit eigen tenant, en alleen permissions die als low impact geclassificeerd zijn
  - Users can consent to all apps; alle users mogen consenten voor elke permission die geen admin consent vereist
  - Custom app consent policy; eigen policy maken met specifiekere condities

- Risk-based step-up consent
  - Vermindert blootstelling aan malicious apps met illegitieme consent requests
  - Standaard enabled, heeft alleen effect als user consent uberhaupt enabled is
  - Bij gedetecteerd risky consent request: vereist step-up naar admin consent i.p.v. normale user consent
  - Met admin consent request workflow enabled: user kan de request direct vanuit het consent scherm doorsturen naar een admin
  - Zonder die workflow: foutmelding AADSTS90094, user moet zelf een admin vragen om de app goed te keuren
  - Risky detection wordt gelogd als audit event: Category ApplicationManagement, Activity Type Consent to application, Status Reason Risky application detected

- Onthouden voor examen
  - 4 user consent opties: Disable, Verified publishers only (low impact permissions), All apps, Custom policy
  - Risk-based step-up consent is default aan, maar heeft alleen effect als user consent zelf ook aan staat
  - AADSTS90094 is de specifieke foutcode die verschijnt als een user een permission probeert te consenten die admin consent vereist

---

### Integrate on-premises apps with Microsoft Entra application proxy

- Wat het is
  - Feature van Entra ID, geeft remote clients toegang tot on premises web applicaties
  - Bestaat uit 2 delen: Application Proxy service (in de cloud) en Application Proxy connector (draait op een on premises server)
  - Samen geven ze het user sign on token veilig door van Entra ID naar de on premises web applicatie

- Wat het biedt
  - Secure remote access tot on premises web apps
  - Na 1x SSO bij Entra ID: toegang tot zowel cloud als on premises apps via externe URL of intern applicatie portal
  - Voorbeelden: Remote Desktop, SharePoint, Teams, Tableau, Qlik, en line of business (LOB) applicaties

- Waar Application Proxy mee werkt (examen kernstof)
  - Web apps met Integrated Windows Authentication
  - Web apps met form based of header based access
  - Web APIs die naar rich apps op verschillende devices worden geexposed
  - Apps achter een Remote Desktop Gateway
  - Rich client apps geintegreerd met Microsoft Authentication Library (MSAL)

- Waarvoor aanbevolen, en waarvoor niet
  - Aanbevolen voor remote users die toegang nodig hebben tot interne resources
  - Vervangt de noodzaak van een VPN of reverse proxy
  - Niet bedoeld voor interne users op het corporate netwerk; onnodig gebruik door interne users kan onverwachte performance problemen veroorzaken

- Hoe Application Proxy werkt (stappen, examen kernstof)
  1. User benadert de app via een endpoint, wordt doorgestuurd naar de Entra sign in pagina
  2. Na succesvolle sign in stuurt Entra ID een token naar het client device
  3. Client stuurt het token naar de Application Proxy service, die UPN en SPN uit het token haalt, en het verzoek doorstuurt naar de Application Proxy connector
  4. Bij geconfigureerde SSO: de connector voert eventuele extra authenticatie uit namens de user
  5. Connector stuurt het verzoek naar de on premises applicatie
  6. Response gaat terug via de connector en Application Proxy service naar de user

- Onthouden voor examen
  - Application Proxy = cloud service + on premises connector samen, niet 1 los onderdeel
  - Vervangt VPN/reverse proxy specifiek voor remote toegang, niet bedoeld voor interne netwerkgebruikers
  - De flow gebruikt zowel UPN (user identity) als SPN (service identity), zelfde concept als je eerder zag bij de Kerberos/KCD flow
  - Werkt met meerdere auth types: Integrated Windows Authentication, form/header based, en MSAL geintegreerde apps

---

### Integrate custom SaaS apps for single sign-on

- Wat mogelijk is
  - Entra ID als identity systeem voor bijna elke app
  - Veel apps staan al vooraf geconfigureerd in de App Gallery, minimale setup nodig
  - Apps die niet in de gallery staan: handmatig configureerbaar voor SSO, via SAML-based of OIDC-based SSO

- Waarom delegeren aan een centrale identity provider
  - Apps hoeven zelf geen username/password beheer meer te doen, dat delegeren ze aan Entra ID
  - Maakt scenario's mogelijk zoals Conditional Access (locatie vereisten, MFA vereisten)
  - SSO; 1x inloggen, automatisch ingelogd bij alle apps die dezelfde centrale directory delen

- Microsoft identity platform
  - Biedt identity as a service voor developers, ondersteunt industry standard protocollen: OAuth 2.0 en OpenID Connect
  - Open source libraries beschikbaar voor verschillende platforms
  - Laat developers apps bouwen die met elke Microsoft identity kunnen inloggen, en tokens krijgen voor Microsoft Graph, andere Microsoft APIs, of eigen APIs

- Protocol vergelijkingen (examen kernstof)
  - OAuth vs OpenID Connect (OIDC); OAuth is voor authorization, OIDC is voor authentication. OIDC is gebouwd op OAuth 2.0, vergelijkbare terminologie/flow. Je kunt in 1 request zowel authenticaten via OIDC als autoriseren via OAuth 2.0
  - OAuth vs SAML; OAuth is voor authorization, SAML is voor authentication
  - OIDC vs SAML; beide zijn voor authentication en maken SSO mogelijk. SAML wordt vaak gebruikt met IdPs zoals AD FS gefedereerd met Entra ID, dus vaker in enterprise apps. OIDC wordt vaker gebruikt bij pure cloud apps: mobile apps, websites, web APIs

- Onthouden voor examen
  - OAuth = authorization protocol, OIDC en SAML = authentication protocollen
  - OIDC is gebouwd op OAuth 2.0, dus die twee combineren makkelijk in 1 flow
  - SAML past beter bij enterprise/gefedereerde scenario's (bv. met AD FS), OIDC past beter bij moderne cloud only apps

---

### Implement application-based user provisioning

- Wat app provisioning is
  - Automatisch aanmaken van user identities en roles in cloud (SaaS) applicaties die users nodig hebben
  - Bevat ook: onderhoud en verwijdering van identities zodra status/rol verandert
  - Voorbeeld: een Entra user automatisch provisionen in Dropbox, Salesforce, ServiceNow, etc.

- Wat provisioning mogelijk maakt (examen kernstof)
  - Automate provisioning; nieuwe accounts automatisch aanmaken bij het aannemen van nieuwe mensen
  - Automate deprovisioning; accounts automatisch deactiveren bij vertrek
  - Synchronize data; identities in apps/systemen actueel houden op basis van wijzigingen in de directory of het HR systeem
  - Provision groups; groups provisionen naar apps die dat ondersteunen
  - Govern accesss; monitoren en auditen wie geprovisioned is
  - Brown field deployment; bestaande identities matchen tussen systemen, ook als users al bestaan in het doelsysteem
  - Rich customization; attribute mappings aanpasbaar om te bepalen welke user data van source naar target systeem stroomt
  - Alerts; provisioning service geeft alerts bij kritieke events, Log Analytics integratie mogelijk voor custom alerts

- Manual vs automatic provisioning
  - Manual; geen automatische Entra provisioning connector beschikbaar, accounts handmatig aanmaken (bv. direct in het admin portal van de app, of via een spreadsheet upload)
  - Automatic; een Entra provisioning connector bestaat al voor de app, setup tutorial volgen
  - Apps met automatic provisioning support hebben een Provisioning icoon in de gallery, ook zichtbaar op de Provisioning tab nadat de app is toegevoegd

- System for Cross-domain Identity Management (SCIM)
  - Probleem dat het oplost: elke app implementeert dezelfde basisacties (users aanmaken/updaten, aan groups toevoegen, deprovisionen) net iets anders, met andere endpoints/methodes/schema's
  - SCIM biedt een gemeenschappelijk user schema om users in/uit/rond apps te bewegen
  - Wordt de standaard voor provisioning; in combinatie met federation standards (SAML, OIDC) geeft dit een end to end, standards based oplossing voor access management

- SCIM technisch (examen kernstof)
  - Standaard definitie van 2 endpoints: /Users en /Groups
  - Gebruikt standaard REST verbs om objecten te maken/updaten/verwijderen
  - Voorgedefinieerd schema voor gemeenschappelijke attributes: group name, username, first name, last name, email
  - Apps met een SCIM 2.0 REST API verminderen/elimineren de pijn van een eigen, proprietary user management API
  - Voorbeeld: elke SCIM compliant client weet hoe een HTTP POST van een JSON object naar /Users te doen om een nieuwe user aan te maken
  - Developers die een SCIM endpoint bouwen kunnen integreren met elke SCIM compliant client zonder custom werk, en kunnen open source SCIM libraries gebruiken in plaats van alles zelf te bouwen

- Onthouden voor examen
  - SCIM 2.0 heeft altijd de 2 endpoints /Users en /Groups
  - Automatic provisioning vereist een bestaande Entra provisioning connector, herkenbaar aan het Provisioning icoon in de gallery
  - SCIM + SAML/OIDC samen = end to end, standards based access management oplossing
  - Provisioning omvat niet alleen aanmaken, maar ook synchronisatie en deprovisioning gedurende de hele identity lifecycle

---

### Monitor and audit access to Microsoft Entra integrated enterprise applications

- Usage and insights report
  - Application centric view van sign in data
  - Beantwoordt vragen zoals: top gebruikte applicaties, applicaties met meeste failed sign ins, top sign in errors per applicatie

- Toegang tot het report (stappen)
  1. Entra admin center
  2. Identity > Applications > Enterprise applications
  3. Activity sectie > Usage & insights

- Gebruik van het report
  - Toont lijst van applicaties met 1 of meer sign in poging(en), sorteerbaar op successful sign ins, failed sign ins, en success rate
  - Load more om meer applicaties te zien, date range instelbaar
  - Focus op 1 specifieke app mogelijk: view sign-in activity toont sign in activiteit over tijd plus top errors
  - Selecteren van een dag in de usage graph geeft gedetailleerde lijst van sign in activiteiten die dag

- Audit logs
  - Bevatten records van system activities, voor compliance
  - Toegankelijk voor rollen: Security Administrator, Security Reader, Report Reader, Global Reader, of Administrator
  - Te vinden via: Monitoring sectie > Audit logs

- Standaard velden in de audit log list view (examen kernstof)
  - Datum en tijd van de gebeurtenis
  - Service die de gebeurtenis heeft gelogd
  - Category en Activity name (wat er is gebeurd)
  - Status van de activiteit (success/failure)
  - Target
  - Initiator/actor (wie de activiteit heeft uitgevoerd)
  - Kolommen aanpasbaar via Columns in de toolbar
  - Item selecteren geeft meer gedetailleerde info

- Enterprise applications audit logs
  - Application based audit reports beantwoorden vragen zoals: welke apps toegevoegd/geupdatet/verwijderd zijn, of een service principal is gewijzigd, of app namen zijn gewijzigd, wie consent heeft gegeven aan een app
  - Te vinden via: Activity sectie > Audit logs op het Enterprise applications scherm, met Application Type al voorgeselecteerd op Enterprise applications

- Onthouden voor examen
  - Usage & insights report = focus op sign in gedrag en errors per app
  - Audit logs (algemeen) = bredere systeemactiviteit, met wie/wat/wanneer/status/target
  - Enterprise applications audit logs = specifiek gefilterd op app gerelateerde wijzigingen (toevoegen, verwijderen, consent geven, etc.)
  - Minimale rol vereist voor audit logs: Report Reader (of hoger: Security Reader/Administrator/Global Reader)
 
---

### Create and manage application collections

- Wat een collection is
  - My Apps portal toont standaard alle apps waar een user toegang tot heeft op 1 pagina
  - Collections groeperen gerelateerde apps (bv. per rol, taak, project) op een eigen tab, voor overzicht
  - Werkt als een filter op apps die de user al mag gebruiken; user ziet alleen die apps binnen de collection die ook daadwerkelijk aan hem toegewezen zijn
  - Vereist Entra ID Premium P1 of P2

- Admin collection aanmaken (via Azure/Entra portal, examen kernstof)
  1. Entra admin center, als admin
  2. Identity > Applications > Enterprise Applications
  3. Manage > App Launchers
  4. New collection
  5. Naam invoeren (aanbevolen: niet het woord "collection" in de naam gebruiken), Description invoeren
  6. Applications tab > + Add application, apps selecteren of zoeken, Add
  7. Volgorde van apps aanpasbaar via de pijltjes
  8. Owners tab > + Add users and groups, owners selecteren, Select
  9. Review + Create
  - Belangrijk: als je users/groups als owner toewijst, kunnen zij de collection alleen beheren via de Azure portal, niet via My Apps

- My Apps portal (myapps.microsoft.com)
  - Los, web based portal voor het beheren en starten van applicaties
  - Vereist een organizational account plus toegewezen toegang door de Entra admin
  - Los van de Azure portal, geen Azure of M365 subscription nodig
  - Users gebruiken het om: apps te ontdekken waar ze toegang tot hebben, nieuwe apps aan te vragen (self service), eigen persoonlijke collections te maken, toegang tot apps te beheren
  - Elke app waar een user toegang tot heeft staat standaard in de default Apps collection; user kan apps daaruit verwijderen

- Collection aanmaken via My Apps (stappen)
  1. My Apps portal openen
  2. Ellipsis (...) op het apps scherm
  3. Manage collections
  4. Create collection
  5. + Add apps, gewenste apps selecteren
  6. Add selected apps
  7. Naam geven, Create collection

- Onthouden voor examen
  - Collections vereisen altijd P1 of P2, geen gratis feature
  - Admin collections (via Entra/Azure portal) vs persoonlijke collections (via My Apps) zijn 2 losse concepten met eigen aanmaakproces
  - Een collection filtert alleen binnen wat een user al mag; het geeft zelf geen extra toegang
  - Owners van een admin collection beheren die uitsluitend via de Azure portal, niet via My Apps

---

## Module Assessment — Module 2 (Implement and monitor the integration of enterprise apps for SSO)

**Score:** 100%

### Vraag 1
What service and connector work together to securely pass a user sign-on token from Microsoft Entra ID to a web application running in an organization's on-premises datacenter?

- ✅ The Microsoft Entra Application Proxy service and Application Proxy connector
- An Application Proxy connector and the Azure Firewall service
- The Microsoft Entra Application Proxy service and Application Gateway

### Vraag 2
Which user provisioning mode(s) are supported for applications in the Microsoft Entra ID gallery?

- Administrator approved and automatic.
- You should only use Manual Provisioning to ensure security.
- ✅ Manual and automatic

### Vraag 3
Which of the following groups of information can be found in the Microsoft Entra ID Usage and insights report?

- The top used application in your organization and Who gave consent to an application and The top sign-in errors for each application
- The top used application in your organization and The applications with the most failed sign-ins and The service that logged the occurrence
- ✅ The top used applications in your organization and The application with the most failed sign-ins and The top sign-in errors for each application

---
---

## Learning Path 4: Implement access management for apps
### Module 3: Implement app registration

### Introduction

- Wat deze module behandelt
  - Line of business application registration strategie plannen
  - Application registrations implementeren
  - Application permissions configureren
  - Application governance proces opzetten en onderhouden

- Learning objectives
  - Plan your line-of-business application registration strategy
  - Implement application registrations
  - Configure application permissions
  - Establish and maintain an application governance process

- Prerequisites
  - Ervaring met Microsoft Cloud admin portals
  - Eerdere ervaring met cloud en on premises applicaties

---

### Plan your line of business application registration strategy

- Waarom apps integreren met Entra ID (examen kernstof)
  - Application authentication en authorization
  - User authentication en authorization
  - SSO via federation of password
  - User provisioning en synchronization
  - Role based access control; app roles definieren voor role based authorization checks
  - OAuth authorization services; gebruikt door M365 en andere Microsoft apps om toegang tot APIs/resources te autoriseren
  - Application publishing en proxy; app vanuit een private netwerk naar internet publiceren
  - Directory schema extension attributes; schema van service principal/user objects uitbreiden met extra data

- 2 representaties van een applicatie in Entra ID
  - Application object; definieert en beschrijft de app aan Entra ID
  - Service principal; de instantie van de app binnen een specifieke directory

- Application object, details
  - Beheerd via App Registrations in de Azure portal
  - Bestaat alleen in de home directory, ook bij een multitenant app
  - Bevat: name/logo/publisher, redirect URIs, secrets (symmetric/asymmetric keys), API dependencies (OAuth), published APIs/resources/scopes (OAuth), app roles (RBAC), SSO metadata/config, user provisioning metadata/config, proxy metadata/config

- Manieren waarop application objects ontstaan
  - App registration in de Azure portal
  - Nieuwe app aanmaken in Visual Studio, geconfigureerd voor Entra authenticatie
  - Admin voegt app toe uit de app gallery (creeert ook meteen een service principal)
  - Via Microsoft Graph API of PowerShell
  - Diverse andere developer paden

- Service principal, details
  - Beheerd via Enterprise Applications in de Azure portal
  - Governeert hoe een app verbindt met Entra ID, is de instantie van de app in jouw directory
  - Een app heeft max 1 application object (in de home directory), maar kan meerdere service principals hebben, 1 per directory waar hij actief is
  - Bevat: referentie naar het application object (via application ID), local user/group app role assignments, local user/admin granted permissions, local policies (incl. Conditional Access), alternate local settings (claims transformation rules, attribute mappings, directory specific app roles, directory specific naam/logo)

- Manieren waarop service principals ontstaan
  - User logt in bij een third party app die geintegreerd is met Entra ID, en geeft consent (eerste persoon die consent geeft triggert het aanmaken van de service principal)
  - User logt in bij Microsoft online services zoals M365 (creeert service principals voor de onderliggende services)
  - Admin voegt app toe uit de gallery (creeert ook het application object)
  - App toevoegen voor gebruik met Application Proxy
  - App connecten voor SSO via SAML of password SSO
  - Programmatisch via Microsoft Graph API of PowerShell

- Relatie tussen application object en service principal
  - 1 application object in de home directory, gerefereerd door 1 of meer service principals (1 per directory waar de app actief is, incl. de home directory zelf)
  - Microsoft onderhoudt zelf 2 interne directories voor het publiceren van apps: 1 voor Microsoft apps, 1 voor preintegrated third party apps (app gallery)
  - App publishers/vendors moeten een eigen publishing directory hebben

- Uitzonderingen bij service principals
  - Niet elke service principal wijst terug naar een application object; vroeger (bij de originele Entra ID opzet) was de service principal alleen al genoeg, vergelijkbaar met een Windows Server AD service account
  - Nog steeds mogelijk om via PowerShell een service principal aan te maken zonder eerst een application object
  - Microsoft Graph API vereist wel altijd eerst een application object voordat je een service principal kunt maken
  - Claims transformation rules en attribute mappings (user provisioning) zijn alleen beschikbaar via de UI, niet programmatisch

- Process flow bij het toevoegen van een nieuwe app registration
  1. User vraagt registratie aan, request token wordt uitgegeven
  2. Authorization endpoint stuurt authentication terug
  3. User geeft consent voor de app registration
  4. Service (principal) wordt aangemaakt vanuit de applicatie
  5. Token wordt teruggegeven aan de user

- Wie mag apps toevoegen
  - Rollen: Application Administrator, Cloud Application Administrator
  - Default: alle users mogen zelf apps registreren die ze ontwikkelen, en zelf beslissen welke apps toegang krijgen tot organisatiedata via consent
  - Eerste user die consent geeft aan een app triggert het aanmaken van de service principal, daarna wordt consent info opgeslagen op de bestaande service principal

- Waarom user self-service registratie/consent oke is (redenen, geen technische details, examen kernstof)
  - Apps gebruikten AD al jaren zonder registratie nodig, nu heeft de organisatie juist beter zicht op welke apps de directory gebruiken en waarom
  - Delegeren van deze taak elimineert de noodzaak van een admin driven registratie/publishing proces (vroeger bij AD FS moest een admin elke app als relying party toevoegen)
  - Users die met hun org account inloggen verliezen automatisch toegang als ze de organisatie verlaten
  - Gedeelde data met apps is te auditen
  - API owners (via Entra ID OAuth) bepalen zelf welke permissions users mogen toestaan, en welke permissions altijd admin consent vereisen
  - Elke keer dat een user data deelt met een app wordt dit gelogd, terug te zien in Audit Reports

- Self service registratie/consent uitschakelen (2 losse instellingen)
  - Consent uitschakelen; Enterprise applications > User settings > "Users can consent to apps accessing company data on their behalf" op No. Gevolg: admin moet dan voor elke nieuwe app consent geven
  - Registratie uitschakelen; Entra ID > User settings > "Users can register applications" op No

- Tenancy en app scope (single vs multitenant, examen kernstof)
  - Single tenant; app alleen beschikbaar in de home tenant waarin hij geregistreerd is
  - Multitenant; app beschikbaar voor users in de home tenant en andere tenants

- Audience opties bij app registration

| Audience | Single/Multi | Wie kan inloggen |
|---|---|---|
| Accounts in this directory only | Single tenant | Alle user/guest accounts in jouw eigen directory; geschikt voor puur interne doelgroep |
| Accounts in any Microsoft Entra directory | Multitenant | Alle work/school accounts van Microsoft, incl. scholen/bedrijven met M365; geschikt voor business/educatieve klanten |
| Accounts in any Microsoft Entra directory and personal Microsoft accounts | Multitenant | Work/school EN personal Microsoft accounts (Skype, Xbox, Outlook.com); breedste mogelijke doelgroep |

- Best practices voor multitenant apps
  - Test de app in een tenant met geconfigureerde Conditional Access policies
  - Least privilege; app vraagt alleen de permissions die echt nodig zijn
  - Duidelijke namen/beschrijvingen geven aan permissions die de app blootstelt, zodat users/admins snappen waarmee ze instemmen

- Onthouden voor examen
  - Application object = 1x per app, in de home directory. Service principal = 1x per directory waar de app actief is
  - Microsoft Graph API vereist altijd eerst een application object; PowerShell kan een service principal ook los aanmaken
  - Claims transformation rules en attribute mappings zijn alleen via de UI beschikbaar, niet programmatisch
  - Single tenant = alleen eigen directory, Multitenant = ook andere Entra directories (en evt. personal accounts)

---

### Implement application registration

- Waarom registreren
  - Elke app waar het Microsoft identity platform IAM voor moet doen, moet geregistreerd worden
  - Registratie in de Azure portal, zodat het platform authentication en authorization services kan leveren aan de app en zijn users
  - Geldt voor: client applications (web/mobile) en web APIs die een client app ondersteunen
  - Registratie zet een trust relationship op tussen de applicatie en het identity platform

---

### Register an application

- Wat registratie doet
  - Zet een unidirectionele trust relationship op: de app vertrouwt het Microsoft identity platform, niet andersom

- App registreren (stappen)
  1. Entra admin center, Administrator account
  2. Identity > Applications > App registrations
  3. + New registration
  4. Naam geven (bv. Demo app), default values gebruiken, redirect URI niet verplicht op dit moment
  5. Redirect naar het Demo app scherm

- Redirect URI
  - De locatie waar het identity platform de user's client naartoe stuurt met security tokens na authenticatie
  - In productie vaak een publiek endpoint, tijdens development ook lokale endpoints toe te voegen
  - Geconfigureerd via Platform configurations

- Platform configuratie instellen (stappen)
  1. App selecteren in App registrations
  2. Manage > Authentication
  3. Platform configurations > Add a platform
  4. Platform type kiezen

- Platform types en instellingen (examen kernstof)

| Platform | Configuratie |
|---|---|
| Web | Redirect URI handmatig invullen, voor standaard server based web apps |
| Single-page application | Redirect URI handmatig invullen, voor client side apps in JavaScript/Angular/Vue/React/Blazor WebAssembly |
| iOS/macOS | App Bundle ID invullen (uit XCode), redirect URI wordt automatisch gegenereerd |
| Android | Package name + Signature hash invullen, redirect URI wordt automatisch gegenereerd |
| Mobile and desktop applications | Suggested redirect URI kiezen of custom opgeven. Voor desktop: aanbevolen https://login.microsoftonline.com/common/oauth2/nativeclient. Voor mobile apps zonder recente MSAL of broker |

- Credentials toevoegen
  - Gebruikt door confidential client applications (web apps, web APIs, service/daemon apps) om zichzelf te authenticaten zonder user interactie
  - 2 types: certificates en client secrets

- Certificate toevoegen
  - Aanbevolen credential type, hogere assurance dan een client secret
  - Toegestane formaten: .cer, .pem, .crt
  - Toegevoegd via Certificates & secrets

- Client secret toevoegen (stappen)
  1. App selecteren in App registrations
  2. Certificates and secrets > New client secret
  3. Description invullen, duration kiezen
  4. Add
  5. Secret waarde direct noteren, wordt daarna nooit meer getoond
  - Simpeler te gebruiken dan een certificate, vaak gebruikt tijdens development, maar minder veilig; certificates aanbevolen voor productie

- Web API registreren
  - Zelfde registratieproces, maar redirect URI en platform settings kunnen overgeslagen worden (geen interactieve user login)
  - Credentials alleen nodig als de API zelf weer een downstream API benadert

- Scope toevoegen (voorbeeld: Employees.Read.All, stappen)
  1. Azure portal, juiste tenant kiezen indien meerdere
  2. Entra ID > App registrations > eigen API app registration
  3. Expose an API > Add a scope
  4. Application ID URI instellen indien nog niet gedaan (default: api://, of custom zoals https://contoso.com/api)
  5. Scope attributes invullen

- Scope velden (examen kernstof)

| Veld | Voorbeeld |
|---|---|
| Scope name | Employees.Read.All |
| Who can consent | Admins and users, of Admins only voor high privilige permissions |
| Admin consent display name | Read-only access to employee records |
| Admin consent description | Uitgebreide beschrijving voor admins |
| User consent display name | Zichtbaar voor users, alleen als "Admins and users" gekozen is |
| User consent description | Uitgebreide beschrijving voor users |

  - State op Enabled zetten, Add scope

- Pre-authorized client applications (optioneel)
  - Voorkomt consent prompt voor vertrouwde client apps
  - Authorized client applications > Add a client application > Application (client) ID invullen > scopes selecteren > Add application
  - Alleen doen bij apps die je echt vertrouwt, want users krijgen dan geen kans meer om consent te weigeren

- Scope met verplichte admin consent (voorbeeld: Employees.Write.All)
  - Zelfde proces, maar Who can consent = Admins only
  - Typisch gebruikt voor high privilege operaties, vaak door backend/daemon apps zonder interactieve user login
  - User consent display name en description blijven leeg

- Scopes verifieren
  - Volledige scope string = Application ID URI + Scope name
  - Voorbeeld: https://contoso.com/api/Employees.Read.All

- Scopes gebruiken
  - Client app registration krijgt toegang tot de web API en de gedefinieerde scopes
  - Client krijgt een OAuth 2.0 access token met een scope (scp) claim die de toegestane permissions bevat
  - Web API evalueert de scp claim in het ontvangen token om toegang op runtime te bepalen
  - Extra scopes later toevoegbaar indien nodig

- Wat er achter de schermen gebeurt (examen kernstof)
  1. App registration wordt aangemaakt in de home tenant
  2. App wordt geinstantieerd met een security principal in Entra ID
  3. Security principal krijgt consent, van de eerste user of een admin, afhankelijk van hoe de exposed API is opgezet
  4. Security principal krijgt het security token zodra de user de app benadert en de API gebruikt

- Onthouden voor examen
  - Certificates zijn veiliger dan client secrets, aanbevolen voor productie
  - Web API registratie slaat redirect URI en platform settings over, tenzij de API zelf een downstream API benadert
  - Scope string = Application ID URI + Scope name
  - Admins only consent wordt gebruikt voor high privilege scopes, vaak bij backend/daemon apps

---

### Configure permission for an application

- Wat deze unit behandelt
  - Basisconcepten van het authorization model: scopes, permissions, en consent
  - Regelt hoe apps toegang krijgen tot data via het OAuth 2.0 protocol

- Scopes en permissions
  - Microsoft identity platform gebruikt OAuth 2.0; laat een third party app namens een user toegang krijgen tot web hosted resources
  - Elke resource heeft een Application ID URI (resource identifier), bv:
    - Microsoft Graph; https://graph.microsoft.com
    - M365 Mail API; https://outlook.office.com
    - Azure Key Vault; https://vault.azure.net
  - Resources definieren zelf fijnmazige permissions (scopes), bv. calendar lezen, calendar schrijven, mail versturen namens de user
  - Doel: apps vragen alleen de permissions aan die ze echt nodig hebben (least privilege), users/admins weten precies waar de app toegang toe heeft

- Permission strings (voorbeeld Microsoft Graph)
  - Calendar lezen; Calendars.Read
  - Calendar schrijven; Calendars.ReadWrite
  - Mail versturen; Mail.Send
  - Apps vragen deze scopes aan via het authorize endpoint; sommige high privilege permissions vereisen het administrator consent endpoint

- 2 permission types (examen kernstof)
  - Delegated permissions; voor apps met een ingelogde user aanwezig. User of admin geeft consent, app handelt namens de ingelogde user. Sommige delegated permissions vereisen altijd admin consent (high privilege)
  - Application permissions; voor apps zonder ingelogde user (background services, daemons). Alleen een admin kan hiervoor consent geven

- Effective permissions (belangrijk verschil, examen kernstof)
  - Delegated permissions; effectieve rechten = het minst brede snijpunt tussen wat de app is toegestaan EN wat de ingelogde user zelf mag. App kan nooit meer rechten hebben dan de ingelogde user zelf
    - Voorbeeld: app heeft User.ReadWrite.All delegated permission. Als de ingelogde user application administrator is, kan de app alle profielen updaten. Als de ingelogde user geen adminrol heeft, kan de app alleen het eigen profiel van die user updaten
  - Application permissions; effectieve rechten = het volledige niveau dat de permission zelf impliceert, ongeacht wie er is ingelogd (er is namelijk geen ingelogde user)
    - Voorbeeld: app met User.ReadWrite.All application permission kan altijd alle user profielen updaten

- OpenID Connect (OIDC) scopes
  - 4 well defined scopes, ook gehost op Microsoft Graph: openid, email, profile, offline_access
  - address en phone OIDC scopes worden niet ondersteund
  - OIDC scopes aanvragen geeft ook toegang tot het UserInfo endpoint

- openid scope
  - Verplicht als een app sign in via OIDC uitvoert
  - Verschijnt op consent pagina als "sign you in" (werk account) of "view your profile..." (personal account)
  - Geeft een unieke user identifier via de sub claim, en toegang tot het UserInfo endpoint
  - Gebruikt bij het token endpoint om ID tokens te verkrijgen, voor authenticatie

- email scope
  - Combineerbaar met openid en andere scopes
  - Geeft toegang tot het primaire email adres via de email claim
  - Claim alleen aanwezig als de user account daadwerkelijk een email addres heeft gekoppeld; apps moeten hiermee rekening houden

- profile scope
  - Combineerbaar met openid en andere scopes
  - Geeft toegang tot substantiele user info: given name, surname, preferred username, object ID, en meer

- offline_access scope
  - Geeft de app langdurige toegang namens de user
  - Verschijnt op consent pagina als "Maintain access to data you have given it access to"
  - Nodig om refresh tokens te krijgen; zonder deze scope krijg je alleen een kortlevende access token (meestal 1 uur geldig)
  - Op v2.0 endpoint: moet expliciet aangevraagd worden om refresh tokens te krijgen
  - Uitzondering: bij een Single Page Application (SPA) wordt de refresh token altijd verstrekt, ongeacht deze scope
  - Verschijnt zelfs op consent screens bij flows die geen refresh token geven (implicit flow), om toekomstige overstap naar code flow te ondersteunen

- Individuele user consent aanvragen
  - App specificeert gewenste permissions via de scope query parameter (spatie gescheiden lijst)
  - Elke permission = permission value + resource identifier (Application ID URI)
  - Platform checkt of er al eerder consent is gegeven (door de user zelf, of door een admin namens de hele organisatie); zo niet, wordt de user om consent gevraagd
  - offline_access en user.read worden automatisch meegenomen in de initiele consent, ongeacht wat er expliciet is aangevraagd, omdat ze basaal nodig zijn voor correcte app functionaliteit
  - Eenmaal goedgekeurd: consent wordt onthouden, geen herhaalde consent vraag bij volgende logins

- Consent aanvragen voor de hele tenant
  - Bij organisatiebrede licenties/subscripties kan een admin consent geven namens alle users in de tenant
  - Bij tenant wide admin consent: users zien geen consent pagina meer voor die app
  - Application permissions moeten altijd via het admin consent endpoint aangevraagd worden

- Onthouden voor examen
  - Delegated permissions: effectief = snijpunt van app rechten EN user rechten (nooit meer dan de user zelf mag)
  - Application permissions: effectief = volledige permission, want geen user om tegen te toetsen
  - offline_access is nodig voor refresh tokens, behalve bij SPA's waar dit altijd al gebeurt
  - openid, email, profile, offline_access zijn de 4 OIDC scopes; address en phone worden niet ondersteund

---

### Grant tenant-wide admin consent to applications

- Wat het is
  - Tenant-wide admin consent geven aan zelf ontwikkelde of direct geregistreerde apps, via App registrations in de Azure portal
  - Waarschuwing: geeft de app en de publisher toegang tot organisatiedata, permissions altijd zorgvuldig reviewen voor consent

- Wie mag dit doen
  - User geautoriseerd om te consenten namens de organisatie, o.a. Privileged Role Administrator
  - Ook mogelijk via een custom directory role die de permission bevat om apps permissions te geven

- Consent geven via App registrations (stappen)
  1. App registrations > Demo app
  2. Application (client) ID en Directory (tenant) ID noteren
  3. Manage > API permissions
  4. Configured permissions > Grant admin consent
  5. Bevestigen met Yes
  - Waarschuwing: dit revoked eerder tenant wide gegeven permissions; permissions die users zelf al eerder namens zichzelf hadden gegeven blijven onaangetast

- Consent geven via Enterprise applications (alternatieve manier, stappen)
  1. Enterprise applications > Demo app
  2. Security > Permissions
  3. Grant admin consent
  4. Inloggen als Privileged Role Administrator
  5. Permissions requested dialog reviewen, Accept

- URL construeren voor tenant-wide admin consent
  - Format: `https://login.microsoftonline.com/{tenant-id}/adminconsent?client_id={client-id}`
  - {client-id} = application's client ID (app ID)
  - {tenant-id} = tenant ID of geverifieerde domeinnaam
  - Altijd permissions zorgvuldig reviewen voor consent

- Admin-restricted permissions (examen kernstof)
  - Sommige high privilege permissions zijn admin-restricted, bv:
    - User.Read.All; alle user profielen lezen
    - Directory.ReadWrite.All; schrijven naar de organisatie directory
    - Groups.Read.All; alle groups in de directory lezen
  - Consumer users kunnen dit soort permissions wel zelf goedkeuren; organizational users niet, zij krijgen een foutmelding dat ze niet geautoriseerd zijn
  - Voor deze permissions: direct aanvragen bij een company administrator via het admin consent endpoint
  - Bij delegated high privilege permissions goedgekeurd via admin consent endpoint: geldt voor alle users in de tenant
  - Bij application permissions goedgekeurd via admin consent endpoint: geldt niet namens een specifieke user, wordt direct aan de client applicatie zelf gegeven. Alleen relevant voor daemon/non-interactive apps

- Admin consent endpoint gebruiken
  - Eenmaal admin consent gegeven: users hoeven verder niks te doen, krijgen gewoon een access token met de geconsente permissions via de normale auth flow
  - Bij normaal inloggen via het authorize endpoint: platform detecteert of de user een admin rol heeft en vraagt of hij namens de hele tenant wil consenten
  - Los, dedicated admin consent endpoint beschikbaar om proactief admin consent te vragen, en verplicht voor application permissions (die niet via het gewone authorize endpoint aan te vragen zijn)
  - High privilege operatie, alleen gebruiken als het scenario dit echt vereist

- Permissions aanvragen in de app registration portal
  - Apps kunnen zowel delegated als application permissions statisch vastleggen in de app registration
  - Maakt gebruik van /.default scope en de "Grant admin consent" optie in de portal mogelijk
  - Best practice: statisch gedefinieerde permissions moeten een superset zijn van wat de app dynamisch/incrementeel aanvraagt
  - Stappen: App registrations > API Permissions > Add a permission > Microsoft Graph kiezen > gewenste permissions toevoegen > opslaan

- Aanbevolen: user laten inloggen in de app
  - Apps met een admin consent flow hebben meestal een aparte pagina/view waar de admin de permissions kan goedkeuren (onderdeel van sign-up flow, settings, of los "connect" scherm)
  - Vaak pas tonen nadat de user al is ingelogd met een werk/school account, zodat je de organisatie van de admin al kent

- Permissions gebruiken, admin consent request opbouwen (technisch, examen kernstof)
  - Na consent: app kan access tokens ophalen, die alle toegekende permissions voor 1 specifieke resource bevatten
  - Voorbeeld request: GET naar `login.microsoftonline.com/{tenant}/v2.0/adminconsent` met parameters client_id, state, redirect_uri, scope

- Parameters bij het admin consent request (examen kernstof)

| Parameter | Verplicht | Beschrijving |
|---|---|---|
| tenant | Ja | Tenant ID, friendly name, of "organizations". Nooit "common" gebruiken, personal accounts kunnen geen admin consent geven buiten tenant context |
| client_id | Ja | Application (client) ID van de app |
| redirect_uri | Ja | Moet exact matchen met een geregistreerde redirect URI |
| state | Aanbevolen | Vrije waarde om state van de user te encoderen, komt terug in de token response |
| scope | Ja | Set van gevraagde permissions, statisch (/.default) of dynamisch, kan ook OIDC scopes bevatten |

  - Na dit request moet een tenant administrator inloggen om de gevraagde permissions in de scope parameter goed te keuren

- Onthouden voor examen
  - Consent geven via App registrations revoked eerdere tenant wide consents; via Enterprise applications gebeurt

---

### Implement application authorization

- Wat app roles zijn
  - Worden gebruikt om permissions aan users toe te wijzen
  - Gedefinieerd via de Azure portal
  - Bij sign in geeft Entra ID een roles claim mee, voor elke rol die de user individueel heeft gekregen of via group membership

- 2 manieren om app roles te declareren (Azure portal)
  - App roles UI (Preview)
  - App manifest editor

- Onthouden voor examen
  - Roles claim in de token bevat zowel individueel toegewezen rollen als rollen via group membership
  - App roles zijn te configureren via een simpele UI (preview) of direct via het app manifest
 
---

### Exercise: add app roles to an application and receive tokens
  - [04-sc300/labs/22-add-App-roles-to-an-application-and-receive-tokens](../../04-sc300/labs/22-add-App-roles-to-an-application-and-receive-tokens.md)

---

### Manage and monitor application by using app governance

- Waarom dit belangrijk is
  - Cyberattacks exploiteren steeds vaker de apps in je on premises en cloud infrastructuur
  - Dienen als startpunt voor privilege escalation, lateral movement, en data exfiltratie
  - Vereist zichtbaarheid in app compliance posture, en detectie/respons op anomaal gedrag van apps

- Wat app governance is
  - Add on feature bovenop Defender for Cloud Apps
  - Specifiek voor OAuth enabled apps die M365 data benaderen via Microsoft Graph APIs
  - Biedt zichtbaarheid, remediation, en governance over hoe deze apps en hun users toegang hebben tot, gebruiken en delen van gevoelige M365 data
  - Werkt via actionable insights, automated policy alerts, en acties

- 4 kernonderdelen (examen kernstof)
  - Insights; overzicht van alle third party apps voor M365 in de tenant op 1 dashboard, incl. status en alert activiteiten
  - Governance; proactieve of reactieve policies voor app/user patronen en gedrag, beschermt tegen non compliant of malicious apps, beperkt toegang van risky apps tot data
  - Detection; alerts/notificaties bij anomalieen in app activiteit, of bij gebruik van non compliant/malicious/risky apps
  - Remediation; automatische remediation mogelijkheden, plus tijdige remediation controls om te reageren op gedetecteerde anomale app activiteit

- Defender for Cloud Apps sync inschakelen (stappen)
  1. Office 365 moet verbonden zijn in Defender for Cloud Apps
  2. Office 365 Microsoft Entra ID apps moeten enabled zijn
  3. Defender for Cloud Apps portal openen (portal.cloudappsecurity.com)
  4. Gear icon rechtsboven > Settings
  5. Threat Protection > App Governance
  6. Enable App Governance integration > Save
  7. Verificatie: nieuwe app governance policies verschijnen in Defender for Cloud Apps (kan enkele minuten duren)

- Policies die verschijnen na activatie
  - Microsoft 365 OAuth app Reputation
  - Microsoft 365 OAuth Phishing Detection
  - Microsoft 365 OAuth App Governance

- Onthouden voor examen
  - App governance is specifiek gericht op OAuth apps die via Microsoft Graph bij M365 data komen, niet op apps in het algemeen
  - Het is een add on feature bovenop Defender for Cloud Apps, geen los product
  - De 4 pijlers zijn Insights, Governance, Detection, Remediation
  - Na activatie verschijnen automatisch 3 specifieke policies gericht op OAuth app reputation en phishing detection
 
---

## Module Assessment — Module 3 (Implement app registration)

**Score:** 100%

### Vraag 1
Microsoft maintains which of the following directories and uses them to publish applications?

- SaaS directory
- ✅ App gallery directory
- Single-sign-on app connected directory

### Vraag 2
Which one of the following is a best practice for building multitenant apps?

- ✅ Follow the principle of least user access to ensure that your app only requests permissions it actually needs.
- Test your app in each tenant to ensure functionality.
- Use names and descriptions that are only meaningful to your team.

### Vraag 3
Which two ways do you declare app roles by using the Azure portal?

- Certificates and secrets.
- Use the App manifest editor and API permissions.
- ✅ Use the App roles and App manifest editor.

---
---

# SC-300: Microsoft Identity and Access Administrator
## Learning Path 4: Implement access management for apps
### Module 4: Register Apps Using Microsoft Entra ID
### Introduction

- Wat app registration is
  - Proces waarmee het identity systeem weet welke applicaties gebruikt worden
  - Bevestigt dat de user toegang heeft tot de app, en dat de app toegang heeft tot benodigde resources
  - Waarborgt security en privacy van users, apps, en data

- Scenario ter illustratie
  - Developer bouwt een app die authenticatie/autorisatie nodig heeft
  - Registratie bij Entra ID geeft de app een identity configuratie, integreerbaar met het Microsoft identity platform

- Wat registratie mogelijk maakt
  - Custom branding; eigen branding op het sign in scherm, belangrijk omdat dit de eerste indruk is die een user van de app krijgt
  - Tenant configuration; kiezen tussen single tenant (eigen organisatie) of multitenant (accounts van andere tenants toestaan), evt. ook personal Microsoft accounts of social accounts (LinkedIn, Google, etc.)
  - Permission management; scope permissions aanvragen (bv. user.read om het profiel van de ingelogde user te lezen), scopes definieren voor toegang tot de eigen web API
  - Secure authentication; veilige authenticatie methodes configureren. Voor confidential client applications (bv. web apps met vertrouwde backend servers): client secrets, certificates, of modernere opties zoals managed identities

- Learning objectives
  - Benefits of registering an app
  - Single-tenant versus multitenant apps
  - What happens when an app is registered
  - Relationship between application objects and service principals

- Doel van de module
  - App registreren bij Entra ID en configureren voor integratie met het identity platform
  - Sign in branding aanpassen
  - Scope permissions aanvragen
  - Secrets delen met het identity platform om de app's identity te bewijzen
  - Single tenant vs multitenant, application objects vs service principal objects, en hun onderlinge relatie
 
---

### Plan for app registration

- Wat het is
  - Ervoor zorgen dat het identity systeem weet welke applicaties gebruikt worden
  - Bevestigt user toegang tot de app, en app toegang tot benodigde resources
  - Waarborgt security en privacy van users, apps, en data

- Voordelen van registreren
  - Custom branding op het sign in scherm
  - Tenant configuratie: single tenant (eigen organisatie) of multitenant (work/school accounts van andere tenants), evt. ook personal Microsoft accounts of social accounts (LinkedIn, Google)
  - Scope permissions aanvragen, bv. user.read voor het profiel van de ingelogde user
  - Eigen scope definieren voor toegang tot je web API
  - Secret delen met het identity platform, relevant bij confidential client applications (apps die credentials veilig kunnen bewaren, zoals een web app met een trusted backend server)

- Single tenant versus multitenant
  - Single tenant; alleen beschikbaar in de tenant waar de app geregistreerd is (home tenant)
  - Multitenant; beschikbaar voor users in de home tenant EN andere tenants, bewust te kiezen wanneer nodig
  - Bij multitenant: een service principal object wordt aangemaakt per tenant waar de app users heeft
    - In de source tenant: bij app registration zelf
    - In andere tenants: bij de eerste user authenticatie daar

- Audience opties

| Audience | Single/Multi | Wie kan inloggen |
|---|---|---|
| Accounts in this directory only | Single tenant | Alle user/guest accounts in eigen directory |
| Accounts in any Microsoft Entra directory | Multitenant | Work/school accounts van elke Microsoft tenant, incl. scholen/bedrijven met M365 |
| Accounts in any Microsoft Entra directory and personal Microsoft accounts | Multitenant | Work/school EN personal accounts (Skype, Xbox, Outlook.com) |

- Wat er gebeurt bij registratie
  - App krijgt een unieke identifier, gedeeld met het identity platform bij token requests
  - Confidential client applications delen ook hun secret of public key (afhankelijk van certificates vs secrets)
  - Belangrijk: sinds augustus 2024 krijgen nieuwe apps standaard v2 access tokens (i.p.v. v1), voor verbeterde security. Dit beinvloedt token format en welke claims erin zitten

- 2 representaties van een applicatie
  - Application object; de definitie van de app (met uitzonderingen)
  - Service principal; de instantie van de app, verwijst meestal naar een application object. 1 application object kan door meerdere service principals across directories gerefereerd worden

- Wat het identity platform doet
  - Identificeert de app op basis van ondersteunde authentication protocollen
  - Biedt alle identifiers, URLs, secrets, en gerelateerde info nodig voor authenticatie
  - Bewaart data nodig voor runtime authenticatie
  - Bewaart data om te bepalen welke resources een app nodig heeft, en onder welke omstandigheden een request wordt gehonoreerd
  - Biedt infrastructuur voor app provisioning binnen de developer's eigen tenant, en naar andere Entra tenants
  - Handelt user consent af tijdens token requests, faciliteert dynamische provisioning van apps across tenants

- Consent
  - Proces waarbij een resource owner autorisatie geeft aan een client applicatie om protected resources te benaderen, onder specifieke permissions, namens de resource owner
  - Entra ID laat users en admins dynamisch consent geven of weigeren
  - Uiteindelijk bepalen admins: wat apps mogen doen, welke users specifieke apps mogen gebruiken, en hoe directory resources benaderd worden

- Onthouden voor examen
  - Sinds augustus 2024: nieuwe apps krijgen standaard v2 tokens, niet v1
  - Bij multitenant apps: service principal ontstaat per tenant, in de source tenant bij registratie, elders bij eerste user login
  - Consent is het mechanisme waarmee zowel users als admins bepalen wat een app mag doen namens hen

---

### Explore application objects and service principals

- Na registratie
  - Je hebt een globally unique instance van de app (het application object) in je home tenant
  - Je hebt een globally unique ID (app/client ID)
  - In het Entra admin center voeg je vervolgens secrets/certificates, scopes, branding, etc. toe
  - Registreren via het Entra admin center: application object EN service principal worden automatisch samen aangemaakt
  - Registreren via Microsoft Graph APIs: het aanmaken van de service principal is een aparte, losse stap

- Security best practice
  - Voor application authentication (workload identities): certificates aanbevolen boven passwords/secrets
  - Voor Azure workloads: managed identities de voorkeur, elimineren credential management volledig

- Application object, details
  - Resideert in de home tenant (waar de app geregistreerd is)
  - Dient als template/blueprint om 1 of meer service principal objects te maken, 1 per tenant waar de app gebruikt wordt
  - Vergelijkbaar met een class in object oriented programming: statische properties die worden toegepast op alle aangemaakte service principals

- Application object beschrijft 3 aspecten
  - Hoe de service tokens kan uitgeven om toegang tot de app te krijgen
  - Welke resources de app mogelijk nodig heeft
  - Welke acties de app kan uitvoeren

- Application object bevat o.a.
  - Naam, logo, publisher
  - Redirect URIs
  - Authentication credentials: certificates (aanbevolen) of client secrets (alleen als certificates niet haalbaar zijn)
  - API dependencies (OAuth)
  - Published APIs/resources/scopes (OAuth)
  - App roles
  - SSO metadata/config
  - User provisioning metadata/config
  - Proxy metadata/config

- Service principal object, waarom nodig
  - Elke entiteit die toegang wil tot resources binnen een Entra tenant moet een security principal hebben, zowel users (user principal) als apps (service principal)
  - Security principal definieert de access policy en permissions voor die entiteit
  - Maakt authenticatie bij sign in en autorisatie bij resource toegang mogelijk

- 3 types service principal
  - Application; lokale representatie/instantie van een global application object binnen 1 tenant. Concrete instantie, erft properties van het application object. Ontstaat zodra een app permissie krijgt om resources in een tenant te benaderen
  - Managed identity (aanbevolen voor Azure workloads); representeert een managed identity, elimineert credential management, geeft een identity voor apps om te connecten met resources die Entra authenticatie ondersteunen
  - Legacy; representeert een oudere app, gemaakt voordat app registrations bestonden, of via legacy experiences. Kan credentials, service principal names, reply URLs, etc. hebben. Migreren naar moderne app registrations aanbevolen waar mogelijk

- Service principal bevat o.a.
  - Referentie terug naar het application object via de application ID property
  - Local user/group app role assignments
  - Local user/admin permissions gegeven aan de app
  - Local policies, incl. Conditional Access
  - Alternate local settings voor de app

- Relatie tussen application object en service principal
  - Application object = globale representatie, bruikbaar across alle tenants
  - Service principal = lokale representatie, specifiek voor 1 tenant
  - Application object dient als template waaruit gemeenschappelijke/default properties worden afgeleid voor elke service principal
  - Application object heeft: 1 op 1 relatie met de software applicatie zelf, 1 op meer relatie met zijn service principal(s)
  - Service principal moet in elke tenant waar de app gebruikt wordt aangemaakt worden, om een identity voor sign in/resource toegang te vestigen
  - Single tenant app; slechts 1 service principal (in de home tenant), aangemaakt en geconsent tijdens registratie
  - Multitenant app; extra service principal per tenant waar een user daar consent heeft gegeven voor gebruik

- Beheer van application objects en service principals
  - Altijd een management strategie/proces nodig voor het onderhouden van service principals

- Gevolgen van wijzigingen en verwijdering
  - Wijzigingen aan het application object worden alleen gereflecteerd in de service principal van de home tenant
  - Application object verwijderen verwijdert ook de service principal in de home tenant
  - Application object herstellen via het Entra admin center herstelt NIET automatisch de bijbehorende service principal
  - Service principals in andere tenants (bij multitenant apps) blijven onafhankelijk bestaan van het application object in de home tenant

- Service principals terugvinden
  - Via de app registration overview > Managed application in local directory

- Belangrijk
  - Bij workload identities (non human identities zoals apps): altijd security implicaties van credential management overwegen, managed identities verkiezen voor Azure resources waar mogelijk

- Onthouden voor examen
  - App registration via portal = application object + service principal automatisch samen; via Graph API = apart, 2 stappen
  - Application object verwijderen verwijdert de home tenant service principal, maar herstellen van het application object herstelt die service principal niet automatisch terug
  - 3 service principal types: Application, Managed identity, Legacy
  - Multitenant apps krijgen per tenant een eigen, onafhankelijke service principal
 
  ---

### Create app registrations

- Wat deze unit behandelt
  - Voorbeeld: een Single-Page Application (SPA) registreren in Entra ID
  - Kernproces vergelijkbaar voor andere app types (web apps, mobile apps); verschillen zitten in de platform specifieke configuratie

- App registration aanmaken (stappen)
  1. Entra admin center, minimaal Application Developer rol
  2. Identity > Applications > App registrations > New registration
  3. Naam invoeren (users kunnen deze naam zien, later aan te passen)
  4. Supported account types kiezen; voor de meeste single tenant apps: "Accounts in this organizational directory only". Redirect URI op dit moment NIET invullen
  5. Register
  - Application (client) ID en Directory (tenant) ID van de Overview pagina noteren, nodig voor de app code

- Single-Page Application platform configureren (voor MSAL.js 2.0+)
  - MSAL.js 2.0+ ondersteunt authorization code flow met PKCE (Proof Key for Code Exchange) en CORS (Cross-Origin Resource Sharing), veiliger dan de legacy implicit grant flow

- Stappen
  1. App registration selecteren
  2. Manage > Authentication
  3. + Add a platform
  4. Web applications > Single-page application tile
  5. Redirect URIs invullen, bv. http://localhost:3000/ voor lokale development
  6. Checkboxes onder Implicit grant and hybrid flows NIET aanvinken, legacy patronen niet meer aanbevolen
  7. Save

- Security note
  - SPA platform configuratie schakelt automatisch authorization code flow met PKCE in
  - PKCE veiliger dan legacy implicit grant flow, moderne SPAs zouden dit moeten gebruiken

- Registratie compleet, wat dit betekent
  - Redirect URI geconfigureerd; hier stuurt het platform de client en security tokens naartoe
  - App registration ondersteunt nu authorization code flow met PKCE en CORS

- Vervolgstappen na registratie
  - API permissions configureren indien de app Microsoft Graph of andere APIs nodig heeft
  - Certificates of client secrets toevoegen indien vereist door het app type (niet nodig voor SPAs met authorization code flow)
  - Configuratie testen met de eigen app code

- Best practice
  - Nieuwe app registrations zijn standaard verborgen voor users
  - Zichtbaar maken op de My Apps pagina: Enterprise apps > Properties > "Visible to users?" op Yes zetten

- Onthouden voor examen
  - SPA gebruikt authorization code flow met PKCE, niet de legacy implicit grant flow
  - Bij SPA registratie: redirect URI pas instellen bij de platform configuratiestap, niet tijdens de initiele registratie
  - Nieuwe apps zijn standaard onzichtbaar voor users tot je ze expliciet zichtbaar maakt via Enterprise apps Properties

---

### Configure app authentication

- Platform configuratie algemeen
  - Settings per app type (incl. redirect URIs) worden ingesteld in Platform configurations
  - Web en Single-page applications; redirect URI handmatig invullen
  - Mobile en desktop; redirect URIs vaak automatisch gegenereerd bij het instellen van andere settings
  - Platform specifieke configuratie zorgt dat de app de juiste authentication flow en security settings gebruikt voor die specifieke omgeving

- Configureren (stappen)
  1. App registrations > eigen app selecteren
  2. Manage > Authentication
  3. Platform configurations > Add a platform
  4. Platform type tile selecteren

- Platform types en instellingen (examen kernstof)

| Platform | Configuratie |
|---|---|
| Web | Redirect URI voor server side app. Hier stuurt het platform users en security tokens naartoe na authenticatie. Front channel sign out URLs en token settings ook configureerbaar |
| Single-page application | Redirect URI voor client side JavaScript app (Angular, React, Vue.js, Blazor WebAssembly). Gebruikt authorization code flow met PKCE. Front channel sign out URLs ook configureerbaar |
| iOS / macOS | App Bundle ID invullen (Build Settings of Info.plist in XCode). Redirect URI automatisch gegenereerd |
| Android | Package name (AndroidManifest.xml) + Signature hash genereren. Redirect URI automatisch gegenereerd |
| Mobile and desktop applications | Suggested redirect URI kiezen of custom opgeven. Desktop met embedded browser: https://login.microsoftonline.com/common/oauth2/nativeclient. Desktop met system browser: http://localhost. Keuze hangt af van de gebruikte authentication library |

  - Configure om de platform configuratie af te ronden

- Security note
  - Elk platform type heeft eigen security vereisten
  - SPAs gebruiken altijd authorization code flow met PKCE
  - Web applications kunnen verschillende flows gebruiken, afhankelijk van configuratie

- Redirect URI, wat het is
  - Ook wel reply URL genoemd
  - Locatie waar de authorization server de user naartoe stuurt na succesvolle autorisatie, met een authorization code of access token
  - Moet correct geregistreerd zijn tijdens app registration, anders komt de code/token niet goed aan

- Kritieke security vereisten voor redirect URIs (examen kernstof)
  - HTTPS verplicht; uitzondering voor localhost tijdens development
  - Case sensitive; moet exact matchen met het URL path van de draaiende applicatie
  - Trailing slash gedrag:
    - Redirect URI zonder path segment; krijgt een trailing slash (/) toegevoegd in de response
    - Redirect URI met path segment; geen trailing slash toegevoegd
  - Niet ondersteunde speciale tekens: ! $ ' ( ) , ;

- Best practice
  - Redirect URIs altijd eerst testen in een development omgeving voordat je naar productie gaat, voor correcte token handling en security

- Onthouden voor examen
  - SPA = altijd authorization code flow met PKCE
  - Redirect URI moet altijd https zijn, behalve localhost tijdens development
  - Redirect URIs zijn case sensitive en ondersteunen geen: ! $ ' ( ) , ;
  - Trailing slash gedrag verschilt afhankelijk van of de URI al een path segment bevat
 
---

### Configure API permissions

- Context (herhaling van eerdere units)
  - Microsoft identity platform gebruikt OAuth 2.0
  - Elke web hosted resource heeft een Application ID URI
  - Resources definieren permissions (scopes), verdelen functionaliteit in kleinere brokken
  - Microsoft Graph voorbeeld: calendar lezen, calendar schrijven, mail versturen namens de user

- Security voordelen
  - Fijnmazige controle over data en API functionaliteit
  - Apps vragen permissions aan, users/admins moeten goedkeuren voordat de app toegang krijgt
  - Kleine permission sets laten apps alleen aanvragen wat ze echt nodig hebben

- Least privilege principe
  - Users/admins weten precies waar de app toegang toe heeft
  - Meer vertrouwen dat de app geen kwaadaardige intenties heeft
  - Developers moeten altijd least privilege toepassen; alleen aanvragen wat echt nodig is

- API permissions configureren (delegated permissions voorbeeld, stappen)
  1. Entra admin center > Applications > App registrations > eigen client applicatie
  2. API permissions > Add a permission > Microsoft Graph
  3. Delegated permissions selecteren (meest gebruikte permissions staan bovenaan de lijst)
  4. Gewenste permissions selecteren
  5. Add permissions

- Belangrijk over delegated permissions
  - Werken namens de ingelogde user; de app kan alleen data benaderen die de user zelf ook zou kunnen benaderen
  - Extra beveiligingslaag bovenop de permissions van de app zelf

- Basis OIDC permissions (voorbeeld, examen kernstof)

| Permission | Beschrijving | Use case |
|---|---|---|
| email | View users' email address | Email tonen in de app UI |
| offline_access | Maintain access to data you gave it access to | Refresh tokens voor langdurige toegang |
| openid | Sign users in | Basis authenticatie, verplicht voor sign in |
| profile | View users' basic profile | Naam en basisprofiel info tonen |

  - Dit zijn de meest gebruikte basis OIDC scopes; extra permissions nodig afhankelijk van de specifieke app vereisten

- Admin consent
  - Admin kan consent geven namens alle users in de organisatie, geen individuele user consent meer nodig
  - Nuttig voor organisatie brede apps waar admin goedkeuring gewenst of verplicht is volgens beleid

- Onthouden voor examen
  - Delegated permissions zijn altijd beperkt tot wat de ingelogde user zelf mag; extra beveiligingslaag bovenop de app permissions zelf
  - email, offline_access, openid, profile zijn de meest voorkomende basis OIDC scopes bij een nieuwe app
  - Admin consent elimineert de noodzaak van losse user consent per persoon
 
---

### Create app roles

- Wat een app role is
  - Custom claim, toepasbaar op users, groups, of applicaties
  - Verschijnt in het token dat gegenereerd wordt als een user authenticeert
  - Data in het token gebruikt door de app voor autorisatie doeleinden

- Kernvoordelen (examen kernstof)
  - Alternatief voor group claims; voorkomt group overage issues, vereist geen Entra ID P1 licentie
  - Fijnmazige autorisatie; precieze controle over wat users mogen binnen de app
  - Vereenvoudigde code; app checkt op specifieke role claims i.p.v. groups naar permissions te mappen

- Hoe in te stellen
  - Bij het aanmaken van app roles: Allowed member types op Users/Groups zetten

- Hoe app roles verschijnen in tokens
  - Nadat de app admin roles heeft aangemaakt, kunnen IT admins users/groups toewijzen
  - App krijgt een roles claim in het token (ID tokens voor apps, access tokens voor APIs), met alle toegewezen rollen van de ingelogde user
  - Voorbeeld token bevat o.a. "roles": ["Approver", "Reviewer"]

- Best practices (examen kernstof)
  - Altijd een baseline user role definieren zonder verhoogde rechten
  - Bij assignment vereiste apps: alleen users met directe assignment of group membership kunnen de app gebruiken
  - Assignment vereist altijd 1 van de gedefinieerde app roles; zonder baseline role zouden alle toegewezen users automatisch de enige (mogelijk elevated, bv. "admin") rol krijgen, wat least privilege schendt
  - Aanbevolen: baseline rol (bv. "user" of "reader") definieren, zodat gewone users/groups die krijgen i.p.v. een elevated rol

- Voordelen van app roles t.o.v. group based authorization
  - Voorkomt group overage claims
  - Vereenvoudigde autorisatie logica; code checkt simpelweg op bv. "admin" role claim, i.p.v. group IDs te doorlopen en te bepalen welke admin rechten geven
  - Duidelijkere intentie; rolnamen zoals "admin", "editor", "viewer" zijn beschrijvender dan group GUIDs
  - Minder complexiteit; geen group ID mappings nodig in de applicatiecode
  - Betere portability; app roles makkelijk te repliceren over verschillende omgevingen

- Onthouden voor examen
  - App roles vereisen geen P1 licentie, in tegenstelling tot sommige group based features (zoals dynamic groups)
  - Altijd een baseline/default role definieren om te voorkomen dat iedereen automatisch de enige (elevated) rol krijgt
  - Roles claim in het token toont alle toegewezen rollen van de ingelogde user
 
---

## Module Assessment — Module 4 (Register Apps Using Microsoft Entra ID)

**Score:** 100%

### Vraag 1
What does the Microsoft identity platform do with the unique identifier of a registered app?

- It stores the identifier in the Microsoft Entra Application object.
- It shares the identifier with all Microsoft Entra directories.
- ✅ It shares the identifier with the Microsoft identity platform when the app requests tokens.

### Vraag 2
What is the purpose of registering an app in Microsoft Entra?

- To request scope permissions for the user's device.
- To customize the branding of your application in the sign in dialog box.
- ✅ To ensure that your identity system is aware of what applications are being used and to confirm the user has access to the app and that the app has access to any needed resources.

### Vraag 3
What is the principle of least privilege and how does it relate to third party app permissions in the Microsoft identity platform?

- The principle of least privilege states that third party apps should request all possible permissions to ensure full functionality.
- The principle of least privilege states that third party apps should not request any permissions to ensure user privacy.
- ✅ The principle of least privilege states that third party apps should only request the permissions they need to perform their function, ensuring fine-grained control over data and API functionality.

---

### Summary — Module 4 (Register Apps Using Microsoft Entra ID)

- Wat app registration is
  - Fundamenteel proces om een identity configuratie voor je app op te zetten binnen het Microsoft identity platform
  - Zorgt voor veilige integratie en fijnmazige controle over authenticatie en autorisatie

- Kern leeruitkomsten van deze module

- Plannen en configureren van app registration
  - Relatie tussen application objects en service principals
  - Juiste supported account types kiezen (single tenant vs multitenant)
  - Plannen voor security vereisten en authentication flows

- Moderne authenticatie implementeren
  - SPA's configureren met authorization code flow en PKCE
  - Platform specifieke authentication settings instellen
  - Veilige redirect URI patronen implementeren

- API permissions en autorisatie beheren
  - Delegated permissions configureren volgens least privilege
  - Verschil tussen delegated en application permissions
  - Juiste consent workflows implementeren

- Geavanceerde security features
  - App roles maken en beheren voor fijnmazige autorisatie
  - Baseline user roles ontwerpen om privilege escalation te voorkomen
  - Certificate based authenticatie boven client secrets

- Behandelde security best practices
  - Moderne authentication flows; authorization code flow met PKCE, correcte token handling/validatie, veilig credential management (certificates boven secrets)
  - Access control; least privilege bij permission requests, role based access control via app roles, duidelijke scheiding tussen user en application permissions
  - Workload identity security; managed identities als voorkeur voor Azure workloads, veilig service principal beheer, certificate based authenticatie

- Moderne terminologie en tools
  - Microsoft Entra admin center als primaire management interface
  - Workload identities voor non human identity management
  - Application objects en service principals relatie
  - PKCE en CORS voor moderne web app security

- Onthouden voor examen
  - Deze module vat samen wat je al in detail hebt geleerd: application object vs service principal, single/multitenant, PKCE bij SPAs, app roles vs group claims, en de voorkeur voor managed identities/certificates boven secrets

---
---




























  
