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
  - Describe the Access Review Agent and how it helps reviewers complete access reviews

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









