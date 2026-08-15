# SC-300: Microsoft Identity and Access Administrator
## Learning Path 2: Implement an identity management solution using Microsoft Entra ID

  - **SC-300 Started:** 2 August, 2026
  - **SC-300 Exam passed:** 🔄

---

## Learning Path 1: Implement initial configuration of Microsoft Entra ID 
### Module 1: Configure company brand

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

### Module 2: Configure and manage Microsoft Entra roles

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

### Module 3: Exercise manage users roles
  - [04-sc300/labs/01-manage-users-roles](../../04-sc300/labs/01-manage-user-roles.md)
  - **Ook uitgevoerd in:** [Oceanic Airlines sandbox](../../00-sandbox/02-adding-first-user.md)



### Module 4: Configure delegation by using administrative units
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
  






















    
