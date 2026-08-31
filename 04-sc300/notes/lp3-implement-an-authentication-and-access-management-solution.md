# SC-300: Microsoft Identity and Access Administrator

## Learning Path 2: Implement an authentication and access management solution
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
  - Blokkade gebeurt op basis van user risk of sign in risk

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












