# SC-300: Microsoft Identity and Access Administrator
## Learning Path 5: Plan and implement an identity governance strategy
### Module 1: Plan and implement entitlement management
### Introduction

- Waarom dit belangrijk is
  - Nieuwe of externe users moeten toegang krijgen tot resources; wachten op toegang kost engagement en productiviteit
  - Deze module leert hoe je juiste toegang toewijst, reviews opzet, en meer

- Learning objectives
  - Define catalogs
  - Define access packages
  - Plan, implement, and manage entitlements
  - Implement and manage terms of use
  - Manage the lifecycle of external users in Microsoft Entra Identity Governance settings
  - Configure and manage connected organizations
  - Review per-user entitlements

---

### Define access packages

- Waarom entitlement management
  - Users weten vaak niet welke toegang ze nodig hebben, of vinden moeilijk wie hun toegang moet goedkeuren
  - Eenmaal toegewezen, houden users toegang vaak langer dan zakelijk nodig
  - Extra problematisch bij externe users (supply chain partners, andere organisaties)
  - Entitlement management zorgt dat iedereen consistent en correct toegang krijgt tot de juiste directories

- Kerncapabilities (examen kernstof)
  - Delegeren aan non-administrators; zij kunnen access packages maken met eigen policies (wie mag aanvragen, wie moet goedkeuren, wanneer verloopt toegang)
  - Connected organizations selecteren; externe users die nog niet in de directory staan worden bij goedkeuring automatisch uitgenodigd en toegewezen. Bij verlopen toegang (zonder andere assignments) wordt hun B2B account automatisch verwijderd

- Terminologie (examen kernstof, cruciaal om te kennen)
  - Access package; bundel resources die een team/project nodig heeft, gegovern met policies, altijd in een catalog
  - Access request; verzoek om toegang tot een access package, gaat door een approval workflow
  - Assignment; toewijzing van een access package aan een user, geeft alle resource roles van dat package, meestal met een tijdslimiet
  - Catalog; container van gerelateerde resources en access packages, voor delegatie zodat non-admins eigen packages kunnen maken
  - Catalog creator; users geautoriseerd om nieuwe catalogs te maken, worden automatisch owner van de catalog die ze aanmaken
  - Connected organization; externe Entra directory/domein waarmee je een relatie hebt, users daarvan kunnen in een policy toegestaan worden om aan te vragen
  - Policy; regels voor de access lifecycle (hoe krijg je toegang, wie keurt goed, hoe lang), gelinkt aan 1 access package. Een package kan meerdere policies hebben (bv. 1 voor employees, 1 voor externe users)
  - Resource; een asset (Office group, security group, applicatie, SharePoint site) met een rol die toegewezen kan worden
  - Resource directory; directory met 1 of meer te delen resources
  - Resource role; permissies gekoppeld aan een resource. Group heeft 2 rollen (member, owner), SharePoint sites meestal 3 (kan custom uitgebreid worden), apps kunnen custom roles hebben

- Wat een access package is en welke resources je ermee kunt beheren
  - Bundel van alle resources + access die een user nodig heeft voor een project/taak
  - Governt toegang voor interne employees EN externe users
  - Resources die je ermee kunt beheren:
    - Membership van Entra security groups
    - Membership van M365 Groups en Teams
    - Assignment aan Entra enterprise applications (incl. SaaS en custom geintegreerde apps met federation/SSO en/of provisioning)
    - Membership van SharePoint Online sites
  - Indirect ook: M365 licenties (via group-based licensing op een security group in het package), Azure resource management (via Azure role assignment op de group), Entra role management (via role-assignable groups)

- Hoe je bepaalt wie toegang krijgt
  - Admin of delegated access package manager lijst resources (groups, apps, sites) + benodigde rollen op
  - 1 of meer policies definieren de regels: wie mag aanvragen, wie moet goedkeuren, hoe lang de toegang geldig is (met expiratie als niet verlengd)

- Wanneer access packages gebruiken (examen kernstof)
  - Employees hebben tijdelijke toegang nodig voor een specifieke taak (bv. extra toegang tot resources van een andere afdeling, naast standaard group-based licensing/dynamic groups voor basis toegang zoals Exchange mailbox)
  - Toegang vereist goedkeuring van een manager of andere aangewezen persoon
  - Afdelingen willen hun eigen access policies beheren zonder IT tussenkomst
  - 2+ organisaties werken samen aan een project, meerdere users van de ene organisatie moeten via B2B toegang krijgen tot resources van de andere

- Voorbeeld structuur (uit diagram)
  - Access package 1; 1 group als resource, 1 policy die een set directory users laat aanvragen
  - Access package 2; group + applicatie + SharePoint site als resources, 2 policies (1 voor interne directory users, 1 voor externe directory users)

- Onthouden voor examen
  - Access package = altijd in een catalog, kan meerdere policies hebben voor verschillende doelgroepen (intern vs extern)
  - Externe B2B users die via entitlement management binnenkomen worden automatisch verwijderd zodra hun laatste assignment verloopt
  - Access packages vervangen geen bestaande mechanismen (group-based licensing, dynamic groups); ze zijn bedoeld voor tijdelijke, goedkeuring-vereisende, of cross-organisatie toegang

---

### Exercise: create and manage a resource catalog with Microsoft Entra entitlement management
  - [04-sc300/labs/23-create-and-manage-a-resource-catalog-with-microsoft-entra-entitlement-management](../../04-sc300/labs/23-create-and-manage-a-resource-catalog-with-microsoft-entra-entitlement-management.md)

---

### Configure entitlement management

- Rollen bij het opzetten
  - Administrator; delegeert beheer van resources
  - Catalog creator; delegeert beheer van resources
  - Catalog owner; delegeert beheer van resources, en delegeert beheer van access packages via de access package manager rol

- Toegang beheren voor users binnen de organisatie
  - Access package manager; laat employees toegang aanvragen tot resources
  - Requestor; vraagt toegang aan tot resources, kan ook zien welke resources hij al heeft
  - Approver; keurt requests goed

- Toegang beheren voor users buiten de organisatie
  - Administrator; werkt samen met een externe partnerorganisatie
  - Access package manager; werkt samen met een externe partnerorganisatie
  - Requestor; vraagt toegang aan als externe user, kan zien welke resources al toegekend zijn
  - Approver; keurt requests goed

- Dagelijks beheer (access package manager taken)
  - Resources van een project updaten
  - Duur van een project updaten
  - Manier van goedkeuren updaten
  - Betrokken personen updaten
  - Specifieke users direct toewijzen aan een access package

- Assignments en rapportages
  - Administrator; ziet wie assignments heeft op een access package, en welke resources aan users toegewezen zijn

- Programmatisch beheren
  - Access packages, catalogs, policies, requests, en assignments beheerbaar via Microsoft Graph
  - Vereist een user in de juiste rol, met een applicatie die de delegated permission EntitlementManagement.ReadWrite.All heeft
  - Aanroepbaar via de entitlement management API

- Onthouden voor examen
  - Catalog owner kan zowel resources beheren als access package management delegeren naar een access package manager
  - Access package manager is de dagelijkse beheerrol (resources, duur, approval flow, mensen, directe assignments)
  - Requestor en Approver zijn de rollen aan de gebruikerskant van het proces, zowel intern als extern
  - Programmatisch beheer via Graph vereist de EntitlementManagement.ReadWrite.All permission
    
---

### Exercise: add terms of use acceptance report
  - [04-sc300/labs/24-add-terms-of-use-acceptance-report](../../04-sc300/labs/24-add-terms-of-use-acceptance-report.md)

---

### Exercise: amanage the lifecycle of external users with Microsoft Entra identity governance
  - [04-sc300/labs/25-manage-the-lifecycle-of-external-users-with-microsoft-entra-identity-governance](../../04-sc300/labs/25-manage-the-lifecycle-of-external-users-with-microsoft-entra-identity-governance.md)

---

### Configure and manage connected organizations

- Wat een connected organization is
  - Externe organisatie waarmee je een relatie hebt, waarvan users toegang moeten kunnen krijgen tot jouw resources (bv. SharePoint sites, apps)
  - Aangezien deze externe users meestal nog niet in jouw Entra directory staan, gebruik je entitlement management om ze naar behoefte binnen te brengen

- 3 manieren om een connected organization te specificeren (examen kernstof)
  - Users in een andere Entra directory (vanuit elke Microsoft cloud)
  - Users in een non-Entra directory die geconfigureerd is voor direct federation
  - Users in een non-Entra directory, waarvan alle email adressen dezelfde domeinnaam delen

- Connected organization toevoegen (stappen, vereist Identity Governance administrator of User administrator rol)
  1. ID Governance > Entitlement management > Connected organizations > + Add connected organization
  2. Basics tab; display name en description invullen. State wordt automatisch Configured
  3. Directory + domain tab; + Add directory + domain
  4. Zoeken op volledige domeinnaam, organisatienaam en authentication type controleren
  5. Add om de directory/domain toe te voegen (max 1 per connected organization)
  6. Select
  7. Sponsors tab (optioneel); interne of externe users toevoegen als sponsor, het aanspreekpunt voor deze relatie. Add/Remove opent een lijst van users/groups in de directory
  8. Review + create tab; instellingen controleren, Create

- Onthouden voor examen
  - Max 1 directory of domain per connected organization
  - 3 herkenbare types externe organisaties: Entra directory, gefedereerde non-Entra directory, of gedeelde email domain zonder federatie
  - Sponsors zijn optioneel en dienen als contactpersoon, niet als technische vereiste

---

### Review per-user entitlements

- Wat je kunt zien
  - Wie is toegewezen aan access packages, hun policy, en status
  - Bij een geschikte policy: ook direct users toewijzen aan een access package

- Governance
  - Zero trust principe: regelmatig entitlement packages reviewen
  - Ingebouwde tools om dit te ondersteunen

- Assignments bekijken (vereiste rollen, examen kernstof)
  - Identity Governance administrator
  - User administrator
  - Catalog owner
  - Access package manager
  - Access package assignment manager

- Stappen om assignments te reviewen
  1. ID Governance > Entitlement management > Access packages > package openen
  2. Assignments; lijst van actieve assignments
  3. Specifieke assignment selecteren voor extra details
  4. Filter status op Delivering; toont assignments waarbij niet alle resource roles correct geprovisioned zijn. Meer detail te vinden via de bijbehorende request op de Requests page
  5. Filter status op Expired; toont verlopen assignments
  6. Download; CSV export van de gefilterde lijst

- Assignments reviewen via PowerShell
  - Query mogelijk voor scripting/automation
  - Voorbeeld flow: Connect-MgGraph met scope EntitlementManagement.Read.All, beta profile selecteren, Get-MgEntitlementManagementAccessPackage om het package op te halen, Get-MgEntitlementManagementAccessPackageAssignment om de assignments op te halen

- Assignment verwijderen (stappen)
  1. ID Governance > Entitlement management > Access packages > package openen
  2. Assignments
  3. Checkbox naast de betreffende user aanvinken
  4. Remove knop

- Onthouden voor examen
  - 5 rollen kunnen assignments bekijken, met verschillende scope (catalog owner vs volledige Identity Governance administrator)
  - Delivering filter = provisioning problemen, Expired filter = verlopen toegang, dit zijn 2 losse statussen om op te filteren
  - PowerShell/Graph maakt scripting en automation van entitlement review mogelijk, los van de portal UI

---

## Module Assessment — Module 1 (Plan and implement entitlement management)

**Score:** 100%

### Vraag 1
What items contained within the catalogs of Microsoft Entra entitlements?

- Device registrations
- ✅ Resources and access packages
- User lists

### Vraag 2
What is the default retention period for deleted users in Microsoft Entra ID?

- 14 days
- ✅ 30 days
- 60 days

### Vraag 3
Your company intends to utilize entitlements for resource access control. What is the most typical use case for an access package in this context?

- To allow one organization access when collaborating on a project.
- An employee requires permanent permissions to perform their job role.
- ✅ For access that requires the approval of an employee's manager or other designated individuals

---

# SC-300: Microsoft Identity and Access Administrator
## Learning Path 5: Plan and implement an identity governance strategy
### Module 2: Plan, implement, and manage access review
### Introduction

- Waarom access reviews belangrijk zijn
  - Naarmate organisaties groeien wordt beheer van wie toegang heeft moeilijker
  - Employees veranderen van rol, guests stapelen ongebruikte permissions op, privileged assignments blijven bestaan na afloop van een project
  - Zonder systematische review accumuleert risico, en volgen audit findings snel

- Wat access reviews doen
  - Gestructureerde manier om user access drift te managen
  - Periodieke reviews van group memberships, application assignments, en privileged role assignments
  - Uitkomst automatiseerbaar; toegang verwijderen die door reviewers wordt afgekeurd, zonder handmatige follow up

- Wat deze module behandelt
  - Access reviews plannen en implementeren binnen Entra ID Governance
  - Waarom ze belangrijk zijn voor security posture
  - Aanmaken/configureren voor verschillende resource types
  - Monitoren en automatiseren van uitkomsten
  - Access Review Agent; gebruikt AI om reviewers te begeleiden, direct in Microsoft Teams

- Learning objectives
  - Plan for access reviews
  - Create access reviews for groups and apps
  - Monitor access review findings
  - Create and manage access review programs
  - Automate access review management tasks
  - Configure recurring access reviews
  - Describe the Access Review Agent and how it helps reviewers complete acess reviews

- Prerequisites
  - Kennis van Entra user creation en access management

- Licentie note
  - Sommige features vereisen Entra ID Governance of Entra Suite subscription
  - Sommige capabilities werken al met Entra ID P2
  - Licenties vooraf checken voor deployment

---

### Plan for access reviews

- Wat een access review is
  - Geplande review van access needs, rights, en history van user access
  - Zorgt dat de juiste mensen de juiste toegang hebben tot de juiste resources
  - Mitigeert access risico door beschermen, monitoren, en auditen van toegang tot kritieke assets, terwijl productiviteit behouden blijft
  - Feature van Entra ID Governance, vereist Entra ID Governance of Entra Suite subscription; sommige capabilities werken met P2

- Juiste stakeholders betrekken (examen kernstof)
  - IT administration; beheert infrastructuur, reviewt privileged access, plant reviews op exception-list groups, bewaakt service principal toegang
  - Security teams; zorgen dat het plan aan security vereisten voldoet, Zero Trust afdwingen, least privilege, centraal overzicht van wie toegang heeft
  - Development teams; bouwen/onderhouden apps, controleren toegang tot SaaS/PaaS/IaaS componenten, beheren groups voor interne app development
  - Business units; beheren projecten en eigen apps, keuren toegang tot groups/apps goed of af voor interne/externe users
  - Corporate governance; zorgt dat de organisatie intern beleid en regelgeving naleeft

- Wat Entra ID Governance is
  - Balanceert security en employee productivity via processen en zichtbaarheid
  - Beantwoordt 4 kernvragen: welke users moeten toegang hebben tot welke resources, wat doen ze met die toegang, zijn er effectieve controls, kunnen auditors verifieren dat controls werken

- Pilot plannen
  - Start met een kleine groep en non-kritieke resources
  - Aanbevolen: reviews zonder automatische toepassing van resultaten (zelf controle houden), geldige email adressen voor alle users, verwijderde toegang documenteren voor snel herstel indien nodig, audit logs monitoren

- Resource types die gereviewd kunnen worden
  - User access tot apps geintegreerd met SSO (SaaS, LOB)
  - Group membership (gesynct, of aangemaakt in Entra ID/M365, incl. Teams)
  - Access Package (bundel van groups/apps/sites)
  - Entra roles en Azure Resource roles via PIM
  - Custom data resources (preview), via externe resource types gekoppeld aan Entra ID Governance

- Wie mag access reviews aanmaken/beheren/lezen (examen kernstof, per resource type)

| Resource type | Kan aanmaken/beheren | Kan resultaten lezen |
|---|---|---|
| Group of application | Global Administrator, User Administrator, Identity Governance administrator, Privileged Role administrator (alleen Entra assignable groups), Group owner | Global administrator, Global reader, User administrator, Identity Governance Administrator, Privileged Role Administrator, Security reader, Group owner |
| Microsoft Entra role | Global Administrator, Privileged Role Administrator | Global administrator, Global reader, User administrator, Privileged Role Administrator, Security reader |
| Azure resource roles | Global Administrator, User Access Administrator, Resource Owner | Global Administrator, User Access Administrator, Resource owner, Reader (voor de resource) |
| Access package | Global Administrator, User Administrator, Identity Governance Administrator | Global reader, User administrator, Identity Governance administrator, Security reader |

- Wie voert de review uit
  - Bepaald door de creator bij aanmaken, niet meer wijzigbaar na start
  - 3 reviewer personas: Resource Owners (business owners), individueel geselecteerde delegates, of end users die zelf attesteren (self-review)
  - 1 of meer reviewers mogelijk, elke reviewer kan de review starten/uitvoeren en toegang goedkeuren of intrekken

- Componenten van een access review policy (examen kernstof, checklist)
  - Welke resource(s) reviewen
  - Wiens toegang wordt gereviewd
  - Hoe vaak
  - Wie voert de review uit
  - Hoe worden ze genotificeerd
  - Welke deadline geldt
  - Welke automatische acties bij het resultaat
  - Wat gebeurt als de reviewer niet op tijd reageert
  - Welke handmatige acties op basis van het resultaat
  - Welke communicatie bij genomen acties

- Voorbeeld access review plan (illustratief)
  - Resource: toegang tot Microsoft Dynamics
  - Frequency: maandelijks
  - Reviewer: Dynamics business group program managers
  - Notificatie: email 24u vooraf
  - Timeline: 48u na notificatie
  - Automatische actie: toegang verwijderen bij geen interactive sign-in binnen 90 dagen
  - Communicatie: email naar verwijderde users met uitleg en hersteloptie

- Access reviews plannen voor access packages
  - Access packages vereenvoudigen governance/review strategie enorm
  - Reviews worden geconfigureerd tijdens het aanmaken/bewerken van een access package policy

- Access reviews plannen voor groups
  - Naast access packages de meest effectieve manier om toegang te governen
  - Aanbevolen: toegang toewijzen via security/M365 groups, users toevoegen aan die groups
  - 1 group kan gekoppeld worden aan meerdere resources of een heel access package; je reviewt dan de group i.p.v. elke individuele app-toegang
  - Group membership reviewbaar door: administrators, group owners, geselecteerde delegates, of members zelf (self-attestation)

- Group ownership, per group type
  - M365/Entra ID groups; hebben meestal al gedefinieerde owners, meestal de beste reviewers (bv. Teams-creator wordt automatisch owner)
  - Handmatig aangemaakte groups (portal/Graph); mogelijk geen owner gedefinieerd, aanbevolen om die zelf toe te wijzen
  - On-premises gesynchroniseerde groups; kunnen geen owner hebben in Entra ID, dus reviewer handmatig aanwijzen
  - Aanbevolen: business policies opstellen voor group creation om duidelijke ownership te waarborgen

- Exclusion groups in CA policies reviewen
  - Sommige groups worden bewust uitgesloten van een Conditional Access policy (bv. sales team dat veel reist, uitgesloten van een "alleen op corporate netwerk" policy)
  - Membership van dit soort exclusion groups moet ook gereviewd worden

- External users' group memberships reviewen
  - Dynamic Groups aanbevolen om membership te baseren op user attributes, vermindert handmatig werk en fouten
  - Interne sponsor kan als reviewer optreden voor deze groups

- On-premises groups reviewen
  - Access reviews kunnen de membership van gesynchroniseerde on-prem groups NIET wijzigen (source of authority is on-prem)
  - Reviews wel te gebruiken om regelmatige controle te plannen; reviewer voert de daadwerkelijke actie uit in de on-prem group zelf
  - Resultaten beschikbaar via CSV of Microsoft Graph voor verdere verwerking

- Access reviews plannen voor applicaties
  - Reviewen wanneer je specifiek wilt weten wie toegang heeft tot 1 app (i.p.v. een package of group)
  - Aanbevolen scenario's: directe toegang buiten een group/package om, app met gevoelige info, compliance vereisten, vermoeden van ongepaste toegang
  - Apps hebben niet altijd een owner in Entra ID, dus "app owner als reviewer" is niet altijd een optie
  - Review kan gescoped worden tot alleen guest users op de app, i.p.v. alle toegang

- Review van Entra en Azure resource roles
  - PIM vereenvoudigt beheer van privileged access, houdt de lijst van privileged roles kleiner
  - Reviews voor deze roltypes zijn geintegreerd in de PIM admin experience
  - Aanbevolen regelmatig te reviewen: Global Administrator, User Administrator, Privileged Authentication Administrator, Conditional Access Administrator, Security Administrator, en alle M365/Dynamics Service Administration roles

- Access reviews API (Microsoft Graph)
  - Beschikbaar voor zowel application als user context
  - Application context vereist de permission AccessReview.Read.All op de service principal
  - Veelvoorkomende automatiseerbare taken: review aanmaken/starten, handmatig eindigen, lopende reviews + status opvragen, historie van een review series, decisions verzamelen (incl. decisions die afwijken van de systeemaanbeveling)
  - Aanbevolen: Graph Explorer gebruiken om queries te bouwen/testen voor je ze in scripts zet

- Access reviews monitoren
  - Activiteiten vastgelegd in Entra audit logs, filterbaar op category/activity type/date range
  - Voor geavanceerdere analyse: audit logs exporteren naar Azure Log Analytics of Azure Event Hubs

- Communicatie plannen
  - Access reviews verschuiven verantwoordelijkheid van IT naar business owners; dit is een culturele verandering die je moet communiceren
  - IT blijft wel verantwoordelijk voor infrastructuur-gerelateerde toegang en privileged role assignments
  - Reviewers krijgen email notificaties bij nieuwe reviews en reminders voor expiratie (op de helft of 1 dag van tevoren, instelbaar)
  - Email aan reviewers customizable met persoonlijk bericht, links naar instructies, en self-review guidance
  - Reviewers komen via de MyAccess portal, die een overzicht + systeemaanbevelingen toont (gebaseerd op laatste sign-in en access info)

- Licentievereisten (examen kernstof)
  - Entra ID Premium P2 licentie vereist per member/guest user die: als reviewer is toegewezen, een self-review uitvoert, group owner is die een review uitvoert, of application owner is die een review uitvoert
  - GEEN licentie nodig voor Global Administrator/User Administrator die reviews opzetten, instellingen configureren, of decisions toepassen

- Onthouden voor examen
  - Access reviews kunnen de membership van on-prem gesynchroniseerde groups niet direct wijzigen, alleen als planningstool dienen
  - P2 licentie nodig voor wie de review daadwerkelijk uitvoert (reviewer/self-review/owner), niet voor wie het opzet als admin
  - 3 reviewer personas: resource owners, delegates, self-attestation
  - Reviewer keuze is definitief zodra de review gestart is, niet meer te wijzigen

---

### Create access reviews for groups and apps

- Prerequisites
  - Entra ID Governance of Entra Suite (P2 biedt beperkte capabilities)
  - Identity Governance Administrator of Global Administrator

- Access review aanmaken (stappen, examen kernstof)
  1. Minimaal Identity Governance Administrator
  2. ID Governance > Access reviews > New access review
  3. Template: Review access to a resource type
  4. Resource type kiezen om te reviewen

- Als Teams + Groups gekozen
  - All Microsoft 365 groups with guest users; recurring reviews op alle guest users over alle Teams/M365 groups, exclusies mogelijk
  - Select teams + groups; specifieke, vaste set groups selecteren

- Als Applications gekozen
  - 1 of meer applicaties selecteren

- Scope van de review
  - Guest users only; alleen B2B guest users
  - Everyone; alle user objects gekoppeld aan de resource
  - Let op: bij "All M365 groups with guest users" is Guest users only de enige optie
  - Bij group membership reviews: optie om alleen inactive users te targeten (tot 730 dagen inactief)

- Reviewers selecteren
  - Group owner(s) (alleen bij team/group review)
  - Selected user(s) or group(s)
  - Users review their own access (self-review)
  - Managers of users
  - Bij Managers of users of Group owner(s): fallback reviewer instelbaar, voor als de user geen manager heeft of de group geen owner heeft

- Recurrence instellen
  - Frequency: Weekly, Monthly, Quarterly, Semi-annually, Annually
  - Duration: hoe lang de review open staat voor reviewer input (bv. max 27 dagen bij monthly, om overlap te voorkomen)
  - Start date en End date instelbaar

- Upon completion settings (examen kernstof)
  - Auto apply results to resource: Enable = automatisch toegang verwijderen bij denied users, Disable = handmatig toepassen
  - If reviewers don't respond, opties:
    - No change; toegang blijft ongewijzigd
    - Remove access; toegang wordt verwijderd
    - Approve access; toegang wordt goedgekeurd
    - Take recommendations; systeemaanbeveling wordt gevolgd
  - Dit geldt alleen voor niet-gereviewde users; bij een expliciete Deny van de reviewer wordt toegang altijd verwijderd

- Action to apply on denied guest users (examen kernstof)
  - Remove user's membership from the resource; verwijdert toegang tot de group/app, tenant sign-in blijft werken
  - Block user from signing in for 30 days, then remove user from the tenant; blokkeert volledige tenant sign-in, na 30 dagen definitief verwijderd tenzij eerder herstelt
  - Niet configureerbaar bij reviews die breder zijn dan alleen guest users, of bij "All M365 groups with guest users" (dan altijd de eerste, mildere optie)

- Review decision helpers
  - Optie om de reviewer aanbevelingen te laten zien tijdens het review proces

- Advanced settings
  - Justification required; reviewer moet reden geven bij goedkeuring
  - Email notifications; bij start van de review naar reviewers, bij afronding naar admins
  - Reminders; automatisch op de helft van de review duur naar reviewers die nog niet klaar zijn
  - Additional content for reviewer email; extra instructies/contactinfo toe te voegen aan de autogenerated email
  - Access Review Agent (Preview); laat reviewers de review afhandelen in Microsoft Teams via natural language, insights, en aanbevelingen (vereist extra setup)

- Afronden
  - Naam en optionele description geven (zichtbaar voor reviewers)
  - Create, daarna Start om de review daadwerkelijk te laten beginnen

- Start van de review
  - Entra ID stuurt standaard een email naar reviewers kort na start
  - Als je dat uitschakelt: zelf reviewers informeren
  - Guest reviewers die hun invite nog niet geaccepteerd hebben, krijgen geen email totdat ze de invite accepteren

- Access review status tabel (examen kernstof)

| Status | Betekenis |
|---|---|
| NotStarted | Review aangemaakt, user discovery moet nog beginnen |
| Initializing | User discovery loopt, identificeert alle betrokken users |
| Starting | Review start, emails worden verstuurd indien enabled |
| InProgress | Review loopt, reviewers kunnen decisions indienen tot de due date |
| Completing | Review wordt afgerond, emails naar de review owner |
| Auto-Reviewing | Systeem registreert decisions voor niet-gereviewde users op basis van aanbevelingen/preconfigured settings |
| Auto-Reviewed | Systeem decisions voor alle niet-gereviewde users vastgelegd, klaar voor Applying indien Auto-Apply enabled |
| Applying | Geen wijziging voor approved users |
| Applied | Denied users worden verwijderd uit de resource/directory |
| Failed | Review kon niet doorgaan (bv. door tenant deletion, licentiewijziging, of andere interne tenant wijzigingen) |

- Reviews aanmaken via APIs
  - Alles wat via de portal UI kan, kan ook via Microsoft Graph APIs

- Onthouden voor examen
  - Auto apply results bepaalt of denied access automatisch of handmatig wordt toegepast
  - Guest users hebben een extra, specifieke denial-actie optie (block + delayed removal) die members niet hebben
  - Fallback reviewer alleen relevant bij Manager of Group owner als reviewer-type
  - Access Review Agent is een Teams geintegreerde, AI-gestuurde manier om reviews te voltooien

---

### Create and configure access reviews programmatically

- Wat het is
  - Access reviews programmatisch implementeren via de access reviews API in Microsoft Graph
  - Nodig: user met minimaal Identity Governance Administrator rol + app met delegated AccessReview.ReadWrite.All permission, OF een app met de application permission AccessReview.ReadWrite.All

- PowerShell alternatief
  - New-MgIdentityGovernanceAccessReviewDefinition cmdlet, uit de Microsoft Graph PowerShell cmdlets for Identity Governance module

- Waarvoor te gebruiken
  - Audit en attest access die identities hebben tot resources (bv. SharePoint site met klant contactinfo)
  - Check en attesteer toegang tot groups en, via extensie, de resources die daaraan gekoppeld zijn

- Hoge-niveau stappen (security groups voorbeeld, examen kernstof)
  1. Access review aanmaken voor de security group
  2. Instances van de review opvragen
  3. Verifieren wie gecontacteerd is voor de review
  4. Decisions opvragen
  5. Self-attesteren op een pending access decision
  6. Decisions en status van de review bevestigen
  7. Resources opschonen

- Onthouden voor examen
  - Application context vereist AccessReview.ReadWrite.All als application permission; user context vereist Identity Governance Administrator + delegated permission

---

### Monitor access review findings

- Toegang tot een pending review
  - Via de notification email (Start review link), of direct via myaccess.microsoft.com > Access reviews
  - Als er geen reviews verschijnen: geen actie nodig, er is niks te reviewen

- 2 manieren om te beslissen
  - Handmatig per user (of meerdere) approve/deny
  - Systeemaanbevelingen accepteren

- Handmatig approven/denyen (stappen)
  1. Cirkel naast 1 of meer users selecteren
  2. Approve of Deny knop
  3. "Don't know" optie beschikbaar; user houdt toegang, keuze wordt gelogd in audit logs
  4. Reden invullen (evt. verplicht gesteld door de admin, anders optioneel maar wel zichtbaar voor andere reviewers)
  5. Save

- Belangrijk over uitkomsten
  - Denied user wordt niet meteen verwijderd; pas bij einde van de review periode, of als een admin de review stopt met Auto apply enabled
  - Bij meerdere reviewers: de laatst ingediende beslissing wordt vastgelegd (bv. Alice approved eerst, Bob denied later op dezelfde request → denied telt)

- Aanbevelingen accepteren (2 methodes waarop het systeem genereert, examen kernstof)
  - No sign-in within 30 days; user zonder sign-in in 30 dagen wordt aanbevolen voor denial, laatste sign-in datum wordt getoond
  - Peer outlier; als een user afwikende toegang heeft t.o.v. peers in de reporting structuur, wordt denial aanbevolen
  - Accepteren: 1 of meer users selecteren > Accept recommendations, of niks selecteren om het voor alle niet-gereviewde users toe te passen > Submit

---

### Automate access review management tasks

- Auto apply results to resource
  - Enable = niet-goedgekeurde users worden automatisch verwijderd bij afronding van de review (group membership, application assignment, of privileged role recht)

- Take recommendations
  - Recommendations tonen laatste sign-in of laatste app-toegang, om reviewers te helpen
  - "Take recommendations" volgt de aanbeveling automatisch; wordt ook automatisch toegepast op users waar de reviewer niet op gereageerd heeft
  - Gebaseerd op de criteria in de review (bv. 30 dagen geen sign-in, geldt voor interactive en non-interactive sign-ins), of op peer outlier analyse

- Guest user access reviewen
  - Gebruikt om collaboration partner identities van externe organisaties op te schonen, kan compliance vereisten ondersteunen
  - Externe identities krijgen toegang via: toegevoegd aan een group, uitgenodigd voor Teams, toegewezen aan een enterprise app of access package, of toegewezen aan een privileged role (Entra ID of Azure subscription)
  - Sample script beschikbaar om te zien waar externe identities gebruikt worden binnen Entra ID (niet buiten Entra ID, zoals directe SharePoint rechten zonder groups)
  - Bij het aanmaken van een review: scope kiezen tussen Everyone of Guest users only

---

### Configure recurring access reviews

- Instelbaar
  - Naam, start date, frequency, duration, en einde van de serie: Never, specifieke einddatum, of vast aantal occurrences
  - Reviewers genotificeerd bij start van elke review, kunnen approven/denyen met smart recommendations

- Waarom belangrijk
  - Lifecycle management; alles wat begint moet een eind hebben
  - Regelmatig checken of permissions nog kloppen (niet te veel, niet te weinig)

- Serie bijwerken (examen kernstof)
  - Settings/reviewers aanpasbaar op elk moment nadat de serie gestart is
  - Current instance; alleen de actieve review wordt aangepast
  - Series; alle toekomstige recurrences worden aangepast
  - Voorbeeld: reviewer verlaat de organisatie → Series updaten om die persoon overal te vervangen. Alleen instelling voor de lopende review aanpassen → Current instance updaten

---

### Explore the Access Review Agent in Microsoft Entra

- Probleem dat het oplost
  - Access reviews zijn historisch een handmatig proces, foutgevoelig
  - Reviewers hebben niet altijd toegang tot de juiste data, of te weinig tijd

- Wat de Access Review Agent doet
  - Levert insights en aanbevelingen zodat reviewers via een simpel gesprek in Microsoft Teams hun werk kunnen doen
  - Scant proactief naar actieve access reviews in de tenant
  - Analyseert reviews, verzamelt extra insights, genereert een aanbeveling (approve/deny) met justificatie samenvatting
  - Begeleidt reviewers in natural language door het hele proces, reviewer kan de redenering bekijken, vragen stellen, en zelf de uiteindelijke beslissing nemen
  - Aanbeveling gebaseerd op een deterministic scoring mechanisme met meerdere signalen

- Signalen die de agent meeneemt (examen kernstof)
  - User inactivity; recent wel/niet ingelogd
  - User-to-Group affiliation; lage affiniteit met andere users die deze toegang hebben
  - Account enabled; accountEnabled property
  - Employment status; employeeLeaveDateTime property
  - Lifecycle workflow history; mover workflow in de laatste 30 dagen
  - Decisions from previous reviews; bij recurring reviews, eerdere iteraties meegenomen
  - Access request history; bij access package assignment reviews, de request/approval historie

- Prerequisites (examen kernstof)
  - Entra ID Governance of Entra Suite licenties
  - Onboarding bij Security Copilot met minimaal 1 security compute unit (SCU)
  - Admin rollen nodig om de agent op te zetten: Identity Governance Administrator, Lifecycle Workflows Administrator, Security Copilot Contributor
  - Reviewers die de agent gebruiken: toegang tot Microsoft Teams, een actieve toegewezen review, en de rol Security Copilot Contributor

- Limitations
  - Eenmaal gestart kan de agent niet gestopt/gepauzeerd worden
  - Kan een paar minuten duren om te draaien, aanbevolen om te starten vanuit het Entra admin center

- Access Review Agent inschakelen (stappen)
  1. Inloggen met alle vereiste rollen (Identity Governance Administrator, Lifecycle Workflows Administrator, Security Copilot Contributor)
  2. Nieuwe home page > Go to agents, of Agents in het linker menu
  3. Access Review Agent tile > View details
  4. Start agent

- Agent inschakelen voor een bestaande review (stappen)
  1. Minimaal Identity Governance Administrator
  2. ID Governance > Access reviews > gewenste review selecteren
  3. Settings (onder Manage voor one time review, of onder Series voor recurring review)
  4. Advanced Settings > Access Review Agent (Preview) aanvinken
  5. Save

- Onthouden voor examen
  - Access Review Agent vereist naast Entra ID Governance ook een Security Copilot onboarding met SCUs, dit is een extra losse licentie/kostenstructuur
  - De agent geeft aanbevelingen, maar de reviewer neemt zelf de uiteindelijke beslissing
  - Agent kan niet gestopt/gepauzeerd worden na start

---

## Module Assessment — Module 2 (Plan, implement, and manage access review)

**Score:** 100%

### Vraag 1
Who should be engaged when planning a technology project?

- ✅ Engage the right stakeholders.
- Start planning with a small team to avoid extra work for others.
- Keep your team small to avoid project creep.

### Vraag 2
What is one reason to regularly review Azure role assignments?

- To ensure naming conventions are properly applied.
- ✅ To reduce the risk associated with stale role assignments.
- To eliminate extra distribution groups that are no longer used.

### Vraag 3
What is an access package?

- An access package is a group of users with the access they need to work on a project or perform a task.
- ✅ An access package is a bundle of all the resources with the access a user needs to work on a project or perform their task.
- An access package is a used to create a transitive trust between B2B organizations.

---












