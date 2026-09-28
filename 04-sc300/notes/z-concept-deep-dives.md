# Concept Deep-Dives

Verdiepende samenvattingen van Entra ID concepten die tijdens het oefenen naar boven kwamen als punten die extra aandacht nodig hadden.

## Domain 1: Implement identities

### Hybrid authentication methods - timing bij account disable
Wanneer een gebruiker disabled wordt in on-premises Active Directory, bepaalt de gekozen authentication method hoe snel dat effect heeft in Entra ID.

- Password Hash Synchronization (PHS): sync-cyclus, vertraging tot circa 30 minuten voordat de disable status doorkomt
- Pass-through Authentication (PTA): valideert elke sign-in real-time tegen een on-prem domain controller via de authentication agent; disable werkt direct door
- Federation (AD FS): valideert ook real-time tegen on-prem AD, zelfde direct effect als PTA
- Conditional Access, Password Protection en password writeback lossen dit niet op; het zijn geen authenticatie-methoden en hebben geen invloed op de sync-timing

Bron: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/whatis-hybrid-identity

### Seamless Single Sign-On (Seamless SSO)
Voor domain-joined Windows 10 clients: de Entra ID login URL (https://autologon.microsoftazuread-sso.com) moet worden toegevoegd aan de Intranet Zone via Group Policy, zodat Kerberos-tickets automatisch worden doorgegeven zonder credential-prompt. Dit is een browser/GPO-instelling, geen agent-installatie (die hoort bij PTA) en geen lokale sign-in optie.

### Password writeback
Synchroniseert wachtwoordwijzigingen die in Entra ID zijn gedaan (bijvoorbeeld via SSPR) terug naar on-premises AD DS. Vereist wanneer wachtwoorden consistent moeten blijven ongeacht waar de reset is uitgevoerd. Los van sync-timing voor account disable.

### Entra ID Domain Services - health notifications
Notificatie-instellingen voor gezondheidswaarschuwingen van een managed domain staan specifiek onder Entra ID Domain Services > Notification settings, niet onder de algemene Entra ID monitoring-sectie.

### Sync scoping via attribute filtering
Om specifieke gebruikers uit te sluiten van synchronisatie (bijvoorbeeld op basis van een custom attribuut) configureer je een inbound synchronization rule op de Active Directory Domain Services connector via de Synchronization Rules Editor, met een scoping filter op het attribuut en een transformation die het object als cloudFiltered markeert.

### Custom domain als primary domain instellen
Vaste volgorde: domeinnaam toevoegen, TXT-record aanmaken in DNS, domein verifieren, daarna pas instellen als primary domain.

## Domain 2: Implement authentication and access management

### Sign-in risk remediation zonder toegang te blokkeren
Eerste stap is altijd MFA voor alle gebruikers implementeren; dat is de basis waarop Identity Protection risk-based Conditional Access kan bouwen zonder gebruikers direct te blokkeren.

### Fraud alert vs Notifications vs Account lockout vs Block/unblock (MFA)
Vier instellingen die makkelijk door elkaar lopen:
- Notifications: stuurt alleen meldingen naar admins/gebruikers, geen actie
- Account lockout: beschermt tegen herhaalde foutieve inlogpogingen (brute force), geen relatie met fraude-meldingen
- Block/unblock users: handmatige actie door een admin
- Fraud alert: enige instelling die automatisch blokkeert wanneer een gebruiker een ongevraagde MFA-prompt meldt als fraude

### Conditional Access - waar hoort welke instelling
- Grant settings: de eisen om toegang te krijgen (MFA vereisen, compliant device vereisen)
- Session settings: wat er gebeurt tijdens de sessie (sign-in frequency, persistent browser sessions, app-enforced restrictions)
- Conditions: wanneer de policy van toepassing is (locatie, device platform, applicatie, tijd)
- Users and groups: op wie de policy van toepassing is

Sign-in frequency (opnieuw laten inloggen na X tijd) hoort dus bij Session settings, niet bij Grant of Conditions.

### App-enforced restrictions voor SharePoint Online
Om downloads/sync te blokkeren op user-owned (alleen Entra ID registered) devices zonder company-owned (Entra ID joined) devices te beperken: Conditional Access policy met session controls, specifiek "Use app enforced restrictions" ingeschakeld. Client apps conditions en Cloud App Security policies lossen dit niet fijnmazig genoeg op.

### Named locations vs trusted IPs
Voor MFA-uitzonderingen op basis van kantoorlocatie: named locations met een publiek IP-bereik (Conditional Access). Trusted IPs is een legacy MFA-instelling en wordt niet meer aanbevolen.

### Leaked credentials - self-remediation
Wanneer gebruikers zelf risico moeten kunnen oplossen (zonder helpdesk): een policy die toegang toestaat maar een wachtwoordwijziging vereist, in combinatie met SSPR en MFA voor self-service unblocking.

### NPS extension voor VPN MFA
Wanneer een VPN-server geen native Azure MFA ondersteunt: de NPS (Network Policy Server) extension for Azure MFA installeren. Valideert credentials tegen on-prem AD en triggert daarna Azure MFA. Application Proxy, Password Protection proxy en PTA proxy zijn hier geen van alle het juiste antwoord.

### MFA methode kiezen op basis van scenario-beperkingen
- Gedeelde desktops, geen mobiel toegestaan, geen biometrie → FIDO2 security keys
- Remote locatie zonder wifi/mobiel bereik maar laptop heeft internet → Microsoft Authenticator app werkt nog (code wordt offline gegenereerd, alleen de app zelf hoeft niet online te zijn op het moment van code genereren)
- Security questions worden nooit geaccepteerd als MFA-methode in Microsoft 365

### Security Operator rol (Identity Protection)
Kan: alle Identity Protection rapporten en de Overview bekijken, user risk dismissen, safe sign-in bevestigen, compromise bevestigen. Kan geen wachtwoorden resetten; dat vereist een andere rol.

## Domain 3: Implement access management for apps

### App registration - juiste rol toewijzen
Wanneer "Users can register applications" op No staat: Application Developer rol geeft precies genoeg rechten om apps te registreren (least privilege). Cloud Application Administrator is bedoeld voor het beheren van bestaande apps (service principals, consent, assignments), niet voor het registreren van nieuwe apps. Azure RBAC-rollen op subscription-niveau (Managed Application Contributor, App Configuration Data Owner) hebben geen invloed op Entra ID app-registratie.

### Wie mag wat rondom apps (default instellingen)
Standaard mogen alle gebruikers zelf apps registreren, tenzij dit expliciet is uitgezet. Het toewijzen van gebruikers aan een enterprise app (assignment) vereist wel een hogere rol: Global Administrator of Cloud Application Administrator.

### Web app met Microsoft Graph directory data laten lezen
Vaste volgorde: app registration aanmaken, app permissions toevoegen, admin consent verlenen.

### Enterprise application vs App registration
Voor SSO naar een gallery-app die OAuth ondersteunt gebruik je een Enterprise application (niet een nieuwe App registration); dat is de juiste blade voor het configureren van SSO naar een bestaande gallery-app.

### B2B bulk invite - verplichte parameters
Alleen twee velden zijn vereist: email address en redirection URL. Geen username, shared key of password; guest users authenticeren met hun eigen bestaande identity provider credentials.

### Waar kunnen B2B collaboration users toe worden uitgenodigd
Niet alleen een directory of group, ook direct een applicatie.

### External collaboration restrictions - allow/deny domeinen
Wanneer een guest user al toegang heeft geaccepteerd voordat een domain-restrictie werd aangescherpt, blijft die toegang bestaan (de restrictie werkt niet met terugwerkende kracht op reeds geaccepteerde invites). Herhaaldelijk terugkerend scenario: check altijd wanneer de toegang precies is geaccepteerd ten opzichte van wanneer de restrictie is ingesteld.

### Email one-time passcode (OTP) voor guests
Wordt alleen gebruikt voor externe gebruikers met een consumer email adres die geen bestaand directory account hebben (bijvoorbeeld Outlook.com zonder Entra ID). Guests van een federated/partner tenant met een eigen directory account loggen in met hun eigen organisatie-credentials. Member users binnen de eigen tenant krijgen nooit een OTP.

### Access packages met domein-restrictie combineren
Toegang tot een access package beperken tot gebruikers van 1 specifiek domein van een connected organization vereist een combinatie van: een access package policy in Identity Governance EN de External collaboration settings in Entra ID. Een van de twee alleen is niet voldoende.

### External Identities pricing op basis van Monthly Active Users (MAU)
Vereist het koppelen van een linked subscription aan de tenant; dat schakelt het MAU-gebaseerde prijsmodel in plaats van het per-gebruiker model.

## Domain 4: Plan and implement identity governance

### Access reviews - welke resources, welke licentie
- Groups en Apps: access reviews via Entra ID Governance (P2)
- Azure resource roles en Entra ID rollen: access reviews via Privileged Identity Management (eveneens P2)
Beide routes vereisen P2, maar het zijn verschillende features voor verschillende resource-typen.

### Access review reviewers correct instellen
- Reviewers = Member (self): gebruiker beoordeelt eigen toegang, geen manager-betrokkenheid
- Reviewers = Manager: elke manager krijgt de reviews van zijn eigen team
- Fallback reviewer: wordt alleen ingezet als de primaire reviewer niet beschikbaar is of geen manager heeft; maakt een manager dus niet automatisch de standaard-reviewer

  - fallback reviewer instellen lost het probleem van "verkeerde persoon krijgt alle reviews" niet op zolang de Reviewers-instelling zelf niet naar Manager staat.

### PIM - rolbeheer
Alleen Global Administrator of Privileged Role Administrator kunnen PIM-instellingen (zoals activation duration) voor een rol beheren. Activation duration wordt gemeten in uren, nooit in dagen of maanden; permanente toewijzing gaat in tegen het hele idee van PIM (eligible + activatie vereist).

### Sentinel integratie met Identity Protection
Om Sentinel incidents te laten genereren op basis van Identity Protection risk alerts: eerst een Sentinel data connector toevoegen voor Entra ID. Notify-instellingen en diagnostics settings zijn hier niet de eerste stap.

### Audit vereisten met Log Analytics
Om administratieve acties in Entra ID te laten wegschrijven naar een Log Analytics workspace: Diagnostics settings configureren in Entra ID.

### Sign-in logs retentie
Sign-in logs worden 30 dagen bewaard in Entra ID (zonder aanvullende export naar Log Analytics of een SIEM).

### Tijdelijke toegang voor externe partners
Voor tijdgebonden toegang (bijvoorbeeld 90 dagen) van partner-gebruikers tot een resource: access package via entitlement management, gekoppeld aan een connected organization voor die partner.
