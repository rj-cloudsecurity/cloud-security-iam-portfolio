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



















