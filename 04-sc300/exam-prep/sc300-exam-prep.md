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
