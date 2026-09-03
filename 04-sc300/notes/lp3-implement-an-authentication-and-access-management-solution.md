# SC-300: Microsoft Identity and Access Administrator

## Learning Path 3: Implement an authentication and access management solution
### Module 1: Secure Microsoft Entra users with multifactor authentication


### Introduction
- Waarom dit belangrijk is
  - Scenario: security engineer bij fabrikant met gevoelige client-designs (bv. voor Microsoft) opgeslagen in Azure. Netwerk is al gehardened en toegang is beperkt tot de juiste mensen, maar er is nog een grote zwakke plek: user accounts
  - Multifactor authentication (MFA) is een van de beste manieren om te voorkomen dat onbevoegden binnenkomen via alleen een username/wachtwoord

- Wat deze module behandelt
  - Microsoft Entra multifactor authentication (MFA)
  - Een plan maken om MFA uit te rollen
  - MFA inschakelen voor users en specifieke apps

- Learning objectives
  - Learn about Microsoft Entra multifactor authentication (MFA)
  - Create a plan to deploy Microsoft Entra multifactor authentication
  - Turn on Microsoft Entra multifactor authentication for users and specific apps

- Prerequisites
  - Basic knowledge of the Azure portal
  - Basic knowledge of Microsoft Entra ID
 
---

### What is Microsoft Entra multifactor authentication?

- Andere features die password-based aanvallen tegengaan (herhaling/context)
  - Password complexity rules; dwingt moeilijker te raden wachtwoorden af
  - Password expiration rules; periodiek wijzigen, geen hergebruik van oude wachtwoorden
  - SSPR (Self-Service Password Reset); user reset zelf wachtwoord zonder IT
  - Microsoft Entra ID Protection; risk-based policies die automatisch blokkeren of remedieren (bv. password change afdwingen)
  - Microsoft Entra password protection; blokkeert veelgebruikte/gecompromitteerde wachtwoorden via een global banned-password list
  - Microsoft Entra smart lockout; herkent en blokkeert brute-force pogingen, onderscheidt valide users van hackers
  - Microsoft Entra application proxy; security-enhanced remote access naar on-prem web apps
  - SSO; toegang tot apps incl. duizenden preintegrated SaaS apps
  - Microsoft Entra Connect; 1 identity across hybrid enterprise (users/groups/devices in sync)

- Waarom deze features niet genoeg zijn
  - Beschermen tegen raden/brute-force van wachtwoorden
  - Beschermen NIET tegen social engineering of slechte physical security (bv. wachtwoord op een sticky note)
  - Hiervoor is MFA nodig

- Wat is MFA
  - Vereist 2 of meer elementen voor volledige authenticatie
  - 3 categorieën (examen-kernstof):
    - Something you know; wachtwoord of security question
    - Something you possess; mobile app notification of token-generating device
    - Something you are; biometrisch, bv. vingerafdruk of face scan

- Waarom MFA werkt
  - Beperkt de impact van een gelekt wachtwoord; hacker heeft ook het 2e factor nodig (telefoon, vingerafdruk, gezicht)
  - Moet altijd aanstaan; meest effectieve manier om unauthorized sign-in te voorkomen
  - Microsoft's naam hiervoor: two-step verification solution
  - Methodes: phone call, text message, mobile app verification
  - Layered approach; wachtwoord alleen is nutteloos zonder het trusted device, en andersom (device alleen is nutteloos zonder wachtwoord)

- Hoe MFA afgedwongen kan worden (2 manieren, niet exclusief)
  - Security Defaults; simpele aan/uit MFA voor iedereen, geen Conditional Access nodig, beschikbaar op elk licentie-niveau incl. Free
  - Conditional Access policies; fijnmazige, situationele MFA-regels (IF-THEN), vereist Entra ID P1

- Hoe krijg je MFA (examen-relevant)
  - Entra ID P1 of P2, of Microsoft 365 Business; MFA via security defaults, plus optie tot Conditional Access voor verfijning
  - Entra ID Free of standalone M365 licenties; alleen security defaults die MFA vereisen voor users en admins

- Onthouden voor examen
  - MFA is beschikbaar op elk licentie-nivaeu (zelfs Free) via security defaults; geen premium licentie strikt vereist voor basis-MFA
  - Conditional Access is de geavanceerde, situationele manier om MFA af te dwingen en vereist P1
  - De 3 categorieën (know/possess/are) zijn de kern van elke MFA-vraag op het examen

---

### Plan your multifactor authentication deployment

- Rollout-strategie
  - MFA uitrollen in golven; start met kleine pilot group om complexiteit/setup-issues/unsupported apps of devices te ontdekken
  - Groep geleidelijk uitbreiden, na elke fase evalueren, tot volledige organisatie is enrolled

- Communicatieplan
  - MFA vereist user-interactie (registratieproces); users goed informeren
  - Wat moeten ze doen, belangrijke data, waar hulp te krijgen bij problemen
  - Microsoft biedt communicatie-templates (posters, email templates)

- MFA policies via Conditional Access
  - Deze unit behandelt specifiek het afdwingen van MFA via Conditional Access policies (vereist P1); IF-THEN statements
  - Voorbeeld: IF payroll manager wil bij payroll app, THEN MFA vereist
  - Andere veelvoorkomende triggers:
    - IF specifieke cloud app wordt benaderd
    - IF specifiek netwerk wordt benaderd
    - IF specifieke client applicatie wordt gebruikt
    - IF een nieuw device wordt geregistreerd

- Authentication methods (examen-kernstof)
  - Altijd meer dan 1 methode aanbieden; backup optie nodig als primaire methode niet beschikbaar is
  - Mobile App Verification code; OATH code via bv. Microsoft Authenticator, wijzigt elke 30 sec, werkt ook met beperkte connectivity. Werkt niet in China op Android
  - Mobile app notification; push notification, user bevestigt sign-in
  - Call to a phone; belt user, bevestiging via keypad; voorkeur als backup-methode
  - FIDO2 security key; unphishable, passwordless, meestal USB, ook Bluetooth/NFC mogelijk
  - Windows Hello for Business; vervangt wachtwoord door 2FA op device zelf, gekoppeld aan device + biometrisch/PIN
  - OATH tokens; software (bv. Authentcator app) of hardware tokens (los te kopen)
  - Admin schakelt 1 of meer methodes in; users kiezen zelf welke ze gebruiken

- Registratie van authentication methods
  - Makkelijkste manier: Microsoft Entra ID Protection; prompt bij volgende sign-in (vereist Identity Protection licentie)
  - Alternatief: prompt bij gebruik van een app/service die MFA vereist
  - Alternatief: afdwingen via Conditional Access policy op een group met alle users; vereist wel handmatig periodiek onderhoud (registered users verwijderen uit de group)

- Onthouden voor examen
  - MFA kan afgedwongen worden via Security Defaults (simpel, gratis) of Conditional Access (P1, fijnmazig, IF-THEN); deze unit gaat specifiek over de Conditional Access-aanpak
  - Altijd meerdere auth-methodes aanbieden voor backup
  - FIDO2 en Windows Hello for Business zijn passwordless opties; de rest werkt naast een wachtwoord
 
---

### Exercise - explore dynamic groups
  - [04-sc300/labs/12-enable-microsoft-entra-multifactor-authentication](../../04-sc300/labs/12-enable-microsoft-entra-multifactor-authentication.md)

---

### Configure multifactor authentication methods

- Registratie flow
  - Eerste keer inloggen bij een service die MFA vereist, wordt user gevraagd hun voorkeursmethode te registreren
  - Daarna: bij elke sign in wordt om de authenticatie informatie gevraagd via de gekozen methode

- Authentication methods en welke services ze ondersteunen (examen kernstof)
  - Password; MFA en SSPR
  - Security questions; alleen SSPR
  - Email address; alleen SSPR
  - Windows Hello for Business; MFA en SSPR
  - FIDO2 Security Key; MFA en SSPR
  - Microsoft Authenticator app; MFA en SSPR
  - OATH hardware token; MFA en SSPR
  - OATH software token; MFA en SSPR
  - Text message; MFA en SSPR
  - Voice call; MFA en SSPR
  - App passwords; alleen MFA, in bepaalde gevallen

- Password
  - Enige methode die je niet kunt uitschakelen

- Security questions
  - Alleen voor non administrative accounts die SSPR gebruiken
  - Vragen en antworden worden prive en security enhanced opgeslagen op het user object; alleen de user zelf kan ze beantwoorden, alleen tijdens registratie. Admin kan ze niet lezen of wijzigen
  - 35 voorgedefinieerde vragen, vertaald/gelokaliseerd op basis van browser locale
  - Zelf aanpasbaar via admin interface, max 200 karakters

- Email address
  - Alleen beschikbaar in SSPR
  - Aanbevolen: gebruik geen email account dat zelf het Entra wachtwoord van de user nodig heeft om te openen

- Windows Hello for Business
  - Biometrische authenticatie: gezichtsherkenning of vingerafdruk
  - Samen met FIDO2 en Microsoft Authenticator een van de passwordless oplossingen

- FIDO2 security keys
  - Unphishable, standards based, passwordless, elke vorm factor mogelijk
  - FIDO staat voor Fast Identity Online, open standaard voor passwordless authenticatie
  - Meestal USB, ook Bluetooth of NFC
  - Werkt voor sign in bij Entra ID of Entra hybrid joined Windows 10 devices, geeft SSO naar cloud en on premises resources, werkt ook in supported browsers

- Microsoft Authenticator app
  - Beschikbaar voor Android en iOS
  - Stuurt push notification bij verdachte/nieuwe sign in poging, user bevestigt of weigert
  - Kan ook als software token gebruikt worden om een OATH verification code te genereren die je zelf invoert
  - User kan zelf kiezen tussen push notification of code invoer

- OATH hardware tokens
  - Open standaard voor one time password codes
  - Entra ID ondersteunt OATH TOTP SHA 1 tokens, 30 of 60 seconden variant
  - Te koop bij losse vendors, secret keys max 128 karakters, niet elk token compatible

- OATH software tokens
  - Apps zoals Microsoft Authenticator of andere authenticator apps
  - Entra ID genereert de secret key/seed die in de app wordt ingevoerd om OTP's te genereren

- Text message
  - SMS met verificatiecode, user voert deze in binnen een bepaalde tijd

- Voice call
  - Automatisch telefoontje, bevestiging via keypad
  - Niet beschikbaar op de free/trial Entra tier

- App password
  - Voor non browser apps die geen MFA ondersteunen
  - Zonder app password kunnen users met MFA enabled niet authenticaten in die apps

- Monitoring adoption
  - Entra ID heeft een Usage & insights view (Monitoring sectie) voor MFA en SSPR adoptie
  - Toont registratie aantallen plus succes/failure per authentication method, gebaseerd op laatste 30 dagen audit logs
  - Drill down mogelijk per user voor registratie details
  - Losse Usage tab specifiek voor SSPR metrics

- Onthouden voor examen
  - Password is de enige methode die je niet kunt uitzetten
  - Security questions en email address werken alleen bij SSPR, niet bij MFA
  - Voice call werkt niet op Free/trial tier
  - Windows Hello for Business, FIDO2 en Microsoft Authenticator zijn de passwordless opties

---

## Learning Path 2: Implement an authentication and access management solution
### Module 2: Manage user authentication

### Introduction

- Wat authentication in Entra ID inhoudt
  - Verifieren van credentials bij inloggen op device, app of service
  - Meer dan alleen username en password checken

- Componenten van Entra authentication (examen kernstof)
  - Self service password reset
  - Multifactor authentication
  - Hybrid integratie om password changes terug te schrijven naar on premises omgeving
  - Hybrid integratie om password protection policies af te dwingen voor on premises omgeving
  - Passwordless authentication
  - Authentication naar virtual machines

- Wat deze module behandelt
  - Plannen, implementeren en beheren van user authentication in Entra ID

- Learning objectives
  - Administer authentication methods (FIDO2/Passwordless)
  - Implement an authentication solution based on Windows Hello for Business
  - Configure and deploy self service password reset
  - Deploy and manage password protection and smart lockouts
  - Implement Kerberos and certificate based authentication
  - Configure Microsoft Entra user authentication to virtual machines

---

### Administer FIDO2 and passwordless authentication methods

- Context
  - Historisch: username en password meest voorkomende manier van inloggen
  - Modern: password moet aangevuld of vervangen worden door veiligere methodes
  - Passwordless (Windows Hello, FIDO2, Microsoft Authenticator) is het veiligst
  - MFA voegt extra beveiliging toe naast alleen een password: push notification, code, SMS, telefoontje

- Onboarding aanbeveling
  - Combined security information registration inschakelen, MFA en SSPR tegelijk laten registreren
  - Meerdere authentication methods laten registreren voor resiliency, backup als 1 methode niet beschikbaar is

- Security, usability en availability per methode (examen kernstof)

| Methode | Security | Usability | Availability |
|---|---|---|---|
| Windows Hello for Business | Hoog | Hoog | Hoog |
| Microsoft Authenticator app | Hoog | Hoog | Hoog |
| FIDO2 security key | Hoog | Hoog | Hoog |
| OATH hardware tokens (preview) | Medium | Medium | Hoog |
| OATH software tokens | Medium | Medium | Hoog |
| SMS | Medium | Hoog | Medium |
| Voice | Medium | Medium | Medium |
| Password | Laag | Hoog | Hoog |

- Tip
  - Microsoft Authenticator app aanbevolen voor flexibiliteit en usability; ondersteunt passwordless, MFA push notifications en OATH codes

- Primaire vs secundaire authenticatie (examen kernstof)

| Methode | Primair | Secundair |
|---|---|---|
| Windows Hello for Business | Ja | MFA |
| Microsoft Authenticator app | Ja (preview) | MFA en SSPR |
| FIDO2 security key | Ja | MFA |
| OATH hardware tokens (preview) | Nee | MFA en SSPR |
| OATH software tokens | Nee | MFA en SSPR |
| SMS | Ja (preview) | MFA en SSPR |
| Voice call | Nee | MFA en SSPR |
| Password | Ja | Geen |

- Belangrijk
  - Password kan niet uitgeschakeld worden als authentication method
  - Als password de primaire factor is, altijd MFA toevoegen voor extra security

- Methodes voor specifieke scenario's
  - App passwords; voor oude apps zonder modern authentication, per user configureerbaar
  - Security questions; alleen SSPR
  - Email address; alleen SSPR

- Wat is FIDO2
  - FIDO Alliance promoot open authentication specs, wil password gebruik verminderen
  - FIDO2 is de nieuwste specificatie, incorporeert WebAuthn
  - Meestal USB, ook Bluetooth of NFC mogelijk
  - Werkt bij sign in op Entra ID of hybrid Entra joined Windows 10/11 devices, geeft SSO naar cloud en on premises resources, werkt ook in supported browsers
  - Geschikt voor security sensitive organisatis of medewerkers die geen telefoon willen/kunnen gebruiken als 2e factor
  - Unphishable, passwordless, elke form factor mogelijk
  - Werkt zonder username of password via externe security key of platform key ingebouwd in een device

- FIDO2 inschakelen (stappen)
  1. Microsoft Entra admin center
  2. Protection > Authentication methods > Authentication method policy
  3. Bij FIDO2 Security Key: Enable Yes/No, Target All users of Select users
  4. Save

- User registratie van FIDO2 key (stappen)
  1. myprofile.microsoft.com > Security Info
  2. Als user al 1 MFA methode heeft: direct FIDO2 key registreren. Zo niet: eerst een methode toevoegen
  3. Add method > Security key > USB of NFC device
  4. PIN aanmaken/invoeren + gesture (biometrisch of touch) op de key
  5. Naam geven aan de key, Next, Done

- Sign in met passwordless credential
  - Werkt in supported browsers op Windows 10 versie 1903 of hoger, of Windows 11

- Prerequisites voor cloud only deployment
  - Windows 10 versie 1511 of later, of Windows 11
  - Microsoft Azure account
  - Microsoft Entra ID
  - Multifactor authentication
  - Modern Management (optioneel: Intune of andere MDM)
  - Entra ID Premium subscription (optioneel, alleen nodig voor automatische MDM enrollment)

- Onthouden voor examen
  - Windows Hello for Business, Microsoft Authenticator app en FIDO2 security key scoren overal hoog (security, usability, availability)
  - Password is de enige methode die je nooit kunt uitschakelen
  - OATH tokens en Voice call kunnen alleen als secundaire factor, nooit als primaire authenticatie
  - FIDO2 en Authenticator app zijn beide "unphishable" doordat er geen wachtwoord getypt wordt dat onderschept kan worden

---

### Explore Authenticator app and OATH tokens

- Microsoft Authenticator app algemeen
  - Extra beveiligingslaag voor Entra ID werk/school account of Microsoft account
  - Beschikbaar voor Android en iOS
  - Kan gebruikt worden voor passwordless sign in, of als extra verificatie bij SSPR of MFA
  - Kan zowel notification als verification code aanbieden; als beide enabled zijn kan de user zelf kiezen welke methode

- Hoe de app werkt
  - Push notification naar smartphone/tablet, user kiest Verify of Deny
  - Voorkomt unauthorized access en fraudulente transacties, geen password nodig bij sign in
  - Kan ook als software token dienen: OATH verification code die de user na username/password invoert als 2e factor
  - Users kunnen tot 5 OATH hardware tokens of authenticator apps tegelijk geconfigureerd hebben

- OATH TOTP (Time based One Time Password)
  - Open standaard voor het genereren van OTP codes
  - Kan via software of hardware geimplementeerd worden
  - Entra ID ondersteunt geen OATH HOTP, een ander soort code generatie standaard
  - Software OATH tokens zijn meestal apps zoals Microsoft Authenticator of andere authenticator apps
  - Entra ID genereert de secret key/seed die in de app wordt ingevoerd om elke OTP te genereren
  - Authenticator app genereert automatisch codes ook bij push notification setup, als backup wanneer een device geen connectivity heeft
  - Third party apps die OATH TOTP gebruiken kunnen ook gebruikt worden

- Onthouden voor examen
  - Entra ID ondersteunt OATH TOTP, niet OATH HOTP
  - Authenticator app kan zowel push notification als OATH code genereren, user kiest zelf welke
  - Max 5 OATH hardware tokens of authenticator apps per user

---

### Implement an authentication solution based on Windows Hello for Business

- Wat het is
  - Vervangt passwords door strong two factor authentication op PC's en mobiele devices
  - Nieuw type user credential, gebonden aan een device, gebruikt biometrisch of PIN
  - Werkt met Active Directory of Entra ID accounts

- Welke password problemen het oplost
  - Sterke wachtwoorden zijn moeilijk te onthouden, users hergebruiken wachtwoorden op meerdere sites
  - Server breaches kunnen symmetrische network credentials (wachtwoorden) blootleggen
  - Wachtwoorden zijn gevoelig voor replay attacks
  - Users kunnen wachtwoorden per ongeluk blootgeven via phishing

- Hoe het werkt, kernpunten 
  - Credentials gebaseerd op certificaat of asymmetrish key pair, gebonden aan het device; ook de token die je krijgt is device bound
  - Identity provider (AD, Entra ID, of Microsoft account) valideert identity en koppelt de Windows Hello public key aan een user account tijdens registratie
  - Keys gegenereerd in hardware (TPM 1.2 of 2.0 voor enterprises, TPM 2.0 voor consumers) of software, afhankelijk van policy
  - Two factor authentication = key/certificaat gebonden aan device + iets wat de persoon weet (PIN) of is (biometrisch)
  - Gesture roamt niet tussen devices, wordt niet gedeeld met de server
  - Biometrische templates blijven lokaal op het device opgeslagen, PIN wordt nooit opgeslagen of gedeeld
  - Private key verlaat het device nooit bij gebruik van TPM; de server heeft alleen de public key, gekoppeld tijdens registratie
  - PIN invoer of biometrisch gesture triggert het device om met de private key data te signeren die naar de identity provider gaat; die verifieert en authenticeert de user
  - Personal (Microsoft account) en corporate (AD of Entra ID) accounts gebruiken 1 container voor keys, gescheiden per identity provider domain voor privacy
  - Certificate private keys kunnen beschermd worden door de Windows Hello container en de gesture zelf

- Security groups voor deployment
  - Windows Server 2016 domain controllers aanwezig: gebruik de bestaande KeyAdmins group, sla KeyCredential Admins group aanmaken over
  - Zo niet: maak de KeyCredential Admins group zelf aan

- KeyCredential Admins group aanmaken
  - Doel: Entra Connect kan public keys op user objects toevoegen/verwijderen via deze group permissions
  - Stappen: inloggen als Domain Admin equivalent op domain controller of management workstation, Active Directory Users and Computers openen, View > Advanced Features, Users container > New > Group, naam KeyCredential Admins, OK

- Windows Hello for Business Users group aanmaken
  - Doel: gefaseerde uitrol vereenvoudigen, Group Policy en Certificate template permissions toewijzen aan deze group
  - Zelfde stappen als hierboven, naam Windows Hello for Business Users

- Microsoft Pluton Security Processor
  - TPM (Trusted Platform Module) is normaal een apart chip naast de CPU, bewaart keys en integriteitsmetingen, al 10+ jaar gebruikt (o.a. Windows Hello, BitLocker)
  - Aanvallers richten zich steeds vaker op de bus interface tussen CPU en TPM, vooral bij fysieke toegang tot een PC
  - Pluton bouwt security direct in de CPU, elimineert die aanvalbare bus interface
  - Pluton emuleert een TPM, werkt met bestaande TPM specs en APIs, dus bestaande TPM afhankelijke features (BitLocker, System Guard) werken meteen
  - Beschermt credentials, identities, encryption keys en persoonlijke data; niet te verwijderen zelfs met malware of volledige fysieke toegang
  - Gebouwd samen met AMD, Intel, Qualcomm en anderen
  - Gebruikt Security Hardware Cryptographic Key (SHACK)
  - Vervanging/upgrade van de TPM chip, gebaseerd op technologie uit Azure Sphere en Xbox security

- Onthouden voor examen
  - Windows Hello for Business is device bound, private key verlaat het device nooit
  - PIN en biometrische data blijven altijd lokaal, worden nooit naar de server gestuurd
  - Pluton lost het risico op van aanvallen op de communicatie tussen CPU en TPM, door security in de CPU zelf te bouwen

---

### Exercise: Configure and Deploy Self-Service Password Reset
  - [04-sc300/labs/13-configure-and-deploy-self-service-password-reset](../../04-sc300/labs/13-configure-and-deploy-self-service-password-reset.md)

---

### Deploy and manage password protection

- Wat het is
  - Voorkomt zwakke wachtwoorden (bv. schoolnaam, sportteam, bekende persoon) via een global en custom banned password list
  - Password change request faalt bij een match met de banned list

- Ontwerpprincipes (examen kernstof)
  - Domain controllers communiceren nooit direct met internet
  - Geen nieuwe netwerkpoorten geopend op DC's (Domain Controller)
  - Geen AD DS schema changes nodig
  - Geen minimum AD DS domain of forest functional level vereist
  - Geen accounts nodig in de beschermde AD DS domains
  - User clear text passwords verlaten de DC nooit
  - Niet afhankelijk van andere Entra features, bv. PHS is niet vereist
  - Incrementele uitrol mogelijk, policy wordt alleen afgedwongen waar de DC Agent geinstalleerd is

- Hoe het werkt (kort)
  - Proxy service en DC Agent maken elk een serviceConnectionPoint object aan in Active Directory
  - DC Agent zoekt een proxy service, vraagt daar een password policy op, proxy haalt die op bij Microsoft Entra
  - Policy wordt lokaal opgeslagen in de sysvol folder, DC Agent checkt elk uur of de policy ouder dan 1 uur is en ververst zo nodig
  - Bij een password change gebruikt de DC de gecachte policy om te accepteren of te weigeren

- Deployment strategie
  - Start altijd in Audit mode (default); zwakke wachtwoorden worden gelogd maar niet geblokkeerd
  - Tijdens audit periode: processen verbeteren, users informeren, minstens 1 DC promotion en 1 DC demotion testen
  - Na een redelijke audit periode: omzetten naar Enforce mode
  - Belangrijk: wachtwoorden die al bestonden voor deployment worden nooit met terugwerkende kracht gevalideerd, tot ze een keer gewijzigd worden. Accounts met "password never expires" blijven hier permanent buiten

- Multiple forest overwegingen
  - Geen extra vereisten voor multi forest deployment
  - Elke forest apart geconfigureerd, proxy ondersteunt alleen DC's uit de eigen forest
  - Forests weten niets van elkaars password protection configuratie, ook niet bij AD trust

- Read only domain controllers (RODC's)
  - Password events op RODC's worden doorgestuurd naar writable DC's
  - DC Agent hoeft niet op RODC's geinstalleerd te worden
  - Proxy service draaien op een RODC wordt niet ondersteund

- High availability
  - DC Agent gebruikt round robin tussen proxy servers, slaat niet reagerende proxies over
  - 2 proxy servers is meestal genoeg voor de meeste omgevingen
  - DC Agent houdt een lokale cache van de laatste policy aan, blijft die afdwingen ook als alle proxies onbereikbaar zijn
  - Policy updates gebeuren meestal maar eens in de paar dagen, dus korte proxy uitval is geen probleem

- Licensing requirements (examen kernstof)

| Users | Global banned password list | Custom banned password list |
|---|---|---|
| Cloud only users | Entra Free | Entra Premium P1 of P2 |
| Users gesynchroniseerd vanuit on premises AD DS | Entra Premium P1 of P2 | Entra Premium P1 of P2 |

- Kernvereisten voor deployment
  - Domain Admin acount nodig om de forest te registreren bij Entra
  - Key Distribution Service moet enabled zijn op Windows Server 2012 DC's
  - Netwerkconnectivteit tussen DC en proxy server nodig (RPC endpoint mapper poort 135 plus RPC server poort)
  - Proxy machines hebben toegang nodig tot login.microsoftonline.com en enterpriseregistration.windows.net

- DC Agent vereisten
  - Windows Server 2012 R2 of hoger
  - Geen minimum domain of forest functional level nodig
  - .NET 4.7.2 vereist
  - Domain moet DFSR gebruiken voor sysvol replicatie

- Proxy service vereisten
  - Windows Server 2012 R2 of hoger, proxy deployment is verplicht ook al heeft de DC zelf internet toegang
  - .NET 4.7.2 vereist
  - DC's moeten kunnen inloggen op de proxy via "Access this computer from the network" recht
  - Uitgaand TLS 1.2 HTTP verkeer moet toegestaan zijn
  - Global Administrator nodig voor de eerste proxy registratie in een tenant, daarna volstaat Security Administrator
  - Waarschuwing: proxy service en Application Proxy gebruiken verschillende versies van de Connect Agent Updater service, nooit samen op dezelfde machine installeren

- Installatie en upgrades (kort, praktisch)
  - 2 installers nodig: DC agent (msi) en proxy (exe)
  - DC Agent installatie vereist altijd een reboot, ook bij upgrade
  - Proxy upgrade vereist geen reboot, ondersteunt automatische upgrade via de Connect Agent Updater service
  - DC Agent kan alvast geinstalleerd worden op een machine die nog geen DC is, blijft dan inactief tot promotie

- Onthouden voor examen
  - Global banned list werkt al op Entra Free, custom banned list vereist altijd P1 of P2
  - Gesynchroniseerde on premises users vereisen altijd P1 of P2, ongeacht welke lijst
  - Audit mode eerst, dan pas Enforce mode
  - Bestaande wachtwoorden worden nooit met terugwerkende kracht afgekeurd

---

### Configure smart lockout thresholds

- Wat het is
  - Beschermt tegen brute force en password guessing aanvallen
  - Onderscheidt sign ins van valide users versus aanvallers/onbekende bronnen
  - Aanvallers worden gelockt, echte users blijven toegang houden

- Hoe het werkt (default settings)
  - Lockt account 1 minuut na 10 mislukte pogingen
  - Bij elke volgende mislukte poging: opnieuw locken, eerst 1 minuut, daarna oplopend
  - Exacte groeisnelheid van de lockout periode wordt niet openbaar gemaakt, om workarounds door aanvallers te bemoeilijken
  - Tracked de laatste 3 foute password hashes; hetzelfde foute wachtwoord meerdere keren invoeren verhoogt de lockout counter niet

- Federated deployments
  - AD FS 2016 en 2019 kunnen vergelijkbare bescheming krijgen via AD FS Extranet Lockout en Extranet Smart Lockout

- Licentie (examen relevant)
  - Smart lockout staat altijd aan, voor alle Entra ID klanten, met default instellingen
  - Custom instellingen (eigen waarden) vereisen Entra ID Premium P1 of hoger

- Belangrijk: geen garantie
  - Smart lockout garandeert niet dat een echte user nooit gelockt wordt, probeert dit wel zoveel mogelijk te voorkomen
  - Elk Entra datacenter trackt lockouts onafhankelijk; user heeft in theorie threshold_limit maal datacenter_count aan pogingen als alle datacenters geraakt worden
  - Onderscheid tussen bekende en onbekende locatie, met elk hun eigen lockout counter

- Hybrid integratie (PHS of PTA)
  - Smart lockout policies in Entra ID kunnen aanvallen filteren voordat ze on premises AD DS bereiken
  - Beschermt on premises accounts tegen lockout door aanvallers

- Configuratie regels bij pass-through authentication (examen kernstof)
  - Entra lockout threshold moet lager zijn dan AD DS lockout threshold; AD DS threshold minstens 2 tot 3 keer groter dan de Entra threshold
  - Entra lockout duration moet langer zijn dan AD DS lockout duration; Entra duration in seconden, AD duration in minuten
  - Voorbeeld: Entra duration 120 seconden (2 minuten), AD DS duration 60 seconden (1 minuut). Entra threshold 5, AD DS threshold 10
  - Doel van deze configuratie: smart lockout vangt brute force aanvallen op voordat on premises AD accounts zelf gelockt raken

- Onthouden voor examen
  - Default: 10 pogingen, 1 minuut lockout, daarna oplopend
  - Custom smart lockout settings vereisen P1 of hoger
  - Bij PTA: Entra threshold lager dan AD threshold, Entra duration langer dan AD duration; dit zorgt dat Entra als eerste linie van verdediging werkt

---

### Exercise: Configure and Deploy Self-Service Password Reset
  - [04-sc300/labs/14-manage-microsoft-entra -mart-lockout-values](../../04-sc300/labs/14-manage-microsoft-entra-mart-lockout-values.md)

---

### Implement Kerberos and certificate-based authentication in Microsoft Entra ID

- Context
  - SSO voor on premises apps via Application Proxy
  - Apps zijn beveiligd met integrated Windows authentication, hebben een Kerberos ticket nodig
  - Application Proxy gebruikt Kerberos Constrained Delegation (KCD) om dit te ondersteunen
  - Application Proxy connectors krijgen permissie in Active Directory om users te impersoneren, zodat ze namens de user tokens kunnen versturen en ontvangen

- Kerberos authentication flow (examen kernstof, stappen)
  1. User voert de URL in om via Application Proxy bij de on premises app te komen
  2. Application Proxy stuurt het verzoek naar Entra authentication services voor preauthenticatie; Entra ID past policies toe (bv. MFA); bij succes maakt Entra ID een token en stuurt die naar de user
  3. User geeft de token door aan Application Proxy
  4. Application Proxy valideert de token en haalt de UPN (User Principal Name) eruit; de Connector haalt UPN en SPN (Service Principal Name) op via een dubbel geauthenticeerd secure channel
  5. Connector doet KCD onderhandeling met on premises AD, impersoneert de user om een Kerberos token voor de app te krijgen
  6. Active Directory stuurt het Kerberos token voor de app naar de Connector
  7. Connector stuurt het originele verzoek naar de app server, met het Kerberos token van AD
  8. App stuurt de response terug naar de Connector, die teruggaat naar Application Proxy en uiteindelijk naar de user

- Vereisten om de omgeving klaar te maken (examen relevant)
  - Apps (bv. SharePoint) moeten integrated Windows authentication gebruiken
  - Alle apps moeten een Service Principal Name (SPN) hebben
  - De server met de Connector en de server met de app moeten beide domain joined zijn
  - De Connector server moet het TokenGroupsGlobalAndUniversal attribuut van users kunnen lezen

- Onthouden voor examen
  - KCD (Kerberos Constrained Delegation) is de kern technologie die dit mogelijk maakt
  - Connector impersoneert de user om namens hen een Kerberos token te krijgen, niet de user zelf die rechtstreeks met AD praat
  - Preauthenticatie en policies (bv. MFA) gebeuren altijd eerst via Entra ID, voordat de Kerberos flow met on premises AD start

---

### Configure Microsoft Entra user authentication for virtual machines

- Wat het is
  - Entra ID integreren als core authentication platform voor Windows en Linux VM's in Azure
  - Ondersteund voor: Windows Server 2022, 2025 of later met Desktop Experience, Windows 11 24H2 of later, Linux VM's
  - Centraal RBAC en Conditional Access policies toepassen om toegang tot VM's toe te staan of te blokkeren

- Voordelen
  - Inloggen op Windows VM's met Entra credentials
  - Minder afhankelijkheid van local administrator accounts
  - Password complexity en lifetime policies via Entra ID zelf
  - Conditional Access mogelijk voor MFA, risky user, sign in risk, etc.

- Windows VM configureren (2 stappen)
  1. Microsoft Entra sign in optie inschakelen voor de VM
  2. Azure role assignments configureren voor users die mogen inloggen op de VM

- Linux VM configureren (voorbeeld met Ubuntu Server 18.04 LTS)
  1. Azure portal > + Create a resource
  2. Create onder Ubuntu Server 18.04 LTS
  3. Management tab > vinkje bij "Login with Microsoft Entra ID"
  4. System assigned managed identity aanvinken
  5. VM setup afronden

- Onthouden voor examen
  - Werkt voor zowel Windows als Linux VM's
  - Vereist naast het inschakelen van Entra sign in ook een Azure role assignment voor wie mag inloggen
  - System assigned managed identity is een vereiste stap bij Linux VM's
 
---

## Module Assessment — Module 2 (Manage user authentication)

**Score:** 100%

### Vraag 1
Which of these authentication methods offers the highest level of security?

- SMS verification
- ✅ Microsoft Authenticator App
- Voice call verification

### Vraag 2
In the answer list, which is a security group used by Hybrid Windows Hello for Business when no Windows Server 2016 or later domain controllers are deployed?

- ✅ KeyCredential Admins
- Enterprise Key Admins
- Windows Authorization Access Group

### Vraag 3
Which is the recommended mode to start with when deploying Microsoft Entra Password Protection?

- ✅ Audit mode
- None
- Enforced mode

---
---

## Learning Path 2: Implement an authentication and access management solution
### Module 3: Plan, implement, and administer Conditional Access

### Introduction

- Wat Conditional Access is
  - Fijnmazige controle over welke users/identities specifieke activiteiten mogen uitvoeren, resources mogen benaderen, en data/systemen veilig houden
  - Met Microsoft Entra Agent ID: dezelfde Zero Trust principes worden nu ook toegepast op AI agent identities, net als op users en workload identities

- Learning objectives
  - Plan and implement security defaults
  - Plan Conditional Access policies
  - Implement Conditional Access policy controls and assignments (targeting, applications, and conditions)
  - Test and troubleshoot Conditional Access policies
  - Implement application controls
  - Implement session management
  - Configure continuous access evaluation
  - Identify how agent identities are protected using Conditional Access

---

### Plan security defaults

- Wat het is
  - Gratis, vooraf geconfigureerde security instellingen die Microsoft namens organisaties beheert
  - Bedoeld voor organisaties die nog geen eigen identity security strategie hebben
  - Onderdeel van: MFA registratie verplicht voor alle users, MFA verplicht voor admins, legacy authentication protocols geblokkeerd, MFA when necessary, bescherming van privileged activities (bv. Azure portal toegang)

- Beschikbaarheid
  - Gratis voor iedereen, ongeacht licentie
  - Tenants aangemaakt op of na 22 oktober 2019 hebben security defaults mogelijk al standaard aan
  - Alle nieuwe tenants krijgen security defaults automatisch bij creatie
  - In/uitschakelen: Entra admin center, minimaal Conditional Access Administrator rol, via Entra ID > Overview > Properties > Manage security defaults

- Voor wie wel/niet (examen relevant)
  - Wel geschikt: organisaties die security willen verbeteren maar niet weten waar te beginnen; organisaties op de gratis Entra ID tier
  - Niet geschikt: organisaties die al Conditional Access policies gebruiken; organisaties met Entra ID Premium licenties; organisaties met complexe security vereisten die Conditional Access nodig hebben

- Policies die worden afgedwongen

  - Unified MFA registration
    - Alle users moeten MFA registreren via Microsoft Authenticator app
    - Geen grace period, direct verplicht bij volgende sign in
    - Gebruikt number matching: user voert een getal op scherm in via de Authenticator app, voorkomt MFA fatigue aanvallen

  - Protecting administrators
    - Privileged accounts moeten extra beschermd worden, MFA vereist bij elke sign in na registratie
    - Geldt voor deze rollen: Global Administrator, Application Administrator, Authentication Administrator, Authentication Policy Administrator, Billing Administrator, Cloud Application Administrator, Conditional Access Administrator, Exchange Administrator, Helpdesk Administrator, Identity Governance Administrator, Password Administrator, Privileged Authentication Administrator, Privileged Role Administrator, Security Administrator, SharePoint Administrator, User Administrator

  - Protecting all users
    - Niet alleen admins zijn doelwit, aanvallers richten zich vaak op gewone end users
    - Eenmaal binnen kunnen aanvallers namens die user toegang aanvragen tot gevoelige info, of de hele directory downloaden voor phishing
    - MFA voor iedereen beschermt alle apps geregistreerd bij Entra ID, incl. SaaS apps

  - Blocking legacy authentication
    - Legacy authentication = requests van clients zonder modern authentication (bv. Office 2010) of via mail protocollen zoals IMAP, SMTP, POP3
    - Ondersteunt geen MFA, ook niet als een MFA policy actief is; aanvallers kunnen legacy protocollen gebruiken om MFA te omzeilen
    - Meeste succesvolle aanvallen komen via legacy authentication
    - Security defaults blokeert alle legacy authentication requests, incl. Exchange Active Sync basic authentication

- Onthouden voor examen
  - Security defaults zijn gratis en altijd beschikbaar, Conditional Access vereist P1
  - Security defaults en Conditional Access sluiten elkaar praktisch uit; als je Conditional Access gebruikt, gebruik je meestal geen security defaults meer
  - MFA registratie via security defaults heeft geen grace period
  - Legacy authentication is de meest voorkomende bron van succesvolle aanvallen, en wordt volledig geblokkeerd door security defaults

---

### Exercise: Work with security defaults
  - [04-sc300/labs/15-work-with-security-defaults](../../04-sc300/labs/15-work-with-security-defaults.md)

---

### Plan Conditional Access policies

- Waarom plannen belangrijk is
  - Users benaderen resources overal, met verschillende devices en apps
  - Focus niet alleen op wie toegang heeft, maar ook waar, met welk device, tot welke resource

- Wat Conditional Access (CA) doet
  - Analyseert signalen (user, device, locatie) om toegang te automatiseren en policies af te dwingen
  - Kan bv. MFA vereisen wanneer nodig, en users met rust laten wanneer niet nodig
  - Biedt meer granulariteit dan security defaults

- Voordelen (examen kernstof)
  - Productiviteit; alleen onderbreken met MFA als signalen dat rechtvaardigen
  - Risk management; automatische detectie en remediatie/blokkade van risky sign ins, vooral in combinatie met Identity Protection
  - Compliance en governance; audit van app toegang, terms of use, restricties op basis van compliance policies
  - Kostenbeheer; minder afhankelijkheid van custom of on premises CA oplossingen
  - Zero Trust; helpt richting een zero trust omgeving

- Structuur van een CA policy (IF THEN, examen kernstof)
  - Assignments; users/groups, cloud apps/acties, conditions waaronder de policy geldt
  - Access controls; grant of block toegang, bv. MFA vereisen, compliant device, hybrid joined device
  - Session controls; app enforced permissions, Conditional Access App Control

- Vragen die je jezelf stelt bij het opzetten
  - Users and Groups; wie zit in scope, alle users, specifieke groep, directory roles, external users
  - Cloud apps or actions; welke apps, welke user acties
  - Conditions; welke device platforms, welke trusted locations
  - Access controls; MFA, compliant devices, hybrid joined devices
  - Session controls; app enforced permissions, App Control

- Agent identities en CA
  - Met Microsoft Entra Agent ID zijn agent identities nu first class principals in Entra ID
  - Kunnen net als users of service principals getarget worden door CA policies
  - Zelfde Zero Trust controls toepasbaar op AI agents als op mensen
  - Behandel agent identities zoals workload identities: policies scopen per identity type, juiste access controls afdwingen, emergency/trusted agents uitzonderen waar nodig

- Access token issuance
  - Access tokens laten clients veilig protected web APIs benaderen, gebruikt voor authenticatie en autorisatie
  - Format niet vastgelegd door OAuth spec, varieert per identity provider
  - Belangrijk: als geen assignment van toepassing is en geen CA policy van kracht is, wordt standaard een token uitgegeven
  - Voorbeeld: policy zegt IF user in Group 1, THEN MFA vereist voor App 1. Een user buiten Group 1 die de app benadert voldoet niet aan de IF conditie, dus krijgt gewoon een token; om die users echt te blokkeren is een aparte policy nodig

- Best practices

- Emergency access accounts
  - Verkeerd geconfigureerde policy kan de organisatie buitensluiten van de Azure portal
  - Mitigatie: minstens 2 emergency access accounts aanmaken

- Report only mode
  - Laat je CA policies evalueren voordat ze echt geactiveerd worden
  - Handig bij impactvolle wijzigingen: legacy authentication blokkeren, MFA vereisen, sign in risk policies

- Landen uitsluiten waar nooit sign ins vandaan komen
  - Named location aanmaken met alle onverwachte landen
  - Policy maken die sign in vanuit die named location blokkeert voor alle apps
  - Admins altijd uitzonderen van deze policy

- Veelvoorkomende policy types
  - MFA vereisen; voor admins, specifieke apps, alle users, of onvertrouwde netwerklocaties
  - Reageren op mogelijk gecompromitteerde accounts; 3 default policies: alle users MFA laten registreren, password change vereisen bij high risk users, MFA vereisen bij medium/high sign in risk
  - Managed devices vereisen; voor resources die niet vanaf onbekende devices benaderd mogen worden
  - Approved client applications vereisen; relevant bij BYOD, alleen data beschermen i.p.v. het hele device
  - Access blokkeren; overschrijft alle andere assignments, kan hele organisatie blokkeren. Voorbeeld: app migratie naar Entra ID nog niet klaar voor gebruik. Let op: bij een blokkerende policy altijd emergency accounts en overweeg alle admins uit te sluiten

- Policies bouwen en testen
  - Elke fase van deployment evalueren of resultaten kloppen
  - Gefaseerde uitrol: communiceren naar users, starten met kleine groep, admins blijven uitgesloten tijdens uitbreiding, pas na grondig testen toepassen op alle users
  - Altijd minstens 1 admin account behouden waar de policy niet op van toepassing is

- Test users aanmaken
  - Set van test users die de productieomgeving weerspiegelen
  - Sommige organisaties gebruikn aparte test tenants, maar dat maakt het moeilijk om alle condities/apps volledig te simuleren

- Testplan opstellen
  - Vergelijking tussen verwacht en daadwerkelijk resultaat, altijd vooraf een verwachting vastleggen
  - Voorbeelden: MFA vereisen op trusted locatie (geen MFA prompt) vs niet trusted locatie (wel MFA prompt), Global Admin altijd MFA, risky sign in via unapproved browser triggert MFA, managed vs unmanaged device (toegang wel/niet), risky sign in met gecompromitteerde credentials triggert

---

### Implement Conditional Access policy controls and assignments

- Wat het is
  - Geavanceerde Entra ID capability voor gedetailleerde policies wie toegang krijgt
  - Baseert beslissingen op group membership, device compliance, netwerk locatie, sign in risk

- Basis stappen om een CA policy aan te maken
  1. Entra admin center, minimaal Conditional Access Administrator
  2. Protection > Conditional Access > + New policy
  3. Naam geven
  4. Assignments configureren; users/groups/roles
  5. Target resources configureren; cloud apps of user actions
  6. Conditions toevoegen; sign in risk, device platform, locatie
  7. Access controls; Grant of Session controls
  8. Enable policy op Report only zetten om eerst te testen, dan Create
  - Aanbevolen: altijd starten in report only mode, sign in logs monitoren voordat je op On zet

- Sign in risk based Conditional Access
  - Sign in risk = kans dat een authenticatie poging niet door de echte owner is gedaan
  - Vereist Entra ID Premium P2, gebruikt Identity Protection sign in risk detections
  - Toewijsbaar via Conditional Access zelf of via Identity Protection

- User risk based Conditional Access
  - Microsoft vindt gelekte username/password paren via onderzoekers, wetshandhaving, security teams
  - Vereist ook P2, gebruikt Identity Protection user risk detections
  - Zelfde toewijs opties als sign in risk

- Securing security info registration
  - User actions in CA policy kunnen beperken wanneer/hoe users MFA en SSPR registreren
  - Preview feature, vereist combined registration preview enabled
  - Voorbeeld: alleen registratie toestaan vanaf trusted network location

- Voorbeeld: registratie alleen vanaf trusted locatie (stappen)
  1. Protection > Conditional Access > + Create new policy
  2. Naam geven
  3. Assignments > Users and groups > include gewenste users/groups, exclude emergency/break glass accounts
  4. Cloud apps or actions > User actions > Register security information
  5. Conditions > Locations > Yes > Include Any location > Exclude All trusted locations
  6. Conditions > Client apps (Preview) > Yes
  7. Access controls > Grant > Block access
  8. Enable policy On > Save

- Let op: agent identities i.p.v. users
  - Als je AI agents target in plaats van users, kies je Workload identities bij Assignments en seletceer je de agent identity via Microsoft Entra Agent ID
  - Rest van de policy structuur blijft hetzelfde

- Alternatief voor locatie: device state
  - Conditions > Device state (Preview) > Yes > Include All device state > Exclude Hybrid Entra joined en/of marked as compliant

- Block access by location
  - Locatie conditie gebruikt om toegang te blokkeren vanuit landen/regio's waar nooit legitiem verkeer vandaan komt

- Named location aanmaken (stappen)
  1. Protection > Conditional Access > Named locations > New location
  2. Naam geven
  3. IP ranges of Countries/Regions kiezen, evt. unknown areas meenemen
  4. Save

- Policy aanmaken om die locatie te blokkeren (stappen)
  1. Conditional Access > + Create new policy, naam geven
  2. Assignments > Users and groups > Include All users, Exclude emergency accounts
  3. Cloud apps or actions > Include All cloud apps
  4. Conditions > Location > Yes > Include Selected locations > de geblokkeerde locatie kiezen
  5. Access controls > Block Access
  6. Enable policy On > Create

- Compliant devices vereisen
  - Vereist Intune, compliance criteria zoals PIN vereist, encryption vereist, min/max OS versie, geen jailbreak/root
  - Compliance info gaat naar Entra ID, CA gebruikt dit om te grant/blocken

- Policy voor compliant devices (stappen)
  1. Conditional Access > + Create new policy, naam geven
  2. Assignments > Users and groups > Include All users, Exclude emergency accounts
  3. Cloud apps or actions > Include All cloud apps, evt. specifieke apps excluden
  4. Conditions > Client apps (Preview) > defaults laten staan
  5. Access controls > Grant > Require device to be marked as compliant
  6. Enable policy On > Create

- Belangrijk
  - Vereisen van compliant device blokkeert geen Intune enrollment zelf, ook al staat de policy op All users/All cloud apps

- Bekend gedrag
  - Op Windows 7, iOS, Android, macOS en sommige third party browsers gebruikt Entra ID een client certificate voor device identificatie
  - Bij eerste sign in via browser moet de user dit certificate zelf selecteren

- Block access (all)
  - Optie voor organisaties met conservatieve cloud migratie aanpak
  - Waarschuwing: misconfiguratie kan de hele organisatie buitensluiten van de Azure portal
  - Gebruik report only mode en de What If tool voor testen voordat je activeert

- User exclusions (examen kernstof)
  - Emergency/break glass accounts; voorkomt tenant wide lockout
  - Service accounts/service principals (bv. Entra Connect Sync Account); niet interactief, MFA kan niet programmatisch voltooid worden, dus uitsluiten. Beter alternatief: managed identities gebruiken i.p.v. losse accounts
  - Agent identities; AI agents in Microsoft Entra Agent ID kunnen getarget of uitgesloten worden net als service principals. Trusted agents die ononderbroken toegang nodig hebben expliciet uitsluiten, agent policies samen met workload identity policies reviewen

- Conditional Access Terms of Use (TOU)
  - Aanmaken via Identity Governance > Terms of use, vereist een PDF met de voorwaarden
  - Regels instelbaar: wanneer terms verlopen, of user ze moet openen voor accepteren
  - Kan direct gekoppeld worden aan een conditional rule in Identity Governance, of gebruikt worden als Conditional Access control
  - Doel: consent afdwingen voor toegang tot bepaalde cloud apps, consent kan laten verlopen of terms wijzigen en opnieuw laten accepteren

- Onthouden voor examen
  - Sign in risk en user risk based CA vereisen beide P2 en Identity Protection
  - Emergency accounts, service accounts/principals, en nu ook agent identities horen standaard uitgesloten te worden van brede policies
  - Compliant device requirement blokkeert geen Intune enrollment
  - Altijd eerst report only mode en What If tool gebruiken voordat een policy live gaat

---

### Exercise: Implement conditional access policies roles and assignments
  - [04-sc300/labs/16-implement-conditional-access-policies-roles-and-assignments](../../04-sc300/labs/16-implement-conditional-access-policies-roles-and-assignments.md)

---

### Test and troubleshoot Conditional Access policies

- Risicovolle configuraties om te vermijden (examen kernstof)
  - Voor all users, all cloud apps
    - Block access; blokkeert de hele organisatie
    - Require Hybrid Entra domain joined device; kan iedereen blokkeren die geen hybrid joined device heeft
    - Require app protection policy; kan iedereen blokkeren zonder Intune policy, incl. jezelf als admin, waardoor je niet eens meer bij Intune/Azure portal kunt
  - Voor all users, all cloud apps, all device platforms
    - Block access; blokkeert de hele organisatie

- Troubleshooten van een sign in interrupt (2 methodes)

- Methode 1: het error bericht zelf
  - Foutpagina in de browser geeft vaak al gedetailleerde info en een suggestie voor oplossing
  - Voorbeeld: melding dat de app alleen toegankelijk is vanaf devices/apps die aan het mobile device management beleid voldoen

- Methode 2: Microsoft Entra sign in events
  - Meer detail te vinden via More Details op de foutpagina zelf
  - Stappen om de juiste policy te vinden:
    1. Entra admin center, als Security Administrator of Global Reader
    2. Identity > Monitoring and Health > Sign ins
    3. Event zoeken, filteren op Correlation ID, Conditional access (scope naar failures), Username, Date
    4. Conditional Access tab openen bij het juiste event, toont welke policy/policies de interrupt veroorzaakten
    5. Troubleshooting and support tab geeft de exacte reden (bv. device voldeed niet aan compliance)
    6. Policy Name aanklikken opent de policy configuratie zelf, voor review/aanpassing
    7. Extra context beschikbaar in Basic Info, Location, Device Info, Authentication Details, Additional Details tabs

- Policy details (ellipsis menu)
  - Geeft extra info waarom een policy wel of niet werd toegepast
  - Links: details verzameld tijdens sign in. Rechts: of die details voldoen aan de vereisten van de toegepaste policy
  - Belangrijk: een CA policy wordt alleen toegepast als alle conditions voldaan zijn, of niet geconfigureerd zijn

- Support incident openen
  - Als de event info niet genoeg is: Troubleshooting and support tab > Create a new support request
  - Geef request ID en datum/tijd van het sign in event mee, zodat Microsoft support het juiste event kan terugvinden

- Onthouden voor examen
  - De grootste valkuil is een policy die op All users + All cloud apps staat met een blokkerende control, dat kan de hele organisatie of jezelf als admin buitensluiten
  - Sign in logs met de Conditional Access tab zijn de primaire troubleshooting tool, niet alleen de foutmelding zelf
  - CA policy wordt alleen toegepast als alle conditions matchen of niet geconfigureerd zijn

---

### Implement application controls

- Conditional Access App Control
  - Monitort en controleert app toegang en sessions in real time, gebaseerd op access en session policies
  - Access/session policies worden geconfigureerd in Microsoft Defender for Cloud Apps
  - Gebruikt een reverse proxy architectuur, uniek geintegreerd met Conditional Access
  - CA bepaalt de conditions (wie, welke apps, welke locaties/netwerken), en routeert users vervolgens naar Defender for Cloud Apps voor de daadwerkelijke acces/session controls

- Wat je ermee kunt (examen kernstof)
  - Data exfiltratie voorkomen; bv. download/cut/copy/print blokkeren van gevoelige documenten op unmanaged devices
  - Protect on download; document labelen en beschermen met Azure Information Protection i.p.v. download volledig blokkeren
  - Upload van ongelabelde bestanden voorkomen; bestand moet eerst juiste label/protection krijgen voordat upload wordt toegestaan
  - Monitoren van user sessions voor compliance; risky users volgen, acties loggen binnen de sessie
  - Access blokkeren; granulair blokkeren op basis van riscofactoren, bv. als client certificates gebruikt worden als device management
  - Custom activities blokkeren; bv. berichten met gevoelige content scannen en blokkeren in Teams of Slack

- Approved client app vereisen (2 voorbeeldscenario's, Contoso)
  - Beide scenario's vereisen Entra ID Premium P1 of P2 plus Intune
  - Scenario 1: alle M365 services toegankelijk op mobiel, mits approved client app (Outlook mobile, OneDrive, Teams)
  - Scenario 2: alleen Exchange Online en SharePoint Online toegankelijk op mobiel, mits approved client app

- Scenario 1, stap 1: policy voor Android/iOS modern authentication clients bij Exchange Online
  1. Conditional Access > Create new policy, naam geven
  2. Assignments > Users and groups > Include All users of specifieke users/groups
  3. Cloud apps or actions > Include Office 365
  4. Conditions > Device platforms > Yes > Include Android en iOS
  5. Conditions > Client apps (preview) > Yes > Mobile apps and desktop clients + Modern authentication clients
  6. Access controls > Grant > Grant access > Require approved client app
  7. Enable policy On > Create

- Scenario 1, stap 2: policy voor Exchange ActiveSync (EAS)
  1. Zelfde als hierboven, maar Cloud apps or actions > Office 365 Exchange Online
  2. Conditions > Client apps (preview) > Yes > Mobile apps and desktop clients + Exchange ActiveSync clients
  3. Access controls > Require approved client app > Enable policy On > Create

- Scenario 1, stap 3: Intune app protection policy configureren voor iOS/Android (los proces, zie aparte documentatie)

- Scenario 2, stap 1: policy voor Exchange Online + SharePoint Online, modern authentication clients
  - Zelfde structuur als scenario 1 stap 1, maar Cloud apps or actions > Office 365 Exchange Online + Office 365 SharePoint Online

- Scenario 2, stap 2: policy voor Exchange ActiveSync clients
  - Zelfde als scenario 1 stap 2

- Scenario 2, stap 3: Intune app protection policy (zelfde als scenario 1)

- App protection policies (APP) overzicht
  - Regels die organisatiedata veilig houden binnen een managed app
  - Kan een rule zijn bij toegang/verplaatsen van corporate data, of acties die verboden/gemonitord worden binnen de app
  - Onderdeel van Mobile Application Management (MAM)
  - MAM-WE (without enrollment); werk/school app met gevoelige data beheerbaar op bijna elk device, ook BYOD, zonder dat het device zelf enrolled hoeft te zijn
  - Veel productivity apps (bv. Microsoft Office apps) ondersteunen dit via Intune MAM

- Waarom app protection policies
  - Voorkomt data loss (intentioneel en onintentioneel) op devices die je niet beheert
  - Werkt onafhankelijk van MDM; bescherming met of zonder device enrollment
  - App level policies beperken toegang tot company resources, data blijft binnen bereik van IT

- Op welke devices toepasbaar
  - Enrolled in Intune; meestal corporate owned
  - Enrolled in thrid party MDM; meestal corporate owned
  - Niet enrolled in enige MDM; meestal employee owned/BYOD
  - Let op: MAM policies niet combineren met third party MAM of secure container oplossingen
  - Belangrijk: Outlook voor iOS/iPadOS en Android met hybrid Modern Authentication kan on premises Exchange mailboxes beschermen via Intune app protection; andere apps die met on premises Exchange/SharePoint verbinden worden niet ondersteund

- Voordelen van app protection policies (examen kernstof)
  - Bescherming op app niveau, werkt op zowel managed als unmanaged devices, identity centered i.p.v. device centered
  - Geen impact op end user productivity in personal context; policy geldt alleen in work context
  - App layer protections: bv. PIN vereist om app te openen in work context, controle over data sharing tussen apps, voorkomen dat company data naar personal storage wordt opgeslagen
  - MDM (naast MAM) beschermt ook het device zelf; bv. PIN voor het hele device, apps deployen via MDM

- MAM met en zonder MDM combineren
  - Kan tegelijk gebruikt worden; bv. bedrijfstelefoon enrolled in MDM + app protection, persoonlijke tablet alleen app protection
  - MAM policy zonder device state setting geldt op zowel BYOD als Intune managed devices
  - Kan ook gescopet worden op device managed state: minder strikte MAM policy voor Intune managed devices, strengere MAM policy voor niet enrolled devices, of MAM alleen voor unenrolled devices. Hiervoor zet je bij het aanmaken van de policy "Target to all app types" op No

- Onthouden voor examen
  - Conditional Access App Control werkt via Defender for Cloud Apps, niet los binnen Conditional Access zelf
  - Approved client app policies vereisen altijd P1/P2 plus Intune
  - App protection policies (MAM) zijn onafhankelijk van device enrollment, in tegenstelling tot MDM
  - MAM en MDM kunnen gecombineerd worden, met verschillende striktheid per device managed state

  ---

### Implement session management and continuous access evaluation

- Waarom session management
  - Sommige scenario's vragen om beperkte auth sessies: unmanaged/shared device, gevoelige info vanaf extern netwerk, high priority/executive users, kritieke business apps
  - CA controls laten je policies maken die specifieke use cases targeten, zonder alle users te raken

- User sign in frequency
  - Bepaalt hoe lang het duurt voordat een user opnieuw moet inloggen
  - Default in Entra ID: rolling window van 90 dagen
  - Te vaak om credentials vragen is niet altijd veiliger; users die gewend zijn om zonder nadenken in te loggen kunnen makkelijker slachtoffer worden van een phishing prompt
  - Elke policy violation revoked de sessie sowieso, ongeacht sign in frequency: password change, incompliant device, account disabled. Kan ook expliciet via PowerShell
  - Kernidee: geen credentials vragen zolang de security posture van de sessie niet veranderd is

- Welke apps dit ondersteunen
  - Werkt met apps die OAuth2 of OIDC correct implementeren; de meeste Windows, Mac en mobile apps, incl. web apps zoals Word/Excel/PowerPoint Online, OneNote Online, Office.com, M365 Admin portal, Exchange Online, SharePoint/OneDrive, Teams web client, Dynamics CRM Online, Azure portal
  - Werkt ook met SAML apps, mits ze geen eigen cookies droppen en regelmatig terug redirecten naar Entra ID voor authenticatie

- Sign in frequency en MFA
  - Vroeger alleen van toepassing op first factor authentication bij Entra joined, hybrid joined, en Entra registered devices
  - Op basis van klantfeedback: sign in frequency geldt nu ook voor MFA zelf

- Sign in frequency en device identities
  - Unlock van een device of interactief inloggen telt ook als sign in event voor de policy
  - Voorbeeld 1: user werkt continu door, wordt na 1 uur (ingestelde frequency) gevraagd opnieuw in te loggen
  - Voorbeeld 2: user pauzeert en locked het device, unlock telt als nieuw sign in moment, dus de 1 uur telt vanaf dat moment opnieuw

- Persistence van browsing sessions
  - Persistent browser session: user blijft ingelogd na sluiten/heropenen van de browser
  - Default: op personal devices krijgt de user een 'Stay signed in?' prompt na succesvolle authenticatie, user kiest zelf

- Validatie
  - What If tool simuleert een sign in voor een user naar een target app onder bepaalde conditions
  - Toont de session management controls die van toepassing zouden zijn

- Policy deployment
  - Best practice: eerst testen voordat je uitrolt naar productie, idealiter in een test tenant

- Continuous Access Evaluation (CAE)
  - Access tokens zijn standaard 1 uur geldig, daarna refresh via Entra ID; dat refresh moment is een kans om policies opnieuw te evalueren
  - Probleem: er zit vertraging tussen een wijziging in de situatie van de user en het daadwerkelijk afdwingen van policy wijzigingen
  - CAE lost dit op via een "conversation" tussen token issuer (Entra ID) en de relying party (de app): de app kan wijzigingen (bv. netwerklocatie) doorgeven, en Entra ID kan de app vertellen om tokens niet langer te vertrouwen (bv. bij account compromise of disablement)

- Voordelen van CAE (examen kernstof)
  - User termination of password change/reset; sessie wordt near real time revoked
  - Netwerklocatie wijziging; Conditional Access location policies worden near real time afgedwongen
  - Token export naar een machine buiten een trusted network kan voorkomen worden via CA location policies

- Evaluation en revocation flow (stappen, examen kernstof)
  1. CAE (Continuous Access Evaluation) capable client vraagt met credentials of refresh token een access token aan bij Entra ID
  2. Access token wordt teruggegeven aan de client
  3. Admin revoked expliciet alle refresh tokens voor de user; revocation event gaat naar de resource provider
  4. Client biedt access token aan bij de resource provider; die checkt geldigheid en of er een revocation event is
  5. Resource provider weigert toegang, stuurt een 401+ claim challenge terug naar de client
  6. CAE capable client herkent de 401+ challenge, negeert caches, en start opnieuw bij stap 1 met refresh token + claim challenge; Entra ID herevalueert alle conditions en laat de user opnieuw authenticaten

- Onthouden voor examen
  - Sign in frequency default = 90 dagen rolling window, geldt nu ook voor MFA, niet alleen first factor
  - Policy violations (password change, incompliant device, disabled account) revoken de sessie sowieso, los van de ingestelde frequency
  - CAE lost de vertraging op tussen wijziging en handhaving via een 401+ claim challenge flow, in plaats van te wachten op de normale 1 uur token refresh

---

### Exercise: Configure authentication session controls
  - [04-sc300/labs/17-configure-authentication-session-controls](../../04-sc300/labs/17-configure-authentication-session-controls.md)

---

### Microsoft Entra Conditional Access Optimization Agent

  - Overzicht
    - De Conditional Access optimization agent helpt organisaties om Conditional Access policies te verbeteren en te zorgen dat alle gebruikers correct beschermd worden. De agent doet aanbevelingen op basis van Zero Trust‑principes en Microsoft best practices.

  - Functionaliteit
    - Evaluatie van MFA‑dekking: Controleert of alle gebruikers onder een MFA‑policy vallen en kan bestaande policies automatisch aanpassen.

  - Device-based controls: Handhaaft device compliance, app protection policies en domain-joined device vereisten.

  - Blokkeren van legacy authentication: Detecteert accounts die nog legacy auth gebruiken en blokkeert deze.

  - Policy consolidatie: Identificeert overlappende policies en stelt samenvoeging voor.

  - Blokkeren van device code flow: Controleert of er een policy is die device code flow blokkeert.

  - one-click remediation: Aanbevelingen kunnen direct worden toegepast via *Apply suggestion*.

  - Vereisten
    - Microsoft Entra ID Premium P1  
    - Security Compute Units (SCU) beschikbaar  
    - Security Administrator (of hoger) voor eerste activatie  
    - Conditional Access Administrators kunnen toegang krijgen tot Security Copilot  
    - Device-based controls vereisen Microsoft Intune licenties

- Wat de agent doet
  - Scant de tenant op nieuwe gebruikers en applicaties  
  - Controleert of Conditional Access policies van toepassing zijn  
  - Past policies automatisch aan wanneer nodig  
  - Helpt organisaties richting Zero Trust configuraties

---

## Module Assessment — Conditional Access Optimization Agent

**Score:** 100%

### Vraag 1
What does Conditional Access do?

- It's the component that enforces multifactor authentication policies for access.
- ✅ It analyzes signals such as user, device, and location to enforce organizational access policies.
- It monitors and logs all access attempts.

### Vraag 2
When would you use Mobile Application Management (MAM) without enrollment to protect sensitive data in a work or school-related app?

- ✅ Bring-your-own-device (BYOD) scenarios
- Smart lockout policies
- Session management controls

### Vraag 3
What is user sign-in frequency?

- ✅ User sign-in frequency defines the time period before a user is asked to sign in again when attempting to access a resource.
- User sign-in frequency defines the number of times a user signs in from a single device in a 24-hour period
- User sign-in frequency defines the number of devices a single user is signed in to.

---
---

## Learning Path 2: Implement an authentication and access management solution
### Module 4: Manage Microsoft Entra Identity Protection

### Introduction

- Wat deze module behandelt
  - Identity beschermen door usage en sign in patronen te monitoren, voor een veilige cloud oplossing
  - Ontwerpen en implementeren van Microsoft Entra Identity Protection
  - High level overzicht van Identity Protection als feature van Entra ID
  - Verschillende soorten detections, risks, en risk policies binnen Identity Protection
  - Voordelen van risk policies, recente UX verbeteringen, APIs, verbeterde risk assessment, alignment tussen risky users en risky sign ins

- Learning objectives
  - Review Identity Protection basics
  - Implement and manage a user risk policy
  - Implement and manage sign-in risk policies
  - Implement and manage mutlifactor authentication (MFA) registration policy
  - Monitor, investigate, and remediate elevated risky users
  - Explore Microsoft Defender for Identity

---

### Review identity protection basics

- Wat Identity Protection is
  - Service om de security posture van accounts te bekijken
  - 3 kerntaken: automatisch detecteren/remedieren van identity based risks, risks onderzoeken via de portal, risk detection data exporteren naar third party tools

- Licentie
  - Vereist altijd Entra ID Premium P2

- Waar de detectie op gebaseerd is
  - Microsoft's kennis uit Entra ID organisaties, consumer accounts, en Xbox gaming
  - Analyseert 6.5 triljoen signalen per dag
  - Signalen kunnen doorstromen naar Conditional Access voor access beslissingen, of naar een SIEM tool (security information and event management) voor verder onderzoek

- Risk detection types (examen kernstof)
  - Anonymous IP address; sign in vanaf een anonieme IP, bv. Tor of anonymizer VPN
  - Atypical travel; sign in vanaf een atypische locatie t.o.v. recente sign ins
  - Malicious IP address; sign in vanaf een bekend kwaadaardig IP
  - Unfamiliar sign in properties; sign in met eigenschappen die niet recent gezien zijn bij deze user
  - Leaked credentials; user's geldige credentials zijn gelekt
  - Password spray; merdere usernames aangevallen met veelgebruikte wachtwoorden, uniforme brute force aanpak
  - Microsoft Entra threat intelligence; bekend aanvalspatroon herkend via interne/externe threat intelligence bronnen
  - Anomalous token; ongebruikelijke kenmerken in een token, bv. ongebruikelijke levensduur of hergebruik vanaf onbekende locatie
  - Token issuer anomaly; SAML token issuer mogelijk gecompromitteerd
  - Suspicious browser; anomale sign in activiteit over meerdere tenants vanaf dezelfde browser
  - Verified threat actor IP; sign in vanaf IP adressen bekend gekoppeld aan geverifieerde threat actors
  - New country; gedetecteerd via Microsoft Defender for Cloud Apps (MDCA)
  - Activity from anonymous IP address; ook via MDCA
  - Suspicious inbox forwarding; ook via MDCA

- Permissions (examen kernstof)
  - Security Administrator; volledige toegang tot Identity Protection, kan geen password reset voor een user doen
  - Security Operator; alle reports en Overview bekijken, user risk dismissen, safe sign in bevestigen, compromise bevestigen. Kan geen policies configureren/wijzigen, geen password reset, geen alerts configureren
  - Security Reader; alleen reports en Overview bekijken. Kan geen policies configureren, geen password reset, geen alerts configureren, geen feedback geven op detections
  - Belangrijk: Security Operator heeft geen toegang tot het Risky sign ins report
  - Conditional Access Administrators kunnen ook policies maken die sign in risk als conditie gebruiken

- Licentie vereisten per capability (examen kernstof)

| Capability | Free/M365 Apps | Premium P1 | Premium P2 |
|---|---|---|---|
| User risk policy | Nee | Nee | Ja |
| Sign-in risk policy | Nee | Nee | Ja |
| Overview report | Nee | Nee | Ja |
| Risky users report | Beperkt, alleen medium/high risk, geen details | Beperkt, alleen medium/high risk, geen details | Volledig |
| Risky sign ins report | Beperkt, geen risk detail/level | Beperkt, geen risk detail/level | Volledig |
| Risk detections | Nee | Beperkt, geen details drawer | Volledig |
| Users at risk detected alerts | Nee | Nee | Ja |
| Weekly digest | Nee | Nee | Ja |
| MFA registration policy | Nee | Nee | Ja |

- Onthouden voor examen
  - Identity Protection vereist altijd P2, ongeacht welk specifiek onderdeel je gebruikt
  - Security Operator kan risks beheren/dismissen maar geen policies wijzigen, en mist toegang tot Risky sign ins report specifiek
  - P1 geeft alleen zeer beperkte, read only inzage in risky users/sign ins; volledige functionaliteit vereist P2

---

### Implement and manage user risk policy

- 2 risk policies (examen kernstof)
  - Sign in risk policy; focust op de sign in activiteit zelf, analyseert kans dat de sign in door iemand anders dan de user is gedaan
  - User risk policy; detecteert kans dat een user account gecompromitteerd is, via risk events die afwijken van typisch gedrag van die user
  - Beide automatiseren de response op risk detections, laten users zelf remedieren waar mogelijk

- Prerequisites voor self remediation
  - Users moeten geregistreerd zijn voor zowel self service password reset (SSPR) als multi factor authentication (MFA)
  - Aanbevolen: combined security information registration experience gebruiken
  - Self remediation laat users sneller weer productief zijn zonder admin tussenkomst; admins kunnen events achteraf nog steeds bekijken en onderzoeken

- Acceptabele risk levels kiezen
  - Balans tussen user experience en security posture
  - Microsoft aanbeveling: user risk policy threshold op High, sign in risk policy op Medium en hoger
  - High threshold; minder vaak getriggerd, minder user interrupts, maar Low/Medium risk detections vallen buiten de policy, wat een aanvaller ruimte kan geven
  - Low threshold; meer user interrupts, maar hogere security posture

- Exclusions
  - Alle policies staan toe om users uit te sluiten, bv. emergency access/break glass accounts
  - Organisaties bepalen zelf welke andere accounts uitgesloten moeten worden, afhankelijk van hoe die accounts gebruikt worden
  - Exclusions regelmatig herzien of ze nog van toepassing zijn
  - Trusted network locations worden door Identity Protection gebruikt bij sommige risk detections om false positives te verminderen

- Onthouden voor examen
  - Sign in risk = over de sign in activiteit zelf, User risk = over de waarschijnlijkheid dat het account zelf gecompromitteerd is
  - Aanbevolen thresholds: User risk = High, Sign in risk = Medium en hoger
  - Self remediation vereist zowel SSPR als MFA registratie

---

### Exercise: enable sign-in risk policy
  - [04-sc300/labs/18-enable-sign-in-risk-policy](../../04-sc300/labs/18-enable-sign-in-risk-policy.md)

---

### Exercise: configure Microsoft Entra multifactor authentication registration policy
  - [04-sc300/labs/19-configure-microsoft-entra-multifactor-authentication-registration-policy](../../04-sc300/labs/19-configure-microsoft-entra-multifactor-authentication-registration-policy.md)

---

### Monitor, investigate, and remediate elevated risky users

- 3 reports voor risk investigation
  - Risky users, Risky sign ins, Risk detections
  - Te vinden in Entra admin center > Identity > Protection > Identity Protection
  - Allemaal downloadbaar als CSV; risky users en risky sign ins max 2500 entries, risk detections max 5000 records
  - Microsoft Graph API integraties mogelijk om data te combineren met andere bronnen

- Navigeren door de reports
  - Elk report toont alle detections voor de gekozen periode, kolommen aanpasbaar, download in CSV of JSON
  - Filters bovenaan beschikbaar
  - Individuele entries selecteren geeft extra opties (bv. sign in bevestigen als compromised/safe, user als compromised bevestigen, user risk dismissen) en opent een details venster

- Risky users report
  - Toont: welke users at risk zijn/geremedieerd/gedismissed, detectie details, historie van risky sign ins, risk history
  - Acties: password reset, user compromise bevestigen, user risk dismissen, user blokkeren voor sign in, onderzoeken in Microsoft Defender for Identity

- Risky sign ins report
  - Data filterbaar tot 30 dagen terug
  - Toont: classificatie (at risk/compromised/safe/dismissed/remediated), real time en aggregate risk levels, welke detection types getriggerd zijn, welke Conditional Access policies toegepast zijn, MFA details, device info, app info, locatie info
  - Acties: sign in compromised bevestigen, sign in safe bevestigen

- Risk detections report
  - Data filterbaar tot 90 dagen terug
  - Toont: info per detection type, andere risks die tegelijk getriggerd werden, locatie van de sign in poging
  - Klikbare link naar de detectie in Microsoft Defender for Cloud Apps (MDCA) voor meer logs/alerts
  - Systeem kan een risk automatisch dismissen als het een false positive blijkt, of als de user de risk al heeft geremedieerd (bv. via MFA of password change); toont dan "AI confirmed sign in safe"

- Remediation opties (examen kernstof)
  - Self remediation via risk policy; user lost het zelf op via MFA/SSPR, vereist voorafgaande registratie
  - Manual password reset; twee varianten:
    - Temporary password genereren; direct veilg, maar admin moet contact opnemen met de user om het tijdelijke wachtwoord door te geven, user moet het bij volgende sign in wijzigen
    - User zelf laten resetten; werkt alleen als de user geregistreerd is voor MFA en SSPR, geen contact met helpdesk nodig
  - Dismiss user risk; sluit alle events, maar verandert het wachtwoord niet, dus brengt de identity niet echt terug in een veilige staat (bv. te gebruiken als de user is verwijderd)
  - Individuele risk detections handmatig sluiten; typisch na eigen onderzoek, opties: user compromised bevestigen, user risk dismissen, sign in safe bevestigen, sign in compromised bevestigen

- Unblocking users
  - Blokkade gebeurt op basis van user risk of sing in risk

- Unblock bij user risk
  - Password reset
  - Dismiss user risk, of handmatig gerelateerde detections sluiten om het risk level te verlagen
  - User uitsluiten van de policy als de configuratie specifiek voor die user problemen geeft
  - Policy volledig uitschakelen als de configuratie voor alle users problemen geeft

- Unblock bij sign in risk
  - Inloggen vanaf een bekende locatie/device kan het probleem vaak al oplossen
  - User uitsluiten van de policy
  - Policy volledig uitschakelen

- PowerShell en Microsoft Graph API
  - Microsoft Graph PowerShell SDK Preview module beschikbaar voor risk management via PowerShell
  - 3 relevante Graph APIs: riskDetection (lijst van user/sign in gekoppelde risk detections), riskyUsers (info over als risky gedetecteerde users), signIn (sign in info met risk state/detail/level)

- Verbinden met Microsoft Graph (4 stappen, kort)
  1. Domeinnaam ophalen (.onmicrosoft.com)
  2. Nieuwe app registration aanmaken, Application ID noteren
  3. API permissions configureren: Microsoft Graph > Application permissions > IdentityRiskEvent.Read.All en IdentityRiskyUser.Read.All, admin consent geven
  4. Credential configureren: client secret aanmaken (secret goed bewaren, bij verlies moet een nieuwe aangemaakt worden)

- Authenticatie en API call (kort)
  - POST naar login.microsoft.com met grant_type client_credentials, resource, client_id, client_secret
  - Bij succes: authentication token terug, gebruikt in Authorization header
  - API call naar graph.microsoft.com/v1.0/identityProtection/riskDetections geeft een collectie risk detections terug in OData JSON

- Praktische voorbeelden van API queries
  - Offline risk detections ophalen; riskDetection API met filter detectionTimingType eq 'offline', voor detecties die niet real time zijn getriggerd
  - Users die een MFA challenge succesvol doorstonden na een risky sign in policy; riskyUsers API met filter riskDetail eq 'userPassedMFADrivenByRiskBasedPolicy', helpt false positives identificeren

- Onthouden voor examen
  - Risky users en risky sign ins reports: max 2500 CSV entries, risk detections: max 5000
  - Risky sign ins report: 30 dagen data, risk detections report: 90 dagen data
  - Self remediation vereist vooraf geregistreerde MFA en SSPR
  - Dismiss user risk sluit het risico maar verandert het wachtwoord niet, dus brengt de identity niet automatisch terug in een veilige staat
  - riskDetection, riskyUsers, en signIn zijn de 3 kern Graph APIs voor Identity Protection data

---

### Implement security for workload identities

- Wat het is
  - Identity Protection is uitgebreid van alleen users naar ook workload identities: applicaties, service principals, Managed Identities
  - Workload identity; laat een applicatie of service principal toegang krijgen tot resources, soms in de context van een user

- Waarom workload identities lastiger te beheren zijn 
  - Kunnen geen multi factor authentication (MFA) doen
  - Vaak geen formeel lifecycle proces
  - Moeten ergens hun credentials/secrets opslaan
  - Deze verschillen maken ze moeilijker te beheren en kwetsbaarder voor compromise

- Vereisten om workload identity protection te gebruiken
  - Entra ID Premium P2 licentie
  - Ingelogde user moet een van deze rollen hebben: Security administrator, Security operator, Security reader

- Soorten gedetecteerde risico's (kernstof)
  - Microsoft Entra threat intelligence (offline); activiteit die overeenkomt met bekende aanvalspatronen uit interne/externe threat intelligence bronnen
  - Suspicious Sign-ins (offline); ongebruikelijke sign in eigenschappen/patronen voor deze service principal. Systeem leert de baseline over 2 tot 60 dagen, triggert bij afwijkende IP/ASN, target resource, user agent, hosting verandering, IP land, credential type
  - Unusual addition of credentials to an OAuth app (offline); gedetecteerd via Microsoft Defender for Cloud Apps, verdachte toevoeging van privileged credentials aan een OAuth app, kan wijzen op een gecompromitteerde app
  - Admin confirmed account compromised (offline); admin heeft handmatig Confirm compromised geselecteerd in de UI of via de riskyServicePrincipals API, terug te vinden in de account's risk history
  - Leaked Credentials (offline); geldige credentials zijn gelekt, bv. via een publiek GitHub repo of een data breach

- Conditional Access voor workload identities
  - Kan toegang blokkeren voor specifieke accounts die als "at risk" gemarkeerd zijn door Identity Protection
  - Toepasbaar op single tenant service principals die in jouw tenant geregistreerd zijn
  - Buiten scope: third party SaaS apps, multi tenant apps, en Managed Identities

- Onthouden voor examen
  - Workload identity protection vereist altijd P2, net als de user gerichte Identity Protection features
  - Alle genoemde detection types zijn offline (niet real time), in tegenstelling tot sommige user risk detections
  - Conditional Access voor workload identities werkt alleen op single tenant service principals, niet op multi tenant apps of Managed Identities

---

### Explore Microsoft Defender for Identity

- Wat het is
  - Cloud based security oplossing, voorheen Azure Advanced Threat Protection
  - Gebruikt on premises Active Directory signalen om advanced threats, gecompromiteerde identities, en kwaadaardige insider acties te identificeren, detecteren, en onderzoeken

- Waar het SecOp analysts mee helpt (kernstof)
  - Users, entity behavior en activiteiten monitoren met learning based analytics
  - User identities en credentials in Active Directory beschermen
  - Verdachte user activiteiten en advanced attacks onderzoeken door de hele kill chain heen
  - Duidelijke incident informatie op een simpele tijdljn tonen voor snelle triage

- Componenten (examen kernstof)
  - Microsoft Defender portal (security.microsoft.com); beheer, monitoring en onderzoek van data die binnenkomt van de sensors
  - Defender for Identity sensor; direct te installeren op:
    - Domain controllers; monitort direct het verkeer, geen aparte server of port mirroring configuratie nodig
    - Active Directory Federated Services (AD FS); monitort netwerkverkeer en authentication events
  - Defender for Identity cloud service; draait op Azure infrastructuur, gedeployed in US, Europa, en Azie, gekoppeld aan Microsoft's threat intelligence

- Onthouden voor examen
  - Defender for Identity werkt op basis van on premises AD signalen, in tegenstelling tot Identity Protection dat zich meer op cloud/Entra ID sign ins richt
  - Sensor kan direct op domain controllers of AD FS servers geinstalleerd worden, zonder extra dedicated server of port mirroring
  - Onderdeel van hetzelfde Microsoft Defender portal als andere Defender producten (bv. Defender for Cloud Apps)

---

### Explore the Identity Risk Management Agent

- Wat het is
  - Onderdeel van Microsoft Entra ID Protection, biedt proactief risk management door user behavior te analyseren
  - Stelt acties voor om potentiele identity risks te mitigeren
  - Gebruikt een Large Language Model (LLM) om security administrators te helpen risky activities te reviewen en aan te pakken voordat ze tot een security incident leiden
  - Instellingen configureerbaar naar de behoeften van de organisatie

- Prerequisites (examen relevant)
  - Minimaal Entra ID Premium P2 licentie
  - Beschikbare security compute units (SCU)
  - Juiste Entra rol:
    - Security Administrator; vereist om de agent voor het eerst te activeren, de agent te bekijken, en actie te ondernemen op suggesties
    - Security Reader en Global Reader; kunnen de agent en suggesties bekijken, maar geen acties ondernemen

- Hoe de agent werkt
  - Checkt eerst op nieuwe risky identities die nog niet eerder geidentificeerd waren (verbruikt geen SCUs)
    1. Checkt op nieuwe risky users met risk state "At risk"
    2. Identificeert risky users binnen de gedefinieerde scope settings
  - Als er nieuwe suggesties gevonden worden (verbruikt wel SCUs):
    - Investigate the risky user; checkt risky sign ins en risk detections van de user
    - Generate findings and a risk summary; genereert bevindingen inclusief uitgebreide risk summary en key risk factors
    - Generate a recommended remediation action; stelt een remediation actie voor op basis van het onderzoek
    - Answer questions through chat; IT admins kunnen de agent vragen stellen over risky users en de risk summary
    - Store custom instructions in agent memory; klant kan via chat custom instructies geven die de agent onthoudt voor toekomstige runs, momenteel alleen voor preferred remediation actions

- Agent gebruiken (stappen)
  1. Entra admin center, minimaal Security Administrator
  2. ID Protection > Risky users
  3. Banner bovenaan de pagina zoeken
  4. Start agent selecteren

- Agent settings configureren
  - Risky users pagina > Agent view > ellipses rechtsboven > Settings
  - Controls; rollen en permissions nodig om de agent te draaien
  - Triggers; wanneer/hoe de agent draait
    - Continuous monitoring; checkt elke 5 minuten op nieuwe risky users
    - Daily trigger; agent draait 1x per dag
    - Manual run; alleen handmatig gestart
  - Scope; default: meest recente 100 risky users binnen de laatste 90 dagen
    - Select users and groups; specifieke users/groups kiezen om te scannen
    - Maximum recent risky users instelbaar tussen 1 en 100
    - Risk levels selecteren om mee te nemen in de scan, standaard alle levels geselecteerd
    - Tijdsspanne instellen: laatste 7, 14, 30 dagen, of custom tot 90 dagen
  - Communications; users instellen die notificaties krijgen van de agent run
  - Memory; lijst van door de user bevestigde false positives (safe items)

- Agent findings report
  - Agent summary; bovenaan de Agent view, toont recente agent activiteiten, snelle toegang tot Chat with agent en Manage agent (handmatige run triggeren of settings openen)
  - Agent suggestions; onder de summary, hover highlight de betrokken users in de tabel, selecteren filtert de tabel, elke suggestie heeft een bulk action knop
  - Huidige beschikbare remediation acties in suggestions: Dismiss risk, Reset password
  - Risky users table; alle risky users, per user agent findings/risk factors/suggestions bekijken, Agent suggestion kolom toont aanbevolen actie direct in de tabel

- Risky user details, Agent view
  - Basic user info; username, huidig risk level, User Principal Name (UPN)
  - Agent findings; verdict Compromised of Not compromised, gebaseerd op het onderzoek
  - Risk summary; gedetailleerde uitleg van de bevindingen, gebaseerd op analyse van sign ins en gedrag
  - Risk factors; belangrijkste risico indicatoren samengevat
  - Suggested remediation action; call to action knop om direct te remedieren

- Onthouden voor examen
  - Vereist P2 plus beschikbare SCUs (security compute units), naast de juiste rol
  - Alleen Security Administrator kan de agent activeren en acties ondernemen; Security Reader/Global Reader kunnen alleen bekijken
  - Default scope: 100 meest recente risky users, laatste 90 dagen, alle risk levels
  - Beschikbare remediation acties momenteel beperkt tot Dismiss risk en Reset password

---

## Module Assessment — Module 4 (Manage Microsoft Entra Identity Protection)

**Score:** 100%

### Vraag 1
Which task can a user with the Security Operator role perform?

- Configure alerts
- ✅ Confirm safe sign-in
- Reset a password for a user

### Vraag 2
There are two risk policies that can be enabled in the directory. One is user risk policy. Which is the other risk policy?

- Mobile device access risk policy
- ✅ Sign-in risk policy
- Hybrid identity sign-in risk policy

### Vraag 3
In Microsoft Graph, which three APIs expose information about risky users and sign-ins?

- ✅ riskDetection, riskyUsers, signIns
- riskDetection, itemActivity, signIns
- riskyUsers, signIns, IdentitySet

---
---

## Learning Path 2: Implement an authentication and access management solution
### Module 5: Implement access management for Azure resources 

### Introduction

- Wat deze module behandelt
  - Toegang toewijzen en beheren tot Azure resources via Azure roles
  - Doel: alleen specifieke toegang geven aan users/groups die het echt nodig hebben, via een rol met de juiste permissions
  - Built-in Azure roles beschikbaar, custom roles zelf te maken indien nodig
  - Applicaties kunnen ook permissions nodig hebben om data/resources te benaderen; managed identities laten een applicatie alleen toegang krijgen tot resources die jij toestaat
  - Granulaire toegang tot secrets, keys, en certificates opgeslagen in een key vault, voor zowel users als applicaties
  - Microsoft Entra Permissions Management; permissions verzamelen, reviewen en beperken across cloud oplossingen

- Learning objectives
  - Assign Azure roles and custom roles to access Azure resources
  - Create and manage application access with managed identities
  - Configure and manage access into Azure Key Vault
  - Retrieve object from a key vault securely
  - Explore the capabilities of Microsoft Entra Permissions Management

---

### Assign Azure roles

- Wat het is
  - Azure role based access control (Azure RBAC); authorization systeem om toegang tot Azure resources te beheren
  - Rollen toegewezen aan users, groups, service principals, of managed identities, op een bepaalde scope

- Stap 1: wie heeft toegang nodig
  - User; voor 1 specifieke persoon, ook toewijsbaar aan users uit andere tenants
  - Group; voor een set users die dezelfde rol nodig hebben
  - Service Principal; als een applicatie toegang moet krijgen tot een Azure resource
  - Managed Identity; als een applicatie zelf credentails moet beheren voor authenticatie

- Stap 2: de juiste rol kiezen
  - Built-in roles gebruiken, of een custom role maken met specifieke capabilities

- Belangrijkste built-in Azure roles (kernstof)
  - Owner; volledige toegang tot alle resources
  - Contributor; kan alle types Azure resources aanmaken en beheren, maar kan geen toegang toewijzen
  - Reader; kan beschikbare Azure resources bekijken
  - User Access Administrator; kan toegang tot Azure resources toewijzen
  - Andere task specifieke rollen mogelijk, bv. Virtual Machine Contributor

- Stap 3: het juiste niveau bepalen (Scope)
  - Scope = set resources waar de toegang op van toepassing is
  - 4 niveaus, in parent child relatie: management group, subscription, resource group, resource
  - Hoe hoger het niveau, hoe breder de scope; lagere niveaus erven permissions van hogere niveaus
  - Voorbeelden:
    - Reader rol op management group scope; user kan alles lezen in alle subscriptions binnen die management group
    - Billing Reader rol op subscription scope; group kan billing data lezen van elke resource group en resource in die subscription
    - Contributor rol op resource group scope; applicatie kan alle resource types beheren in die resource group, maar niet in andere resource groups binnen de subscription
  - Best practice: least privilege, geen bredere rollen op bredere scopes toewijzen puur voor het gemak; beperkt de impact als een security principal ooit gecompromitteerd wordt

- Stap 4: bevestigen dat de ingelogde user zelf de rechten heeft om de rol toe te wijzen

- Stap 5: rol toewijzen
  - Mogelijk via Azure portal, Azure PowerShell, Azure CLI, Azure SDKs, of REST APIs
  - Limiet: max 4000 role assignments per subscription (incl. subscription, resource group, en resource scope niveaus samen)
  - Limiet: max 500 role assignments per management group

- Toewijzen via de portal
  - Gebeurt via de Access control (IAM) pagina, official name: identity and access management (IAM), te vinden op meerdere plekken in de portal (User, Group, Resource Group, Subscription niveau)

- Toewijzen via script
  - PowerShell: New-AzRoleAssignment met ObjectId, RoleDefinitionName, en Scope parameters
  - CLI: az role assignment create met assignee, role, en resource-group parameters

- Onthouden voor examen
  - 4 scope niveaus: management group > subscription > resource group > resource, met inheritance van boven naar beneden
  - Owner kan alles incl. toegang beheren, Contributor kan resources beheren maar geen toegang toewijzen, User Access Administrator kan specifiek alleen toegang toewijzen
  - Least privilege: kies het laagst mogelijke scope niveau dat nog steeds voldoet
  - Max 4000 role assignments per subscription, max 500 per management group

---

### Configure custom Azure roles

- Wat het is
  - Custom roles maken als de built-in roles niet aan de specifieke behoeften voldoen
  - Toewijsbaar aan users, groups, en service principals op management group scope (alleen in preview), subscription scope, en resource group scope
  - Opgeslagen in Entra ID, deelbaar over meerdere subscriptions
  - Max 5000 custom roles per directory
  - Aan te maken via Azure portal, Azure PowerShell, Azure CLI, of de REST API

- Custom role aanmaken via de UI (stappen)
  1. Microsoft Entra admin center
  2. Identity > Roles and administration
  3. + New custom role
  4. Naam geven en de benodigde capabilities toewijzen
  - Zelfde least privilege principe: alleen de capabilities kiezen die echt nodig zijn

- Custom role aanmaken via JSON template
  - JSON bestand met o.a. roleName, description, assignableScopes, en permissions (actions, notActions, dataActions, notDataActions)
  - Voorbeeld: "Billing Reader Plus" rol met leesrechten op Authorization, Billing, Commerce, Consumption, Management (management groups), CostManagement, en volledige toegang tot Support
  - Wildcard (*) gebruikt om brede permissions in 1 keer toe te kennen, kan op elk niveau in het pad staan (bv. Microsoft.Billing/*/read voor alle read permissions binnen Billing)

- Onthouden voor examen
  - Custom roles zitten in Entra ID, niet in een specifieke subscription, en zijn dus deelbaar over subscriptions heen
  - Management group scope voor custom roles is nog in preview
  - Max 5000 custom roles per directory (let op: dit is een ander limiet dan de max 4000/500 role assignments uit de vorige unit)
  - JSON structuur: actions/notActions voor management plane, dataActions/notDataActions voor data plane acties
 
---

### Create and configure managed identities

- Het probleem dat het oplost
  - Cloud oplossingen moeten secrets, credentials, certificates, en keys beheren om communicatie tussen services te beveiligen
  - Managed identities elimineren de noodzaak voor developers om deze credentials zelf te beheren
  - Zelfs als secrets veilig in Azure Key Vault staan, hebben services nog steeds een manier nodig om bij die Key Vault te komen; managed identities lossen dat op

- Wat het is
  - Automatisch beheerde identity in Entra ID, voor applicaties om mee te vebrinden met resources
  - Ondersteunt authenticatie via Entra ID
  - Applicaties krijgen Entra tokens zonder zelf credentials te hoeven beheren

- Voordelen (kernstof)
  - Geen credentials zelf beheren, credentials zijn zelfs niet toegankelijk voor jou
  - Bruikbaar voor authenticatie naar elke resource die Entra authenticatie ondersteunt, incl. eigen applicaties
  - Geen extra kosten

- 2 types managed identity (kernstof)
  - System assigned; direct enabled op een service instance, identity word aangemaakt in Entra ID, gebonden aan de lifecycle van die service instance. Resource verwijderd = identity automatisch verwijderd. Alleen die ene resource kan deze identity gebruiken
  - User assigned; los, standalone Azure resource, toewijsbaar aan 1 of meerdere service instances tegelijk. Identity wordt los beheerd van de resources die hem gebruiken

- Belangrijk om te onthouden
  - Managed identities zijn toegewezen aan een applicatie; je configureert en beheert de identity binnen de service waar hij gebruikt wordt (bv. VM, cloud app, function, app service)

- Managed identity toevoegen aan een App Service (stappen, portal)
  1. App bouwen
  2. App openen in de Azure portal
  3. Identity in het menu > System assigned of User assigned kiezen
  4. + Add item, wizard doorlopen

- Alternatieve methodes 
  - CLI: az webapp identity assign met resource group, app name, en identty name
  - PowerShell: Update-AzFunctionApp met IdentityType UserAssigned en IdentityId
  - Template: identity blok met type UserAssigned en userAssignedIdentities

- Waarde van managed identities
  - Sluit aan bij zero trust: alleen minimale privileges toewijzen die de managed identity nodig heeft, alleen toegang tot de minimaal benodigde resources
  - Least privilege houdt applicaties en data beschermd

- Onthouden voor examen
  - System assigned = 1 op 1 gebonden aan 1 resource, verdwijnt automatisch met die resource
  - User assigned = los beheerd, herbruikbaar over meerdere resources
  - Managed identities kosten niets extra en vereisen geen credential management door de developer

---

### Access Azure resources with managed identities

- Waar rekening mee te houden
  - Managed identities zijn een feature van Entra ID
  - Elke Azure service die managed identities ondersteunt heeft zijn eigen tijdlijn qua beschikbaarheid
  - Altijd de availability status en known issues checken voor je specifieke resource voordat je begint

- Toegang toevoegen tot andere resources 
  - Nadat een managed identity is enabled op een resource (bv. App Service of virtual machine), kan het nodig zijn om die identity ook toegang te geven tot een andere resource
  - Voorbeeld: een virtual machine's managed identity toegang geven tot een storage account

- Stappen
  1. Azure portal, ingelogd met een account gekoppeld aan de subscription waar de managed identity is geconfigureerd
  2. Navigeren naar de resource waar je de toegang wilt instellen (in het voorbeeld: de storage account, niet de VM zelf)
  3. Access control (IAM) selecteren
  4. Add > Add role assignment
  5. Rol kiezen (Owner, Contributor, of Reader) op basis van least privilege voor wat de applicatie nodig heeft
  6. De gewenste managed identity selecteren
  7. Review + assign om de toewijzing af te ronden

- Onthouden voor examen
  - De rol wordt toegewezen op de resource waar de managed identity toegang toe moet krijgen, niet op de resource waar de managed identity zelf op draait
  - Zelfde IAM/Access control flow als bij normale role assignments, alleen kies je nu een managed identity als de security principal in plaats van een user/group
 
---

### Analyze Azure role permissions

- Wat is een permission
  - Consent/autorisatie om een specifieke actie uit te voeren
  - Range: van alleen bekijken tot instellingen wijzigen tot users toevoegen/verwijderen
  - Toegewezen op user of group niveau, komt uiteindelijk altijd bij de user terecht
  - Member user vs Guest user; guest heeft standaard iets minder rechten

- Voorbeeld default permissions (subset)

| Member Users | Guest Users |
|---|---|
| Users + contacts opsommen | Alleen eigen properties lezen |
| Guest users uitnodigen | Guest users uitnodigen |
| Security/M365 Groups aanmaken | Alleen niet verborgen groups zoeken op naam |
| Nieuwe apps registreren | Properties van registered/enterprise apps lezen |

- Permissions controleren, 2 manieren
  - User Settings (Entra ID > Manage); default permissions beperken. Kan blokkeren: apps registreren, Azure portal toegang, LinkedIn connections, external collaboration settings
  - Roles and administrators; nieuwe permissions toevoegen via rollen aan users/groups/service principals
  - Kernprincipe: altijd least privilege

- Permissions van een rol bekijken
  - Entra ID > Roles and administrators > rol selectern > (...) menu > description page (Attribute definition reader)
  - Elke rol toont 2 soorten permissions: Role permissions, en Guest and service principal basic read permissions

- Onthouden voor examen
  - Check altijd de volledige permissions lijst van een rol voordat je hem toewijst, rollen kunnen meer bevatten dan de naam doet vermoeden
  - Deze unit herhaalt in essentie dezelfde stof als de eerdere "Analyze Microsoft Entra role permissions" unit uit Module 1, nu toegepast in context van Azure resource access i.p.v. puur Entra ID beheer

---

### Configure Azure Key Vault RBAC policies

- 2 manieren om Key Vault toegang te regelen
  - Role based access control (RBAC)
  - Key Vault access policies
  - Beide beschermen secrets, certificates, en keys; access policies geven iets granulairdere controle maar zijn lastiger te beheren

- Key Vault access policy toewijzen
  - Bepaalt of een user, application, of group operaties mag uitvoeren op secrets, keys, certificates
  - Toewijsbaar via Azure portal, CLI, of PowerShell
  - Max 1024 access policy entries per key vault, elke entry geeft een specifieke set permissions aan 1 security principal
  - Vanwege deze limiet: aanbevolen om policies aan groups toe te wijzen i.p.v. individuele users, makkelijker te beheren

- Stappen om een access policy toe te voegen
  1. Key Vault openen in de Azure portal
  2. Key vault selecteren of nieuwe aanmaken
  3. Access policies > + Add Access Policy
  4. Gewenste permissions toewijzen aan de service principal (user, group, of applicatie)
  5. Add om op te slaan en toe te passen

- Key Vault toegang via Azure RBAC
  - RBAC laat users Key, Secrets, en Certificates permissions beheren vanuit 1 centrale plek, over alle key vaults heen
  - Zelfde 4 scope niveaus als bij normale Azure roles: management group, subscription, resource group, of individuele resource
  - RBAC voor key vault laat ook losse permissions per individuele key, secret, of certificate toe
  - Aanbeveling: 1 vault per applicatie per omgeving (Development, Pre-Production, Production)

- 2 stappen om RBAC te gebruiken voor Key Vault data toegang
  1. Role based access control inschakelen in de key vault
  2. Key vault Identity and Access (IAM) openen, rol toewijzen zoals bij andere scenario's (bv. managed identity)

- Built-in Key Vault rollen (examen kernstof)

| Rol | Beschrijving |
|---|---|
| Key Vault Administrator | Alle data plane operaties op alles in de vault (certificates, keys, secrets). Kan geen key vault resources of role assignments beheren |
| Key Vault Certificates Officer | Alle acties op certificates, behalve permissions beheren |
| Key Vault Crypto Officer | Alle acties op keys, behalve permissions beheren |
| Key Vault Crypto Service Encryption User | Metadata van keys lezen, wrap/unwrap operaties uitvoeren |
| Key Vault Crypto User | Cryptografische operaties uitvoeren met keys |
| Key Vault Reader | Metadata lezen van key vaults en hun certificates/keys/secrets. Kan geen gevoelige waarden lezen (secret content of key material zelf) |
| Key Vault Secrets Officer | Alle acties op secrets, behalve permissions beheren |
| Key Vault Secrets User | Secret content lezen |

- Onthouden voor examen
  - Access policies: max 1024 entries per vault, beter groups gebruiken dan individuele users
  - RBAC: centraal beheer over alle vaults, met granulariteit tot op individuele key/secret/certificate niveau
  - Key Vault Reader kan metadata zien maar niet de daadwerkelijke gevoelige waarden, dat vereist Secrets User/Crypto User rollen
  - RBAC moet eerst expliciet ingeschakeld worden in de key vault voordat je rollen kunt toewijzen
 
---

### Retrieve objects from Azure Key Vault

- Wat het is
  - Key Vault is een veilige plek om secrets, keys, en certificates op te slaan
  - Eenmaal opgeslagen kunnen users en applicaties deze items veilig gebruiken
  - Het proces om ze op te halen is vergelijkbaar voor elk type item, hier uitgelegd via een secret

- Een secret toevoegen aan de key vault (stappen)
  1. Key vault openen in de Azure portal
  2. Key Vault settings > Secrets
  3. Generate/Import
  4. Create a secret: Upload options = Manual, Name = mySC300keyvaultSecret, Value = This is my secret
  5. Create

- Secret ophalen via de Azure portal
  - Key vault openen, de aangemaakte secret openen, Show secret value selecteren om de waarde in platte tekst te zien/kopieren

- Secret ophalen via CLI of PowerShell
  - CLI: az keyvault secret show met name, vault-name, en query "value"
  - PowerShell: Get-AzKeyVaultSecret met VaultName, Name, en AsPlainText

- Secret ophalen binnen een applicatie
  - Mogelijk via .NET, Node.js, Python, en andere talen om vanuit code toegang te krijgen tot secrets/keys/certificates in de key vault

- Onthouden voor examen
  - Het ophaalproces is grotendeels hetzelfde ongeacht of het om een secret, key, of certificate gaat
  - Toegang via portal, CLI, PowerShell, of programmatisch vanuit een applicatie zijn allemaal mogelijk, mits de juiste permissions (RBAC of access policy) zijn toegewezen

---

## Module Assessment — Module 5 (Implement access management for Azure resources)

**Score:** 100%

### Vraag 1
What tool is available in Azure to give administrators the ability to provide comprehensive visibility into permissions assigned to all identities, users and workloads, actions, and resources across cloud infrastructures and identity providers? It detects, right-sizes, and monitors unused and excessive permissions and enables Zero Trust security through least privilege access in Microsoft Azure, AWS, and GCP?

- Azure Monitor
- Microsoft Defender for Identity
- ✅ Microsoft Entra Permissions Management

### Vraag 2
You want to assign the Azure role Contributor to a specific user; what tools can you use to make this assignment?

- ✅ Azure portal, PowerShell, and CLI
- Azure portal only
- Scripting only with PowerShell and CLI

### Vraag 3
You want to create a managed identity for your application. You want the identity to be created and deleted dynamically when the resource is started and stopped. What type of managed identity do you need to create?

- User-assigned
- ✅ System-assigned
- Dynamic-assigned

---
---

## Learning Path 2: Implement an authentication and access management solution
### Module 6: Deploy and Configure Microsoft Entra Global Secure Access

### Introduction

- Waarom dit belangrijk is
  - De moderne workforce werkt niet meer alleen op kantoor, maar bijna overal vandaan
  - Dit vraagt om een identity aware, cloud delivered network perimeter, ook wel Security Service Edge (SSE) genoemd
  - Microsoft's SSE oplossing bestaat uit Microsoft Entra Internet Access en Microsoft Entra Private Access, samen Global Secure Access genoemd
  - Gebaseerd op Zero Trust principes: least privilege, explicit verification, assume breach

- Scenario ter illustratie
  - Sales rep werkt remote vanaf een coffee shop, moet bij gevoelige customer data in de cloud
  - Gebruikt Microsoft Entra Private Access om veilig te verbinden, identity te authenticaten, en de data te benaderen
  - Toegang gebeurt zonder data bloot te stellen aan het publieke internet, met least privilege en explicit verification

- Wat deze module behandelt
  - Implementeren van Microsoft Entra Private Access en Microsoft Entra Internet Access via Azure en Entra ID


---

### Explore Global Secure Access

- Wat het is
  - Microsoft's Security Service Edge (SSE) oplossing, bestaat uit Entra Internet Access en Entra Private Access
  - Combineert network, identity, en endpoint access controls, voor veilige toegang tot elke app/resource, vanaf overal
  - Access orchestration voor employees, business partners, en digital workloads
  - Continue monitoring en real time aanpassing van user access bij wijzigingen in permissions of risk level
  - Beheerd via 1 unified portal
  - Geleverd via het Microsoft Wide Area Network, over globale regio's en edge locaties, waardoor users/devices veilig kunnen verbinden met publieke en private resources

- Microsoft Entra Internet Access
  - Beveiligt toegang tot Microsoft services, SaaS, en publieke internet apps
  - Beschermt users, devices, en data tegen internet threats
  - Werkt via een identity centric, device aware, cloud delivered Secure Web Gateway (SWG)

- Key features Internet Access 
  - Voorkomt stolen token reply attacks via compliant network checks in Conditional Access
  - Universal tenant restrictions tegen data exfiltratie
  - Verrijkte logs met network en device signalen
  - Preciezere risk assessments op users, locaties, en devices
  - Netwerkverkeer verzamelen via de desktop client of vanaf een remote network
  - Dedicated forwarding profile specifiek voor publiek internetverkeer
  - Bescherming van user toegang tot publiek internet via het SWG
  - Toegang regelen op basis van content categorieen en domeinnamen van websites
  - Universal Conditional Access policies toepasbaar op alle internet destinations

- Microsoft Entra Private Access
  - Veilige toegang tot private, corporate resources
  - Bouwt voort op Entra application proxy, uitgebreid naar elke private resource, poort, en protocol
  - Remote users verbinden met private apps over hybrid en multicloud omgevingen, private netwerken, en datacenters, vanaf elk device/netwerk, zonder VPN
  - Per app adaptive access, gebaseerd op Conditional Access policies

- Key features Private Access 
  - Zero Trust based toegang tot IP adressen en/of Fully Qualified Domain Names (FQDNs), zonder legacy VPN
  - Modernisering van legacy app authenticatie via Conditional Access
  - Naast bestaande non Microsoft SSE oplossingen te deployen, voor een naadloze end user experience

- Voordat je begint

- Licenties 
  - Entra ID P1 of P2 licentie
  - Entra Internet Access licentie en/of Entra Private Access licentie

- Rollen
  - Global Secure Access Administrator rol toegewezen aan minimaal 1 administrator

- Aanbevolen: Zero Trust Guidance Center raadplegen voor implementatie planning. Configuratie gebeurt in het Entra admin center (entra.microsoft.com)

- Onthouden voor examen
  - Internet Access = publieke internet/SaaS bescherming via SWG, Private Access = private corporate resources zonder VPN, beide samen vormen Global Secure Access
  - Private Access is een uitbreiding op het bestaande Entra application proxy concept
  - Vereist altijd P1 of P2, plus een aparte Internet Access en/of Private Access licentie

---

### Deploy and configure Microsoft Entra Internet Access

- 4 hoofdstappen (examen kernstof)
  1. Microsoft traffic forwarding profile inschakelen
  2. Global Secure Access Client instaleren op end user devices
  3. Tenant restrictions inschakelen
  4. Enhanced Global Secure Access signaling en Conditional Access inschakelen

- Belangrijk om te onthouden
  - Conditional Access policies voor Microsoft traffic worden alleen afgedwongen als de user de Global Secure Access client heeft
  - Zonder de client is Microsoft traffic wel toegankelijk via remote network connectivity, maar dan zonder dat de Conditional Access policy wordt afgedwongen

- Stap 1: Microsoft traffic forwarding profile inschakelen
  - Global Secure Access Administrator > Global Secure Access > Connect > Traffic forwarding
  - Microsoft traffic profile enablen
  - Zet automatisch 3 configuraties klaar:
    - Policies (network routing); Exchange Online, SharePoint Online + OneDrive for Business, en Entra ID + MSGraph, via FQDNs of IP subnets
    - Conditional Access Policy; gekoppelde policy die alle Microsoft traffic vangt en routeert volgens de policies hierboven als condities matchen
    - User and Group; specifieke users/groups waarop deze traffic forwarding van toepassing is

- Stap 2: Global Secure Access Client installeren
  - Deploybaar via Intune, of handmatig per device
  - Download client: Global Secure Access Administrator > Global Secure Access > Connect > Client download
  - Installatie Windows: setup file kopieren, GlobalSecureAccessClient.exe draaien, licentievoorwaarden accepteren, user logt in met Entra credentials, connectie icoon wordt groen bij succesvolle verbinding
  - Android: installeerbaar via Intune of Microsoft Defender for Endpoint on Android, client komt uit de Android store

- Stap 3: Tenant Restrictions configureren
  - Controleert user toegang tot externe tenants op het netwerk
  - Werkt samen met cross tenant access settings, voegt tenant level restricties toe plus granulariteit op user/group/app niveau
  - Verplaatst policy management van network proxies naar een cloud based portal
  - Kan: interne identities (employees) toegang geven tot specifieke externe tenants, toegang blokkeren tot niet toegestane tenants, externe identities (contractors/vendors) volledig blokkeren van alle externe tenants

- Tenant restrictions instellen (stappen)
  1. Minimaal Security Administrator
  2. Identity > External Identities > Cross tenant access settings > Organizational settings
  3. Add organization, volledige domeinnaam of tenant ID invullen
  4. Organisatie selecteren uit zoekresultaten, Add
  5. Organisatie verschijnt in de lijst, standaard geerfd van default settings
  6. Instellingen aanpassen via de "Inherited from default" link onder Inbound/Outbound access

- Global Secure Access enablen voor tenant restrictions
  - Vereist zowel Global Secure Access Administrator als Security Administrator rol
  - Global Secure Access > Global Settings > Session Management > Tenant Restrictions
  - Toggle Enable tagging aanzetten, Save

- Hoe tenant restrictions werken (voorbeeldflow, examen kernstof)
  1. Organisatie configureert een tenant restrictions v2 policy die externe accounts/apps blokkeert, afgedwongen via Global Secure Access universal tenant restrictions
  2. User met managed device probeert een Entra integrated app te benaderen met een niet toegestane externe identity
  3. Authentication plane protection; Entra ID blokkeert de externe account op basis van de policy
  4. Data plane protection; via universal tenant restrictions v2, dekt Microsoft Graph. Hergebruik van een geinfiltreerd Entra token voor Graph wordt geblokkeerd, anonieme toegang tot SharePoint Online eveneens. Data plane protection voor third party apps (bv. Slack) valt hier niet onder

- Stap 4: Enhanced Global Secure Access signaling en Conditional Access
  - Combinatie van Conditional Access + Global Secure Access voorkomt kwaadaardige toegang tot Microsoft apps, SaaS apps, en private line of business (LoB) apps
  - Meerdere condities te combineren voor defense in depth (device compliance, locatie, etc.)
  - Introduceert het concept van een compliant network binnen Conditional Access; checkt of de user verbindt via een geverifieerde netwerkverbinding
  - Voordeel: geen lijst van alle IP adressen van organisatielocaties meer nodig, geen verplichte VPN egress meer nodig voor security
  - Continuous Access Evaluation (CAE) met compliant network momenteel ondersteund voor SharePoint Online, biedt token theft replay protection

- Global Secure Access signaling inschakelen (stappen)
  1. Global Secure Access Administrator > Global Secure Access > Global settings > Session management > Adaptive access
  2. Toggle Enable Global Secure Access signaling in Conditional Access aanzetten
  3. Protection > Conditional Access > Named locations
  4. Controleren of er een locatie "All Compliant Network locations" bestaat (type Network Access), optioneel als trusted markeren

- Conditional Access policy bouwen voor networks (stappen)
  1. Minimaal Conditional Access Administrator
  2. Protection > Conditional Access > Create new policy, naam geven
  3. Assignments > Users or workload identities > Include All users, Exclude emergency/break glass accounts
  4. Target resources > Include > Select apps: Office 365 Exchange Online en/of SharePoint Online en/of SaaS apps. Let op: de brede "Office 365" cloud app optie wordt hier NIET ondersteund, dus niet selecteren
  5. Conditions > Location > Yes > Include Any location, Exclude Selected locations > All Compliant Network locations
  6. Access controls > Grant > Block Access
  7. Enable policy On > Create

- Onthouden voor examen
  - Zonder de Global Secure Access client wordt Conditional Access niet afgedwongen op Microsoft traffic, ook al is de traffic zelf wel toegankelijk
  - Tenant restrictions v2 beschermt zowel de authentication plane (Entra ID zelf) als de data plane (Microsoft Graph, SharePoint Online), maar dekt geen third party apps zoals Slack
  - De brede "Office 365" cloud app optie wordt niet ondersteund in deze specifieke Conditional Access policy voor compliant network, gebruik de losse apps (Exchange Online, SharePoint Online) in plaats daarvan
  - CAE met compliant network is momenteel alleen ondersteund voor SharePoint Online

---

### Deploy and configure Microsoft Entra Private Access

- 4 hoofdstappen (examen kernstof)
  1. Microsoft Entra private network connector en connector group configureren
  2. Quick Access configureren voor private resources
  3. Private Access traffic forwarding profile inschakelen
  4. Global Secure Access Client installeren en configureren op end user devices

- Stap 1: Connector en connector groups
  - Connectors zijn lightweight agents op een server in het private netwerk, faciliteren outbound connectie naar Global Secure Access
  - Moeten geinstalleerd worden op Windows Server met toegang tot de backend resources/applicaties
  - Connectors organiseerbaar in connector groups, elke group handelt traffic naar specifieke applicaties af

- Server vereisten voor connector (examen kernstof)
  - Windows Server 2016 of later
  - Aanbevolen: meer dan 1 server voor high availability
  - Minimaal .NET v4.7.2+
  - TLS 1.2 vereist op de Windows Server

- Benodigde outbound poorten
  - Poort 80; downloaden van certificate revocation lists (CRLs) tijdens TLS/SSL certificate validatie
  - Poort 443; alle outbound communicatie met de Application Proxy service

- Benodigde URLs (referentie, niet uit het hoofd leren)
  - Verschillende Microsoft/DigiCert URLs nodig voor communicatie met de Application Proxy cloud service, certificate verificatie, en het registratieproces, via poort 443/HTTPS en 80/HTTP

- Connector installeren via Entra (stappen)
  1. Global Administrator van de directory die Application Proxy gebruikt
  2. Bevestigen dat je in de juiste directory zit (Switch directory indien nodig)
  3. Global Secure Access > Connect > Connectors
  4. Download connector service
  5. Terms of Service accepteren, Accept terms & Download
  6. Installeren via Run
  7. Wizard doorlopen, Global Administrator credentials invoeren om de connector te registreren bij Application Proxy

- Connector installatie verifieren
  - Op de Windows Server: services.msc openen, checken of "Microsoft Entra private network connector" en "Microsoft Entra private network connector Updater" op Running staan, anders handmatig starten
  - In Entra: Global Secure Access > Connect > Connectos, connector uitklappen voor details. Groen label = kan verbinden met de service (netwerkproblemen kunnen berichten alsnog blokkeren, ondanks groen label)

- Connector groups aanmaken (stappen)
  1. Global Secure Access > Connect > Connectors
  2. New connector group
  3. Naam geven, connectors selecteren via dropdown
  4. Save

- Stap 2: Quick Access configureren
  - Definieert specifieke FQDNs of IP adressen van private resources die onder Private Access traffic vallen
  - 3 onderdelen: naam voor de Quick Access app, connector group koppelen, application segments toevoegen (kan gelijktijdig of later)

- Quick Access opzetten (stappen)
  1. Global Secure Access > Applications > Quick access
  2. Naam invoeren (aanbevolen: "Quick Access")
  3. Connector group selecteren uit dropdown
  4. Save (app zonder FQDNs/IP's kan al opgeslagen worden)

- Application segment toevoegen (destination types, examen kernstof)
  - IP address; IPv4 adres, plus poorten
  - Fully qualified domain name (incl. wildcard FQDNs); domeinnaam, plus poorten. NetBIOS niet ondersteund (gebruik contoso.local/app1, niet contoso/app1)
  - IP address range (CIDR); bv. 192.0.2.0/24, eerste 24 bits = network address, resterende 8 bits = host address
  - IP address range (IP to IP); van start IP tot eind IP, plus poorten
  - Poorten: komma voor meerdere poorten, hyphen voor een range, spaties worden verwijderd (bv. 400-500, 80, 443)

- Meestgebruikte poorten en protocollen (examen kernstof)

| Poort | Protocol |
|---|---|
| 22 | Secure Shell (SSH) |
| 80 | Hypertext Transfer Protocol (HTTP) |
| 443 | Hypertext Transfer Protocol Secure (HTTPS) |
| 445 | Server Message Blocks (SMB) file sharing |
| 3389 | Remote Desktop Protocol (RDP) |

- Users en groups toewijzen aan Quick Access
  - Global Secure Access > Applications > Quick Access > Edit application settings > Users and groups
  - Users/groups toevoegen, Conditional Access policies optioneel toepasbaar

- Stap 3: Private Access traffic forwarding profile inschakelen
  - Routeert traffic naar het private netwerk via de Global Secure Access Client
  - Laat remote workers zonder VPN verbinden met interne resources
  - Controle over welke private resources getunneld worden, plus Conditional Access policies toepasbaar
  - Stappen: Global Secure Access > Connect > Traffic forwarding > checkbox Private access profile aanvinken

- Stap 4: Global Secure Access Client installeren (zelfde proces als bij Internet Access)
  - Deploybaar via Intune, of handmatig
  - Download: Global Secure Access Administrator > Global Secure Access > Connect > Client download
  - Installatie Windows: setup file kopieren, GlobalSecureAccessClient.exe draaien, licentievoorwaarden accepteren, inloggen met Entra credentials, connectie icoon wordt groen
  - Android: via Intune of Microsoft Defender for Endpoint on Android, client uit de Android store

- Onthouden voor examen
  - Connector vereist minimaal Windows Server 2016, .NET 4.7.2+, en TLS 1.2
  - Groen label bij een connector betekent dat hij kan verbinden, maar garandeert niet dat er geen netwerkproblemen zijn
  - NetBIOS wordt niet ondersteund bij FQDN based application segments
  - Private Access vervangt in dit scenario de noodzaak van een traditionele VPN voor remote toegang tot interne resources
    
---

### Explore how to use the Dashboard to drive Global Secure Access

- Toegang tot het dashboard
  - Global Secure Access Administrator > Global Secure Access > Dashboard

- Wat het dashboard doet
  - Visualisaties van network traffic verzameld door Private Access en Internet Access
  - Aggregeert data van network configuraties, devices, users, en tenants
  - Bestaat uit meerdere widgets

- Widgets, overzicht
  - Volume devices met de Global Secure Access client
  - Wijzigingen in aantal actieve devices
  - Alerts en belangrijke notificaties
  - Service usage patterns
  - Meest gebruikte destinations
  - Unique users over alle tenants
  - Populairste website categorieen
  - Meest gebruikte private application segments

- Global Secure Access snapshot
  - Samenvatting van users, devices, en secured applications
  - Users; distincte users laatste 24 uur, gebaseerd op user principal name (UPN)
  - Devices; distincte devices laatste 24 uur, gebaseerd op device ID
  - Workloads; distincte destinations laatste 24 uur, gebaseerd op FQDNs en IP adressen
  - Filterbaar op Internet Access, Private Access, of Microsoft traffic

- Alerts and notifications (preview)
  - Toont netwerkactiviteit en helpt verdachte activiteiten/trends te identificeren
  - Veelvoorkomende alerts:
    - Unhealthy remote network; 1 of meer device links disconnected
    - Increased external tenants activity; toename in users die externe tenants benaderen
    - Token and device inconsistency; origineel token gebruikt op een ander device
    - Web content blocked; toegang tot een website geblokkeerd

- Usage profiling (preview)
  - Toont usage patterns over een gekozen periode
  - Display by filter: Transactions, Users, Devices, Bytes sent, Bytes received

- Top used destinations
  - Toont alle traffic types, gesorteerd op aantal transacties, filterbaar per traffic type
  - Filters: Transactions (meeste transacties laatste 24u), Users (meeste distincte users), Devices (meeste distincte device IDs), Bytes sent, Bytes received (per IP adres, laatste 24u)
  - View all destinations knop voor meer detail

- Cross-tenant access
  - Zichtbaarheid in users/devices die andere tenants benaderen
  - Sign-ins; aantal sign ins via Entra ID naar Microsoft services laatste 24u
  - Total distinct tenants; aantal unieke tenant IDs laatste 24u
  - Unseen tenants; tenant IDs gezien in laatste 24u maar niet in de 7 dagen ervoor
  - Users; aantal unieke user sign ins naar andere tenants laatste 24u
  - Devices; aantal unieke devices die inlogden bij andere tenants laatste 24u
  - Configure tenant restrictions knop leidt naar Session management, om tenant restriction settings te checken

- Web category filtering
  - Toont top categorieen van geblokkeerde/toegestane webcontent
  - Helpt bepalen welke sites/categorieen je wilt blokkeren
  - Sorteerbaar op Transactions, Users, Devices
  - View all web categories voor meer detail

- Device status
  - Active devices; distincte device IDs laatste 24u, met % verandering
  - Inactive devices; distincte device IDs gezien in laatste 7 dagen maar niet in laatste 24u, met % verandering

- Onthouden voor examen
  - De meeste widgets werken met een 24 uur venster, tenzij anders vermeld (bv. inactive devices kijkt naar 7 dagen)
  - UPN wordt gebruikt om users te identificeren, device ID om devices te identificeren, FQDN/IP om destinations te identificeren
  - Cross tenant access widget koppelt direct terug naar de tenant restrictions configuratie
 
---

### Create remote networks for use with Global Secure Access

- Wat een remote network is
  - Een remote locatie (bv. branch office) of netwerk dat internetconnectiviteit nodig heeft
  - Verbindt users op afstand met Global Secure Access
  - Na configuratie: traffic forwarding profile toewijsbaar om corporate network traffic te beheren
  - Laat network security policies toepassen op outbound traffic

- Hoe de verbinding technisch werkt
  - Een IPSec tunnel tussen een core router (customer premises equipment, CPE) op de remote locatie en het dichtstbijzijnde Global Secure Access endpoint
  - Alle internet bound traffic gaat via die core router, voor security policy evaluatie in de cloud
  - Geen client installatie nodig op individuele devices, in tegenstelling tot Internet/Private Access die wel de Global Secure Access Client gebruiken

- 5 stappen om een Remote Network te configureren (examen kernstof)

| Stap | Beschrijving |
|---|---|
| Basics | Naam van het remote network en de regio waarmee verbonden wordt |
| Connectivity | Gegevens over de on premises router, waar het signaal vandaan komt |
| Traffic Forwarding | Traffic forwarding profile toevoegen om te bepalen welk type verkeer wordt toegelaten |
| Review Configuration | Setup bevestigen, instellingen verzamelen voor de on premises router |
| Setup on-premises router | Microsoft connectivity settings invoeren in het management console van de on premises router |

  - Uitvoerbaar via Microsoft Entra admin center of Microsoft Graph API
  - De laatste stap gebeurt op de on premises router zelf, niet in Entra

- Configure Basics
  - Global Secure Access Administrator > Global Secure Access > Connect > Remote networks
  - Create remote network, invullen: Name, Region

- Setup Connectivity
  - Next: Connectivity, invullen: Name, Device type (meestal router), IP address van het device, type redundancy, Bandwidth

- Enable Traffic forwarding profiles
  - Nieuwe traffic forwarding profile aanmaken, of een bestaande selecteren die eerder is gemaakt bij Private Access of Internet Access

- Configuratie afronden: on premises router instellen
  - Alle remote networks staan op de Remote network pagina
  - View configuration link in de Connectivity details kolom geeft de connectiviteitsgegevens vanaf de Microsoft kant
  - Deze gegevens moet je invoeren in het management console van je eigen CPE, niet in het Entra admin center
  - IPsec is bidirectioneel; Internet Key Exchange (IKE) onderhandelingen moeten plaatsvinden tussen beide partijen voordat de tunnel werkt
  - Zonder deze laatste stap werkt de IPsec verbinding niet

- Onthouden voor examen
  - Remote networks gebruiken geen client software op devices, in tegenstelling tot Internet Access/Private Access die de Global Secure Access Client vereisen
  - De verbinding is een IPSec tunnel tussen CPE en het dichtstbijzijnde Global Secure Access endpoint
  - De laatste configuratiestap gebeurt altijd op de router zelf, buiten Entra om
  - Traffic forwarding profile kan hergebruikt worden vanuit Private Access of Internet Access configuratie

---

### Use Conditional Access with Global Secure Access

- Waarom combineren
  - Extra beveiligingslagen na deployment van Global Secure Access
  - Voorkomt kwaadaardige toegang tot Microsoft apps, SaaS apps, en private line of business (LoB) apps
  - Meerdere condities combineerbaar voor defense in depth (device compliance, locatie, etc.)

- 3 nieuwe checks in Conditional Access (examen kernstof)
  - Compliant network check; verifieert dat users verbinden via een geverifieerd netwerk connectivity model voor hun tenant, compliant met security policies
  - Private Access apps; Conditional Access policies toepasbaar op Private Access apps, voor interne/private resources
  - Source IP restoration; herstelt de originele source IP van de user, die anders verloren gaat door de cloud based network proxy tussen user en resource

- Vereiste eenmalige stap: Global Secure Access signaling enablen
  - Nodig voor zowel Compliant network check als Source IP restoration
  - Global Secure Access Administrator > Global Secure Access > Global settings > Session management > Adaptive access
  - Toggle Enable CA Signaling for Microsoft Entra ID (covering all cloud apps)
  - Continuous Access Evaluation (CAE) signaling wordt automatisch enabled voor Office 365 (preview)
  - Protection > Conditional Access > Named locations; controleren of "All Compliant Network locations" bestaat (type Network Access), optioneel als trusted markeren

- Compliant Network Check, hoe het werkt
  - Handhaving op 2 niveaus: authentication plane en data plane (preview)
  - Authentication plane; Entra ID handhaaft tijdens user authenticatie zelf
  - Data plane; werkt met services die Continuous Access Evaluation (CAE) ondersteunen, momenteel alleen Exchange Online en SharePoint Online. Biedt token theft replay protection
  - Voorkomt dat andere organisaties die ook Global Secure Access gebruiken toegang krijgen tot jouw resources (bv. Contoso beschermt Exchange/SharePoint zo dat Fabrikam's eigen compliant network check niet voldoet aan Contoso's eisen)

- Policy om resources achter compliant network te beschermen (stappen)
  1. Minimaal Conditional Access Administrator
  2. Protection > Conditional Access > Create new policy, naam geven
  3. Assignments > Users or workload identities > Include All users, Exclude emergency/break glass accounts
  4. Target resources > Include > Select apps: Exchange Online en/of SharePoint Online en/of SaaS apps. Let op: brede "Office 365" cloud app NIET ondersteund, niet selecteren
  5. Conditions > Location > Yes > Include Any location, Exclude Selected locations > All Compliant Network locations
  6. Access controls > Grant > Block Access
  7. Enable policy On > Create
  - Typische policy: blokkeer toegang vanaf alle netwerklocaties, behalve Compliant Network

- Conditional Access voor Private Access apps (stappen)
  1. Minimaal Conditional Access Administrator
  2. Global Secure Access > Applications > Enterprise applications
  3. Applicatie selecteren uit de lijst
  4. Conditional Access in het zijmenu, bestaande policies verschijnen als lijst
  5. Create new policy; de geselecteerde app wordt automatisch als Target resource toegevoegd
  6. Conditions, access controls, en users/groups verder configureren
  - Vanuit Global Secure Access starten voegt de app automatisch toe als target, dus dat hoef je niet los te doen

- Source IP Restoration
  - Herstelt de originele user Source IP voor backward compatibility
  - Voordelen: Source IP based location policies blijven werken in Conditional Access en CAE, Identity Protection krijgt consistente originele Source IP voor risk scoring, originele Source IP zichtbaar in Entra sign in logs

- Known limitations Source IP Restoration (examen kernstof)
  - Als het enabled is, zie je alleen de source IP, niet het IP van de Global Secure Access service zelf
  - Momenteel alleen ondersteund voor Microsoft traffic (SharePoint Online, Exchange Online, Teams, Microsoft Graph)
  - Met CAE's strict location enforcement kunnen users alsnog geblokkeerd worden, ondanks dat ze in een trusted IP range zitten

- Source IP Restoration inschakelen
  - Wordt automatisch enabled zodra je Global Secure Access signaling aanzet, geen aparte configuratie nodig

- User exclusions (herhaling van eerdere unit)
  - Emergency/break glass accounts; voorkomt tenant wide lokcout
  - Service accounts/service principals (bv. Entra Connect Sync Account); niet interactief, niet gekoppeld aan een specifieke user

- Onthouden voor examen
  - Compliant network check werkt op authentication plane (altijd) en data plane (alleen Exchange/SharePoint via CAE)
  - Global Secure Access signaling enablen is een eenmalige, verplichte voorstap voor zowel compliant network check als source IP restoration
  - Source IP restoration dekt alleen Microsoft traffic, geen third party apps
  - De brede "Office 365" cloud app optie wordt ook hier niet ondersteund in de compliant network policy
 
--- 

### Explore logs and monitoring options with Global Secure Access

- Waarom monitoring belangrijk is
  - Activiteit van traffic door je netwerken moet gevolgd worden
  - Logs geven inzicht in netwerkverkeer

- Global Secure Access Audit logs
  - Entra audit log is een waardevolle bron bij onderzoek/troubleshooting van wijzigingen in de Entra omgeving
  - Wijzigingen gerelateerd aan Global Secure Access worden hierin vastgelegd
  - Categorieen: filtering policy, forwarding profiles, remote network management, en meer

- Audit logs bekijken (2 manieren)
  - Via Global Secure Access: Global Secure Access > Audit logs, filters staan al vooraf ingevuld met relevante categorieen/activiteiten
  - Via Entra monitoring: Identity > Monitoring & health > Audit logs, Date range kiezen, Service filter op Global Secure Access, Category filter minimaal 1 optie selecteren, Apply

- Traffic logs (preview)
  - Overzicht van netwerkverbindingen en transacties: wie benaderde wat, vanwaar, met welk resultaat
  - Snapshot van alle verbindingen, gecategoriseerd, incl. traffic type destination, source IP, etc.

- 3 niveaus van traffic logs (examen kernstof)
  - Session; start bij de eerste URL die een user benadert, kan meerdere connections openen (bv. een nieuwssite met ads van meerdere andere sites)
  - Connection; bevat source/destination IP, source/destination port, en FQDN, samen de 5 tuple genoemd
  - Transaction; 1 unieke request/response paar

- Traffic logs bekijken (stappen)
  - Minimaal Reports Reader rol
  - Global Secure Access > Monitor > Traffic logs
  - Verschillende filters en export opties beschikbaar

- Enriched Office 365 logs (preview)
  - Inzicht in performance, experience, en availability van M365 apps
  - Te integreren met Log Analytics workspace of een SIEM tool voor verdere analyse
  - Geeft network diagnostic data, performance data, en security events relevant voor M365 apps
  - Voorbeeld nut: als M365 toegang geblokkeerd is voor een user, zie je hoe het device verbindt met het netwerk

- Wat deze logs bieden
  - Verbeterde latency
  - Extra informatie toegevoegd aan originele logs
  - Nauwkeurig IP adres

- Enriched M365 logs bekijken (eenmalig, 2 stappen)
  1. Global Secure Access Network Traffic logs en M365 Unified Audit logs verzamelen op hetzelfde endpoint (Microsoft Sentinel aanbevolen)
  2. Eigen join query maken om de 2 tabellen te correleren, of de kant en klare Global Secure Access Enriched Microsoft 365 Logs workbook gebruiken
  - Gebruikt de bestaande tabellen Microsoft 365 OfficeActivity en Global Secure Access NetworkAccessTraffic, gecombineerd via een Unique Token ID
  - Let op: momenteel alleen SharePoint Online logs beschikbaar voor deze log enrichment

- Logs naar een endpoint sturen (stappen)
  1. Minimaal Security Administrator
  2. Identity > Monitoring & health > Diagnostic settings
  3. Add Diagnostic setting
  4. Naam geven
  5. NetworkAccessTrafficLogs selecteren
  6. Destination kiezen: Log Analytics workspace, storage account (archief), event hub (stream), of partner solution

- Log retention en storage (examen kernstof)
  - Traffic logs en remote network health logs; 30 dagen bewaard
  - Audit logs; retentieperiode varieert per Entra ID licentie
  - Office logs; kortste bewaartermijn, slechts 24 uur

- Onthouden voor examen
  - 5 tuple = source IP, destination IP, source port, destination port, en FQDN (onderdeel van de Connection laag)
  - Enriched M365 log correlatie werkt momenteel alleen voor SharePoint Online
  - Office logs hebben veruit de kortste retentie (24 uur) vergeleken met traffic logs (30 dagen) en audit logs (licentie afhankelijk)
 
---

## Module Assessment — Module 6 (Deploy and Configure Microsoft Entra Global Secure Access)

**Score:** 100%

### Vraag 1
What is the main function of Microsoft Entra Private Access?

- ✅ It provides your users secure access to your private, corporate resources without requiring a VPN.
- It secures access to Microsoft services, SaaS, and public internet apps while protecting users, devices, and data against internet threats.
- It provides a unified portal to streamline the roll-out and management of the access control capabilities.

### Vraag 2
What is the purpose of enabling the Microsoft traffic forwarding profile in Microsoft Entra Internet Access?

- It allows users to bypass the Global Secure Access client when accessing Microsoft resources, like Exchange Online and SharePoint Online.
- It enables users to access Microsoft resources without any restrictions.
- ✅ With the Microsoft profile enabled, Microsoft Entra Internet Access acquires the traffic going to Microsoft services, like Exchange Online and SharePoint Online.

### Vraag 3
What is the purpose of configuring a Microsoft Entra private network connector and connector groups?

- To facilitate inbound connection to the Global Secure Access service and handle traffic to specific applications.
- To install on a Windows device that doesn't have access to the backend resources and applications.
- ✅ To facilitate the outbound connection to the Global Secure Access service and handle traffic to specific applications.

### Vraag 4
What does the Global Secure Access snapshot widget provide in the Dashboard?

- ✅ It provides a summary of how many users and devices are using the service and how many applications were secured through the service.
- It provides a summary of the number of users and devices using the service and how many applications blocked by the service.
- It provides a summary of the number of users and devices using the service and how many alerts were generated.

### Vraag 5
What is the final step in configuring a Remote Network for use with Global Secure Access?

- Defining the name of your remote network and the region where you want to connect.
- Reviewing the configuration in the Microsoft Entra admin center.
- ✅ Updating the on-premises router configuration with the Microsoft connectivity settings.

### Vraag 6
What is the purpose of the Compliant Network Check in Conditional Access with Global Secure Access?

- It allows any organization using Microsoft's Global Secure Access services to access your resources.
- It checks if the network is compliant with the security policies of any tenant.
- ✅ It ensures users connect from a verified network connectivity model for their specific tenant and are compliant with security policies enforced by administrators.

### Vraag 7
What is the purpose of Global Secure Access Audit logs?

- They provide information about Microsoft 365 workloads, so you can review network diagnostic data, performance data, and security events relevant to Microsoft 365 apps.
- ✅ They provide information when researching or troubleshooting changes to your Microsoft Entra environment, capturing changes related to Global Secure Access in several categories.
- They provide a summary of the network connections and transactions that are occurring in your environment.


---
---


### Samenvatting Module 6 termen

- Global Secure Access; de overkoepelende Security Service Edge (SSE) solution van Microsoft, bestaat uit Internet Access en Private Access
- Microsoft Entra Internet Access; service die publieke internet/SaaS/Microsoft app toegang beveiligt via een Secure Web Gateway (SWG)
- Microsoft Entra Private Access; service die veilige toegang geeft tot private corporate resources, zonder VPN
- Global Secure Access Client; de app/client die op end user devices geinstalleerd wordt om traffic te herkennen en te beveiligen
- Traffic forwarding profile; configuratie die bepaalt welk soort verkeer (Microsoft, Internet, of Private) via Global Secure Access gerouteerd wordt
- Tenant restrictions; policy die bepaalt welke externe tenants users wel/niet mogen benaderen
- Connector; lightweight agent op een on premises Windows Server, faciliteert de outbound verbinding naar Global Secure Access
- Connector group; verzameling connectors, gebruikt om traffic naar specifieke applicaties te routeren
- Quick Access; app binnen Private Access waarin je FQDNs/IP adressen van private resources definieert die toegankelijk worden
- Application segment; de specifieke FQDN, IP adres, of IP range die je toevoegt aan Quick Access
- Remote network; een externe locatie (bv. branch office) die via een IPSec tunnel (CPE naar Global Secure Access endpoint) verbonden wordt, zonder client op individuele devices
- Compliant network check; Conditional Access controle die verifieert dat een user verbindt via een goedgekeurd netwerk model voor zijn tenant
- Source IP restoration; herstelt de originele IP van de user, die anders verloren gaat door de cloud proxy
- Dashboard; overzichtspagina met widgets (snapshot, alerts, usage profiling, top destinations, cross tenant access, web category filtering, device status)
- Audit logs; logt wijzigingen aan de Global Secure Access configuratie zelf
- Traffic logs; logt daadwerkelijke netwerkverbindingen en transacties (session, connection, transaction niveaus)
- Enriched Office 365 logs; gecombineerde data van M365 en Global Secure Access traffic logs, voor performance/security inzicht in M365 apps

  











































