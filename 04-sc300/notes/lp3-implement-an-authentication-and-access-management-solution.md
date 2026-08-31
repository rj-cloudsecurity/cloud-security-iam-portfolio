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
    - Security defaults blokkeert alle legacy authentication requests, incl. Exchange Active Sync basic authentication

- Onthouden voor examen
  - Security defaults zijn gratis en altijd beschikbaar, Conditional Access vereist P1
  - Security defaults en Conditional Access sluiten elkaar praktisch uit; als je Conditional Access gebruikt, gebruik je meestal geen security defaults meer
  - MFA registratie via security defaults heeft geen grace period
  - Legacy authentication is de meest voorkomende bron van succesvolle aanvallen, en wordt volledig geblokkeerd door security defaults

---

### Exercise: Work with security defaults
  - [04-sc300/labs/15-work-with-security-defaults](../../04-sc300/labs/15-work-with-security-defaults.md)

---


















