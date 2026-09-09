# Exercise: Implement Access Management for Apps

**Bron:** SC-300 Learning Path; Implement access management for apps

## Doel
Een enterprise app (GitHub Enterprise Cloud) toevoegen aan de tenant en een user toewijzen, om te oefenen met app-toegang beheer.

## Wat ik heb gedaan
1. P2 trial activeren: niet uitgevoerd/overgeslagen
2. Enterprise app toevoegen:
   - Identity > Enterprise applications > + New application
   - Gezocht op GitHub, geselecteerd: GitHub Enterprise Cloud – Enterprise Account
   - Instellingen bekeken (SAML-based Sign-on, provisioning niet ondersteund), Create geklikt
   - App succesvol aangemaakt, Overview toont Name, Application ID, Object ID
3. User toewijzen aan de app:
   - Getting Started > Assign users and groups (of Manage > Users and groups)
   - + Add user/group
   - Groups niet beschikbaar voor assignment: melding dat dit de licentie/plan level vereist, alleen individuele users mogelijk
   - Eigen account (Robert-Jan Paulides) geselecteerd als User, Assign
   - Bevestigd zichtbaar in de lijst met role "msiam_access" (default role, geen custom app roles gedefinieerd)

## Resultaat
Grotendeels uitgevoerd zonder P2. Enterprise app aanmaken en individuele user toewijzen werkte volledig. Group-based assignment was geblokkeerd, met een expliciete melding dat dit een hogere licentie/plan vereist.

## Wat dit aantoont
- Praktische ervaring met het toevoegen van een gallery enterprise app en het toewijzen van users
- Begrip van het verschil tussen individuele user assignment (werkt op elk niveau) en group-based assignment (vereist hogere licentie)
- Kennis van de default "msiam_access" role die verschijnt als een app geen eigen custom app roles heeft
