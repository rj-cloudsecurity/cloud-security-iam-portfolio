# Sandbox: Sign-in Risk Policy That Requires MFA (Report-only)

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Een sign-in risk policy moet bij risicovolle inlogpogingen om MFA vragen in plaats van de toegang te blokkeren. Gebruikers moeten die MFA-vraag kunnen beantwoorden, en het beleid moet eerst in report-only draaien.

## Doel
Uitzoeken wat er eerst moet zijn ingesteld zodat gebruikers de MFA-vraag kunnen beantwoorden, en een sign-in risk policy in report-only aanmaken.

## Stappen
1. Entra admin center -> **Entra ID** -> **ID Protection** -> **Multifactor authentication registration policy**
2. Daar stonden Assignments op **All users**, de control **Require Microsoft Entra ID multifactor authentication registration** aangevinkt en Policy enforcement op **Disabled**. Op **Enabled** gezet en opgeslagen
3. **ID Protection** -> **Sign-in risk policy** geopend: de melding "Legacy risk policy management is retired" verscheen, met het advies sign-in risk beleid in Conditional Access te maken
4. **Entra ID** -> **Conditional Access** -> **Policies** -> **New policy**, naam `Sign-in risk: require MFA`
5. Users: All users, met mijn twee beheerdersaccounts uitgesloten. Target resources: All resources
6. Conditions -> **Sign-in risk**: Medium en High
7. Grant -> **Require multifactor authentication**
8. Enable policy: **Report-only** -> **Create**

## Resultaat
- Het beleid "Sign-in risk: require MFA" staat in de lijst met Conditional Access policies met de status **Report-only**
- De legacy sign-in risk policy in ID Protection kon ik niet meer bekijken of wijzigen
- Niet getest: of het beleid daadwerkelijk wordt toegepast. In report-only wordt niets afgedwongen en ik heb geen risicovolle inlog opgewekt, dus ik heb in de sign-in logs niets gezien dat bij dit beleid hoort

## Wat dit aantoont
- Wat eerst op orde moet zijn, is MFA-registratie: de MFA registration policy in ID Protection laat gebruikers zich voor MFA registreren, zodat ze de MFA-vraag van een risicobeleid kunnen beantwoorden
- Een sign-in risk policy stel je nu in via Conditional Access (conditie Sign-in risk), niet meer in ID Protection zelf
- Met "Require multifactor authentication" in plaats van "Block access" worden risicovolle inlogs gevraagd om MFA in plaats van geweigerd
- Report-only laat de impact zien zonder iets af te dwingen
