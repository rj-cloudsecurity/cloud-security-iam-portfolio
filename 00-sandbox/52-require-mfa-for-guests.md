# Sandbox: Requiring MFA for External Guests with Conditional Access

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Externe gasten moeten extra worden beveiligd. Uitzoeken wat er gebeurt als een Conditional Access-policy MFA eist van gasten.

## Doel
Een policy maken die MFA vereist voor de group External User Group en testen met een gast.

## Stappen
1. Entra admin center -> **Entra ID** -> **Conditional Access** -> **Policies** -> **New policy**
2. **Users** -> Include: de group **External User Group**; Exclude: mijn eigen gastaccount met de rol Global Administrator
3. **Target resources**: **All resources**
4. **Grant** -> **Require multifactor authentication**
5. **Enable policy**: **On** -> **Create**
6. Als een van de gasten ingelogd bij `myapps.microsoft.com` in een privévenster, na het accepteren van de uitnodiging
7. De policy daarna op **Report-only** gezet

## Resultaat
- De policy werkte zoals verwacht bij het inloggen als gast
- Het gast-admin-account was uitgesloten, zodat ik zelf niet buitengesloten kon raken

## Wat dit aantoont
- Een Conditional Access-policy kan MFA eisen van externe gasten via een group
- Een uitsluiting voorkomt dat een beheerder onder een policy valt die hem buitensluit
- Voor een test met een echte prompt moet de policy aan staan; Report-only laat alleen in de logs zien wat er zou gebeuren
- Niet getest: de instelling Cross-tenant access settings (inbound trust voor MFA van de eigen tenant van de gast)
