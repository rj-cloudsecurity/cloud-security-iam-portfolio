# SC-300 Quick Reference

## Kernwoord → welke tool

| Kernwoord | Tool |
|---|---|
| locatie/device/app/gebruiker + MFA, blokkeren of opnieuw inloggen | Conditional Access |
| welke methoden beschikbaar zijn voor een groep | Authentication Methods policy |
| phishing-resistant alleen voor admins of buiten het netwerk | Conditional Access + authentication strength |
| risico detecteren, wachtwoordwijziging bij leaked credentials | Identity Protection (risk policy) |
| definiëren wat "compliant" is | Intune compliance policy |
| wie of welk platform zich mag registreren | Intune enrollment restrictions |
| wie gasten mag uitnodigen | External collaboration settings |
| welke apps een partner-tenant mag openen | Cross-tenant access settings |
| rol tijdelijk of op aanvraag (JIT) | PIM |
| periodiek controleren wie nog toegang nodig heeft | Access reviews |
| toegang aanvragen/goedkeuren als bundel, partner-toegang | Entitlement management (access package) |
| downloads blokkeren in een third-party app | Conditional Access App Control (session policy) |
| gebruiker zelf wachtwoord resetten | SSPR |
| VPN/RADIUS/Wi-Fi met MFA | NPS extension |
| on-prem (legacy) webapp publiceren | Application Proxy |
| service principal beperken op locatie of risico | Conditional Access voor workload identities (alleen Block) |
| secrets blokkeren, certificaten afdwingen | App management policy |
| inactieve guests opruimen, afdeling gewijzigd (mover) | Lifecycle Workflows |
| detecteren, alerts, automatisch reageren op logs | Sentinel (analytics rule + playbook) |
| shadow IT, welke apps gebruikt men | Cloud Discovery (Defender for Cloud Apps) |
| interne apps zonder VPN | Global Secure Access: Private Access |
| internet/SaaS-verkeer filteren | Global Secure Access: Internet Access |

## Entra-rollen

| Rol | Wat |
|---|---|
| Global Administrator | alles in Entra ID |
| Privileged Role Administrator | rollen toewijzen, PIM beheren |
| User Administrator | gebruikers en groepen beheren |
| Helpdesk Administrator | wachtwoorden resetten van non-admins |
| Password Administrator | wachtwoorden resetten (non-admins) |
| Authentication Administrator | auth-methoden en MFA van gebruikers beheren |
| Authentication Policy Administrator | Authentication Methods policy en SSPR configureren |
| Conditional Access Administrator | Conditional Access policies beheren |
| Security Administrator | security-instellingen en -policies |
| Security Operator | security events beheren, user risk dismissen |
| Security Reader | security data lezen |
| Application Administrator | apps beheren, inclusief Application Proxy |
| Cloud Application Administrator | apps beheren, zonder Application Proxy |
| Application Developer | app registrations aanmaken (ook als gebruikers dat niet mogen) |
| Guest Inviter | gasten uitnodigen |
| License Administrator | licenties toewijzen |
| Hybrid Identity Administrator | Connect Sync en Cloud Sync beheren |
| Identity Governance Administrator | entitlement management en access reviews |

## Licenties

| Licentie | Bevat o.a. |
|---|---|
| Entra ID Free | security defaults, basis-SSO |
| Entra ID P1 | Conditional Access, dynamic groups, group-based licensing, SSPR met writeback, Application Proxy |
| Entra ID P2 | alles van P1 + Identity Protection, PIM, access reviews, entitlement management |
| Workload ID Premium | Conditional Access voor workload identities |
| Entra Suite | Private Access, Internet Access, ID Governance, ID Protection (ook los te licentiëren) |

## Getallen

| Wat | Waarde |
|---|---|
| Verwijderde gebruiker terugzetten | 30 dagen |
| Risk detections-rapport | 90 dagen |
| Risky sign-ins-rapport | 30 dagen |
| Sign-in en audit logs (P1/P2) | 30 dagen |
| PHS sync-vertraging | ±30 minuten |
| PIM activation duration | uren |

## Verwarringspaar

| X | Y |
|---|---|
| Sign-in risk: één login verdacht, oplossing MFA | User risk: account gecompromitteerd, oplossing wachtwoordwijziging |
| Block access: in beide risk policies | MFA: alleen sign-in risk; password change: alleen user risk |
| Resource audit: alle PIM-activiteit op een object | My audit: alleen eigen acties |
| Eligible: eerst activeren | Active: direct bruikbaar |
| Activation duration: hoe lang de rol actief blijft | Request duration: hoe lang een pending aanvraag geldig blijft |
| B2B Collaboration: guest-account in jouw tenant | B2B Direct Connect: Teams shared channels, geen guest-account |
| Private Access: interne apps, vervangt VPN | Internet Access: secure web gateway |
| Delegated: namens gebruiker, scope = `Mail.Read` | Application: zonder gebruiker, scope = `.default` |
| System-assigned: leeft en sterft met de resource | User-assigned: losstaand, deelbaar over resources |
| Enterprise application: SSO naar bestaande apps | App registration: eigen apps en API's |
| Authentication Methods policy: welke methoden bestaan | Authentication strength: welke methoden CA accepteert |
| Connect Sync: Synchronization Rules Editor | Cloud Sync: scoping filters in de configuratie |
| Entra joined: bedrijfsdevice, cloud-native | Entra registered: BYOD, alleen app-toegang |
| Hybrid joined: in AD én Entra | PRT: SSO onafhankelijk van locatie |
| PTA: real-time, dwingt AD-policies af | PHS: hash-sync, sync-vertraging |
| Snapshot report: eenmalig log uploaden | Continuous report: log collector of Defender for Endpoint |
| App connector: SaaS via API | Session policy: real-time acties blokkeren |
