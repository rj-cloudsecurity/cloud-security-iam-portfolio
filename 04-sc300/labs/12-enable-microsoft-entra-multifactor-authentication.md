# Exercise: Enable Microsoft Entra Multifactor Authentication

**Bron:** SC-300 Learning Path; Implement an authentication and access management solution

## Doel
MFA instellingen bekijken en een Conditional Access policy aanmaken die MFA afdwingt voor guest users die specifieke apps benaderen.

## Wat wel kan (zonder P1)
- Conditional Access Overview pagina bekijken: Entra ID > Security > Conditional Access
- De uitleg, voorbeeld conditions/controls en Get Started stappen lezen op de Overview pagina

## Wat niet kan (vereist Entra ID P1 of P2)
- MFA instellingen bekijken: Entra ID > Security > Multifactor authentication toont direct een premium landingspagina ("Get a free Premium trial to use this feature"), de Service Settings zelf (incl. app passwords) zijn niet toegankelijk zonder P1 of P2
- Een Conditional Access policy aanmaken: de knoppen "Create new policy" en "Create new policy from templates" staan grijs/disabled op de Overview pagina, dus zelfs het invulscherm is niet te openen zonder P1 of P2
- MFA daadwerkelijk afdwingen bij het inloggen van een guest user

## Stappen (theorie, volledige flow)

### Configure multifactor authentication options
1. Azure portal > Microsoft Entra ID > Security > Multifactor authentication
2. Onder Configure > Additional cloud based multifactor authentication settings
3. Service Settings bekijken (o.a. app passwords aan/uit voor apps die geen MFA ondersteunen)

### Set up Conditional Access rules for MFA
1. Microsoft Entra ID > Security > Conditional Access > Create new policy
2. Naam: bv. "All guests"
3. Users: specifieke users/groups selecteren onder Include
4. Target resources: Cloud apps > specifieke apps selecteren onder Include
5. Conditions: Locations > Yes > Any location
6. Grant: Grant access > Require multifactor authentication > Select
7. Enable policy: On > Create

## Resultaat
Niet uitvoerbaar in de sandbox, verder dan alleen de Overview pagina van Conditional Access. Zowel de MFA Service Settings als het aanmaken van een nieuwe Conditional Access policy zijn volledig premium gated, niet alleen het opslaan van een policy met MFA grant.

## Wat dit aantoont
- Begrip van hoe Conditional Access policies zijn opgebouwd (Users, Target resources, Conditions, Grant), ook zonder ze zelf te kunnen aanmaken
- Kennis van de IF THEN structuur: IF een guest een specifieke app benadert, THEN MFA vereist
- Bewustzijn van de licentie vereisten en grenzen van een Free tier tenant, inclusief dat zowel MFA settings als Conditional Access volledig premium gated zijn op Free tier
