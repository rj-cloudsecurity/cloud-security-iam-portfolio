# Exercise: Implement Conditional Access Policies Roles and Assignments

**Bron:** SC-300 Learning Path; Implement an authentication and access management solution

## Doel
Een Conditional Access policy aanmaken die toegang blokkeert tot alle apps vanaf elke locatie, om de basis flow te oefenen, en daarna testen en weer uitschakelen.

## Wat wel kan (zonder P1)
- Conditional Access > Policies pagina bekijken

## Wat niet kan (vereist Entra ID P1 of P2)
- Expliciete melding: "Your organization does not have sufficient licensing to access this product"
- New policy en New policy from template knoppen staan grijs/disabled
- Een Conditional Access policy aanmaken, testen of uitschakelen is volledig niet mogelijk

## Stappen (theorie, volledige flow)

### Policy aanmaken
1. Microsoft Entra admin center > Identity > Protection > Conditional access
2. + Create new policy
3. Naam: Test app conditional access
4. Assignments > Users and groups > Include > eigen administrator account
5. Cloud apps or actions > Cloud apps > Select apps > My apps
6. Conditions > Locations > Yes > Any location
7. Access controls > Grant > Block access
8. Enable policy: On > Create

### Policy testen
1. Nieuw browser tabblad > myapps.microsoft.com
2. Verifieren dat toegang tot My Apps geblokkeerd wordt
3. Als je nog ingelogd bent: tab sluiten, 1 tot 2 minuten wachten, opnieuw proberen

### Policy uitschakelen
1. Terug naar Conditional Access
2. Test app conditional access policy selecteren
3. Enable policy: Off > Save

## Resultaat
Niet uitvoerbaar. De Conditional Access Policies pagina toont expliciet dat de licentie ontoereikend is, en het aanmaken van een nieuwe policy is volledig geblokkeerd, consistent met de eerdere Conditional Access exercise.

## Wat dit aantoont
- Begrip van de volledige levenscyclus van een CA policy: aanmaken, valideren dat hij werkt, en weer uitzetten
- Herkenning van hetzelfde premium gated patroon als bij eerdere Conditional Access, MFA, SSPR en Smart Lockout labs
