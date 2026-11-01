# Sandbox: Exploring SSPR Authentication Methods

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Uitzoeken welke authenticatiemethoden beschikbaar zijn voor self-service password reset (SSPR) bij 1 en bij 2 vereiste methoden.

## Doel
De SSPR-instellingen voor het aantal methoden bekijken en vaststellen waar de beschikbare methoden worden beheerd.

## Stappen
1. Entra admin center -> Entra ID -> **Password reset** -> **Authentication methods**
2. *Number of methods required to reset* op **1** en daarna op **2** gezet
3. Bij beide instellingen stond onder *Methods available to users* alleen **Security questions**, met de melding dat andere methoden via het auth methods policy worden beheerd
4. Entra ID -> **Authentication methods** -> **Policies** geopend
5. Bekeken welke methoden aanstaan

## Resultaat
- De lijst met methoden verandert niet als het aantal vereiste methoden van 1 naar 2 gaat
- Bij Password reset kan ik alleen security questions aan- of uitzetten; de portal meldt dat security questions in maart 2027 worden uitgefaseerd
- In het auth methods policy staan **Microsoft Authenticator**, **Temporary Access Pass**, **Software OATH tokens** en **Email OTP** aan voor alle users
- **Passkey (FIDO2)**, **SMS**, **Hardware OATH tokens**, **Voice call**, **Certificate-based authentication**, **Verified ID** en **QR code** staan uit

## Wat dit aantoont
- Welke methoden SSPR kan gebruiken, stel je in via het auth methods policy en niet meer bij Password reset
- Het aantal vereiste methoden (1 of 2) staat bij Password reset, de beschikbare methoden bij Authentication methods > Policies
- Admins hebben een eigen beleid en zijn altijd verplicht twee methoden te gebruiken
- Niet getest: de reset zelf als een gewone user (registreren op aka.ms/ssprsetup en resetten op aka.ms/sspr)
