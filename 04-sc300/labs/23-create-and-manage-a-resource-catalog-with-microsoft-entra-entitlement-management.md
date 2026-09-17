# Exercise: Add App Roles to an Application and Receive Tokens

**Bron:** SC-300 Learning Path; Implement access management for apps

## Doel
Een custom app role aanmaken voor een applicatie, en een user aan die rol toewijzen.

## Wat ik heb gedaan

### App role aanmaken
1. Microsoft Entra admin center > Identity > App registrations
2. GitHub Enterprise Cloud - Enterprise Account geselecteerd (bestaande gallery app registration)
3. App roles > Create app role
4. Display name: Survey Writer
5. Allowed member types: User/Groups
6. Value: Survey.Create
7. Description: Writers can create surveys
8. Enable this app role aangevinkt, Apply

### User toewijzen aan de rol
1. Enterprise applications > GitHub Enterprise Cloud - Enterprise Account
2. Manage > Users and groups > + Add user/group
3. Users and groups > eigen account geselecteerd
4. Select a role > Survey Writer geselecteerd
5. Assign

## Resultaat
Volledig gelukt. De app role "Survey Writer" staat naast de default "msiam_access" role in de App roles lijst. Op de user's Overview pagina bevestigd: Assigned roles = 1.

## Wat dit aantoont
- Praktische ervaring met het aanmaken van custom app roles binnen een app registration
- Begrip van het onderscheid tussen de default msiam_access role en zelf gedefinieerde app roles
- Kennis van de assignment flow: role definieren in App registrations, toewijzen via Enterprise applications
- Bevestiging dat app roles en role assignment geen premium licentie vereisen
