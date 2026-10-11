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
