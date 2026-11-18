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
| regels voor één partner-organisatie | Cross-tenant access > Organizational settings |
| Teams shared channels met partner, geen guest-account | B2B Direct Connect (beide tenants) + inbound MFA trust |
| rol tijdelijk of op aanvraag (JIT) | PIM |
| JIT voor member of owner van een groep | PIM > Groups (assigned security- of Microsoft 365-groep) |
| periodiek controleren wie nog toegang nodig heeft | Access reviews |
| gasttoegang regelmatig controleren, minste beheerlast | recurring access review (met auto-apply) |
| toegang aanvragen/goedkeuren als bundel, partner-toegang | Entitlement management (access package) |
| externe gebruiker nog niet in de tenant vraagt access package aan | My Access portal link |
| downloads blokkeren in een third-party app | Conditional Access App Control (session policy) |
| gebruiker zelf wachtwoord resetten | SSPR |
| gebruiker meldt een MFA-prompt die niet van hem is, account automatisch blokkeren | Fraud alert (Block user when fraud is reported) |
| VPN/RADIUS/Wi-Fi met MFA | NPS extension |
| on-prem (legacy) webapp publiceren | Application Proxy |
| service principal beperken op locatie of risico | Conditional Access voor workload identities (alleen Block) |
| secrets blokkeren, certificaten afdwingen | App management policy |
| inactieve guests opruimen, afdeling gewijzigd (mover) | Lifecycle Workflows |
| detecteren, alerts, automatisch reageren op logs | Sentinel (analytics rule + playbook) |
| shadow IT, welke apps gebruikt men | Cloud Discovery (Defender for Cloud Apps) |
| interne apps zonder VPN | Global Secure Access: Private Access |
| internet/SaaS-verkeer filteren | Global Secure Access: Internet Access |
| extra authenticatie voor één gevoelige actie | Authentication context → CA policy op die context → context aan protected action koppelen |
| noodtoegang-account | andere (phishing-resistant) MFA-methode, uitgesloten van CA, alerts op activiteit |
| MFA voor Azure-beheer | CA template "Require MFA for Azure management" (sluit de maker van de policy uit) |
| welke detecties veroorzaakten een flagged sign-in | Risk detections-rapport |
| Windows Hello for Business bij hybrid tenant | Hybrid Entra join + cloud Kerberos trust |
| leaked credentials-rapport en sign-in disaster recovery | PHS (federation + PHS als AD DS ook valideert) |
| certificate-based authentication | on-prem CA toevoegen aan de Entra tenant |
| Entra Connect: attribuut-filter voor beide forests, bestaande objecten | Inbound attribute-based filtering + full synchronization |
| Connect Health: orphaned of dubbele objecten herstellen | Duplicate Attribute-rapport (Diagnose-kolom) |
| Sentinel koppelen aan een bron | data connector |
| Entra-logs naar Log Analytics | diagnostic settings |

## Entra-rollen

| Rol | Wat |
|---|---|
| Global Administrator | alles in Entra ID |
| Global Reader | alles lezen |
| Privileged Role Administrator | Entra-rollen toewijzen, PIM beheren, admin consent voor Graph application permissions |
| User Administrator | gebruikers en groepen beheren |
| Helpdesk Administrator | wachtwoorden resetten van non-admins |
| Password Administrator | wachtwoorden resetten (non-admins) |
| Authentication Administrator | auth-methoden en MFA van gebruikers beheren |
| Authentication Policy Administrator | Authentication Methods policy en SSPR configureren |
| Conditional Access Administrator | Conditional Access policies beheren |
| Security Administrator | security-instellingen en -policies |
| Security Operator | security events beheren, user risk dismissen, confirm safe sign-in |
| Security Reader | security data lezen |
| Report Reader | audit logs en sign-in logs lezen |
| Compliance Administrator | Defender for Cloud Apps: alerts, file policies, reports onder Data Management |
| Application Administrator | apps beheren, inclusief Application Proxy |
| Cloud Application Administrator | apps beheren, zonder Application Proxy; App governance-dashboard in het Defender-portaal |
| Application Developer | app registrations aanmaken (ook als gebruikers dat niet mogen) |
| Guest Inviter | gasten uitnodigen |
| License Administrator | licenties toewijzen |
| Billing Administrator | facturatie en abonnementen |
| Hybrid Identity Administrator | Connect Sync en Cloud Sync beheren |
| Identity Governance Administrator | entitlement management en access reviews |

## Azure-rollen (RBAC)

| Rol | Wat |
|---|---|
| Owner | alles op de resource, inclusief roltoewijzing |
| User Access Administrator | roltoewijzingen op Azure-resources, ook voor PIM van Azure resource roles (least privilege) |
| Contributor | resources beheren, geen roltoewijzing |
| Key Vault Administrator, Key Vault Secrets User | secrets lezen (Azure RBAC-model, scope telt) |
| Key Vault Reader | alleen metadata |

## Licenties

| Licentie | Bevat o.a. |
|---|---|
| Entra ID Free | security defaults, basis-SSO |
| Entra ID P1 | Conditional Access, dynamic groups, group-based licensing, SSPR met writeback, Application Proxy |
| Entra ID P2 | alles van P1 + Identity Protection, PIM, access reviews, entitlement management |
| Workload ID Premium | Conditional Access voor workload identities |
| Entra Suite | Private Access, Internet Access, ID Governance, ID Protection (ook los te licentiëren) |
| Entra-workbooks in Azure Monitor | P1 of P2 + Report Reader |

## Getallen

| Wat | Waarde |
|---|---|
| Verwijderde gebruiker terugzetten | 30 dagen |
| Risk detections-rapport | 90 dagen |
| Risky sign-ins-rapport | 30 dagen (P1), 90 dagen (P2) |
| Sign-in en audit logs (P1/P2) | 30 dagen |
| PHS sync-vertraging | ±30 minuten |
| PIM activation duration | uren |
| Bulk invite CSV | rij 1 versienummer, rij 2 kolomkoppen |
| User risk policy met minste onderbrekingen | niveau High |

## Defender for Cloud Apps: policy types

| Policy | Wat |
|---|---|
| Access policy | toegang van een gebruiker blokkeren |
| Session policy | acties in een sessie beperken (bijv. download) |
| Activity policy | alert bij drempel (bijv. massa-downloads) |
| OAuth app policy | alert als meer dan N gebruikers een app met verhoogde rechten autoriseren |
| App discovery policy | alert op nieuw ontdekte app, met categorie, risico en aantal gebruikers |
| Unsanctioned | app blokkeren voor iedereen |
| Cloud app catalog | app risk score en MFA-ondersteuning |

Eerste stap voor session control: staat de app al in Entra (bijv. SharePoint Online, of toegewezen via Entra), dan CA policy met Session > Use Conditional Access App Control. Een nieuwe SaaS-app krijgt eerst SSO.

## Workload identities

| Wat | Keuze |
|---|---|
| Identity verdwijnt mee met de resource | system-assigned managed identity |
| Identity gedeeld over meerdere resources | user-assigned managed identity |
| VM krijgt toegang tot storage | Identity aanzetten in de VM-blade, daarna rol geven op de storage |
| Managed identity van een VM verwijderen | `Update-AzVM` |
| Multitenant app, rechten per klanttenant | service principal per tenant |
| Server-app met redirect-URI | platform Web |
| Browser-app (JavaScript) | platform SPA |
| App op het apparaat van de gebruiker | platform Mobile and desktop |
| Daemon zonder wachtwoord opslaan | certificate |
| Daemon die Graph aanroept | app registration → application permissions → admin consent |
| Namens gebruiker met `Mail.Read` | app registration → delegated permissions → admin consent |

## Verwarringspaar

| X | Y |
|---|---|
| Sign-in risk: één login verdacht, oplossing MFA | User risk: account gecompromitteerd, oplossing wachtwoordwijziging |
| Block access: in beide risk policies | MFA: alleen sign-in risk; password change: alleen user risk |
| Risk detections: welke detecties een flag veroorzaakten | Risky sign-ins: welke sign-ins gemarkeerd zijn; Risky users: risico per gebruiker |
| Account lockout: tijdelijk blok na mislukte pogingen | Fraud alert: gebruiker meldt prompt, blok tot de beheerder het opheft |
| Resource audit: alle PIM-activiteit op een object | My audit: alleen eigen acties |
| Eligible: eerst activeren | Active: direct bruikbaar |
| Activation duration: hoe lang de rol actief blijft | Request duration: hoe lang een pending aanvraag geldig blijft |
| PIM for Groups: Member en Owner hebben eigen role settings | PIM Azure resource roles: Owner of User Access Administrator nodig |
| B2B Collaboration: guest-account in jouw tenant | B2B Direct Connect: Teams shared channels, geen guest-account |
| Organizational settings: regels per partner | Default settings: voor alle externe organisaties |
| Private Access: interne apps, vervangt VPN | Internet Access: secure web gateway |
| Delegated: namens gebruiker, scope = `Mail.Read` | Application: zonder gebruiker, scope = `.default` (nooit samen met `Mail.Read`) |
| System-assigned: leeft en sterft met de resource | User-assigned: losstaand, deelbaar over resources |
| Enterprise application: SSO naar bestaande apps | App registration: eigen apps en API's |
| Application object: één keer, in de thuistenant | Service principal: per tenant waar de app draait |
| Authentication Methods policy: welke methoden bestaan | Authentication strength: welke methoden CA accepteert (vervangt Require MFA) |
| Connect Sync: Synchronization Rules Editor, inbound filtering | Cloud Sync: scoping filters in de configuratie |
| Entra joined: Windows-bedrijfsdevice, cloud-native | Entra registered: BYOD en Android/Linux, alleen app-toegang |
| Hybrid joined: in AD én Entra | PRT: SSO onafhankelijk van locatie |
| PTA: real-time, dwingt AD-policies af | PHS: hash-sync, sync-vertraging |
| Snapshot report: eenmalig log uploaden | Continuous report: log collector of Defender for Endpoint |
| App connector: SaaS via API | Session policy: real-time acties blokkeren |
| Groep in een administrative unit: groep beheren | Gebruiker in een administrative unit: gebruiker beheren (lid van de AU zelf) |
| Entra-rol (Privileged Role Administrator): directory | Azure-rol (User Access Administrator): Azure-resources |
