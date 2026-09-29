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

### Drie soorten gebruikers in Entra ID
Een steeds terugkerend onderscheid dat nodig is om provisioning-vragen goed te lezen:
- Cloud-only user: alleen aangemaakt in Entra ID, geen on-prem bron
- Directory-synced user: bron is on-premises AD, komt via Entra Connect (of Cloud Sync) binnen; wijzigingen horen op de bron plaats te vinden, niet direct in Entra ID
- Guest (B2B) user: externe identiteit, geauthenticeerd via de eigen identity provider van de gast

Vuistregel bij scenario-vragen: kijk eerst naar waar het account origineel vandaan komt voordat je bepaalt welke beheeractie (bijv. wachtwoord resetten, attribuut wijzigen) uberhaupt mogelijk is.

### Zelfregistratie van gebruikers blokkeren (Set-MsolCompanySettings)
Om te voorkomen dat gebruikers zelf een Entra ID tenant of resource kunnen aanmaken via self-service sign-up (bijvoorbeeld via een consumer Microsoft 365-aanmelding), gebruik je de PowerShell-cmdlet `Set-MsolCompanySettings -AllowAdHocSubscriptions $false`. Dit is een tenant-brede instelling en geen Conditional Access policy of external collaboration setting.

### Guest user aanmaken via PowerShell
`New-AzureADMSInvitation` is het PowerShell-equivalent van het handmatig uitnodigen van een B2B guest user via de portal ("Invite external user" / "Create guest user account"). Beide methoden resulteren in hetzelfde onderliggende concept: een guest-object dat authenticeert met de eigen credentials van de externe gebruiker; de kern is steeds dezelfde B2B-invitation flow, ongeacht of dit via de portal, PowerShell of een bulk-invite wordt gedaan.

### Group-based licensing en nested groups
Licenties die via group-based licensing aan een groep zijn gekoppeld, worden alleen toegekend aan de directe leden van die groep. Geneste groepen (een groep als lid van een andere groep) erven de licentie niet door naar hun eigen leden. Voor een gebruiker die licentie moet krijgen via een nested group, moet die gebruiker dus direct lid zijn van de groep waaraan de licentie is gekoppeld, of de licentie moet los aan de bovenliggende groep(en) zelf worden gekoppeld.

Bron: https://learn.microsoft.com/en-us/entra/identity/users/licensing-groups-assign

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

### SSPR vs MFA - welke authenticatiemethode hoort waar
Een terugkerende valkuil: niet elke authenticatiemethode werkt voor zowel SSPR als MFA.

| Methode | SSPR | MFA | Passwordless sign-in |
|---|---|---|---|
| Microsoft Authenticator app (push notification) | Ja | Ja | Ja |
| Microsoft Authenticator app / hardware token (OTP code) | Ja | Ja | Nee |
| SMS | Ja | Ja | Nee |
| Voice call | Ja | Ja | Nee |
| Email adres | Ja (alleen SSPR) | Nee | Nee |
| Security questions | Ja (alleen SSPR) | Nee | Nee |
| FIDO2 security key | Nee | Ja | Ja |
| Windows Hello for Business | Nee | Ja | Ja |
| Certificate-based authentication | Nee | Ja | Ja |
| Temporary Access Pass | Nee (bootstrap-methode) | Ja | Ja |

Vuistregel: email en security questions bestaan uitsluitend voor SSPR, nooit voor MFA. FIDO2, Windows Hello en certificate-based authentication zijn uitsluitend voor sterke/passwordless sign-in en MFA, nooit voor SSPR. Authenticator app (zowel push als code), SMS en voice call werken voor beide.

Bron: https://learn.microsoft.com/en-us/entra/identity/authentication/concept-sspr-howitworks

### Security Operator rol (Identity Protection)
Kan: alle Identity Protection rapporten en de Overview bekijken, user risk dismissen, safe sign-in bevestigen, compromise bevestigen. Kan geen wachtwoorden resetten; dat vereist een andere rol.

### Authentication Strengths vs device-based controls
Authentication Strengths (binnen Conditional Access) laat je per policy afdwingen welke specifieke authenticatiemethoden geaccepteerd worden, bijvoorbeeld "alleen phishing-resistant methoden zoals FIDO2" voor admins, terwijl andere gebruikers een bredere set methoden (waaronder wachtwoord) mogen blijven gebruiken. Dit is een eigenschap van de authenticatiemethode van de gebruiker, niet van het device. Hybrid Entra ID Join is een eigenschap van het device (gekoppeld aan zowel on-prem AD als Entra ID) en heeft geen invloed op welke authenticatiemethode geaccepteerd wordt. Vuistregel: gaat de vraag over WIE inlogt en HOE → Authentication methods/strengths; gaat de vraag over WELK apparaat gebruikt wordt → device compliance/join status (Intune, Hybrid Join).

### Legacy authentication blokkeren via Conditional Access
Om verouderde authenticatieprotocollen (die geen MFA ondersteunen, zoals oudere mailprotocollen) te blokkeren: een Conditional Access policy met als conditie "Client apps" ingesteld op "Other clients" (legacy authentication), met als grant control "Block access". Dit is de aanbevolen route sinds Security Defaults en losse protocol-instellingen in Exchange Online minder fijnmazig zijn.

### Identity Protection: welke rol voor welke taak
Twee taken die vaak door elkaar worden gehaald in scenario-vragen:
- Een User Risk Policy (of Sign-in Risk Policy) configureren/wijzigen: vereist Global Administrator (of Security Administrator, afhankelijk van het exacte beleidsonderdeel) - dit is een beleidswijziging met impact op de hele tenant
- Alleen het Risky Users-rapport bekijken (zonder iets te wijzigen): Security Reader of Security Administrator is voldoende

Vuistregel: rapportages *bekijken* vraagt een lagere rol dan risk-based policies *configureren*.

### User Risk vs Sign-in Risk bij leaked credentials
Wanneer credentials van een gebruiker zijn uitgelekt (bijvoorbeeld gevonden op de dark web), is dat een **user risk** signaal (het account zelf is gecompromitteerd), niet een sign-in risk signaal (dat gaat over de omstandigheden van een specifieke inlogpoging, zoals een onmogelijke reis of anoniem IP). Remediatie hoort dus in een User Risk Policy te worden geconfigureerd (bijvoorbeeld: bij hoog risico wachtwoordwijziging vereisen), niet in een Sign-in Risk Policy.

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

### Cloud App Discovery (Microsoft Cloud App Security / Defender for Cloud Apps)
Onderdeel van Microsoft Cloud App Security (tegenwoordig Microsoft Defender for Cloud Apps) dat shadow IT in kaart brengt: welke cloud-apps gebruikers binnen de organisatie daadwerkelijk gebruiken, ook apps die nooit officieel zijn goedgekeurd of geregistreerd in Entra ID.

- Werkt door verkeerslogs te analyseren: firewall-logs, proxy-logs, of logs die via een geintegreerde security-oplossing (zoals Defender for Endpoint) worden aangeleverd
- Genereert een cloud discovery report met alle gedetecteerde apps, inclusief een risk score per app (gebaseerd op meer dan 90 risicofactoren: compliance, beveiliging, wettelijke certificeringen van de leverancier)
- Doel is zichtbaarheid krijgen in ongeautoriseerd app-gebruik, niet het direct blokkeren ervan; blokkeren/goedkeuren doe je daarna apart via governance-acties (app taggen als sanctioned/unsanctioned) of door de app te integreren met Conditional Access App Control

Onderscheid met andere features die er qua naam op lijken:
- Cloud App Discovery = zichtbaarheid krijgen in welke apps uberhaupt gebruikt worden (shadow IT opsporen)
- App governance (binnen Defender for Cloud Apps) = OAuth permissies en consent van reeds bekende/geregistreerde apps beoordelen en beperken
- Conditional Access met session controls = real-time restricties afdwingen (downloads blokkeren, etc.) op apps die al bekend en geintegreerd zijn

Vuistregel: zodra een vraag gaat over "welke apps gebruiken onze mensen eigenlijk, die we niet kennen" → Cloud App Discovery. Zodra het gaat over "wat mag een bekende/geregistreerde app doen" → app governance of Conditional Access.

### OAuth app policies in Defender for Cloud Apps
Om automatisch gewaarschuwd te worden wanneer een app riskante OAuth-permissies aanvraagt (bijvoorbeeld volledige mailbox-toegang), configureer je een OAuth app policy binnen Defender for Cloud Apps (onderdeel van app governance). Dit is iets anders dan Cloud App Discovery (dat gaat over onbekende apps zichtbaar maken) en iets anders dan admin consent workflows (dat gaat over het proces om consent goed te keuren, niet over doorlopende monitoring van al toegekende permissies).

### Azure AD Application Proxy - architectuur
Application Proxy publiceert on-premises webapplicaties naar externe gebruikers zonder dat er inbound firewall-regels nodig zijn. De connector (geinstalleerd on-premises) legt zelf een uitgaande HTTPS-verbinding naar de Application Proxy service, waarna al het verkeer via die uitgaande tunnel loopt. Vuistregel: zodra een vraag zegt dat er expliciet **geen** inbound firewall-poorten open mogen, is dat de sterkste hint richting Application Proxy in plaats van bijvoorbeeld een VPN of reverse proxy in het datacenter.

Bron: https://learn.microsoft.com/en-us/entra/identity/app-proxy/what-is-application-proxy

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

### PIM - Eligible vs Active assignment
Twee assignment-types die het fundament van het just-in-time model vormen:
- Eligible: de gebruiker heeft de mogelijkheid om de rol te activeren wanneer nodig, maar heeft de rol niet permanent actief; activatie kan MFA, goedkeuring en/of een justification vereisen
- Active: de rol is direct bruikbaar, zonder activatiestap

Voor een scenario waarin toegang alleen tijdelijk en op aanvraag nodig is (het kernidee achter least privilege/JIT), is Eligible de juiste keuze, niet Active - ook al lijkt "Active" intuitief de veiligere/directere optie.

### Sentinel integratie met Identity Protection
Om Sentinel incidents te laten genereren op basis van Identity Protection risk alerts: eerst een Sentinel data connector toevoegen voor Entra ID. Notify-instellingen en diagnostics settings zijn hier niet de eerste stap.

### Audit vereisten met Log Analytics
Om administratieve acties in Entra ID te laten wegschrijven naar een Log Analytics workspace: Diagnostics settings configureren in Entra ID.

### Sign-in logs retentie
Sign-in logs worden 30 dagen bewaard in Entra ID (zonder aanvullende export naar Log Analytics of een SIEM).

### Alert-notificaties omleiden: Action Groups vs Data Collection Rules
Wanneer alert-meldingen (bijvoorbeeld vanuit Identity Protection of Azure Monitor) naar een ander e-mailadres of team moeten worden gestuurd, regel je dat via een Action Group (Azure Monitor): daarin staan de daadwerkelijke ontvangers en acties (e-mail, SMS, webhook) die bij een alert worden getriggerd. Data Collection Rules bepalen alleen *welke data* wordt verzameld en waarheen die wordt gestuurd voor logging/analyse - ze hebben geen rol in het bepalen van wie een notificatie ontvangt.

### Audit logs exporteren voor een SIEM
Voor integratie met een externe SIEM (los van de directe Sentinel-connector) exporteer je audit logs bij voorkeur in JSON-formaat; dat behoudt de volledige structuur van de loggegevens. CSV is geschikter voor handmatige analyse in bijvoorbeeld Excel, maar verliest structuur die de meeste SIEM-integraties verwachten.

### Automatisch verwijderen van externe gebruikers na X dagen
Voor het instellen van automatische verwijdering van externe (guest) gebruikers na een vaste periode van inactiviteit (bijvoorbeeld 90 dagen) is de instelling te vinden onder **Identity Governance > Settings** (niet onder Access packages, Terms of use, of Access reviews - dat zijn gerelateerde maar losstaande features die deze automatische opschoning niet zelf regelen).

### Tijdelijke toegang voor externe partners
Voor tijdgebonden toegang (bijvoorbeeld 90 dagen) van partner-gebruikers tot een resource: access package via entitlement management, gekoppeld aan een connected organization voor die partner.

### Guest users automatisch opruimen bij inactiviteit
Conditional Access kan geen guest-accounts verwijderen op basis van inactiviteit; het regelt alleen runtime-toegang tijdens het inloggen zelf en heeft geen concept van "X dagen niet actief". Voor automatische opschoning na een periode van inactiviteit gebruik je Lifecycle Workflows (trigger op inactiviteit, actie zoals uitschakelen/verwijderen), eventueel in combinatie met Access Reviews die ook op inactiviteit kunnen reviewen.
