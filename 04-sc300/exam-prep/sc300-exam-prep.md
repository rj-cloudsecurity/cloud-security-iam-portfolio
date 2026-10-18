# SC-300 Exam Preparation

## Certification
  - Microsoft Certified: Identity and Access Administrator Associate (SC-300)
  - Result: In preparation
  - Date:

## Study Method
  - Completing all Microsoft Learn modules
  - Creating detailed notes in [Key Concepts](/04-sc300/notes/)
  - Practicing with custom AI-generated exams (claude.ai) based on official SC-300 exam objectives
  - Practicing with the Official Microsoft Practice Assessment
  - Practicing with Tutorials Dojo practice exams
  - Redoing every mistake hands-on in the portal to see the correct configuration and where it is located in [Hands-on Review](/04-sc300/exam-prep/sc300-hands-on-review.md)

## Domains
  - Domain 1 — Implement and manage user identities
  - Domain 2 — Implement authentication and access management
  - Domain 3 — Plan and implement workload identities
  - Domain 4 — Plan and automate identity governance

## Practice Assessment Progression
| Platform | Score | Notes |
|----------|-------|-------|
| Test 1 — Official Microsoft Practice Assessment 1 | 54% | 27/50. Weakest: D1 (administrative units, dynamic groups, WS-Fed, PTA vs PHS), D2 (Identity Protection, CBA, Global Secure Access), D3 (App Proxy, scope, Cloud Discovery), D4 (entitlement management, PIM for Groups, audit logs). |
| Test 2 — Custom Exam Domain 1 | 85% | 17/20. Fouten: B2B direct connect vs collaboration, licentie voor dynamic groups (P1), directory extensions voor custom attributen. |
| Test 3 — Custom Exam Domain 2 | 80% | 16/20. Fouten: security defaults blokkeren Conditional Access, MFA fraud alert (automatisch blokkeren), Global Secure Access compliant network, Identity Protection vereist P2. |
| Test 4 — Custom Exam Domain 3 | 70% | 14/20. Fouten: Enterprise applications vs App registrations, delegated vs application permissions, client credentials flow, snapshot report vs app connector, federated identity credential (GitHub Actions), Application Developer rol. |
| Test 5 — Custom Exam Domain 4 | 95% | 19/20. Fout: Lifecycle Workflows vereist Entra ID Governance. |
| Test 6 — Custom Exam Mixed Domains | 80% | 24/30. Fouten: App registrations vs Enterprise applications, Lifecycle Workflows-licentie, B2B collaboration vs direct connect, Application Proxy-connectiviteit, compliant network vs compliant device, Sentinel data connector + analytics rule. |
| Test 7 — Tutorials Dojo Practice Exam 1 | 55% | 26/50 vragen (31/56 punten). D1 50%, D2 59%, D3 86%, D4 44%. Fouten: PowerShell-cmdlets (licenties, sign-up, uitnodigingen), Connect Sync inbound rules, entitlement management settings en access packages, access reviews, Defender for Cloud Apps-policies, admin consent, SCIM. |

## Next Focus Areas after Test 1

**Domain 1 — Implement and manage user identities**
  - Administrative units: een groep in de AU geeft beheer over de groep en het lidmaatschap, niet over de leden; een gebruiker die zelf in de AU zit kun je wel beheren
  - Dynamic groups: aanmaken in het Entra admin center en het Intune admin center, niet in het Microsoft 365 admin center
  - WS-Fed federation: vereiste claims in het token zijn ImmutableID en emailaddress
  - PTA vs PHS: PTA dwingt user-level AD-policies af, PHS niet
  - Connect Health: Duplicate Attribute-rapport voor sync-fouten met self-service remediation

**Domain 2 — Implement authentication and access management**
  - Certificate-based authentication: high-affinity bindings zijn X509SKI, SHA1PublicKey en IssuerAndSerialNumber
  - Identity Protection: Block access is de enige controle die in zowel de sign-in risk als de user risk policy zit
  - Risk detections-rapport bewaart 90 dagen, Risky sign-ins 30 dagen
  - Global Secure Access: web content filtering (bijv. gambling) = security profile gekoppeld aan een Conditional Access policy
  - Global Secure Access client: Windows moet Entra joined of hybrid joined zijn, macOS mag registered zijn via Company Portal
  - Licentie: Private Access én Internet Access samen = Microsoft Entra Suite

**Domain 3 — Plan and implement workload identities**
  - Federation-SSO methoden: SAML, OpenID Connect en OAuth
  - Legacy on-prem webapp publiceren met MFA: eerste stap is Application Proxy
  - Scope bij application permissions: `https://graph.microsoft.com/.default`
  - Apps registreren bij "Users can register applications = No": Application Developer
  - Cloud Discovery dashboard vullen: snapshot report (log upload), geen app connector
  - Downloads blokkeren op unmanaged devices in third-party apps: Conditional Access App Control (session policy)

**Domain 4 — Plan and automate identity governance**
  - Connected organization: federation en one-time passcode als authenticatiemethoden
  - Externe gebruikers die nog niet in de tenant staan: toegang aanvragen via een My Access portal-link
  - Just-in-time toegang voor member/owner van een security group: PIM for Groups
  - Alle PIM-activiteit voor een groep: Resource audit; My audit toont alleen eigen acties
  - Entra-logs naar Azure Monitor vereist een Entra ID P1- of P2-licentie

## Next Focus Areas after Test 2
  - Domain 1 — B2B direct connect = Teams shared channels zonder guest-account; B2B collaboration = guest users
  - Domain 1 — Dynamic groups vereisen Entra ID P1; de Intune admin center is een portal, geen licentie
  - Domain 1 — Custom attribuut uit on-prem AD naar Entra synchroniseren: directory extensions (cloudFiltered is een uitsluit-markering, geen sync)

## Next Focus Areas after Test 3
  - Domain 2 — Security defaults staan standaard aan in een nieuwe tenant en blokkeren Conditional Access; eerst uitzetten, ook met P1
  - Domain 2 — Fraud alert: gebruiker meldt een ongevraagde MFA-prompt; optie "Automatically block users who report fraud" blokkeert het account
  - Domain 2 — Global Secure Access: Compliant network (onder Conditions > Locations) herkent verkeer via GSA; een named location met IP-ranges kan dat niet
  - Domain 2 — Identity Protection (sign-in en user risk policies) vereist Entra ID P2; P1 geeft alleen Conditional Access
  - Domain 2 — PTA smart lockout: Entra-drempel lager dan AD-drempel, zodat Entra eerder blokkeert dan AD

## Next Focus Areas after Test 4
  - Domain 3 — SSO (SAML) configureer je in Enterprise applications; App registrations is voor eigen apps en API's
  - Domain 3 — Delegated permissions: namens een ingelogde gebruiker; application permissions: zonder gebruiker, altijd admin consent
  - Domain 3 — Daemon zonder gebruiker: client credentials flow; met gebruiker: authorization code flow
  - Domain 3 — Cloud Discovery: snapshot report = eenmalig logbestand uploaden; continuous report = automatisch; app connector = SaaS-app via API koppelen
  - Domain 3 — Workload identity federation (bijv. GitHub Actions zonder secrets): federated identity credential op de app registration; managed identities bestaan alleen voor Azure-resources
  - Domain 3 — Apps registreren bij "Users can register applications = No": Application Developer (least privilege)
  - Domain 3 — Consent: user consent instellen via verified publishers + selected permissions; admin consent workflow voor aanvragen

## Next Focus Areas after Test 5
  - Domain 4 — Lifecycle Workflows vereist Microsoft Entra ID Governance (of Entra Suite); Workload ID Premium is alleen voor workload identities

## Next Focus Areas after Test 6
  - Domain 3 — App registrations: eigen app of API (app roles, API scopes, secrets); Enterprise applications: SSO, toewijzing en Conditional Access voor een bestaande app
  - Domain 4 — Lifecycle Workflows (joiner, mover, leaver) vereisen Microsoft Entra ID Governance, niet P2
  - Domain 1 — B2B collaboration: guest-object in de directory (SharePoint, apps, bestanden); B2B direct connect: alleen Teams shared channels, geen object
  - Domain 3 — Application Proxy connector: alleen uitgaand verkeer op poort 80 en 443, geen inkomende poorten
  - Domain 2 — Compliant network (Conditions > Locations, vereist CA-signalering in Global Secure Access) controleert het verkeer; compliant device (Intune) controleert het apparaat
  - Domain 4 — Sentinel-detectie: data connector voor de logs plus een scheduled analytics rule; playbook is alleen de reactie

## Next Focus Areas after Test 7

**Domain 1 — Implement and manage user identities**
  - Group-based licensing: nieuwe licentie aan de groep toewijzen en oude verwijderen met `Set-MgGroupLicense`; directe licenties in bulk verwijderen via de Licenses blade
  - Self-service sign-up beperken tot verified SMTP-domeinen: `Set-MsolCompanySettings`
  - Gast uitnodigen met PowerShell: `New-AzureADMSInvitation`
  - Connect Sync: gebruikers uitsluiten op attribuutwaarde (bijv. extensionAttribute15 = NoSync): inbound synchronization rule op de AD DS connector
  - Verwijderde gebruiker herstellen: binnen 30 dagen, minimale rol User Administrator
  - Password Administrator kan alleen wachtwoorden resetten binnen de scope waarop de rol is toegewezen (organisatie of administrative unit)
  - SCIM 2.0: standaard voor automatische provisioning naar SaaS-apps; SAML, OIDC en OAuth zijn voor sign-in en autorisatie

**Domain 2 — Implement authentication and access management**
  - PTA dwingt on-prem account lockout af bij cloud sign-ins; smart lockout doet dat niet
  - SSPR met 1 vereiste methode: mobile app code (de notificatie werkt alleen als 2 methoden nodig zijn)
  - Legacy authentication blokkeren: Conditional Access, condition Client apps
  - SSO via Enterprise application; toegang beperken tot Entra-joined devices via een Conditional Access policy

**Domain 3 — Plan and implement workload identities**
  - Defender for Cloud Apps session control voor een third-party SaaS-app: eerste stap is SSO instellen in het Entra admin center
  - Activity policy: alerts bij risicovolle acties in SaaS-apps (mass downloads, herhaalde verwijderingen); session policy: real-time controle
  - App governance dashboard: rol Cloud Application Administrator, via het Microsoft Defender portal
  - Daemon-app naar Graph: app registreren, Graph permissions toewijzen, tenant-wide admin consent geven
  - App in tenant A naar app in tenant B: certificate of secret; managed identity werkt niet over tenants
  - Admin consent requests kan alleen een aangewezen reviewer goedkeuren die ook een rol met consent-rechten heeft (bijv. Cloud Application Administrator)
  - Apps registreren bij "Users can register applications = No": Application Developer

**Domain 4 — Plan and automate identity governance**
  - Entitlement management settings: externe gebruikers automatisch laten verwijderen na een periode (bijv. 90 dagen)
  - Tijdelijke toegang tot groep en SharePoint-site (bijv. 90 dagen): access package met expiration in de policy
  - Periodieke review van gasttoegang die via een groep loopt: access review van die groep
  - Entra audit logs naar Azure Monitor: diagnostic settings naar een Log Analytics workspace
