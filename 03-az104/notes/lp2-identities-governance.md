# AZ-104: Azure Administrator Associate
## Learning Path 2: Manage identities and governance in Azure

  - **AZ-104 Started:** 11-4-2026
  - **AZ-104 Exam passed:** 

  ---
  
## Inhoudsopgave

### Learning Path 2: Manage identities and governance in Azure

- [Module 1: Understand Microsoft Entra ID](#module-1-understand-microsoft-entra-id)
- [Module 2: Create, configure, and manage identities](#module-2-create-configure-and-manage-identities)
- [Module 3: Describe the core architectural components of Azure](#module-3-describe-the-core-architectural-components-of-azure)
- [Module 4: Azure Policy initiatives](#module-4-azure-policy-initiatives)
- [Module 5: Secure your Azure resources with Azure role-based access control (Azure RBAC)](#module-5-secure-your-azure-resources-with-azure-role-based-access-control-azure-rbac)
- [Module 6: Allow users to reset their password with Microsoft Entra self-service password reset](#module-6-allow-users-to-reset-their-password-with-microsoft-entra-self-service-password-reset)

  ---

## Learning Path 2: Manage identities and governance in Azure
### Module 1: Understand Microsoft Entra ID 


**Examine Microsoft Entra ID**
  - Microsoft Entra ID is een PaaS directory service beheerd door Microsoft in de cloud; geen eigen infrastructure nodig, maar ook minder controle over de implementatie
  - Verschil met AD DS: AD DS draait als service op Windows Server (domain controller) en is gericht op on-premises apps. Entra ID is gericht op web-based appes en cloud resources
  - Mogelijkheiden: SSO, MFA, identity protection, SSPR, Conditional Access, Application Proxy, federation tussen organisaties
  - Gratis tier is automatisch inbegrepen bij elke Azure subscription. Premium features vereisen betaalde tiers (Basic/Premium), deels automatisch inbegrepen bij Microsoft 365

  - Tenants
    - Entra ID is multi-tenatn by design; elke tenant is een geisoleerde directory instantie
    - Een tenatn vertegenwoordigt een organisatie die zich heeft aangemeld voor een Microsoft cloud service (Azure, Microsoft 365, Intune)
    - Een Azure subscription is altijd gekoppeld aan precies 1 entra tenant, maar dezelfde tenant kan aan meerdere subscriptions gekoppeld zijn
    - Elke tenant krijgt een standaard DNS naam met het suffix onmicrosoft.com. Een custom domain toevoegen is mogelijk en gebruikelijk
   
  - Schema
    - Het Entra ID schema bevat minder object types dan AD DS; geen computer class (wel device), geen Organizational Units (OUs)
    - Geen OUs betekent geen Group Policy Objects (GPOs); beheer via group membership in plaats van OU-hierarchie
    - Applications worden weergegeven door 2 classes:
      - Application (definitie)
      - servicePrincipal (instantie per tenant)


     
**Compare Microsoft Entra ID and Active Directory Domain Services**
  
| Kenmerk | AD DS | Microsoft Entra ID |
|---|---|---|
| Structuur | Hiërarchisch (X.500) | Flat (geen OUs) |
| Locating resources | DNS | REST API via HTTP/HTTPS |
| Query protocol | LDAP | REST API |
| Authenticatie | Kerberos | SAML, WS-Federation, OpenID Connect |
| Autorisatie | - | OAuth |
| Beheer | OUs en GPOs | Group membership |
| Computer objects | Ja | Nee (wel device objects) |
| Multi-tenant | Nee | Ja |
| Primaire focus | On-premises apps | Web-based / internet apps |
| Communicatie | - | HTTP (port 80) / HTTPS (port 443) |

  - AD DS maakt deel uit van de bredere Windows Active Directory suite: AD CS, AD LDS, AD FS en AD RMS. AD DS op een Azure VM deployen is mogelijk maar maakt geen gebruik van Microsoft Entra ID.



**Examine Microsoft Entra ID as a directory service for cloud apps**
  - Elke cloud service die authenticatie nodig heeft zou standaard een eigen Entra tenant aanmaken; het is efficienter om 1 gedeelde directory te gebruiken voor alle microsoft cloud services
  - Entra ID biedt 1 identity service voor Microsoft 365, Azure, Dynamics 365 en intune, inclusief SSO voor externe services zoals Facebook, Google en Yahoo
  - Ontwikkelaars kunnen Entra ID gebruiken als centralized authentication en authorization provider voor applicaties in Azure, ook in combinatie met on-premises AD DS
  - Voor Azure App Service kun je Entra authenticatie direct inschakelen via de Authentication/Authorization blade in de Azure portal; per deployment slot instelbaar


    
**Compare Microsoft Entra ID P1 and P2 plans**
  - P1 en P2 zijn betaalde tiers bovenop de Free en Office 365 edities, beschikbaar als losse licentie of via Microsoft Enterprise Mobility + Security (inclusief Intune en Auzre Information Protection)

  - P1 Features
    - Self-service group management: Gebruikers kunnen groepen aanmaken en beheren
    - Advanced security reports en alerts: Machine learning-based anomaly detection
    - Multi-factor authentication (MFA): Werkt op on-premises apps (VPN, RADIUS, Azure, Microsoft 365, Dynamics 365 en 3rd party gallery apps
    - Microsoft Identity Manager (MIM): Bridge tussen on-premises authenticaton stores (AD DS, LDAP, Oracle) en Entra ID
    - SLA van 99,9 beschikbaarheid
    - Password reset with writeback: SSPR volgt het on-premises AD password policy
    - Cloud App Discovery: ontdekt meest gebruikte cloud apps
    - Conditional Access op basis van device, group of location
    - Microsoft Entra Connect Health; Monitoring en operationeel inzicht in Entra ID
   
  - P2 Features
    - Microsoft Entra ID Protection: User risk policies en sign-in policies, gedragsanalyse en risk flagging
    - Microsoft Entra Privilged Identity Management (PIM): extra beveiliging voor privileged users, permanent en tijdelijke admins, policy workflow voor gebruik en admin privileges


**Examine Microsoft Entra Domain Services**
  - Microsoft Entra Domain Services (AAD DS) biedt managed domain services in de cloud: Group Policy management, domain joining en Kerberos authenticatie; volleidg compatibel met on-premises AD DS, zonder zelf domain controllers te heoven deployen
    - Vereist Entra ID P1 of P2. Kosten zijn per uur op basis van de grootte van de directory
    - Alternatieven zonder AAD DS: site-to-side VPN naar on-premises AD DS, of replica domain controllers als VMs in Azure; beide duurder en meer beheer

  - Voordelen:
    - Geen beheer van domain controllers, updates of replicatie
    - Geen Domain Admis of Enterprise Admins groepen nodig
    - Bruikbaar als cloud-only service zonder on-premises AD DS
    - Migratie van apps die LDAP, NTLM of Kerberos gebruiken naar de cloud zonder VPN
   
  - Berperkingen:
    - Alleen het basis computer Active Directory object wordt ondersteund
    - Schema uitbreiden is niet mogelijk
    - OU-structuur is flat; geen nested OUs
    - Ingebouwde GPOs zijn beschikbaar maar niet te targeten op OUs, geen WMI filter of security-group filtering



---



## Learning Path 2: Manage identities and governance in Azure
### Module 2: Create, configure, and manage identities 

**Create, configure, and manage users**
  - Elk account dat toegang nodig heeft tot resources vereist een user account in Entra ID. Na authenticatie bouwt Entra ID een access token om te bepalen welke resources de gebruiker kan benaderen
  - Beheer via de Microsoft Entra admin center; je werkt altijd met 1 directory tegelijk, wisselen van Directory + Subscribtion panel of de Switch directory knop

  - 3 typen gebruikers:
    - Cloud identities: bestaan alleen in Entra ID (admins, zelf beheerde gebruiker)
      - Source: Microsoft Entra ID.
    - Directory-synchronized identities; bestaan in on-premises AD DS en worden gesynchroniseerd naar Entra ID. Aanbevolen tool: Microsoft Entra Cloud Sync (lichtgewicht, ondersteunt meerdere forests) Voor complexe scenario's (device sync, groupen > 50.000 leden): Microsoft Entra Connect Sync.
       - Source Windows Server AD
    - Guest users: bestaan buiten de organisateie (externe vendors, contractors, andere cloud providers)
       - Source: invited User. Account verwijderen trekt direct alle toegang in


**Exercise - Restore or remove deleted users**
- [Exercise 3 Assign licenses to users](/03-az104/exercises/03-assign-licenses-to-users.md)


**Exercise - Restore or remove deleted users**
- [Exercise 4 Restore or remove deleted users](/03-az104/exercises/04-restore-or-remove-deleted-users.md)


**Create, configure, and manage groups**
  - 2 typen groepen:
    - Security groups: Beheren toegang tot gedeelde resources. Members: users, devices, service principals. Vereist een Entra administrator.
    - Microsoft 365 groups: Bieden samenwerking via gedeelde mailbox, calender, bestanden en SharePoint. Toegankelijk voor users en admins, ook voor externe gebruikers.

  - 3 membership types:
    - Assigned: Members worden handmatig toegevoegd en beheerd
    - Dynamic User: Users worden automatisch toegevoegd/verwijderd op basis van device attributen. Alleen voor security groups; Microsoft 365 groups ondersteunen geen dynamic devices

  - Dynamic membership vereist Entra ID P1 licentie (of Intune for Education voor device based rules)


**Exercise - Add groups in Microsoft Entra ID**
- [Exercise 5 Add groups in Microsoft Entra ID](/03-az104/exercises/05-add-groups-in-microsoft-entra-id.md)



**Configure and manage device registration**
  - 3 manieren om devices te registreren in Microsoft Entra ID:

| | Entra Registered | Entra Joined | Hybrid Entra Joined |
|---|---|---|---|
| Definitie | Persoonlijk device, geen org-account vereist voor inloggen | Alleen Entra ID, org-account vereist | On-premises AD + Entra ID |
| Doelgroep | BYOD / mobiele devices | Cloud-only of hybrid orgs | Orgs met bestaande on-premises AD |
| Device eigenaar | Gebruiker of org | Organisatie | Organisatie |
| OS | Windows 10+, macOS, iOS, Android, Linux | Windows 10/11 (geen Home), Server 2019+, macOS 13+ | Windows 10/11, Server 2016/2019/2022 |
| Beheer | MDM (Intune) | MDM (Intune) | Group Policy, Configuration Manager, Intune |
| SSO | Cloud resources | Cloud + on-premises | Cloud + on-premises |

  - Device writeback is niet meer ondersteund. Vervangen door Cloud Kerberos Trust voor on-premises SSO en Windows Hello for Business in hybrid omgevingen
  - Dynamic membershpi in groepen en Conditional Access vereisen device identity via Entra ID
  - MDM tools zoals Intune kunnen policies afdwingen: encryptie, wachtwoordcomplexiteit, software-updates



**Manage licenses**
  - Licenties voor Microsoft cloud services (Microsoft 365, EMS, Dynamics 365) worden beheerd via de Microsoft 365 admin center of PowerShell/Microsoft Graph API
  - Group-based licensing voorkomt complexe per-user scripts; wijs een licentie toe aan een groep en Entra ID regelt automatisch toewijzing en intrekking bij membership changes. Wijzigingen zijn doorgaans binnen minuten effecties

  - Vereisten:
    - Entra ID Premium P1 of hoger, of Office365 Enterprise E3 of hoger
    - Voldoende licenties voor alle unieke members in gelicentieerde groepen

  - Belangerijke punten:
    - Werkt met security groups: Zowel synced vanuit on-premises als cloud-only of dynamic groups
    - Individuele service plans binnen een product kunnen uitgeschakeld worden per groep
    - Een user kan licenties ontvangen via meerdere groepen en directe toewijzing; duplicatie licenties worden slechts 1 keer verbruikt
    - Usage location moet ingesteld zijn op het user profiel; users zonder locatie erven de directory locatie


**Exercise - Change group license assignments**
- [Exercise 6 change group license assignments](/03-az104/exercises/06-change-group-license-assignments.md)

| Foutcode | Oorzaak |
|---|---|
| CountViolation | Niet genoeg licenties beschikbaar |
| MutuallyExclusiveViolation | Conflicterende service plans die niet tegelijk toegewezen kunnen worden |
| DependencyViolation | Service plan afhankelijk van een andere licentie die verwijderd wordt |
| ProhibitedInUsageLocationViolation | Usage location niet ondersteund of niet ingesteld op de user |
| LicenseAssignmentAttributeConcurrencyException | Gelijktijdige toewijzing van dezelfde licentie via meerdere groepen — Entra ID lost zelf op |


**Exercise - Change user license assignments**
- [Exercise 7 change user license assignments](/03-az104/exercises/07-change-user-license-assignments.md)


**Create custom security attributes**
  - Create custom security attributes
    - Custom security attributes zijn business-specifieke key-value paris die je kunt definieren en toewijzen aan Entra objecten (users, service principles)
    - Gebruik uitbreiden van user profiles, categoriseren van applicaties, fine-grained access control over Azure resources, attribuut-gebaseerde governance
    - Niet ondersteund in: Entra Domain Services, SAML token claims, JWT clains
   
  - Features:
    - Tenant-wide beschikbaar
    - Data types: Boolean, integer, string
    - Enkelvoudige of meervoudige waarden
    - Vrije invoer of vooraf gedefinieerde waarden
    - Toewijsbaar aan directory-synced users vanuit on-premises AD


**Explore automatic user creation**
  - SCIM (System for Cross-Domain Identity Management) is een open standaard protocol voor het automatisch uitwisselen van user identity informatie tussen systemen
  - Doel: gebruikers die in het HR-systeem (HCM) worden toegevoegd of verwijderd, worden automatisch aangemaakt of gedeprovisioneerd in Entra ID of AD; minder risico op datalekken door verlaten accounts

  - Componenten:
    - HCM systeem: HR applicatie die de employee lifecycle beheert
    - Microsoft Entra Provisioning Service: gebruikt SCM 2.0 protocol, verbindt met de SCIM endpoint van de applicatie
    - Microsoft Entra Id: User repository voor identity lifecyle management
    - Target system: Applicatie met SCIM endpoint die automatische provisioning ondersteunt

  - API-driven inbound provisioning:
    - Voor HR-systemen zonder SCIM endpoint ondersteunt Entra ID API-drivin inbound provisioning (GA maart 2024)
    - Elk automation tool of script kan workforce data ophalen en naar de Entra provisioning API sturen
    - Ondersteunde bronnen: Workday, SAP SuccessFactor, Custom HR systemen


**Summary** Module 2 — Create, configure, and manage identities
  - Entra ID beheert 3 typen gebruikers (cloud identities, directory=synchronized, guest users) en 2 typen groepen (Security en Microsoft 365), met 3 membership types (Assigned, Dynamic User, Dynamic Device). Devices kunnen worden geregistreerd als Entra Registered (BYOD), Entra Joined (cloud-first) of Hybrid Entra Joined (on-premises + cloud)
  - Licenties worden beheerd via group-based licencing; Entra ID P1 vereist, wijzigingen effectief binnen minuten
  - Custom security attributes zijn key-value pairs voor fine-grained access control, ondersteunt Boolean, integer en string
  - SCIM automatiseert user provisioning vanuit HR-systemen, voor systemen zonder SCIM endpoint: API-driven inbound provisioning
  - P2-only: ID Protection en PIM




---



## Learning Path 2: Manage identities and governance in Azure
### Module 3: Describe the core architectural components of Azure

**What is Microsoft Azure**
  - Azure is een continu uitbreidende set van cloud services voor het bouwen, beheren en deployen van applicaties op een wereldwijd netwerk
  - Biedt honderden services: van VMs en managed databases tot AI, IoT, autoscaling en generative AI
  - Migratie pad: bestaande apps op VMs → moderniseren naar managed services, autoscaling, event-driven architectuur
  - Schalen op en af op basis van vraag; alleen betalen voor wat je gebruikt
  - Kernprincipes: innovatie, unified platform management, security en betrouwbaarheid

**Get started with Azure accounts**
  - Een Azure subscription is nodig om services te gebruiken; 1 account kan meerdere subscriptions hebben (bv. dev, test, productie)
  - Aanschaffen via Microsoft direct, Microsoft representative, of Cloud Solution Provider partner
  - Free account: 12 maanden populaire services gratis, $200 credit voor 30 dagen, 65+ altijd gratis services, vereist creditcard
  - Free student account: 12 maanden bepaalde services gratis, $100 credit voor 12 maanden, gratis developer tools, geen creditcard vereist

**Describe Azure physical infrastructure**
  - Azure datacenters zijn gegroepeerd in Regions en Availability Zones; je werkt nooit direct met individuele datacenters
  - Region: geografisch gebied met 1 of meer datacenters, verbonden via low-latency netwerk
  - Availability Zone: fysiek gescheiden datacenter binnen een regio, met eigen power, cooling en networking. Minimaal 3 per AZ-enabled regio
  - Service categorieën voor Availability Zones:
    - Zonal: gepind aan een specifieke zone (VMs, managed disks, IP adressen)
    - Zone-redundant: automatisch gerepliceerd over zones (zone-redundant storage, SQL Database)
    - Non-regional: altijd beschikbaar, resistent tegen zone- en regio-uitval
  - Region Pairs:
    - Meeste regio's zijn gekoppeld aan een andere regio binnen dezelfde geografie, minimaal 300 mijl afstand
    - Bij uitval automatische failover naar paired region
    - Updates worden 1 regio tegelijk uitgerold
    - Data blijft binnen dezelfde geografie (uitzondering: Brazil South, gekoppeld aan South Central US)
  - Sovereign Regions: geïsoleerde Azure instanties voor compliance of juridische doeleinden (US Gov, China)

**Describe Azure management infrastructure**
  - Hiërarchie van hoog naar laag:
    - Management Groups
    - Subscriptions
    - Resource Groups
    - Resources
  - Resources en Resource Groups:
    - Elke resource behoort aan exact 1 resource group
    - Resource groups kunnen niet genest worden en niet hernoemd worden
    - Acties op een resource group gelden voor alle resources erin, inclusief verwijderen en toegangsbeheer
  - Subscriptions:
    - Vereist voor toegang tot Azure; eenheid van beheer, billing en schaal
    - 2 typen boundaries:
      - Billing boundary: aparte factuur per subscription
      - Access control boundary: aparte toegangsbeleid en spending limiets per subscription
    - Redenen voor meerdere subscriptions: omgeving (dev/test/prod), teams, billing scheiding
  - Management Groups:
    - Subscriptions worden georganiseerd in management groups; policies en toegang worden geërfd door alle onderliggende subscriptions
    - Maximaal 6 niveaus diep nestbaar, exclusief root en subscription niveau
    - Maximaal 10.000 management groups per directory
    - Elke management group en subscription heeft precies 1 parent
    - Elke Entra tenant heeft 1 Tenant Root Group bovenaan



---



## Learning Path 2: Manage identities and governance in Azure
### Module 4: Azure Policy initiatives 

**Cloud Adoption Framework for Azure**
  - Het Cloud Adoption Framework (CAF) biedt end-to-end guidance voor cloud adoptie. Best practices, documentatie en tools voor cloud architects, IT experts en business leaders
  - Cloud governance: Beheer van cloud gebruik, gericht op compliance, security, kosten, resource management en AI

  - 5 stappen voor cloud governance:
    - Build a governance team
    - Assess cloud risks
    - Document cloud governance policies
    - Enforce cloud governance policies
    - Monitor cloud governance
   
  - 5 core disciplines
    - Cost management, Security baselin, Resource consistency, Identitiy baseline, Deployment acceleraton

  - Azure Policy als governance tool:
    - Contrale tool voor governance; afdwingen van standards, compliance monitoren, noncompoliant resources remedieren
    - Automatische remediatie voor nieuwe resources, bulk remediate voor bestaande
    - Integreert met Azure DevOps voor CI/CD pipelines policies
    - Voorbeelden: Regio restricties, VM sizes beperken, tags afdwingen, MFA vereisen, diagnostic logs sturen naar Azure Monitor


**Azure Policy design principles**
  - Governance hierarchie (hoog naar laag):
    - Management Groups
    - Subscription
    - Resource Groups
    - Resources
  - Lagere niveaus erven settings van hogere niveau

  - Azure Resource Manager (ARM)
    - Deployment en management service voor Azure; centrale laag voor aanmaken, updaten en verwijderen van resources
    - 2 operatietypes:
      - Control plane: Beheert resources (RBAC, policies, templates, tagging). Azure policy opereert hier. Volgorde: RBAC wordt eerst geevalueerd, daarna Azure Policy
      - Data plane: Directe data operaties (uploaden naar storage, query's op SQL, secruits uit Key Vault). Wordt niet door ARM beheerd maar direct door de resource provide
     
    - 2 deployment scenario's
      - Greenfield (policy first): Nieuwe resources worden direct geevalueerd tegen policies bij aanmaken/update
      - Brownfield (resource-first): bestaande resources bij een nieuwe policy worden geevalueerd via compliance scan, automatisch elke 24 uur of handmatig getriggerd. Noncompliant resources worden geflagd maar niet verwijderd


**Azure Policy resources**
  - 6 policy resources in Azure:
    - Definitions: beschrijven compliance condities en het effect bij een match. Opgeslagen in een management group of subscription. De locatie bepaalt de scope waarvoor de policy gebruikt kan worden
    - Initiatives (policy sets): Groepering van meerdere policy definitions voor vereenvoudigd beheer:
    - 2 types
      - Built-in: Gegenereerd door Azure Resource Providers, standaard beschikbaar
      - Custom: Zelf geschreven wanneer geen buil-in policy voldoet

  - Assignments: Bepalen welke resources geevalueerd worden door een policy of initiative
  - OPties bij assingment:
    - Resources selectors voor gefaseerde uitrol
    - Overrides om effect te wijzigen zonder de definitie aan te passen
    - `enforcementMode` uitschakelen voor what-if scenario's
    - Excluded scopes voor uitzonderingen
    - Parameters en noncompliance messages

  - Exemptions: vrijstelling van evaluatie voor een resource of resource hierarchy
  - 2 categorieen:
    - Mitigated: Policy intent wordt via andere methode bereikt
    - Waiver: Noncompliance tijdelijk geaccepteerd

  - Attestations: Handmatig instellen van compliance status voor resources die niet automatisch geevalueerd kunnen worden
  - Remediations: Brengen noncompliant resources terug naar compliance via een remediation task. Automatisch voor nieuwe/geupdatete resources met `deployIfNotExists` of `modify` effect


**Azure Policy Definitions**
  - Een policy definition bestaat uit 2 delen:
    - If block: Conditie die bepaalt wanneer de policy van toepassing is
    - Then block: Effect dat plaatsvindt als de conditie waar is
   
  - Anatomy van een policy definition (JSON elementen)
    
| Element | Verplicht | Beschrijving |
|---|---|---|
| displayName | Ja | Naam, max 128 tekens |
| description | Nee | Context, max 512 tekens |
| policyType | Readonly | Built-in, Custom, of Static |
| mode | Ja | All, Indexed, of Resource Provider mode |
| parameters | Nee | Herbruikbaarheid via variabele waarden |
| policyRule | Ja | if/then logica |

  - Logische operatoren (if block)
    - `not`: inverteert de conditie
    - `allOf`: alle condities moeten waar zijn (AND)
    - `anyOf`: Minimaal 1 conditie moet waar zijn (OR)
   
  - Effect types (then block):
    
| Effect | Type | Beschrijving |
|---|---|---|
| disabled | Synchroon | Policy gedeactiveerd |
| append | Synchroon | Velden toevoegen bij aanmaken/updaten (grotendeels obsoleet) |
| modify | Synchroon | Properties of tags toevoegen, updaten of verwijderen |
| deny | Synchroon | Request blokkeren |
| denyAction | Synchroon | Acties blokkeren op schaal (alleen DELETE) |
| audit | Asynchroon | Warning in activity log, request niet gestopt |
| auditIfNotExists | Asynchroon | Audit gerelateerde resources die niet aan conditie voldoen |
| deployIfNotExists | Asynchroon | Template deployment triggeren als conditie waar is |
| manual | Handmatig | Compliance handmatig attesteren |


**Evaluation of resources through Azure Policy**
  - Evaluation trigger: policy evaluatie wordt getriggerd door:
    - Nieuwe of geupdatete policy/initiative assignment
    - Resource aangemaakt of geupdated in een scope
    - Subscription aangemaakt of verplaatst in management group hierarchie
    - Exemption aangemaakt, geupdated of verwijderd
    - Automatisch volledige scan elke 24 uur
    - Handmatige scan via `az policy state trigger-scan`
      
  - Timing: Nieuwe policy kan tot 30 minuten nodig hebben om van kracht te worden door ARM caching. Uitloggen en inloggen bypast dit.

  - Compliance states (volgorde van prioriteit):
    - Non-compliant
    - Compliant
    - Error
    - Conflicting
    - Protected
    - Exempted
    - Unknown
   
  - Compilance percentage = (Compliant + Exempt + Unknow) / totaal resources

  - enforcementMode:
    
| Mode | JSON waarde | Effect afgedwongen | Activity log |
|---|---|---|---|
| Enabled | Default | Ja | Ja |
| Disabled | DoNotEnforce | Nee | Nee |

  - Safe deployment best practices:
    - Start met `enforcementMode Disabled` voor what-if evaluatie
    - Gebruik deployment ring; begin met test/dev, daarna productie in gefaseerde uitrol
   
  - Event-driven reacties:
    - Policy state changes worden via Azure Event Grid gepusht naar Event Handlers (Azure Functions, Logic Apps, webhooks). Geen polling nodig.



---


## Learning Path 2: Manage identities and governance in Azure
### Module 5: Secure your Azure resources with Azure role-based access control (Azure RBAC)

**What is Azure RBAC?**
  - Azure RBAC is een autorisatiesysteem gebouwd op Azure Resource Manager voor fine-grained access management van Azure resources. Toegang wordt verleend via role assignment.
    - 3 delen:
    - Security principal (WHO): User, group of application
    - Role definition (WHAT): Verzameling van permissions (read, write, delete).
       - 4 delen
       - Owner: Volledige toegang, inclusief toegang delegeren
       - Contributor: Aanmaken en beheren van resources, geen toegang verlenen
       - Reader: alleen bekijken
       - User Access Administrator: Gebruikerstoegang beheren'
    - Scope (WHERE): Management group, subscription, resource group, of resource. Hogere scopres worden geerfd door lagere scopes
   
  - Allow model: RBAC verleent toegang via `Actions`. Met `NotActions` kun je specifieke permissies uitsluiten. effectieve permissies = Action minus NotActions.


**Exercise - List access using Azure RBAC and the Azure portal**
- [Exercise 8 List access using Azure RBAC and the Azure portal](/03-az104/exercises/08-list-access-using-azure-rbac-and-the-azure-portal.md)


**Exercise - Grant access using Azure RBAC and the Azure portal**
- [Exercise 9 Grant access using Azure RBAC and the Azure portal](/03-az104/exercises/09-grant-access-using-azure-rbac-and-the-azure-portal.md)


**Exercise - View activity logs for Azure RBAC changes**
- [Exercise 10 View activity logs for Azure RBAC changes](/03-az104/exercises/10-view-activity-logs-for-azure-rbac-changes.md)


**Summary** Module 5 — Secure your Azure resources with Azure role-based access control (Azure RBAC)
  - Azure RBAC is een autorisatiesysteem op Azure Resource Manager voor fine-grained toegangsbeheer via role assignments.
    - Role assignment bestaat uit 3 elementen: security principal (who), role definition (what), scope (where)
    - 4 built-in roles: Owner, Contributor, Reader, User Access Administrator
    - Allow model — effectieve permissies = Actions minus NotActions
    - Scopes erven van hoog naar laag: Management Group → Subscription → Resource Group → Resource
    - Toegang beheren via Access control (IAM) in de Azure portal
    - Wijzigingen worden gelogd in de Azure Activity Log



---



## Learning Path 2: Manage identities and governance in Azure
### Module 6: Allow users to reset their password with Microsoft Entra self-service password rese

**What is self-service password reset in Microsoft Entra ID?**
  - SSPR stelt gebruikers in staat hun wachtwoord zelf te resetten zonder de helpdesk. Minder kosten, minder productiviteitsverlies
  - 6 Authenticatiemethoden:
    - Mobile app notification
    - Mobile app code
    - Email
    - Mobile phone (niet aanbevolen, fraduleuze SMS mogelijk)
    - Office phone
    - Security questions (minst aanbevolen, aantwoorden kunnen bekend zijn bij anderen)
   
  - Belangrijke punten:
    - Minimaal 2 methoden aanbevolen, waarvan mobile app notifcation of code als primaire methode
    - Administor accounts: altijd methoden vereist, security questions niet beschikbaar
    - Vereist Entra ID P1 of P2 (of Microsoft 365 Apps for business) voor niet-ingelogde gebruikers
    - Password writeback naar on-premises AD vereist P1 of P2. Via Microsoft Entra Connect of cloud sync
 
**Implement Microsoft Entra self-service password reset**
  - Vereisten
    - Entra organisatie met minimaal P1 of P2 trial licentie
    - Account met Authentication Policy Administrator rol
    - Non-admin testgebruiker met geldige licentie
    - Security group voor testgroep

  - Scope opties:
    - None: Niemand kan SSPR gebuiken (standaard)
    - Selected: Alleen leden van een specifieke security group
    - All: Alle gebruiker
   
  - Configuratiestappen via Azure Portal - Microsoft Entra ID - Manage - Password reset:
    - Properties: SSPR inschakelen voor All of Selected
    - Authentication methods: 1 of 2 methoden vereisen, methoden kiezen
    - Registration: Verplichte registratie bij volgende login, herbevestiginginterval instellen
    - Notifications: Notificaties voor gebruikers en admins instellen
    - Customization: Helpdesk emailadres of URL opgeven


**Exercise - Set up self-service password reset**
- [Exercise 11 Set up self-service password reset](/03-az104/exercises/11-set-up-self-service-password-reset.md)


**Exercise - Customize directory branding**
- [Exercise 12 Customize directory branding](/03-az104/exercises/12-customize-directory-branding.md)
