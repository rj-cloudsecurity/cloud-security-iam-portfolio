# SC-300: Microsoft Identity and Access Administrator

## Learning Path 2: Implement an identity management solution using Microsoft Entra ID
### Module 1: Implement initial configuration of Microsoft Entra ID 

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
  



























