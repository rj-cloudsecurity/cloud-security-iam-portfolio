# Key Concepts

Samenvattingen van Entra ID concepten die tijdens het oefenen naar boven kwamen als punten die extra aandacht nodig hadden.

## Domain 1: Implement identities

### Hybrid authentication methods - timing bij account disable

Wanneer een gebruiker disabled wordt in on-premises Active Directory, bepaalt de gekozen authentication method hoe snel dat effect heeft in Entra ID.

- Password Hash Synchronization (PHS): sync-cyclus, vertraging tot circa 30 minuten voordat de disable status doorkomt
- Pass-through Authentication (PTA): valideert elke sign-in real-time tegen een on-prem domain controller via de authentication agent; disable werkt direct door
- Federation (AD FS): valideert ook real-time tegen on-prem AD, zelfde direct effect als PTA
- Conditional Access, Password Protection en password writeback lossen dit niet op; het zijn geen authenticatie-methoden en hebben geen invloed op de sync-timing

Let op een veelvoorkomende misvatting: PHS "forceert" nooit een wachtwoordwijziging - het synchroniseert alleen de bestaande hash. Het echte voordeel van PTA boven PHS in een overname/fusie-scenario (nog gescheiden tenants, geen forest trust) is niet "password reset forceren", maar de real-time, zonder sync-vertraging validatie tegen de nog zelfstandige on-prem AD van het overgenomen bedrijf tijdens een gevoelige transitieperiode.

Bron: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/whatis-hybrid-identity

### Seamless Single Sign-On (Seamless SSO) en Primary Refresh Token (PRT)

Voor domain-joined Windows 10 clients: de Entra ID login URL (https://autologon.microsoftazuread-sso.com) moet worden toegevoegd aan de Intranet Zone via Group Policy, zodat Kerberos-tickets automatisch worden doorgegeven zonder credential-prompt. Dit is een browser/GPO-instelling, geen agent-installatie (die hoort bij PTA) en geen lokale sign-in optie. Seamless SSO vereist wel netwerk-bereikbaarheid (corporate netwerk of VPN) tot een on-prem domain controller voor de Kerberos-ticketuitwisseling - het werkt niet vanaf een willekeurige externe locatie zonder die lijn naar een DC.

Voor locatie-onafhankelijke SSO (bijv. BYOD of remote devices zonder vaste VPN-lijn naar een DC) is niet Seamless SSO het juiste mechanisme, maar een Primary Refresh Token (PRT) op een Entra Joined, Hybrid Joined of Entra Registered device - de PRT wordt lokaal op het device bewaard en werkt onafhankelijk van netwerklocatie.

- Entra Join: volledig cloud-native device-identity, geen on-prem AD-koppeling
- Hybrid Join: device is zowel in on-prem AD als in Entra ID geregistreerd (dual membership)
- Entra Registered: BYOD/persoonlijk device, alleen voor app-toegang, geen volledige device-management

### Password writeback

Synchroniseert wachtwoordwijzigingen die in Entra ID zijn gedaan (bijvoorbeeld via SSPR) terug naar on-premises AD DS. Vereist wanneer wachtwoorden consistent moeten blijven ongeacht waar de reset is uitgevoerd. Los van sync-timing voor account disable.

### Sync scoping en custom attributen: Connect Sync vs Cloud Sync

Twee verschillende sync-technologieën met elk hun eigen filtering- en attribuutmechanisme - een veelvoorkomende valkuil op SC-300 is ze door elkaar halen.

**Microsoft Entra Connect Sync** (de klassieke, server-based oplossing):
- OU's uitsluiten / objecten scopen: via een inbound synchronization rule op de Active Directory Domain Services connector in de **Synchronization Rules Editor**, met een scoping filter op een attribuut en een transformation die het object als `cloudFiltered` markeert
- Custom on-prem AD-schema-attributen naar de cloud syncen: via **directory extensions** - deze blijven read-only in de cloud en zijn bruikbaar in dynamic groups en app token claims

**Microsoft Entra Cloud Sync** (de lichtere, agent-based oplossing):
- OU's/objecten uitsluiten: via **scoping filters in de Cloud Sync configuratie** zelf, niet via de Connect-wizard en niet via de Synchronization Rules Editor (die bestaat niet in Cloud Sync)
- Attribuut-mapping: eigen, eenvoudigere attribute-mapping binnen de Cloud Sync provisioning configuratie

Vuistregel: gaat het om Cloud Sync, dan zijn de Azure AD Connect wizard en de Synchronization Rules Editor de verkeerde gereedschappen - zoek naar "scoping filters" en "provisioning configuration". Gaat het gewoon om Connect (zonder Cloud Sync), dan zijn wizard en Sync Rules Editor juist wel relevant.

Voor troubleshooting van Cloud Sync-synchronisatiefouten geven de **Azure AD Provisioning Agent logs** het meeste detail (exacte object, attribuut, foutcode); **Microsoft Entra Connect Health** laat alleen zien *dat* er een probleem is (dashboard/health-niveau), niet *waarom*.

### Drie soorten gebruikers in Entra ID

Een steeds terugkerend onderscheid dat nodig is om provisioning-scenario's goed te kunnen beoordelen:

- Cloud-only user: alleen aangemaakt in Entra ID, geen on-prem bron
- Directory-synced user: bron is on-premises AD, komt via Entra Connect (of Cloud Sync) binnen; wijzigingen horen op de bron plaats te vinden, niet direct in Entra ID
- Guest (B2B) user: externe identiteit, geauthenticeerd via de eigen identity provider van de gast

Vuistregel: kijk eerst naar waar het account origineel vandaan komt voordat je bepaalt welke beheeractie (bijv. wachtwoord resetten, attribuut wijzigen) uberhaupt mogelijk is.

### Zelfregistratie van gebruikers blokkeren (Set-MsolCompanySettings)

Om te voorkomen dat gebruikers zelf een Entra ID tenant of resource kunnen aanmaken via self-service sign-up (bijvoorbeeld via een consumer Microsoft 365-aanmelding), gebruik je de PowerShell-cmdlet `Set-MsolCompanySettings -AllowAdHocSubscriptions $false`. Dit is een tenant-brede instelling en geen Conditional Access policy of external collaboration setting.

### Group-based licensing en nested groups

Licenties die via group-based licensing aan een groep zijn gekoppeld, worden alleen toegekend aan de directe leden van die groep. Geneste groepen (een groep als lid van een andere groep) erven de licentie niet door naar hun eigen leden. Voor een gebruiker die licentie moet krijgen via een nested group, moet die gebruiker dus direct lid zijn van de groep waaraan de licentie is gekoppeld, of de licentie moet los aan de bovenliggende groep(en) zelf worden gekoppeld.

Bron: https://learn.microsoft.com/en-us/entra/identity/users/licensing-groups-assign

### System-Assigned vs User-Assigned Managed Identity

Een System-Assigned Managed Identity (S-AMI) is gekoppeld aan de levenscyclus van de resource zelf (bijv. een VM of AKS-cluster): wordt de resource verwijderd, dan verdwijnt ook de identity. Bij het opnieuw aanmaken van diezelfde resource (bijvoorbeeld tijdens een disaster recovery-oefening) moet je dan opnieuw rechten toekennen, en gaat elke koppeling naar externe resources (zoals AcrPull op een Container Registry) verloren. Een User-Assigned Managed Identity (U-AMI) is een losstaand Azure-resource dat los van de levenscyclus van één specifieke resource bestaat en aan meerdere resources gekoppeld kan worden. Voor scenario's waarin resources regelmatig verwijderd/opnieuw aangemaakt worden (DR-oefeningen, geautomatiseerde herbouw) is een U-AMI stabieler, omdat de identity (en de daaraan gekoppelde rechten) behouden blijft ongeacht wat er met de onderliggende resource gebeurt.

Credential rotation van een managed identity is altijd automatisch en platform-beheerd - er is geen admin-handeling of scheduled task voor nodig, en dit is ook niet zichtbaar te configureren. Wordt er gesproken over periodiek zelf een managed identity "roteren", dan gaat dat in werkelijkheid meestal over het wisselen van *welke* (vooraf geprovisionde) U-AMI een resource actief gebruikt, bijvoorbeeld via een config-waarde die door automation wordt aangepast.

### Self-service group management combineren met delegatie

Om gebruikers zelf Microsoft 365-groepen te laten aanmaken, maar wel beperkt tot een specifieke groep gebruikers: self-service group management inschakelen in de Entra ID Group settings, gecombineerd met het beperken van wie mag aanmaken (bijvoorbeeld via een specifieke security group als toegestane makers). Voor verdergaande delegatie van beheertaken naar een subset van de organisatie (zonder volledige tenant-brede adminrechten) zijn Administrative Units het middel om rechten te scopen tot een specifieke afdeling of gebruikersgroep.

## Domain 2: Implement authentication and access management

### Conditional Access - kernwoorden: WANNEER geldt het, WAT dwingt het af

Elke CA-policy is één zin: **Als** [wie + welke app + welke conditie], **dan** [grant of session control]. Een eis bevat vaak beide helften. Splits ze eerst; dan wijst het kernwoord naar het onderdeel.

**WANNEER (de "als"-kant: users, resources, conditions)**

| Kernwoord in de eis | Onderdeel |
|---|---|
| buiten het bedrijfsnetwerk, land, risicoland, VPN | Conditions > Locations (named locations) |
| BYOD, unmanaged, joined, hybrid joined, compliant device | Conditions > Filter for devices (bijv. `trustType`) |
| deze specifieke/gevoelige app(s) | Target resources (app, authentication context, filter for apps) |
| admins, guests, specifieke rollen | Users (include/exclude) |
| gelekte credentials, anonymous IP, risicovolle login | Conditions > User risk / Sign-in risk (komt uit Identity Protection) |
| oude protocollen, legacy | Conditions > Client apps |

**AFDWINGEN (de "dan"-kant)**

| Kernwoord in de eis | Onderdeel |
|---|---|
| MFA vereisen, compliant device vereisen, wachtwoordwijziging | Grant controls |
| FIDO2, phishing-resistant, "alleen deze methoden" | Grant > Require authentication strength |
| blokkeren | Grant > Block access |
| elke X dagen opnieuw inloggen | Session > Sign-in frequency |
| geen downloads, web-only, read-only | Session > App enforced restrictions of Conditional Access App Control (met een session policy in Defender for Cloud Apps) |

**Wie doet wat (de rest hoort niet bij "wanneer" of "afdwingen" in CA)**

- Authentication Methods policy: welke methoden *beschikbaar* zijn voor gebruikers/groepen. Heeft **geen condities** (geen locatie, app of risico). Moet iets alleen buiten het netwerk of alleen voor één app gelden, dan is dit nooit het juiste middel.
- Authentication strength: *welke* methoden in een CA-policy geaccepteerd worden.
- Identity Protection: **detecteert** risico (en kan via risk policies reageren). In CA is het alleen een conditie.
- Intune compliance policy: definieert wát "compliant" is. CA eist het.
- Intune enrollment restrictions: wie/welk platform zich mag *registreren*. Geen toegangscontrole.
- Named location = alleen de definitie van een plek; het blokkeert niets zonder CA-policy.

**Voorbeelden die hier uit volgen:**
- Blokkeren vanuit risicolanden, tenzij via VPN: policy met Locations (risicolanden), exclude de VPN-locatie, grant Block.
- Guests: alleen werk-e-mail én elke 30 dagen opnieuw inloggen: domeinen/identity providers regelen de eerste eis, CA sign-in frequency de tweede.
- Alle Windows-devices moeten (hybrid) joined zijn: CA met filter for devices op `trustType`.
- FIDO2 alleen buiten het netwerk: CA met Locations + grant authentication strength (niet de Authentication Methods policy).
- Meerdere risicovolle sign-ins vanaf Tor leiden tot een automatische reactie: Identity Protection risk policy (user risk), geen CA-IP-lijst.

**Vuistregel in één zin:** *voorwaarde of "wanneer" = condition; eis of "moet" = grant; "tijdens de sessie" = session control.*

### Security Token Service (STS) - wie geeft het token uit

De STS is de component die een gebruiker authenticeert, claims verzamelt en een token uitgeeft. In de cloud is dat Microsoft Entra ID zelf; on-prem/federated is dat AD FS. Een veelgebruikte verwarring op SC-300:

- STS: geeft het token uit ("hier is je toegangsbewijs")
- Conditional Access: beslist of een token uberhaupt mag worden uitgegeven (MFA vereisen, device compliance, locatie) - de "portier", niet de tokenfabriek
- Enterprise Application: consumeert/vertrouwt het token, geeft het zelf niet uit

Vuistregel bij termen als "token issuance", "claims issuance", "SAML assertion", "federation", "trust relationship" → denk aan de STS, niet aan Conditional Access of een Enterprise App.

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

Voor een groeiende lijst gevoelige apps die dezelfde CA-eisen moeten krijgen is een **statische app-lijst per policy** foutgevoelig en moet steeds handmatig worden bijgewerkt. De schaalbare aanpak is een **Filter for apps**-conditie op **custom security attributes** die aan de apps zijn toegekend (bijv. een "sensitivity tier"-attribuut) - nieuwe apps met dat attribuut vallen dan automatisch onder de policy, net zoals dynamic groups automatisch meegroeien bij gebruikers.

### App-enforced restrictions voor SharePoint Online

Om downloads/sync te blokkeren op user-owned (alleen Entra ID registered) devices zonder company-owned (Entra ID joined) devices te beperken: Conditional Access policy met session controls, specifiek "Use app enforced restrictions" ingeschakeld. Client apps conditions en Cloud App Security policies lossen dit niet fijnmazig genoeg op.

### Named locations vs trusted IPs

Voor MFA-uitzonderingen op basis van kantoorlocatie: named locations met een publiek IP-bereik (Conditional Access). Trusted IPs is een legacy MFA-instelling en wordt niet meer aanbevolen.

### Leaked credentials - self-remediation

Wanneer gebruikers zelf risico moeten kunnen oplossen (zonder helpdesk): een policy die toegang toestaat maar een wachtwoordwijziging vereist, in combinatie met SSPR en MFA voor self-service unblocking.

### NPS extension voor VPN/RADIUS MFA, vs Application Proxy voor webapps

Wanneer een netwerk-apparaat (VPN-server, Wi-Fi, RADIUS-client) geen native Azure MFA ondersteunt: de NPS (Network Policy Server) extension for Azure MFA installeren. Valideert credentials tegen on-prem AD en triggert daarna Azure MFA.

Vuistregel voor het onderscheid met Application Proxy (zie Domain 3): RADIUS/VPN/Wi-Fi/netwerkauthenticatie → NPS extension. Interne webapplicatie extern toegankelijk maken → Application Proxy. Application Proxy, Password Protection proxy en PTA proxy lossen het RADIUS-scenario niet op.

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

### Authentication Strengths en Authentication Context vs device-based controls

Authentication Strengths (binnen Conditional Access) laat je per policy afdwingen welke specifieke authenticatiemethoden geaccepteerd worden, bijvoorbeeld "alleen phishing-resistant methoden zoals FIDO2" voor admins, terwijl andere gebruikers een bredere set methoden (waaronder wachtwoord) mogen blijven gebruiken. Dit is een eigenschap van de authenticatiemethode van de gebruiker, niet van het device. Hybrid Entra ID Join is een eigenschap van het device en heeft geen invloed op welke authenticatiemethode geaccepteerd wordt.

Vuistregel: WIE inlogt en HOE → Authentication methods/strengths; WELK apparaat gebruikt wordt → device compliance/join status (Intune, Hybrid Join).

Belangrijk: zo'n Authentication Strengths-policy wordt geschaald door de policy te **scopen op de gebruikersrol** (bijv. alle privileged admin-rollen), niet door het netwerk/IP waar legacy apps toevallig op draaien uit te sluiten - IP-scoping regelt niets over wie welke methode moet gebruiken en laat een gat open als een admin toevallig vanaf dat uitgesloten IP inlogt.

Authentication Context is een apart, gerelateerd concept: het is alleen een **label** op een gevoelige resource/actie (bijv. "HighSecurity"), dat zelf niets afdwingt. De daadwerkelijke handhaving (step-up MFA, phishing-resistant methode) gebeurt via een Conditional Access policy die op die Authentication Context reageert. Authentication Context = trigger/label, Conditional Access = handhaving.

TAP (Temporary Access Pass) is geen phishing-resistant methode en zit dus niet in de ingebouwde strength *Phishing-resistant MFA*; je voegt het toe via een **custom authentication strength** (bijv. FIDO2 + Windows Hello + TAP). TAP omzeilt MFA niet: het telt zelf als sterke authenticatie (denk aan bootstrap of herstel). Break-glass accounts sluit je volgens Microsoft juist uit van CA-policies en beveilig je met een lang wachtwoord of FIDO2.

### Legacy authentication blokkeren of uitsluiten via Conditional Access

Om verouderde authenticatieprotocollen (die geen MFA ondersteunen, zoals oudere mailprotocollen) te blokkeren: een Conditional Access policy met als conditie "Client apps" ingesteld op "Other clients" (legacy authentication), met als grant control "Block access". Dit is de aanbevolen route sinds Security Defaults en losse protocol-instellingen in Exchange Online minder fijnmazig zijn.

Omgekeerd geldt ook: CA kan sign-ins die geen moderne authenticatie gebruiken (zoals bepaalde legacy apps) helemaal niet evalueren op device compliance of andere grant-eisen - dat is een technische beperking, geen keuze. Wanneer een CA-policy device compliance afdwingt voor moderne apps maar bepaalde legacy apps dat niet ondersteunen, moeten die apps dus expliciet van die policy worden **uitgesloten** (eigen policy-scope), niet via session controls of risk-based policies - die vereisen allebei ook moderne authenticatie.

### Identity Protection: welke rol voor welke taak

Twee taken die vaak door elkaar worden gehaald:

- Een User Risk Policy (of Sign-in Risk Policy) configureren/wijzigen: vereist Global Administrator (of Security Administrator, afhankelijk van het exacte beleidsonderdeel) - dit is een beleidswijziging met impact op de hele tenant
- Alleen het Risky Users-rapport bekijken (zonder iets te wijzigen): Security Reader of Security Administrator is voldoende

Vuistregel: rapportages bekijken vraagt een lagere rol dan risk-based policies configureren.

### User Risk vs Sign-in Risk bij leaked credentials

Wanneer credentials van een gebruiker zijn uitgelekt (bijvoorbeeld gevonden op de dark web), is dat een user risk signaal (het account zelf is gecompromitteerd), niet een sign-in risk signaal (dat gaat over de omstandigheden van een specifieke inlogpoging, zoals een onmogelijke reis of anoniem IP). Remediatie hoort dus in een User Risk Policy te worden geconfigureerd (bijvoorbeeld: bij hoog risico wachtwoordwijziging vereisen), niet in een Sign-in Risk Policy.

### Anomalous token/sign-in detectie - welke tools

Voor het detecteren van tokens/sign-ins vanuit ongebruikelijke locaties of patronen zijn er twee complementaire, daadwerkelijk detecterende tools:

- Identity Protection risky sign-ins: detecteert patronen als impossible travel, atypical travel, sign-ins vanaf verdachte/onbekende locaties
- Microsoft Sentinel UEBA (User Entity Behavior Analytics): analyseert gedrag over tijd tegen een baseline en signaleert afwijkingen

Niet-detecterend: Azure Monitor Workbooks tonen alleen data (monitoren/rapporteren, geen anomaliedetectie); Conditional Access blokkeert/staat toe op basis van vooraf ingestelde condities, maar detecteert zelf geen anomalieën.

Vuistregel: "detect/investigate anomalous behavior" → Identity Protection of Sentinel UEBA. "Block/enforce" → Conditional Access. "View/report" → logs/Workbooks.

### Azure RBAC en Key Vault Access Policy samen op dezelfde Key Vault

Wanneer een Key Vault zowel Azure RBAC-roltoewijzingen als een (legacy) Access Policy heeft voor dezelfde gebruiker, worden deze niet tegen elkaar afgewogen of overschreven: de effectieve rechten zijn de unie van beide modellen. De gebruiker krijgt dus alles wat via RBAC is toegewezen, plus alles wat via de access policy is toegewezen - ongeacht welk model "strenger" is. Dit kan onbedoeld de toegang verbreden, wat precies de reden is waarom Microsoft aanraadt om nog maar één model (bij voorkeur RBAC) consistent te gebruiken per vault in plaats van beide te combineren.

## Domain 3: Implement access management for apps

### App registration - juiste rol toewijzen

Wanneer "Users can register applications" op No staat: Application Developer rol geeft precies genoeg rechten om apps te registreren (least privilege). Cloud Application Administrator is bedoeld voor het beheren van bestaande apps (service principals, consent, assignments), niet voor het registreren van nieuwe apps. Azure RBAC-rollen op subscription-niveau (Managed Application Contributor, App Configuration Data Owner) hebben geen invloed op Entra ID app-registratie.

### Wie mag wat rondom apps (default instellingen)

Standaard mogen alle gebruikers zelf apps registreren, tenzij dit expliciet is uitgezet. Het toewijzen van gebruikers aan een enterprise app (assignment) vereist wel een hogere rol: Global Administrator of Cloud Application Administrator.

### Enterprise application vs App registration

Voor SSO naar een gallery-app die OAuth ondersteunt gebruik je een Enterprise application (niet een nieuwe App registration); dat is de juiste blade voor het configureren van SSO naar een bestaande gallery-app. In STS-termen: de Enterprise Application consumeert/vertrouwt het token dat de STS uitgeeft, het geeft zelf geen tokens uit.

### B2B Collaboration vs B2B Direct Connect

Twee te onderscheiden Entra-features voor externe samenwerking:

- B2B Collaboration: guest users, uitnodigingen, redemption, toegang tot apps/SharePoint/M365-resources - het "klassieke" externe-gebruikersmodel
- B2B Direct Connect: specifiek voor Teams Shared Channels, directe cross-tenant samenwerking zonder dat er een guest-account wordt aangemaakt

Vuistregel: zie je "guest user", "invitation", "external user" → B2B Collaboration. Zie je "Teams shared channel" of "geen gastaccount nodig" → B2B Direct Connect. Het beperken van welke *apps* een partner-tenant mag openen is geen Direct Connect-scenario, ook al klinkt "application-level" verleidelijk.

### App access vs app permissions

Twee verschillende lagen die vaak worden verward:

- App access (welke apps mag iemand uberhaupt openen): geregeld via **Cross-Tenant Access Settings met application allowlisting** (inbound access restrictions) voor externe/partner-tenants, of simpelweg app-assignment voor interne gebruikers
- App permissions (wat mag iemand binnen een app doen, eenmaal toegelaten): geregeld via rollen/scopes binnen de app zelf (Reader, Contributor, API permissions)

Vuistregel: "mag App2/3/4 helemaal niet openen" → access/allowlisting. "Mag binnen App1 alleen lezen" → permissions/rollen. B2B Direct Connect regelt geen van beide specifiek voor dit soort scenario's (zie hierboven).

### B2B bulk invite, external collaboration restrictions en OTP voor guests

Een B2B bulk invite vereist alleen twee velden: email address en redirection URL - geen username, shared key of password; guest users authenticeren met hun eigen bestaande identity provider credentials. B2B collaboration users kunnen worden uitgenodigd tot een directory, een group, of direct een applicatie.

Wanneer een guest user al toegang heeft geaccepteerd voordat een domain-restrictie werd aangescherpt, blijft die toegang bestaan (de restrictie werkt niet met terugwerkende kracht op reeds geaccepteerde invites). Check dus altijd wanneer de toegang precies is geaccepteerd ten opzichte van wanneer de restrictie is ingesteld.

Email one-time passcode (OTP) wordt alleen gebruikt voor externe gebruikers met een consumer email adres die geen bestaand directory account hebben (bijvoorbeeld Outlook.com zonder Entra ID). Guests van een federated/partner tenant met een eigen directory account loggen in met hun eigen organisatie-credentials. Member users binnen de eigen tenant krijgen nooit een OTP.

### Access packages met domein-restrictie combineren

Toegang tot een access package beperken tot gebruikers van 1 specifiek domein van een connected organization vereist een combinatie van: een access package policy in Identity Governance EN de External collaboration settings in Entra ID. Een van de twee alleen is niet voldoende.

### Cloud App Discovery (Microsoft Defender for Cloud Apps)

Onderdeel van Microsoft Defender for Cloud Apps dat shadow IT in kaart brengt: welke cloud-apps gebruikers binnen de organisatie daadwerkelijk gebruiken, ook apps die nooit officieel zijn goedgekeurd of geregistreerd in Entra ID.

- Werkt door verkeerslogs te analyseren: firewall-logs, proxy-logs, of logs die via een geintegreerde security-oplossing (zoals Defender for Endpoint) worden aangeleverd
- Genereert een cloud discovery report met een risk score per app (gebaseerd op meer dan 90 risicofactoren)
- Doel is zichtbaarheid, niet direct blokkeren; blokkeren/goedkeuren gebeurt apart via governance-acties of Conditional Access App Control

Onderscheid met features die er qua naam op lijken:

- Cloud App Discovery = zichtbaarheid in welke apps uberhaupt gebruikt worden (shadow IT opsporen)
- App governance (binnen Defender for Cloud Apps) = OAuth-permissies en consent van reeds bekende/geregistreerde apps beoordelen en beperken - inclusief een **OAuth app policy** die automatisch waarschuwt wanneer een app riskante permissies aanvraagt (bijv. volledige mailbox-toegang)
- Conditional Access met session controls = real-time restricties afdwingen (bijv. downloads/exports blokkeren) op apps die al bekend en geintegreerd zijn, specifiek via een **Session Policy** (niet een Access Policy - die is alles-of-niets op sessieniveau, geen fijnmazige actie-blokkade)

Wanneer een gecompromitteerd account consent heeft gegeven aan een kwaadaardige OAuth-app: de structurele preventie is **admin consent verplicht stellen voor alle apps** gecombineerd met een **app governance policy** - niet B2B-restricties (gaat over gebruikers, niet apps) en niet alleen Conditional Access (blokkeert geen consent-acties).

### Azure AD Application Proxy - architectuur

Application Proxy publiceert on-premises webapplicaties naar externe gebruikers zonder dat er inbound firewall-regels nodig zijn. De connector (geinstalleerd on-premises) legt zelf een uitgaande HTTPS-verbinding naar de Application Proxy service, waarna al het verkeer via die uitgaande tunnel loopt. Vuistregel: zodra een scenario expliciet vereist dat er geen inbound firewall-poorten open mogen, is dat de sterkste indicatie richting Application Proxy in plaats van bijvoorbeeld een VPN of reverse proxy in het datacenter.

Legacy-integratie kort samengevat: RADIUS/VPN/Wi-Fi/netwerkauthenticatie → NPS extension (zie Domain 2). Interne webapplicatie extern beschikbaar maken → Application Proxy. SAML-app → Enterprise Application. OAuth/OIDC-app → App Registration.

Bron: https://learn.microsoft.com/en-us/entra/identity/app-proxy/what-is-application-proxy

### B2C custom attributes tijdens sign-up toevoegen

Om tijdens de sign-up journey van een B2C-toepassing een volledig nieuw custom attribuut te verzamelen (bijvoorbeeld een loyaliteitsnummer, naast standaardvelden zoals e-mail en wachtwoord), volstaat een built-in user flow niet - die biedt beperkte, vooraf gedefinieerde opties voor welke attributen verzameld worden. Voor een op maat gemaakte sign-up journey met een nieuw custom attribuut, validatie en garantie dat het veld bij elk sign-up-pad (ook via social login) wordt afgedwongen, is een custom policy nodig binnen de Identity Experience Framework.

### Least privilege bij app-registratie: flow, permission type en scope

Voor een app die alleen mag handelen wanneer er een gebruiker actief is ingelogd (en dus niet als achtergrondservice): gebruik de Authorization Code flow met Delegated permissions, geschaald tot precies wat nodig is (bijv. User.Read in plaats van het bredere User.Read.All). Delegated permissions zijn gebonden aan de ingelogde gebruiker en diens consent; Application permissions werken app-only, zonder ingelogde gebruiker.

Hetzelfde principe geldt voor een externe/third-party vendor die alleen read-only API-toegang tot Microsoft Graph nodig heeft: de permissies beperken tot read-only **in de app registration zelf** (bijv. alleen `.Read`-scopes, geen `.ReadWrite`). Dat is de enige plek waar de daadwerkelijke rechten van een applicatie worden vastgelegd - Conditional Access (regelt wanneer/vanaf waar), B2B guest-restricties (regelt gebruikers, niet apps) en Defender for Cloud Apps API-controls (monitoring, geen permissie-afdwinging) doen dit geen van alle rechtstreeks.

Om te voorkomen dat gebruikers (of admins zonder formele review) toestemming geven aan multi-tenant apps voor high-privilege permissies zoals Directory.ReadWrite.All: admin consent verplicht stellen voor alle applicaties, gecombineerd met een formeel goedkeuringsproces (bijv. Microsoft Entra Permissions Management of een Entitlement Management-workflow). Een gedeeltelijke maatregel zoals "user consent toestaan voor verified publishers met geselecteerde permissies" voldoet niet wanneer de eis is dat niemand zonder formele review high-privilege consent mag geven.

### Service principal credentials: secrets blokkeren en CA voor workload identities

Om te voorkomen dat een service principal met een gestolen client secret kan inloggen: certificaten verplicht stellen en secrets blokkeren. Dat doe je met een **app management policy** (tenant-breed of per app), niet met een schakelaar op de app registration zelf. Aanvullend beperkt **Conditional Access voor workload identities** (Workload Identities Premium) waar een service principal vandaan mag komen.

Let op de beperkingen: CA voor workload identities ondersteunt alleen **locatie** en **service principal risk** als conditie, alleen **Block** als actie, en alleen single-tenant service principals. MFA of device compliance bestaan niet voor een service principal. CA dwingt zelf geen certificaten af; dat doet de app management policy.

## Domain 4: Plan and implement identity governance

### Access reviews - welke resources, welke licentie

- Groups en Apps: access reviews via Entra ID Governance (P2)
- Azure resource roles en Entra ID rollen: access reviews via Privileged Identity Management (eveneens P2)

Beide routes vereisen P2, maar het zijn verschillende features voor verschillende resource-typen.

### Access review reviewers correct instellen

- Reviewers = Member (self): gebruiker beoordeelt eigen toegang, geen manager-betrokkenheid
- Reviewers = Manager: elke manager krijgt de reviews van zijn eigen team
- Fallback reviewer: wordt alleen ingezet als de primaire reviewer niet beschikbaar is of geen manager heeft; maakt een manager dus niet automatisch de standaard-reviewer

Voor een snelgroeiende/snel-wisselende gebruikerspopulatie (hoge turnover) die efficient gereviewed moet worden: een **dynamic group** als reviewdoelgroep onderhoudt het lidmaatschap automatisch op basis van attributen, in plaats van een statische groep die steeds handmatig moet worden bijgewerkt. Hetzelfde "automatisch vs handmatig onderhouden"-principe keert terug bij CA app-targeting via custom security attributes (zie Domain 2).

Let op: dit principe geldt niet universeel. Bij een eis die draait om een **intrinsieke eigenschap van het policy-object zelf** (zoals een Terms of Use met jaarlijkse herbevestiging en versiebeheer per attribuut-tier) is de vollediger oplossing meerdere ToU-policies met Conditional Access-targeting, niet simpelweg "een dynamic group aan de ToU hangen" - dat mist de CA-handhavingslaag die de ToU daadwerkelijk afdwingt.

### PIM - rolbeheer en terminologie

Alleen Global Administrator of Privileged Role Administrator kunnen PIM-instellingen (zoals activation duration) voor een rol beheren. Activation duration wordt gemeten in uren, nooit in dagen of maanden; permanente toewijzing gaat in tegen het hele idee van PIM (eligible + activatie vereist).

Twee PIM-instellingen die makkelijk worden verward:

- Activation duration: hoe lang een geactiveerde rol actief/bruikbaar blijft nadat iemand hem heeft geactiveerd
- Request/approval duration: hoe lang een **pending approval-aanvraag** geldig blijft staan voordat die automatisch verloopt als niemand erop reageert - zegt niets over hoe snel de approval zelf moet gebeuren, alleen over de levensduur van het verzoek in de wachtrij

Vuistregel: een eis geformuleerd als "approval must occur within X minutes, otherwise the request expires" beschrijft letterlijk het expiry-gedrag van **request duration**, niet van activation duration - lees dit soort eisen woord voor woord, want de twee termen worden vaak door elkaar gebruikt.

Voor resource-roles (zoals rollen op een Key Vault, niet een Entra ID-rol) met verplichte approval en justification-logging zijn twee configuraties nodig: PIM for resource roles inschakelen EN de specifieke Azure RBAC-rol daarbinnen via PIM configureren - een van de twee alleen is onvolledig.

Om te garanderen dat niemand permanent Global Admin heeft (audit-eis): rollen zo instellen dat permanente toewijzingen worden uitgeschakeld (role settings), zodat alleen eligible/tijdelijke toewijzingen mogelijk zijn.

### PIM - Eligible vs Active assignment

Twee assignment-types die het fundament van het just-in-time model vormen:

- Eligible: de gebruiker heeft de mogelijkheid om de rol te activeren wanneer nodig, maar heeft de rol niet permanent actief; activatie kan MFA, goedkeuring en/of een justification vereisen
- Active: de rol is direct bruikbaar, zonder activatiestap

Voor een scenario waarin toegang alleen tijdelijk en op aanvraag nodig is (het kernidee achter least privilege/JIT), is Eligible de juiste keuze, niet Active.

### Sentinel integratie met Identity Protection

Om Sentinel incidents te laten genereren op basis van Identity Protection risk alerts: eerst een Sentinel data connector toevoegen voor Entra ID. Notify-instellingen en diagnostics settings zijn hier niet de eerste stap. Sentinel zelf is het centrale SIEM/SOAR-platform: het haalt Sign-in logs, Audit logs en PIM-events via kant-en-klare connectors binnen in één workspace en correleert ze via (custom) detection rules - Identity Protection is daarbij een databron, niet andersom. Voor een eenmalig, retrospectief rapport over meerdere identity-signalen tegelijk is dit efficienter dan zelf een exportpijplijn naar bijvoorbeeld Synapse op te zetten, omdat Sentinel die connectors en datamodellen al kant-en-klaar heeft.

### Audit vereisten met Log Analytics

Om administratieve acties in Entra ID te laten wegschrijven naar een Log Analytics workspace: Diagnostics settings configureren in Entra ID.

### Alert-notificaties omleiden: Action Groups, notification settings en Connect Health

Wanneer alert-meldingen naar een ander e-mailadres, Teams of een ITSM-systeem (zoals ServiceNow) moeten worden gestuurd, is dit een keten van twee onderdelen:

- Notification settings (bijv. binnen Entra ID Connect Health): bepalen **wat** er gemeld moet worden en **wie** de ontvanger(s) zijn
- Azure Monitor Action Groups: het daadwerkelijke **transportmiddel** - verstuurt naar e-mail, SMS, Teams-webhook, of triggert een ServiceNow-integratie via webhook/Logic App

Log Analytics workspace alerts zijn alleen relevant wanneer je zelf custom alerts bouwt op KQL-queries - niet nodig wanneer je al bestaande Connect Health-alerts wil doorsturen. Microsoft Defender for Identity staat hier volledig los van (gaat over on-prem AD-dreigingen zoals lateral movement, niet over sync/AD FS-health).

Om een wijziging in een gebruikerskenmerk (bijv. primair e-mailadres) niet alleen te detecteren maar ook automatisch terug te draaien: audit logs doorsturen (diagnostic settings of Sentinel) en een **analytics rule met een playbook (Logic App)** laten reageren. Sentinel alleen levert detectie en alerts; de herstelactie zit in het playbook. Identity Protection kijkt naar sign-in- en gebruikersrisico en detecteert zulke attribuutwijzigingen niet.

### Alerting op specifieke PIM-activaties zonder alert fatigue

Om alleen gewaarschuwd te worden bij activatie van specifieke, hoog-risico rollen (en niet bij elke willekeurige PIM-activatie) - bijvoorbeeld alleen buiten kantoortijden - configureer je een Azure Monitor alert rule op de AuditLogs, gefilterd op rolnaam en tijdsvenster. PIM's eigen ingebouwde notificaties zijn niet zo fijnmazig instelbaar per rol/tijdvak.

### Licentiegeschiedenis auditen (ook na verwijdering)

Voor een audit-rapport dat moet aantonen wie een specifieke licentie op enig moment binnen een periode heeft gehad - inclusief gebruikers bij wie de licentie inmiddels weer is verwijderd - is een momentopname van de huidige licentiestatus niet voldoende. Voor een historisch overzicht van toekenningen én verwijderingen gebruik je de Entra ID audit logs, gefilterd op de "Assign license" (en "Remove license") activiteit.

### Lifecycle Workflows: automatische remediatie op attribuutwijziging

Lifecycle Workflows kan triggeren op een attribuutwijziging (bijv. `department`) die binnenkomt via HR-brondata ("Mover"-scenario), en vervolgens een samengestelde set taken uitvoeren: groepslidmaatschap/access package-assignments intrekken, account tijdelijk uitschakelen, notificatie versturen - allemaal gelogd als één gestructureerd proces.

Een **dynamic group** kan hetzelfde attribuut gebruiken om iemand uit een groep te laten vallen, maar dat is een bijproduct van groepsevaluatie, geen doelbewust, volledig remediatiemechanisme: het raakt alleen toegang die uitsluitend via die ene groep loopt, en de evaluatie loopt bovendien op een verwerkingscyclus (niet instant). Identity Protection is hier geen alternatief - dat detecteert sign-in/compromise-risico, geen HR-attributen zoals afdeling.

Voor inactieve guest users specifiek bestaat een kant-en-klaar Lifecycle Workflow-template "Offboard inactive guest users" met trigger "inactive for X days" (gebaseerd op `signInActivity`). Access Reviews met auto-apply is een legitiem alternatief, maar is een beoordelingsproces (iemand/iets beslist per cyclus), geen directe attribuut-trigger. Conditional Access kan geen guest-accounts verwijderen op basis van inactiviteit - het regelt alleen runtime-toegang tijdens het inloggen zelf.

### Tijdelijke en automatische toegang voor externe partners

Voor tijdgebonden toegang (bijvoorbeeld 90 dagen) van partner-gebruikers tot een resource: access package via entitlement management, gekoppeld aan een connected organization voor die partner. Voor automatisch verwijderen van externe gebruikers na een vaste inactiviteitsperiode: Identity Governance > Settings (niet Access packages, Terms of use, of Access reviews los - dat zijn gerelateerde maar losstaande features).
