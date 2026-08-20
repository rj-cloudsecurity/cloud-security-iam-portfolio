# SC-300: Microsoft Identity and Access Administrator

## Learning Path 2: Implement an identity management solution using Microsoft Entra ID
### Module 1: Implement initial configuration of Microsoft Entra ID 


### Introduction
  - Wat deze module behandelt
    - Hoe je een Microsoft Entra tenant configureert en beheert: Entra roles, custom domains, company branding opties, delegation via administrative units, en tenant-wide settings.

  - Learning objectives
    - Company branding
    - Configure and manage Microsoft Entra roles
    - Configure delegation by using administrative units
    - Configure and manage custom domains
    - Evaluate permissions based on role assignments and settings
    - Configure tenant-wide settings

  - Prerequisites
    -Ervaring met de Azure portal user interface of het Microsoft Entra admin center.

---

### Configure company brand
  - **Wat is het:**
    - Eigen logo + custom kleurenschema op sign-in pagina's; toegepast bij inloggen op web-based apps (bv. M365 via Entra ID)
    - Vereist licentie: Entra ID P1, P2, of Office 365

  - **Hoe instellen:**
    - Azure Portal -> Microsoft Entra ID -> Manage -> Company branding
    - Premium licentie vereist om deze menu optie te zien

  - **Instellingen**
    - Language: automatisch default, niet aan te passen
    - Sign-in page background image: png/.jpg, max 1920x1080px, max 300.000 bytes
    - Banner logo: .png/.jpg, verschijnt na username-invoer + op My Apps portal
    - Username hint: tekst bij "vergeten username", Unicode, geen links/code, max 64 tekens. Niet aanraden bij guest users
    - Sign-in page text and formatting: tekst onderaan sign-in pagina (bv. helpdesk-nummer, legal statement), Unicode, max 1.024 tekens

---

### Configure and manage Microsoft Entra roles

  - **Wat is Microsoft Entra ID**
    - Cloud-based IAM service voor toegang tot externe resources (M365), Azure portal, SaaS) en interne resources (corporate apps, intranet, eigen cloud apps)
    - Gebruikers:IT admins (access control, MFA, provisionig automation), app developers (SSO,APIs), M365/Azure/Dynamics subscribers (elke subscription = automatische een Entra tenant)
   
  - **Belangrijkste Entra Roles**

| Role | Permissions |
|---|---|
| Global Administrator | Alle admin features in Entra ID + gefedereerde services. Rollen toewijzen aan anderen. Password reset voor iedereen. Eerste tenant-signup = automatisch Global Admin |
| User Administrator | Users/groups volledig beheren. Support tickets, service health. Password reset voor users, Helpdesk admins, andere User Admins |
| Billing Administrator | Aankopen doen, subscriptions beheren, support tickets, service health monitoren |

  - **Azure roles vs Entra Roles; Verschillen**
    - Azure roles: Beheren van Azure resources. Scope: management group / subscription / resource group / resource (meerdere niveaus). Toegankelijk via Portal, CLI, PowerShell, ARM templates, REST API
    - Entra Roles: Beheren Entra resources (identity). Scope: tenant-level of Administrative Unit. Toegankelijk via Entra admin portal, M365 admin center, Graph, PowerShell
    - Beide ondersteunen custom roles

  - **Overlap tussen Azure roles en Entra roles**
    - Standaard geen overlap tussen Azure en Entra
    - Global Admin kan zichzelf elevaten via "Access management for Azure resources" switch -> krijgt dan User Access Administrator (Azure role) op alle subscriptions in de tenant. Handig om terug toegang te krijgen tot een subscription
    - Sommige Entra roles (global Admin heeft standaard geen Azure resource-toegang
    - Microsoft raadt Global Administrator gebruik af; least privilege toepassen
   
  - **Manieren om rollen toe te wijzen**
    - Rol -> user/group (Roles and administration -> rol selecteren -> +Add Assignment
    - User/group -> rol (Users/Group -> select -> Assigned roles -> +Add Assignment
    - Broad-scope (Subscription/RG/Management Group) -> via Access Control (IAM)
    - Via PowerShell / Microsoft Graph API
    - Via PIM (Privileged Identity Management)
   
  - **Geen ingebouwde restricties:** Je kunt perongeluk een admin rol aan de verkeerde groep toewijzen. Governance is hierbij cruciaal

  - **PIM + P2 licentie**
    - Met P2 + PIM: Alle role management gebeurt via de PIM-experience
    - Beperking: Kan maar 1 rol per keer toewijzen; geen bulk multi-role assignment
   
  - **Custom roles aanmaken**
    - Entra ID -> Roles and administrators -> New custom role
    - Basics (naam/beschrijving) _> Permissions (zoeken + selecteren, bv. `microsoft.directory/applications/credentials/update`) -> Review + create
    - Scope: directory-level of alleen app registration resource-scope

---

### Exercise manage users roles
  - [04-sc300/labs/01-manage-users-roles](../../04-sc300/labs/01-manage-user-roles.md)
  - **Ook uitgevoerd in:** [Oceanic Airlines sandbox](../../00-sandbox/02-adding-first-user.md)

---

### Configure delegation by using administrative units
  - Wat is een Administrative Unit (AU)
    - Entra Id resource; container voor users, groups, devices
    - Beperkt permissions van een rol tot een specifiek deel van je organisatie
    - Beheer via: Azure Portal, PowerShell, Microsoft Graph
    - Vergelijkbaar met on-prem AD Organizational Units (OUs)
   
  - Waarom AU's; het probleem
    - Zonder AU: een admin-rol toewijzen = admin over de hele tenant, niet alleen een deel
    - AU's lossen dit op via least privilege: bv. een User Administrator alleen laten beheren binnen 1 afdeling (voorbeeld uit tekst: Research Department van een ziekenhuis)
    - Rol + AU samen = "Admin-for-research" kan alleen die specifieke users/groups beheren, niet de rest van de tenant
   
  - Rollen die je binnen een AU kunt toewijzen
    - Authentication administrator
    - Helpdesk administrator
    - License administrator
    - Password administrator
    - User administrator
   
  - Plannen van AU's; 3 fasen
      1. Initial adoptation: AU's aanmaken op basis van eerste criteria, aantal groeit
      2. Pruning: Overbodige AU's verwijderen zodra criteria duidelijk zijn
      3. Stabilization: Structuur staat vast, weinig verandering meer

    - Waaneer gebruiken: Geografische spreiding van IT, of semi-autonome suborganisaties binnen een groter bedrijf. Voorbereiden met M365-brede toepassing in het achterhoofd voor maximale waarde
   
  - Delegation van App management (breder dan alleen AU's)
    - 4 manieren om app creation/management te delegeren:
      - Beperken wie apps ma gregistreren (standaard mag iedereen dit)
      - Owner(s) toewijzen aan een specifieke app
      - Built-in admin role toewijzen (breed, voor alle apps)
      - Custom role maken voor precieze permissions
     
  - Waarom delegeren: Minder administratieve overhead + betere security posture (minder unauthorized access risico)

    - Delegation model; 8 stappen
      1. Rollen definieren
      2. App administration delegeren
      3. REcht geven om apps te registreren
      4. App ownership delegeren
      5. Security plan ontwikkelen
      6. Emergency accounts opzetten
      7. Admin roles beveiligen
      8. Privileged elevation tijdelijk maken
     
    - Rollen definieren; criteria
      - Routinematig + laag risico + makkelijk -> goede kandidaat voor delegatie
      - Zeldzaam + hoog risico + hoge skill vereist -> niet delegeren, liever tijdelijk elevaten of taak herverdelen
     
    - App administration rollen
    - 
| Role | Permissions | Mist |
|---|---|---|
| Application Administrator | Alle apps beheren: registrations, SSO, user/group assignments, licensing, App Proxy, consent | Geen Conditional Access |
| Cloud Application Administrator | Zelfde als Application Administrator | Geen App Proxy (geen on-prem permissions) |

  - App registration delegeren
    - Standaard: Iedereen mag apps registreren
    - Om te beperken: "Users can register applications" -> No + rol Application Developer toewijzen aan wie het wel mag
    - Application Developer die een nieuwe registratie maakt = automatische eerste owner

  - App ownership delegeren
    - Owner toewijzen per individuele enterprise app (bv. iemand alleen owner van Salesforce, niks ander)
    - 1 App kan meerdere owners hebben, 1 user kan owner van meerdere apps zijn
   
  | Role | Permissions | Mist |
|---|---|---|
| Enterprise Application Owner | SSO settings, user/group assignments, owners toevoegen — voor apps die ze bezitten | Geen App Proxy, geen Conditional Access |
| Application Registration Owner | App registrations beheren (manifest, owners toevoegen) — voor apps die ze bezitten | — |

  - Security-onderdelen van het delegation-plan
    - Emergency access accounts: Break-glass accounts om altijd toegang te behouden
    - Security Defaults" Gratis Feature voor alle Entra orgs, dwingt MFA af op privileged accounts

  ---

### Analyze Microsoft Entra role permissions
  - Wat is een permission
    - Consent/autorisatei om een specifieke actie uit te voeren
    - Range: van alleen bekijken tot instellingen wijzigen tot users toevoegen/verwijderen
    - Toegewezen op **user-** of **group-niveau**' komt uiteindelijk altijd bij de user terecht
    - **Member-user** vs **Guest-user**: guest heeft standaard iets minder rechten
   
  - Voorbeeld default permissions

| Member Users | Guest Users |
|---|---|
| Users + contacts opsommen | Alleen eigen properties lezen |
| Guest users uitnodigen | Guest users uitnodigen |
| Security/M365 Groups aanmaken | Alleen niet-verborgen groups zoeken op naam |
| Nieuwe apps registreren | Properties van registered/enterprise apps lezen |

  - Permissions controleren; 2 manieren
    1. User settings (Entra ID -> Manage): Default permissions beperken. Kan blokkeren: apps registreren, Azure portal toegang, Linkedin connections, external collaboration settings
    2. Roles and administrators: Nieuwe permissions toevoegen via rollen aan users/groups/service principals
   
  - Kernprincipe: Altijd least privilege; alleen rechten geven die echt nodig zijn
 
  - Permissions van een rol bekijken
    - Entra ID -> Roles and aministrators -> rol selecteren _> (...)menu -> description page
    - Elke rol toont 2 soorten permissions:
      - Role permissions: Specifiek voor die rol
      - Guest and service principal basic read permissions: Standaard leesrechten die erbij horen
   
  - Onthouden: Check altijd de volledige permissions-lijst van een rol voordat je hem toewijst; rollen kunnen meer bevatten dan de naam doet vermoeden

---

### Configure and manage custom domains
  - Wat is een domain
    - Onderdeel van identifiers: username/email, group address, some app ID URI
    - Alleen Global Administrator kan domains beheren
   
  - Primary domain
    - Bij tenant-creatie = initial domain (bv. `contoso.onmicrofosft.com`)
    - Persoon die tenant aanmaakt = Automatisch Global Admin; Least privilege toepassen bij extra domains beheren
   
  - Primary domain wijzigen
    - Entra- ID -> Custom domain names -> domain selecteren -> Make primary -> bevestigen
    - Alleen mogelijk naar een verified, niet-gefedereerde custom domain
    - Bestaande usernames van huidige users veranderen niet mee
   
  - Custom domains toevoegen
    - Max 900 managed domains
    - bij federatie met on-prem AD: max 450 per organisatie

  - Subdomains
    - Eerst root domain toevoegen + verieferen (bv. `contoso.com`)
    - Subdomain (bv. `europe.contoso.com`) wordt automatisch geverifieerd
    - Root domain al in andere Entra org? -> Subdomian kan ook daar apart geverifieerd worden (TXT record nodig in DNS)
   
  - DNS registrar wijzigen
    - Geen extra configuratie nodig in Entra ID; domain blijft gewoon werken
    - Wel checken bij gekoppelde services (M365, Intune, etc.)
   
  - Custom domain verwijderen
    - Kan niet als domain nog in gebruik is bij:
      - Username/email/proxy address van een user
      - Email/proxy address van een group
      - App ID URI van een applicatie
    - Eerst deze resources aanpassen/verwijderen, dan pas domain deletion mogelijk
   
  - ForceDelete
    - Verwijdert domain + update automatisch alle references naar het initial default domain (bv. `User@contoso.com` -> `user@contoso.onmicrosoft.com`)
    - Asynchrone operatie, via Entra admin center of Graph API
    - Voorwaarden:
      - Minder dan 1000 references naar het domain
      - Exchange-provisioned references eerst aanpassen in Exchange Admin Center (incl. Mail-Enabled Security Groups, distribution lists)
    - Lukt niet als:
      - Domain gekocht via M365 domain subscription service
      - Je bent partner-admin names een andere klantorganisatie
      - Aantal te hernoemen objecten > 1000
      - 1 Van de apps is een multitenant app
    - Wat ForceDelete hernoemt: UPN/EmailAddress/ProxyAddress van users, EmailAddress van groups, identifierUris van apps
   
    ---

### Configure tenant-wide setting
  - 3 hoofdcategorieën tenant-wide settings

| Setting | Locatie | Wat |
|---|---|---|
| Tenant Properties | Identity -> Overview > Properties | Naam directory, primary contact, etc. |
| User Settings | Identity -> Users -> User Settings | Globale rechten van users (bv. apps registreren) |
| External Collaboration Settings | Identity -> External Identities -> User Settings -> Manage external collaboration | Wat guest users mogen (bv. andere guests uitnodigen) |

  - Default permissions — Member vs Guest
    - Member users: apps registreren, eigen profielfoto/mobiel nr beheren, eigen wachtwoord wijzigen, B2B guests uitnodigen, alle directory info lezen (met uitzonderingen)
    - Guest users: beperkter; eigen profiel beheren, eigen wachtwoord wijzigen, beperkte info over andere users/groups/apps ophalen. Kunnen niet alle users/groups enumereren. Kunnen wel andere guests uitnodigen. Kunnen ook admin-rollen krijgen (dan wel volledige rechten van die rol)


  - Restricties voor member users

| Permission | Setting |
|---|---|
| Users can register applications | Default: Yes. Op No → alleen Application Developer role mag nog apps registreren |
| Restrict access to Microsoft Entra admin portal | No = non-admins mogen portal gebruiken. Yes = alleen admins. Blokkeert NIET PowerShell/andere clients. Bij Yes: specifieke user toch toegang geven via bv. Directory Readers role |

  - Sign in with LinkedIn
    - 500M+ leden, professionele identity-bron
    - Voordelen: minder friction bij sign-up, geen eigen identity/profile management nodig, profielen personaliseren met LinkedIn-data
     
  - Security Defaults
    - Gratis, preconfigured basisbeveiliging voor iedereen (geen extra kosten)
    - Regelt:
      - MFA-registratie verplicht voor alle users
      - MFA verplicht voor admins
      - Legacy authentication protocols geblokkeerd
      - MFA "when necessary" voor users
      - Bescherming van privileged activities (bv. Azure portal toegang)
     
  - External user options
    - Guest user access: range van bijna-full-user tot alleen eigen content zien
    - Guest invite settings: wie mag guests uitnodigen (guests zelf t/m alleen admins)
    - Guest self-service: self-service opties voor guests aan/uit

  - Tenant properties (velden)
    - Name: friendly name in Azure portal
    - Country/region: locatie hoofdkantoor + gebruikte Azure datacenters
    - Notification language: taal voor notificaties/alerts
    - Tenant ID: unieke identifier (programmatisch gebruikt)
    - Technical contact: default = tenant-creator
    - Global privacy contact: voor privacy-vragen
    - Privacy statement URL: link naar privacy-regels
      
---

### Exercise - setting tenant-wide properties
  - [04-sc300/labs/02-setting-tenant-wide-properties](../../04-sc300/labs/02-setting-tenant-wide-properties.md)


---


# Knowledge Check

**Score:** 100%

## Vraag 1
A domain name is included as part of a user name or email address for users and groups. Can a domain name also be included as part of an application or other resource?

- ✅ Yes, a domain name can be included as part of an application or other resource if the organization owns the domain name that contains the resource.
- ❌ No, a domain name can't be included as part of an application or other resource.

**Toelichting:** A domain name can be included as part of the app ID URI for an application, but can't be included as part of other resources.

## Vraag 2
The proliferation of many types of devices and bring your own device (BYOD) concept require IT professionals to accommodate two rather different goals. One goal is to allow users to be productive wherever and anytime. What is the other goal?

- ❌ Provide anti-malware apps for a various devices.
- ❌ Establish baseline security guidelines for users.
- ✅ Protect the organization's assets.

## Vraag 3
Microsoft Entra guest users have restricted directory permissions. Which of the following answers best describes guest users capabilities?

- ❌ They can manage their own profile, change their own password, and add other B2B guests to groups.
- ✅ They can manage their own profile, change their own password, and retrieve some information about other users, groups, and apps.
- ❌ They can manage their own profile, change their own password, and identify group members or other directory objects.

---
---

## Learning Path 2: Implement an identity management solution using Microsoft Entra ID
### Module 2: Create, configure, and manage identities

---

### Introduction
  - Waarom dit belangrijk is
  - Workloads naar de cloud verplaatsen is meer dan alleen servers, websites en data migreren. Bedrijven moeten resources beveiligen door geautoriseerde users te definiëren, ervoor zorgen dat users alleen toegang hebben tot data die ze nodig hebben, en alleen operaties mogen uitvoeren waarvoor ze geautoriseerd zijn. Centrale controle gebeurt via twee dingen: (1) een definitieve identity per user voor elke service, en (2) zorgen dat employees/vendors precies genoeg toegang hebben om hun werk te doen.

  - Microsoft Entra ID (cloud-based IAM service) biedt end-to-end identity management, inclusief SSO en MFA, om users en data te beschermen.

  - Wat deze module behandelt
    - Basis van users en groups aanmaken, configureren, beheren
    - Licenties beheren
    - Device registration beheren

  - Learning objectives
    - Create, configure, and manage users
    - Create, configure, and manage groups
    - Manage licenses
    - Configure and manage device registration
    - Explore custom security attributes and automatic provisioning

  - Prerequisites
    - Basic understanding of identity management
    - Some experience with Active Directory a plus
    - Experience with Zero Trust helpful

---

### Create, configure, and manage users
  - Wat is een user account
    - Bevat alle info nodig voor een authenticatie tijdens sign-on
    - Na authenticatie bouwt Entra ID een Access token -> bepaalt welke resources + welke acties toegestaan zijn

  - Beheer via Microsoft Entra Admin center
    - Kan maar 1 directory tegelijk actief hebben
    - Wisselen via: Directory + Subscription panel, of Switch directory knop in toolbar
   
  - Users bekijken
    - Identity -> Users -> All users
    - User Type kolom toont: member vs guest

  - 3 soorten users
    - Cloud identities: Bron; Entra ID zelf (of External Entra directory). Bestaan alleen in Entra ID (bv. Admin-account). Verwijderd uit primary directory = permanent weg
    - Directory-synchronized identites: Bron; Windows Server AD. Bestaan on-prem, gesynchroniseerd naar Entra ID. Sync-tools: Entra Cloud Sync (aanbevolen, lightweight could agent, ondersteunt meerdere disconnected forests) of Entra Connect Sync (voor complexe scenario's: Device sync, groups met >50.000 member)
    - Guest users: Bron; Invited user. Extern (andere cloud providers, Microsoft-accounts). Handig voor vendors/contractors; makkelijk te verwijderen incl alle toegang zodra samenwerking stopt
   
  - Onthouden: Entra Cloud Sync = default/aanbevolen keuze tegenwoordig, Connect Sync alleen nog voor specifieke edge cases (device sync, zeer grote groups).

---

### Exercise - assign licenses to users
  - [04-sc300/labs/03-assign-licenses-to-users](../../04-sc300/labs/03-assign-licenses-to-users.md)
  - **Ook uitgevoerd in:** [Oceanic Airlines sandbox](../../00-sandbox/03-creating-security-group-and-users.md)

---

### Exercise - restore or remove deleted users
  - [04-sc300/labs/04-restore-or-remove-deleted-users](../../04-sc300/labs/04-restore-or-remove-deleted-users.md)

---

### Create, configure, and manage groups
  - Waarom groups?
    - Makkelijker permissions beheren: 1x toewijzen aan de group i.p.v. per user
    - Definieert een security boudary: users toevoegen/verwijderen = toegang geven/intrekken met minimale moeite
    - Membership kan gebaseerd zijn op rules (bv. department, job title)
   
  - 2 types groups
    - Security groups: meest gebruikt, voor toegang tot shared resources. Members: users, devices, service principals. Vereist Entra administrator
    - Microsoft 365 groups: Collaboration (shared mailbox, calendar, files, SharePoint site). Kan ook externe mensen toegang geven. Beschikbaar voor zowel users als admins
   
  - Groups bekijken
    - Identity -> Groups. Nieuwe Entra ID deployment heeft standaard geen groups
   
  - 3 Membership Types
    - Assigned: Members handmatig toegevoegd/beheerd
    - Dynamic User: Automatisch toegevoegd/verwijderd op basis van user-attributes (departement, job title, location)
    - Dynamic Device: Automatisch op basis van device-attributes. Alleen bij security groups. M365 ondersteunen wel dynamic users, geen dynamic devices

  - Dynamic groups; details
    - Bij attribute-wijziging (bv. user verandert van department) worden alle dynamic rules in de tenant herevalueerd -> automatische toevoeging/verwijdering
    - Vereist Entra ID P1 (of intune for Education voor device-based rules)
    - Voorbeeld: Rule die alle users met `Department = Marketing` automatisch toevoegt aan een Marketing security group

---

### Exercise - add groups in Microsoft Entra ID
  - [04-sc300/labs/05-add-groups-in-microsoft-entra-id](../../04-sc300/labs/05-add-groups-in-microsoft-entra-id.md)
  - **Ook uitgevoerd in:** [Oceanic Airlines sandbox](../../00-sandbox/04-add-groups-in-microsoft-entra-id.md)

---

### Configure and manage device registration
  - Waarom device management
    - 2 tegengestelde doelen: users productief laten zijn overal/altijd/elke device, en organisatie assets beschermen
    - Basis: device identities beheren -> daarna aanuvllen met tools zoals Microsoft Intune voor security/compliance-standaarden
   
  - 3 device types:
    - 1 Microsoft Entra Registered
        - Doel: BYOD / mobile devices
        - Device ownership: User of organization
        - Sign-in: lokaal account (vb. Microsoft account) + Entra Account toegevoegd voor org-resources
        - Os: Windows 10+, MacOS 10.15+, iOS 15+, Android, Linux (Ubuntu/RHEL LTS)
        - Management: MDM (Intune) of Mobile Application Management
        - Key capabilities: SSO naar cloud resources, Conditional Access (als enrolled in Intune, of via App protection policy)
        - Scenario: User gebruikt prive-PC voor werk-mail/HR-tools -> registreert PC bij Entra ID -> Intune-Polices worden afgedwongen -> toegang verleend. Ander scenario: geroote android telefon -> Intune compliance policy blokkeert toegang
     
    - 2 Microsoft Entra Joined
      - Doel: Cloud-first/Cloud-only organisaties (elke grootte/industrie)
      - Device ownership: Alleen organization
      - Sign-in: volledig met org Entra-account (geen lokaal account ernaast)
      - OS: Windows 10/11 (niet Home), Windows Server 2019+ VMs in Azure, macOS 13+ (preview)
      - Management: MDM (Intune) of co-management met Configuration Manager
      - Key capabilities: SSO naar cloud én on-premises resources, Conditional Access, Self-service Password Reset, Windows Hello PIN reset
      - Deployment: OOBE, bulk enrollment, Windows Autopilot
      - Wanneer gebruiken: geen on-prem AD, mobile devices (tablets/phones), primair M365/SaaS-gebruik, seasonal workers/contractors/studenten apart beheren, remote branch offices met weinig infra
     
    - 3 Hybrid Microsoft Entra Joined
      - Doel: organisaties met bestaand on-prem AD die ook Entra ID-voordelen willen
      - Device ownership: Organization
      - Sign-in: Password of Windows Hello for Business
      - OS: Windows 10/11 (niet Home), Windows Server 2016/2019/2022
      - Management: Group Policy, Configuration Manager standalone, of co-management met Intune
      - Key capabilities: SSO naar cloud én on-premises, Conditional Access, SSPR, Windows Hello PIN reset
      - Wanneer gebruiken: Win32-apps die AD machine authentication nodig hebben, blijven gebruiken van Group Policy, bestaande imaging-oplossingen behouden
     

- Device writeback — LET OP, verouderd
  - Niet meer ondersteund / niet aanbevolen
  - Vervangen door Cloud Kerberos Trust; laat Entra joined/hybrid joined devices authenticeren tegen on-prem resources zonder device objects terug te schrijven naar on-prem AD
  - Voor nieuwe hybrid deployments: gebruik Cloud Kerberos Trust voor on-prem SSO + Windows Hello for Business
 
- Onthouden voor examen — kern van het onderscheid:
  - Registered = user/personal device + org account ernaast (BYOD)
  - Joined = volledig org-device, geen on-prem AD nodig (cloud-only)
  - Hybrid joined = org-device, wél on-prem AD aanwezig (brug tussen oud en nieuw)

---

### Exercise - change group license assignments
  - [04-sc300/labs/06-change-group-license-assignments](../../04-sc300/labs/06-change-group-license-assignments.md)

---

### Exercise - change user license assignments
  - [04-sc300/labs/07-change-user-license-assignments](../../04-sc300/labs/07-change-user-license-assignments.md)


---

### Create custom security attributes
  - Wat is een custom security attribute?
    - Business-specifieke attributes (key-value pairs); zelf te definieren en toe te wijzen aan Entra objects
    - Gebruik: informatie opslaan, objecten categoriseren, fine-grained access control op specifieke Azure resources
   
  - Waarom gebruiken
    - User profiles uitbreiden (bv. Hourly Salery toevoegen aan employee-profielen
    - Zorgen dat alleen admins zo'n gevoelig attribute kunnen zien
    - Honderderen/duizenden applicaties categoriseren -> filterbare inventory voor auditing
    - Users toegang geven tot Azure Storage blobs die bij een specifiek project horen

  - Wat kun je ermee doen
    - Business-specifieke info definieren voor je tenant
    - Toevoegen aan users en enterprise applicatons (service principals)
    - Objecten beheren via queries/filters op basis van de attricutes
    - Attribute governance; attributes bepalen wie toegang krijgt
   
  - Waar niet ondersteunt
    - Microsoft Entra Domain Services
    - SAML token claims
    - JWT (JSON Web Token) claims
   
  - Features
    - Tenant-wide beschikbaar
    - Description toe te voegen
    - Data types: Boolean, integer, string
    - Single of multiple values
    - Vrije invoer (free-form) of predefined values
    - Ook toewijsbaar aan directory-synced users vanuit on-premises AD
   
---

## Explore automatic user creation

### SCIM — wat en waarom
- SCIM (System for Cross-Domain Identity Management) = open standaard protocol voor het automatisch uitwisselen van user identity info tussen systemen
- Doel: users automatisch aangemaakt in Entra ID (of on-prem AD) zodra ze in het HCM/HR-systeem worden toegevoegd
- Attributes/profielen blijven gesynchroniseerd tussen systemen; updates of removal op basis van status/rol-wijzigingen
- Kernvoordeel: snelle deprovisioning; user weg uit HR-systeem = automatisch weg uit Entra ID, minder breach-risico

### 4 componenten van SCIM (examen-relevant)
- **HCM system**: HR-systeem dat het hele employee lifecycle proces ondersteunt/automatiseert
- **Microsoft Entra Provisioning Service**: gebruikt SCIM 2.0 protocol. Verbindt met SCIM endpoint van de app, gebruikt SCIM user object schema + REST APIs voor provisioning/deprovisioning
- **Microsoft Entra ID**: de user repository die de identity lifecycle + entitlements beheert
- **Target system**: de app/systeem met een SCIM endpoint die met Entra provisioning samenwerkt

### API-driven inbound provisioning
- Voor HR-systemen die geen SCIM endpoint hebben
- General Availability sinds maart 2024
- In plaats van dat het source-systeem SCIM-data pusht, kan een automation tool/script data ophalen uit elk systeem en naar de Entra provisioning API sturen
- Ondersteunde bronnen: Workday, SAP SuccessFactors, en elk custom HR-systeem via de API
- Voordeel: flexibiliteit; werkt ook als het HR-platform geen native SCIM-integratie heeft

**Onthouden:** SCIM = protocol voor systemen die het native ondersteunen. API-driven inbound provisioning = workaround voor systemen die dat niet doen.

---

## Module Assessment — Module 2 (Create, configure, and manage identities)

**Score:** 89%

### Vraag 1
What is the main difference between a security group and a Microsoft 365 group in Microsoft Entra ID?

- Security groups are for managing access to servers, while Microsoft 365 groups are for managing user profiles.
- ✅ Security groups manage permissions, while Microsoft 365 groups provide collaboration features.
- Security groups are only for on-premises users, while Microsoft 365 groups are for cloud users.

### Vraag 2
How should an administrator handle users in an error state due to 'MutuallyExclusiveViolation' during group-based license assignment?

- ✅ Remove conflicting licenses or service plans from the user.
- Increase the number of licenses available for the group.
- Assign the licenses directly to the users instead of using group-based licensing.

### Vraag 3
How do custom security attributes in Microsoft Entra ID contribute to the management of user roles within an organization?

- By automatically assigning users to predefined security groups.
- By providing single sign-on capabilities for users accessing cloud resources.
- ✅ By defining business-specific information that can be used to categorize users and enforce access policies.

### Vraag 4
An administrator discovers users in a licensing error state due to 'LicenseAssignmentAttributeConcurrencyException'. What is the recommended course of action?

- ✅ Allow Microsoft Entra ID to retry processing the user license automatically.
- ❌ Manually reprocess the user's license assignments in the admin center. *(fout beantwoord)*
- Remove the user from all licensed groups and reassign them.

**Toelichting:** Entra ID lost dit type error automatisch op via retry — geen handmatige actie vereist.

### Vraag 5
A company needs to track and manage project access for various departments using Microsoft Entra ID. What is the most effective way to implement custom security attributes to achieve this?

- ✅ Define project-specific custom security attributes and assign them to users based on their department and project involvement.
- Rely on dynamic group membership rules based on user roles for project access.
- Create a single security attribute for all projects and assign it to all users.

### Vraag 6
You are managing licenses for a newly formed team that needs access to Microsoft 365 services. What is the most efficient way to assign licenses to this team if it consists of a large number of users?

- Assign licenses individually to each user.
- ✅ Assign licenses to the team through a security group.
- Ask each user to request a license from the admin.

### Vraag 7
A user is unable to receive a license due to a 'CountViolation' error. What should be done to resolve this issue?

- Disable unused service plans in the current license assignment.
- Reassign the user to a different group that has available licenses.
- ✅ Increase the number of available licenses for the product.

### Vraag 8
What is the primary advantage of using custom security attributes to manage access control in Microsoft Entra ID?

- They reduce the need for multifactor authentication for users.
- ✅ They allow for fine-grained access control based on specific business logic and requirements.
- They automatically synchronize user data across all cloud services.

### Vraag 9
If a user in your organization has licenses assigned from multiple groups, how is the user's final license state determined?

- The user can choose which group licenses to apply.
- ✅ The user receives a combination of all assigned licenses.
- The user is assigned only the licenses from the first group they were added to.


---
---

## Learning Path 2: Implement an identity management solution using Microsoft Entra ID
### Module 3: Implement and manage external identities 

---

## Introduction
  - Waarom dit belangrijk is
    - Externe users uitnodigen om je Azure resources te gebruiken is waardevol, maar moet veilig gebeuren. Deze module behandelt hoe je veilige B2B collaboration scenario's opzet met users buiten je organisatie.

  - Wat deze module behandelt
    - External collaboration settings beheren in Entra ID
    - Externe users uitnodigen (individueel of bulk)
    - External user accounts beheren in Entra ID
    - Identity providers configureren (social en SAML/WS-Fed)
    - Microsoft Entra Verified ID verkennen

  - Learning objectives
    - Manage external collaboration settings in Microsoft Entra ID
    - Invite external users (individually or in bulk)
    - Manage external user accounts in Microsoft Entra ID
    - Configure identity providers (social and SAML/WS-fed)
    - Explore Microsoft Entra Verified ID

---

### Describe guest access and Business to Business accounts
  - Wat is B2B collaboration
    - Onderdeel van Microsoft Entra External Identities (onder de Entra-paraplu)
    - Laat je guest users uitnodigen om samen te werken met je organisatie
    - Deel je apps/services veilig met externe users, terwjil je zelf controle houdt over je corporate data
    - Werkt ook met partners die zelf geen Entra ID of IT-afdeling hebben
   
  - Hoe guest users toetreden
    - Invitation + redemption processl; partner gebruikt eigen credentials om toegang te krijgen (self-service sign-up user flows ook mogelijk voor apps/resources)
    - Na redemption/sign-up: verschijnen als user object in jouw directory
    - Type: "guest", herkenbaar aan #EXT# in de user principal name
    - Develpoers kunnen het invitation-proces customizen via Entra ID B2B API (bv. eigen self-service sign-up portals bouwen)
   
  - B2B collaboration
    - Externe user logt in met eigen credentials; geen apart account nodig dat jij beheert
    - User object wordt aangemaakt in dezelfde directory als je eigen employees
    - Default: beperkte privileges in je directory
    - Kan verder beheerd worden zoals een gewone employee: toevoegen aan groups etc
   
  - Onthouden: #EXT# in UPN= herkenningsteken voor B2B guest users.
    - Guest + eigen credentials, eigen identity provider beheert de authenticatie, jij beheert alleen de toegang

---
   
### Manage external collaboration
  - Wat is External Identities
    - Externe users "brengen eigen identity mee"; corporate, government-issued, of unmanaged social identity (Google/Facebook)
    - Hun eigen identity provider beheert de identity, jij beheert alleen de toegang via Entra ID
   
  - Invitation redemption flow (stap-voor-stap, belangrijk voor examen)
    - Entra ID doet user-based discovery; check of user al bestaat in een managed tenant (unmanaged accounts kunnen niet meer gebruikt worden voor redemption). UPN mathct zowel Entra account als personal MSA -> userkiest zelf werlk account
    - Als SAML/WS-Fed IdP federation is ingeschakeld: domain suffix matcht een geconfigureerde IdP -> redirect daarnaartoe
    - Als google federation is ingeschakeld: domain = gmail.com/googlemail.com -> redirect naar google
    - Check op bestaande personal MSA -> inloggen met die MSA
    - Home directory geidentificeerd -> user naar juiste identity provider gestuurd om in te loggen
    - Geen home directory gevonden + email on-time passcode enabled -> passcode naar utigenodigde email, usr vult in op Entra sign-in pagina
    - Geen home directory gevonden +one-time passcode disabled -> user moet consumer MSA aanmaken met het uitgenodigde emailadres (ook mogelijk met work-emails op niet-geverfifieerde domains)
    - Na authenticatie bij juiste IdP -> terug naar Entra ID voor consent experience
   
  - External Identities scenarios; focus ligt op HOE de user wil inloggen, niet op relatie tot je organisatie

  - B2B collaboration scenario
    - Primary scenario: Collaboration via Microsoft apps (M365, Teams) of eigen apps (SaaS, custom)
    - Intended for: externe partners/suppliers/vendors; verschijnen als guest users
    - Identity providers supported: work/school accounts, elk emailadres, SAML/WS-Fed IdPs, Gmail, Facebook
    - External user management: in dezelfde directory als employees, geannoteerd als guest, beheerd zoals employees (groups etc.)
    - SSO: werkt voor alle Entra-connected apps (M365, on-prem apps, SaaS zoals Salesforce/Workday)
    - Security policy/compliance: beheerd door de host/inviting organization (bv. via Conditional Access)
    - Branding: van de host/inviting organization
   
  - Externe collaboration settings beheren
    - Default: iedereen (ook guests) mag guests uitnodigen, zelfs zonder admin-rol
    - External collaboration settings → guest invitations aan/uit zetten per type user, of delegeren via rollen
   
  - Guest permissions
    - Default: beperkt; guests kunnen geen users/groups/directory resources listen, maar wel membership van non-hidden groups zien
    - Admins kunnen dit verder beperken -> guest kan dan alleen eigen profiel zien.
   
  - B2B invitation policies (4 opties)
    - Turn off invitations; niemand kan externen uitnodigen
    - Only admins + Guest Inviter role; beperkt tot die twee
    - Admins + Guest Inviter role + members; members mogen ook uitnodigen
    - All users, including guests; iedereen mag uitnodigen (dit is de default)

---

### Exercise - configure external collaboration
  - [04-sc300/labs/08-configure-external-collaboration](../../04-sc300/labs/08-configure-external-collaboration.md)
  - **Ook uitgevoerd in:** [Oceanic Airlines sandbox](../../00-sandbox/05-configure-external-collaboration.md)

---

### Exercise - Invite external users - individually and in bulk
  - [04-sc300/labs/09-invite-external-users-individually-and-in-bulk](../../04-sc300/labs/09-invite-external-users-individually-and-in-bulk.md)
  - **Ook uitgevoerd in:** [Oceanic Airlines sandbox](../../00-sandbox/06-invite-external-users.md)


---


### Exercise - add guest users to directory
  - Zelfde oefening als eerder al uitgevoerd; enige nieuwe info hier: group email-adressen worden niet ondersteund en het +-symbool in een emailadres moet weggelaten worden.

---

### Exercise - invite guest users bulk
  - [04-sc300/labs/10-invite-guest-users-bulk](../../04-sc300/labs/10-invite-guest-users-bulk.md)

---

### Demo - manage guest users in Microsoft Entra ID
  - Externe users uitnodigen voor B2B collaboration
  - Resources toewijzen aan guest users
  - Conditional Access policies opzetten om guest-toegang te beveiligen
  - Dekt dezelfde kernconcepten als eerder praktisch uitgevoerd (Desmond Hume guest-invite in de sandbox), aangevuld met het gebruik van Conditional Access specifiek voor guest-scenario's.

---

### Manage external user accounts in Microsoft Entra ID
  - Guests kunnen hogere privileges krijgen
    - Default: beperkte permissions, maar guests kunnen aan elke rol toegevoegd worden als de organisatie dat nodig heeft
    - Least privilege blijft de aanbeveling; gebruik PIM om toegang voor guests te regelen (tijdelijk, just-in-time i.p.v. permanent)

  - UserType; kernproperty
    - Member; employee, op de payroll, verwacht toegang tot interne sites, wordt niet als externe collaborator gezien
    - Guest; niet intern, bv. externe collaborator/partner/klant. Verwacht geen interne memo's of company benefits
    - Belangrijk: UserType zegt niets over hoe de user inlogt of welke directory role ze hebben; het is puur een indicatie van de relatie tot de organisatie, gebruikt om policies op te baseren

  - Identities property; welke IdP gebruikt de user
    - External Microsoft Entra tenant; eigen Entra-account van andere organisatie
    - Microsoft account; inlog via MSA
    - host's domain}; eigen Entra-account van jouw organisatie
    - google.com; Gmail, self-service signup
    - facebook.com; Facebook, self-service signup
    - mail*; via Entra Email one-time passcode (OTP)
    - (issuer URI}; externe org met SAML/WS-Fed IdP (niet Entra ID)

  - Kunnen B2B users als Member i.p.v. Guest toegevoegd worden?
    - Normaal: B2B user = Guest (default, synoniem in de praktijk)
    - Uitzondering: partnerorganisatie is deel van dezelfde grotere organisatie als de host -> dan kun je die users als Member behandelen i.p.v. Guest
    - Aanpassen via de user properties

  - UserType converteren (Member <-> Guest)
    - Technisch mogelijk via PowerShell
    - Niet aanbevolen als losstaande actie; UserType weerspiegelt de relatie tot de organisatie, dus alleen wijzigen als die relatie echt verandert. Denk ook aan gevolgen: UPN-wijziging, resource-toegang, mailbox-toewijzing
    - Microsoft: bouw geen afhankelijkheid op deze waarde, kan in de toekomst immutable worden

  - Guest restricties verwijderen
    - Mogelijk om guest dezelfde permissions als members te geven
    - Instelbaar via: User settings in Entra ID -> External users optie

  - Dynamic groups + B2B (herhaling + toepassing)
    - Rules gebaseerd op user attributes (bv. userType, depatrment, country/region)
    - Members automatisch toegevoegd/verwijderd op basis van attributes
    - Gebruikt voor: app/resource-toegang, license-toewijzing
    - Vereist Entra ID P1 of P2

  - Onthouden voor examen: UserType (Member/Guest) ≠ sign-in method ≠ directory role; dit zijn 3 losse dingen die vaak door elkaar gehaald worden in examenvragen.

---

### Manage external users in Microsoft 365 workloads
  - Wat het is
    - M365 kan, net als Entra ID, guest users uitnodigen voor collaboration
    - Guests verschijnen als external in de user list, standaard beperkte/geen rechten
    - Kunnen collaboration rights krijgen op elke M365 workload, en zelfs licenties om specifieke acties uit te voeren

  - External collaboration opties; activiteiten en defaults

| Activiteit | Account type | Default |
|---|---|---|
| Authenticated file/folder sharing | Guest account | Enabled |
| Site sharing | Guest account | Enabled |
| Team sharing | Guest account | Enabled |
| Shared channel in Teams | Existing M365 external account | Disabled |
| External chat/meetings | Existing M365 external account | Enabled |
| Anonymous meeting join | None (geen account nodg) | Enabled |
| Unauthenticated file/folder sharing | None (geen account nodig) | Enabled |

**Kernpunt:** externen krijgen nooit uit zichzelf toegang; een user binnen je organisatie moet altijd eerst de activiteit initieren (bv. een file delen, iemand uitnodigen). Elke instelling hierboven kan uitgeschakeld worden als je die activiteit niet wilt toestaan.

  - Governance
    - Regelmatig reviewen/valideren van alle accounts, met extra aandacht voor guests
    - Onnodige capabilities/licenties/toegang verwijderen zodra niet meer nodig; geldt voor guests en members

  - Beheertools voor M365 guest users
    - Microsoft 365 admin center (admin.microsoft.com)
    - Microsoft Entra admin center (entra.microsoft.com)
    - Entra ID binnen de Azure portal
    - Scripting: Microsoft Graph, PowerShell, CLI
    - Direct binnen de meeste M365 workloads zelf

  - **Onthouden:** dit is een verlengstuk van B2B collaboration die je al kent; nu specifiek toegepast op M365-workloads (Teams, SharePoint, files) i.p.v. puur Entra ID zelf. Let vooral op welke defaults enabled vs disabled zijn; dat soort details komt vaak terug in examenvragen.

---

### Exercise - explore dynamic groups
  - [04-sc300/labs/11-explore-dynamic-groups](../../04-sc300/labs/11-explore-dynamic-groups.md)
  - **Ook uitgevoerd in:** [Oceanic Airlines sandbox](../../00-sandbox/07-jacobs-security-group.md)
    
---

### Implement and manage Microsoft Entra Verified ID
  - Wat is het?
    - Decentralized identity-oplossing; issuen en verifieren van verifiable credentials
    - Voor issuers: service om eigen verifiable credentials te customizen en uit te geven
    - Voor verifiers: gratis REST API om credentials op te vragen/accepteren in apps/services
   
  - Analogie (herhaling van eerdere unit; decentralized identity)
    - Vergelijkbaar met rijbewijs, diploma, paspoort; bewijs van iets, uitgegeven door een vertrouwde partij
    - Verifiable credential = data object met claims van de issuer over een subject
    - Geïdentificeerd via schema, bevat DID van issuer + subject
    - Issuer's DID zet een digitale handtekening als bewijs van attestatie

  - Wat je nodig hebt om te deployen
    - Azure tenant met subsciption
    - Microsoft Entra ID premium licentie (P1/P2)
    - Ingelogd als Global Administrator
    - Geconfigureerde Azure Key Vault instance

  - Setup; stappen
    - Azure Portal -> zoek "verifiable credentials" -> Verifiable Credentials (Preview)
    - Linker menu → Getting started
    - Organisatie instellen:
      - Organization name — intern referentie-naam, klanten zien dit niet
      - Domain — gekoppeld aan een service endpoint in het DID-document. Bindt de DID aan iets tastbaars (jouw domein). Wallets (bv. Microsoft Authenticator) gebruiken dit om de DID te verifiëren — tonen een verified-symbool als het klopt, of een waarschuwing als het niet gevalideerd kan worden
      - Key vault — naam van je bestaande key vault
    - Save and create credential
   
---

### Configure identity providers
  - SAML/WS-Fed IdP federation (direct federation)
    - Federatie met een partner-organisatie's IdP (SAML 2.0 of WS-Fed protocol)
    - Guests loggen in met eigen IdP-managed org account; geen apart Entra account nodig
    - Gekoppeld aan domain namespaces (bv. contoso.com)
    
  - Wanneer wordt een guest via SAML/WS-Fed geauthenticeerd?
    - Al eerder geredeemde guests behouden hun oorspronkelijke authenticatie-methode; federatie instellen verandert niks retroactief
    - Federatie verwijderen -> guests die de federated IdP gebruikten kunnen niet meer inloggen
    - Auth-methode van een guest aanpassen kan via reset van redemption status
   
  - End-user experience
    - Sign-in -> redirect naar eigen IdP -> terug naar Entra ID voor resource-toegang
    - Als federated IdP SSO heeft en Entra-sessie is verlopen: user krijgt gewoon SSO, geen nieuwe login nodig

  - SAML 2.0 vereisten
    - Response moet bevatten: AssertionConsumerService, Audience (`urn:federation:MicrosoftOnline`), Issuer
    - Claims: NameID Format (persistent), emailaddress
    - Target domain mag niet DNS-verified zijn op Entra ID
      - Kort samengevat: het externe SAML-systeem moet Entra ID vertellen (1) waar het antwoord naartoe moet, (2) dat het bericht echt voor Microsoft bedoeld is, (3) wie het verstuurt, (4) een consistente ID van de gebruiker, en (5) hun emailadres; en het domein waarmee je federeert mag niet toevallig al van jezelf zijn.

  - WS-Federation vereisten
    - Getest voor: AD FS en Shibboleth
    - Message moet bevatten: PassiveRequestorEndpoint, Audience, Issuer
    - Claims: ImmutableID, emailadress
    - Zelfde regel: domain niet DNS-verified
      - Kort samengevat: het externe WS-Fed-systeem moet Entra ID vertellen (1) waar het antwoord naartoe moet, (2) dat het bericht echt voor Microsoft bedoeld is, (3) wie het verstuurt, (4) een vaste onveranderlijke ID van de gebruiker, en (5) hun emailadres; en het domein waarmee je federeert mag niet toevallig al van jezelf zijn.


  - Google en Facebook als identity provider
    - Google: Guests loggen in met eigen Gmail-account, werkt via een gewone invite. Alleen voor Gmail (niet G Suite; daarvoor gebruik je SAML/WS-Fed)
    - Facebook: Alleen via self-service sign-up user flows, NIET via een normale invite
    - Beide vereisen een Client ID + Client Secret, ingesteld in Entra ID onder External Identities -> All identity providers

   - Onthouden voor examen:
    - Google = Gmail-only, via invite mogelijk
    - Facebook = self service sign-up only, NIET via invite
    - SAML/WS-Fed = voor organisaties met eigen IdP, domain-gebaseerd, niet DNS-verified vereist

---

### Implement cross-tenant access controls
  - Wat het is
    - Regelt hoe jouw Entra organisatie samenwerkt met andere Entra organisaties (of Microsoft clouds)
    - Inbound access: Hoe externe organisaties met jou samenwerken
    - Outbound access: Hoe jouw users samenwerken met externe organisaties

  - Default settings
    - B2B collaboration: Standaard enabled
    - B2B direct connect: Standaard blocked

  - 4 instellingen (examen-kernstof)
    - Outbound access settings: Bepaalt of jouw users toegang krijgen tot externe organisaties. Toepasbaar op iedereen, of specifieke users/groups/apps
    - Inbound access settings: Bepaalt of externe users toegang krijgen tot jouw resources. Zelfde granulariteit (iedereen of specifiek)
    - Trust settings (inbound): Bepaalt of jouw Conditional Access policies externe MFA, compliant device, en hybrid Entra joined device vertrouwen. Als de externe user dit al heeft voldaan in hun eigen tenant, hoeft dat niet opnieuw
    - B2B direct connect: Mutual trust tussen 2 Entra organisaties voor naadloze samenwerking, werkt nu specifiek met Teams shared channels

  - Organization-specific configuratie
    - Default settings gelden voor alle externe verbindingen
    - Kan per organisatie apart ingesteld worden: Cross-tenant access control -> Organizational settings -> tenant toevoegen -> inbound/outbound per tenant configureren

  - Microsoft Cloud-specific configuratie
    - Voor connectie met Azure Government of Azure China (bv. bij overheidscontracten); apart te configureren via Microsoft Cloud settings
   
  - B2B Direct Connect; details
    - Vereist mutual trust; beide organisaties moeten het inschakelen in hun cross-tenant access settings
    - Na trust: gebruiker heeft SSO-toegang tot externe resources met eigen (home tenant) credentials.
    - Werkt momenteel alleen met Teams shared channels
    - Praktisch: org A maakt shared channel -> nodigt B2B direct connect user van org B uit -> die user krijgt naadloos toegang vanuit hun eigen Teams-instance, geen aparte login nodig
   

  - Onthouden voor examen:
    - B2B collaboration ≠ B2B direct connect; collaboration = guest user object in je directory, direct connect = geen guest object, alleen Teams shared channel trust
    - B2B direct connect vereist wederzijdse instelling (beide tenants moeten het aanzetten)

---

## Knowledge Check — Module 3 (Implement and manage external identities)

**Score:** 100%

### Vraag 1
Users assigned limited administrator directory roles can use the Azure portal to invite B2B collaboration users. You can invite B2B collaboration users to a directory or to a group. What other activities can B2B collaboration users be invited?

- Limited self-service functionality for modifying their profiles.
- Network resources such as printers.
- ✅ An application.

### Vraag 2
Microsoft Entra B2B can be configured to federate with identity providers that use either of two protocols. One protocol is Security Assertion Markup Language (SAML); what is the other protocol?

- ✅ WS-Federation (WS-Fed)
- Layer 2 Tunneling Protocol (L2TP)
- Resource Location Protocol (RLP)

### Vraag 3
What are dynamic groups?

- Dynamic groups are Microsoft 365 groups whose memberships consist of Dynamics 365 users, who require special attribute configurations.
- ✅ Dynamic groups are security groups whose memberships are based on user attributes (such as userType, department, or country/region).
- Dynamic groups are groups whose membership numbers fluctuate significantly within a given timeframe.


---
---

## Learning Path 2: Implement an identity management solution using Microsoft Entra ID
### Module 4: Implement and manage hybrid identity

### Introduction
  - Wat is hybrid identity
    - Identity-oplossingen die zowel on-premises als cloud omgevingen overspannen
    - Unified authentication/authorization, ongeacht waar de resource staat

  - Waarom nodig
    - Organisaties voegen cloud-apps toe naast bestaande on-prem apps -> worden "hybrid companies"
    - On-prem AD alleen is niet genoeg -> uitbreiden met Entra ID nodig voor een volledige hybrid identity-oplossing

  - Wat deze module behandelt
    - Microsoft Entra Connect -> implementeren en beheren
    - Password Hash Synchronization (PHS) en Pass-through Authentication (PTA) -> juiste authenticatiemethode kiezen
    - Seamless SSO -> gebruikers toegang geven zonder herhaaldelijk in te loggen
    - Federation (excl. handmatige AD FS deployments) -> koppeling met externe directories
    - Entra Connect Health -> monitoring van de sync-oplossing
    - Troubleshooting synchronization errors

  - Learning objectives
    - Plan, design, and implement Microsoft Entra Connect
    - Manage Microsoft Entra Connect
    - Implement and manage password hash synchronization (PHS)
    - Implement and manage pass-through authentication (PTA)
    - Implement and manage seamless single sign-on (seamless SSO)
    - Implement and manage federation excluding manual AD FS deployments
    - Troubleshoot synchronization errors
    - Implement and manage Microsoft Entra Connect Health

  - **Onthouden:** dit is een technisch zwaardere module dan de vorige; gaat over de mechanica van hoe on-prem en cloud identities gesynchroniseerd blijven, niet alleen over UI-configuratie zoals eerdere modules.

---

### Plan, design, and implement Microsoft Entra Connect

- Wat is het
  - Brug tussen on-prem AD en cloud Entra ID; synchroniseert identties, zorgt voor consistente identity op beide platforms
  - Enables: PHS, PTA, seamless SSO

- 5 capabilities
  - Synchronization; users/groups/objects aanmaken + matchen tussen on-prem en cloud (incl. password hashes)
  - PHS; sync van password hash naar Entra ID
  - PTA; zelfde wachtwoord on-prem/cloud, zonder federatie-infrastructuur
  - Federation integration; optioneel, voor AD FS-hybrid setups
  - Health monitoring; via Entra Connect Health

- Waarom gebruiken
  - 1 identity voor cloud + on-prem resources, vervangt oudere sync-tools, inbegrepen in Entra ID subscription

- Cloud authentication; Password Hash Synchronization (PHS)
  - Simpelste optie; geen extra infrastructuur nodig
  - Draait als onderdeel van Connect sync, elke 2 minuten
  - Voordeel: hoge beschikbaarheid (cloud-schaal), werkt met Identity Protection (P2); leaked credentials report
  - Nadeel: on-prem account-status wijzigingen (bv. account uitschakelen) worden niet direct doorgevoerd; pas na volgende sync cyclus
  - Aanbevolen: tweede Connect-server in staging mode voor business continuity

- Cloud authentication; Pass-through Authentication (PTA)
  - Lightweight agent(s) op on-prem servers, valideert direct tegen on-prem AD; wachtwoord verlaat het netwerk niet
  - Aanbevolen: 3 agents voor redundantie (agents mogen niet in perimeter network staan; hebben internet + domain controller toegang nodig)
  - Voordeel: on-prem account policies direct afgedwongen (disabled/locked/expired/sign-in hours)
  - PHS kan als backup dienen bij PTA-uitval; geen automatische failover, moet handmatig via Connect

- Federated authentication (bv. AD FS)
  - Entra ID geeft authenticatie door aan extern trusted systeem
  - Nodig voor: smartcard/certificate auth, on-prem MFA-servers, third-party MFA, sAMAccountName-based sign-in (DOMAIN\username i.p.v. UPN)
  - Meest complex, vereis eigen server-farm (perimeter + internal network), meer on-prem investering
  - Beheer/onderhoud valt buiten Entra ID's controle

- Aanbeveling; gebruik altijd PHS, ongeacht welke methode je kiest als primaire auth
  - HA/disaster recovery; PHS is cloud-schaal, altijd beschikbaar; PTA/federation hangen af van on-prem infra die kan uitvallen
  - On-prem outage survival; organisaties met PHS enabled konden binnen uren overschakelen bij on-prem uitval (bv. ransomware); zonder PHS duurde herstel weken
  - Identity Protection; leaked credentials report vereist PHS, ongeacht primaire auth-methode

- sourceAnchor (= immutableId)
  - Attribute dat een object uniek en onveranderlijk koppelt tussen on-prem en cloud
  - Gebruikt bij: nieuwe sync-server (her)bouwen, overstap van cloud-only naar sync, federatie-claims
  - Regels: minder dan 60 karakters, geen speciale tekens, globally unique, string/integer/binary, niet gebaseerd op username (kan wijzigen), niet case-sensitive
  - Default: objectGUID (single forest). Alternatief: bv. employeeID (mits nooit case-wijzigend)

- UPN bij sign-in
  - Entra ID gebruikt UPN om te authenticeren
  - Moet: RFC 822-formaat (username@domain), suffix matcht een verified custom domain
  - Express settings = default UPN attribute -> als dat niet klopt: Custom Installation nodig

- Custom domain vereiste
  - UPN-suffix moet een geverifieerd domain zijn, anders vervangt de tool het automatisch door contoso.onmicrosoft.com
  - Non-routable domains (bv. contoso.local) kunnen niet geverifieerd worden -> Connect waarschuwt en adviseert custom settings i.p.v. express

- Topologieën (herkennen, niet allemaal uit hoofd)
  - Single forest + single tenant; meest voorkomend, enige optie bij express install
  - Multiple forests + single tenant; 1 Connect-server moet alle forests bereiken
  - Multiple forests, users in 1 directory; losse forests, unified GAL in Entra ID
  - Full mesh + optional GALSync; two-way trusts, GALSync via FIM/MIM (niet via Connect zelf)
  - Account-resource forest; resource forest bevat Exchange/Teams, account disabled maar mailbox gelinkt
  - Staging server; leest overal, schrijft nergens, back-up/test rol
  - Multiple Entra tenants; 1:1 relatie Connect-server -> tenant, tenants zijn geïsoleerd
  - Elk object maar 1x per tenant; meerdre Connect-servers met mutually exclusive filtering (bv. per domain/OU)

- Componenten van de sync engine
  - Connector Space (CS); staging area per connected directory (elke forest + Entra ID heeft eigen CS)
  - Metaverse (MV); centrale plek waar te syncen objects samenkomen, maar 1 MV totaal
  - Sync rules; bepalen projectie/join naar MV + welke attributes gekopieerd/getransformeerd worden
  - Run profiles; bundelen de sync-stappen tussen staging areas en directories

- Microsoft Entra Connect Cloud Sync (alternatief/aanvulling)
  - Gebruikt lightweight cloud provisioning agent i.p.v. de volledige Connect-applicatie
  - Voordelen:
    - Werkt met multi-forest, disconnected AD-omgevingen (bv. na overname, geïsoleerde forests)
    - Simpele installatie; agent is puur een brug, config zit in de cloud
    - Meerdere agents mogelijk voor high availability
    - Ondersteunt groups tot 50.000 members (aanbevolen: alleen OU-scoping filter gebruiken)
  - Kan naast reguliere Connect sync gebruikt worden
  - Sync-interval: ook elke 2 minuten

- Onthouden voor examen
  - PHS = simpel + altijd als backup aan
  - PTA = agents nodig, directe policy-enforcement
  - Federation = complex, voor geavanceerde auth-eisen
  - sourceAnchor = default objectGUID, nooit gebaseerd op naam
  - Cloud Sync = lightweight alternatief voor multi-forest/disconnected scenario's
 
- Summary:
  - Deze unit draait om Microsoft Entra Connect, de tool die je on-prem Active Directory (georganiseerd in forests, elk met eigen domains) verbindt met je cloud-based Entra ID, zodat je één consistente identity hebt voor beide werelden. De kern is de keuze uit 3 authenticatiemethodes: PHS (Password Hash Synchronization; simpelst, synct alleen een wachtwoord-hash naar de cloud, geen extra infra nodig), PTA (Pass-through Authentication; een agent op je eigen server checkt live tegen je on-prem AD, dus policies zoals account-lockout werken direct), en Federation (bv. via AD FS; het meest complex, voor geavanceerde eisen zoals smartcards, maar valt buiten Entra ID's eigen controle). Ongeacht welke methode je kiest als hoofdmethode, wordt aangeraden altijd PHS als backup te hebben, omdat het als enige blijft werken bij een on-prem storing. Verder behandelt de unit een aantal technische bouwstenen: de sourceAnchor (ook wel immutableId) die een gebruiker uniek koppelt tussen on-prem en cloud, de UPN (user principal name) die bepaalt waarmee iemand inlogt en die een geverifieerd domain nodig heeft, verschillende topologieën voor bedrijven met één of meerdere forests, en de onderliggende sync engine (Connector Space, Metaverse, sync rules, run profiles) die bepaalt hoe data precies stroomt. Tot slot is er Microsoft Entra Connect Cloud Sync, een lichter alternatief met cloud-agents, vooral handig bij complexe of losstaande (disconnected) multi-forest omgevingen.

---

### Implement manage password hash synchronization (PHS)
- Wat is het
	- Password hash synchronization is één van de sign-in methodes voor hybrid identity
	- Microsoft Entra Connect synchroniseert een hash-van-de-hash van het wachtwoord van on-premises Active Directory naar cloud Entra ID

- Hoe het werkt
	- AD DS slaat wachtwoorden op als hash value (one-way mathematische functie); onmogelijk terug te rekenen naar plain text
	- Entra Connect sync haalt de password hash op uit on-premises AD, past extra security processing toe, en synct dit naar de Entra authentication service
	- Synchronisatie gebeurt per user, chronologisch
	- Draait elke 2 minuten; interval niet aanpasbaar
	- Nieuwe sync overschrijft het bestaande cloud-wachtwoord

- Eerste synchronisatie
	- Bij inschakelen: initiele sync van alle in-scope users tegelijk; geen mogelijkheid om vooraf een subset te kiezen
	- Na de initiële sync: selective password hash sync instelbaar voor toekomstige syncs
	- Bij meerdere connectors: mogelijk om PHS voor somige connectors uit te schakelen, andere niet

- Wijzigingen en foutafhandeling
	- Wachtwoordwijziging on-premises wordt meestal binnen enkele minuten gesynchroniseerd
	- Mislukte sync-pogingen worden automatisch opnieuw geprobeerd
	- Fouten worden gelogd in de event viewer

- Inschakelen
	- Express Settings installatie: PHS automatisch ingeschakeld
	- Custom settings installatie: PHS als losse optie beschikbaar op de sign-in pagina

- PHS en FIPS (Federal Information Processing Standard)
	- Als de server FIPS-locked is: MD5 staat standaard uit
	- MD5 activeren: ga naar %programfiles%\Azure AD Sync\Bin, open miiserver.exe.config, voeg in configuration/runtime node toe: <enforceFIPSPolicy enabled="false"/>, opslaan

- PingFederate (federation-optie)
	- Vereisten: PingFederate 8.4 of later; TLS/SSL certificaat voor de federation service name (bv. sts.contoso.com)
	- Setup: domain selecteren in Entra Connect -> Export Settings delen met PingFederate admin -> admin configureert server -> URL/poort teruggeven aan Entra Connect om metadata te verifiëren

---

### Implement manage pass-through authentication (PTA)
- Wat is het
	- Pass-through authentication laat users inloggen op zowel on-premises als cloud-apps met hetzelfde wachtwoord
	- Valideert wachtwoorden direct tegen on-premises Active Directory (geen sync van hashes)
- Inschakelen; eerste installatie
	- Custom installation path kiezen bij Entra Connect setup
	- Bij User sign-in page: Pass-through authentication selecteren als Sign On method
	- Na succesvolle installatie: PTA-agent geïnstalleerd op dezelfde server als Entra Connect; feature ingeschakeld op de tenant
- Inschakelen; al eerder geïnstalleerd (express of custom)
	- Change user sign-in task selecteren in Entra Connect -> Next
	- Pass-through authentication selecteren als sign-in method
	- Na succesvolle installatie: PTA-agent geïnstalleerd + feature ingeschakeld op de tenant
- Belangrijk
	- PTA is een tenant-level feature; inschakelen beïnvloedt sign-in voor alle users in alle managed domains van de tenant
	- Bij overstap van AD FS naar PTA: minimaal 12 uur wachten voordat je de AD FS infrastructuur uitschakelt, zodat users tijdens de overgang kunnen blijven inloggen op Exchange ActiveSync

---

### Explore pass-through authentication and seamless single sign-on (SSO)
- Wat is het
	- Seamless SSO logt users automatisch in vanaf hun netwerk-verbonden corporate desktop
	- Toegang tot cloud-apps zonder extra on-premises componenten
	- Kan gecombineerd worden met PHS of PTA; niet toepasbaar op AD FS

- Key benefits
	- Great user experience: automatisch ingelogd op zowel on-premises als cloud-apps; geen herhaaldelijk wachtwoord invoeren
	- Easy to deploy & administer: geen extra on-premises componenten nodig; werkt met zowel PHS als PTA; uitrolbaar via Group Policy naar (een deel van) users

- Sign-in flow op web browser
	- User probeert een web app te openen (bv. Outlook Web App) vanaf een domain-joined device binnen het corporate network
	- Niet al ingelogd -> redirect naar Microsoft Entra sign-in pagina
	- User voert username in
	- Entra ID daagt de browser uit (401 Unauthorized) om een Kerberos ticket te leveren
	- Browser vraagt ticket op bij Active Directory voor het AZUREADSSOACC computer account (representeert Entra ID)
	- AD vindt het computer account, geeft een Kerberos ticket terug, versleuteld met het secret van dat account
	- Browser stuurt het Kerberos ticket door naar Entra ID
	- Entra ID ontsleutelt het ticket (met de eerder gedeelde key), herkent de identity van de ingelogde user
	- Entra ID geeft een token terug aan de app, of vraagt extra bewijs (bv. MFA)
	- Bij succes: toegang tot de applicatie

- Sign-in flow op native client
	- User probeert een native app te openen (bv. Outlook client) vanaf een domain-joined device
	- Niet al ingelogd -> app haalt username op uit de Windows-sessie van het device
	- App stuurt username naar Entra ID, haalt het WS-Trust MEX endpoint van de tenant op (exclusief voor Seamless SSO)
	- App checkt via dat endpoint of integrated authentication beschikbaar is (ook exclusief voor Seamless SSO)
	- Bij succes: Kerberos challenge uitgevoerd
	- App haalt Kerberos ticket op, stuurt door naar Entra's integrated authentication endpoint
	- Entra ID ontsleutelt en valideert het ticket
	- Entra ID logt de user in, geeft een SAML token aan de app
	- App stuurt het SAML token door naar Entra ID's OAuth2 token endpoint
	- Entra ID valideert het SAML token, geeft access token, refresh token, en ID token aan de app
	- User krijgt toegang tot de resource van de app	


