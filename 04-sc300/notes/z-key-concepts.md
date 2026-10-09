# Key Concepts

Korte samenvatting van Entra ID-concepten die extra aandacht nodig hadden.

## Domain 1: Implement identities

### Hybrid authentication
- **PHS**: hash-sync, vertraging tot ±30 min (ook bij account disable)
- **PTA**: real-time validatie tegen on-prem DC via agent; dwingt AD-policies af (logon hours, disabled account)
- **Federation (AD FS)**: real-time validatie via on-prem STS
- **Seamless SSO**: autologon-URL via GPO in de Intranet Zone; vereist verbinding met een DC
- **PRT**: SSO onafhankelijk van locatie op joined/registered devices

### Device identity
- **Entra joined**: bedrijfsdevice, cloud-native
- **Hybrid joined**: in on-prem AD én Entra
- **Entra registered**: BYOD, alleen app-toegang

### Sync
- **Connect Sync**: OU's scopen via Synchronization Rules Editor (`cloudFiltered`); extra attributen via directory extensions
- **Cloud Sync**: scoping filters in de provisioning-configuratie; foutdetails in Provisioning Agent logs
- **Connect Health**: health-dashboard; Duplicate Attribute-rapport met self-service remediation
- **Password writeback**: wachtwoordwijziging in Entra (SSPR) terug naar on-prem AD

### Users en groepen
- Gebruikerstypen: cloud-only, directory-synced (wijzig op de bron), guest (B2B)
- Soft delete: 30 dagen terug te zetten
- Custom domain verifiëren: TXT- of MX-record
- Self-service sign-up uitzetten: `Set-MsolCompanySettings -AllowAdHocSubscriptions $false`
- Group-based licensing: alleen directe leden (nested groups erven niet)
- Dynamic groups: P1; aanmaken in Entra admin center en Intune admin center
- Administrative unit: gebruiker direct toevoegen om die te beheren; een groep in de AU geeft beheer over de groep en het lidmaatschap
- Self-service group management + Administrative Units voor delegatie

### Managed identity
- **System-assigned**: levenscyclus van de resource
- **User-assigned**: losstaand, deelbaar over meerdere resources (minste identities, stabiel bij rebuild/DR)
- Rotatie van credentials: automatisch

### Externe identiteiten
- Bulk invite CSV: `inviteeEmail` + `inviteRedirectUrl`
- Wie mag uitnodigen: External collaboration settings (Guest Inviter, User Administrator)
- WS-Fed claims: `ImmutableID` + `emailaddress`
- One-time passcode: externe gebruikers met consumer-mail zonder directory-account
- Reeds geaccepteerde invites blijven bestaan na een strengere domeinrestrictie

## Domain 2: Implement authentication and access management

### Conditional Access: als → dan
Elke policy is één zin: **als** [voorwaarde], **dan** [eis]. Eerst splitsen, dan wijst het kernwoord naar het onderdeel.

| Kernwoord | Onderdeel |
|---|---|
| **Voorwaarde (als)** | |
| buiten het netwerk, land, VPN | Conditions > Locations |
| BYOD, unmanaged, joined, hybrid joined | Conditions > Filter for devices (`trustType`) |
| gevoelige app(s) | Target resources (app, authentication context, filter for apps) |
| admins, guests, rollen | Users |
| gelekte credentials, risicovolle login | Conditions > User risk / Sign-in risk |
| legacy, oude protocollen | Conditions > Client apps |
| **Eis (dan)** | |
| MFA, compliant device, wachtwoordwijziging | Grant controls |
| FIDO2, phishing-resistant | Grant > Require authentication strength |
| blokkeren | Grant > Block access |
| elke X dagen opnieuw inloggen | Session > Sign-in frequency |
| geen downloads, web-only | Session > App enforced restrictions (SharePoint/Exchange) of Conditional Access App Control (andere apps, session policy) |

Vuistregel: waar, welk device, wie of welk risico = voorwaarde. "Moet" of "vereist" = eis. "Tijdens de sessie" = session control.

### Wie doet wat
- **Authentication Methods policy**: welke methoden bestaan (geen condities)
- **Authentication strength**: welke methoden een CA-policy accepteert; TAP via custom strength
- **Authentication context**: label op een resource; CA dwingt af (step-up)
- **Identity Protection**: detecteert risico
- **Intune compliance policy**: definieert "compliant"
- **Named location**: definitie van een plek (vervangt trusted IPs)
- **Break-glass accounts**: uitgesloten van CA, beveiligd met lang wachtwoord of FIDO2
- **STS**: geeft het token uit (Entra ID of AD FS)

### CA details
- Legacy auth blokkeren: Client apps = **Exchange ActiveSync clients + Other clients**, grant Block
- Groeiende lijst apps: Filter for apps op custom security attributes
- Security defaults aan: eerst uitzetten om CA te kunnen gebruiken
- MFA bij registreren buiten het netwerk: user action **Register security information** + Locations
- Workload identities (service principals): alleen **Block**, conditions locations en service principal risk, single-tenant
- Compliant network: Global Secure Access als locatieconditie

### Identity Protection
- **Sign-in risk** (omstandigheden van de login): MFA of Block
- **User risk** (account gecompromitteerd, o.a. leaked credentials): password change of Block
- Gemeenschappelijk in beide: **Block**
- MFA registration: eigen policy
- Retentie: Risk detections 90 dagen, Risky sign-ins 30 dagen
- Rollen: Security Operator (rapporten, dismiss, confirm compromise); policies configureren: Security Administrator of Global Administrator; Security Reader kan rapporten bekijken
- Anomalieën detecteren: Identity Protection en Sentinel UEBA

### MFA en SSPR

| Methode | SSPR | MFA | Passwordless |
|---|---|---|---|
| Authenticator (push) | ja | ja | ja |
| Authenticator/hardware (OTP), SMS, voice | ja | ja | nee |
| E-mail, security questions | ja | nee | nee |
| FIDO2, Windows Hello, CBA | nee | ja | ja |
| Temporary Access Pass | bootstrap | ja | ja |

- Primaire authenticatie (passwordless): FIDO2 passkey
- CBA high-affinity binding: `X509SKI`, `SHA1PublicKey`, `IssuerAndSerialNumber`
- Gedeelde desktops zonder mobiel: FIDO2 security keys
- Fraud alert: blokkeert automatisch na een als fraude gemelde MFA-prompt
- VPN/RADIUS/Wi-Fi met MFA: NPS extension
- Eerste stap bij risk-based CA: MFA voor alle gebruikers
- Key Vault met RBAC + access policy: effectieve rechten = unie van beide

## Domain 3: Implement access management for apps

### App registration en tokens
- Apps registreren bij "Users can register applications = No": **Application Developer**
- Owners van enterprise apps: users
- Enterprise application: SSO naar gallery-apps; App registration: eigen apps/API's
- Federation-SSO: **SAML, OpenID Connect, OAuth**

| Type | Flow | Scope |
|---|---|---|
| Delegated (namens gebruiker) | authorization code | `Mail.Read` (naam van de permission) |
| Application (zonder gebruiker) | client credentials | `https://graph.microsoft.com/.default` |

- Application permissions: altijd admin consent; `.default` combineer je niet met een losse scope
- Client credentials: app ID + **certificaat** (veiliger dan secret); managed identity nog beter
- Least privilege: minimale scopes (`User.Read`, alleen `.Read`) in de app registration
- High-privilege consent voorkomen: admin consent voor alle apps + goedkeuringsproces
- Secrets blokkeren, certificaten afdwingen: **app management policy**

### Extern en B2B
- **B2B Collaboration**: guest users; **B2B Direct Connect**: Teams shared channels
- Apps van een partner-tenant toestaan: Cross-tenant access settings met application allowlist
- Access package beperken tot één domein: access package policy + External collaboration settings

### Application Proxy
- Publiceert on-prem (legacy) webapps; connector maakt alleen uitgaande verbindingen
- Pre-authenticatie met Entra, dus CA en MFA mogelijk
- Eerste stap: Application Proxy deployen; custom domain via CNAME naar msappproxy.net
- Overzicht: RADIUS/VPN → NPS extension; interne webapp → Application Proxy; SAML-app → Enterprise application; OAuth/OIDC-app → App registration

### Defender for Cloud Apps
- **Cloud Discovery dashboard** vullen: logs uploaden (snapshot report) of continuous report (log collector, Defender for Endpoint)
- **App connector**: koppelt SaaS-apps via API
- **OAuth app policy** (app governance): waarschuwt bij riskante permissies
- **Session policy** (Conditional Access App Control): real-time acties blokkeren, bv. downloads

### Global Secure Access

| | Private Access | Internet Access |
|---|---|---|
| Voor | interne apps en servers | internet en SaaS |
| Vervangt | VPN | secure web gateway |
| Verbinding | connector in het netwerk | GSA-client op het device |

- Web content filtering (bv. gambling): filtering policy in een **security profile**, gekoppeld aan een CA-policy
- GSA-client: Windows Entra joined of hybrid joined; macOS registered via Company Portal
- Licentie: **Entra Suite** bevat beide (ook los te licentiëren)
- Joined = bedrijfsdevice; registered = persoonlijk device (BYOD)

### B2C
- Nieuw custom attribuut in de sign-up journey: **custom policy** (Identity Experience Framework)

## Domain 4: Plan and implement identity governance

### Entitlement management
- Partner-toegang: access package gekoppeld aan een **connected organization**
- Connected organization-login: federation of one-time passcode
- Externe gebruikers die nog niet in de tenant staan: **My Access portal link**
- Externe gebruikers automatisch verwijderen na inactiviteit: Identity Governance > Settings

### Access reviews
- Groups en apps: Entra ID Governance; Entra- en Azure-rollen: PIM (beide P2)
- Reviewers: member (zelf), manager (eigen team), fallback reviewer (bij afwezigheid)
- Terugkerend beoordelen: recurring access review met fallback reviewers
- Hoge turnover: dynamic group als reviewdoelgroep
- Terms of Use met jaarlijkse herbevestiging: meerdere ToU-policies met CA-targeting

### PIM
- **Eligible**: activeren wanneer nodig (MFA, approval, justification); **Active**: direct bruikbaar
- **Activation duration**: hoe lang een geactiveerde rol actief blijft (uren)
- **Request duration**: hoe lang een pending approval-aanvraag geldig blijft voordat die verloopt
- Geen permanente Global Admin: permanente toewijzing uitzetten in role settings
- Resource roles (bv. Key Vault): PIM for resource roles + Azure RBAC-rol via PIM
- JIT voor member/owner van een security group: **PIM for Groups**
- Instellingen beheren: Global Administrator of Privileged Role Administrator
- Audit: **Resource audit** (alle activiteit op een object); **My audit** (eigen acties)

### Monitoring en remediatie
- Entra-logs naar Log Analytics: diagnostic settings (P1/P2)
- Provisioning door third-party: tabel `AADProvisioningLogs`
- Licentiegeschiedenis: audit logs (Assign/Remove license)
- Sentinel incidents uit Identity Protection: eerst de Entra ID data connector
- Detectie = alert/Sentinel; automatische actie = analytics rule + playbook (Logic App)
- Alerts doorsturen: notification settings + Action Groups
- Alert op specifieke PIM-rollen: Azure Monitor alert rule op AuditLogs

### Lifecycle Workflows
- **Mover**: trigger op attribuutwijziging (bv. department), taken zoals toegang intrekken
- Inactieve guests: template "Offboard inactive guest users"
