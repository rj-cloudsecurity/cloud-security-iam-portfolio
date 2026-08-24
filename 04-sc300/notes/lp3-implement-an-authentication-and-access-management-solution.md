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
































