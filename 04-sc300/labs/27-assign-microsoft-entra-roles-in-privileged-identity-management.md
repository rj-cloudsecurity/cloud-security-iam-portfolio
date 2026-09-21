# Exercise: Assign Microsoft Entra Roles in Privileged Identity Management

**Bron:** SC-300 Learning Path; Plan and implement an identity governance strategy

## Doel
Een user eligible maken voor de Compliance Administrator rol, de rol activeren via My roles, een role assignment met restricted scope proberen, en een bestaande assignment updaten/verwijderen.

## Wat niet kan (vereist Entra ID P2 of Entra ID Governance)
- Privileged Identity Management > Microsoft Entra roles > Roles toont dezelfde licentiemelding en lege rollenlijst als bevestigd in de vorige exercise
- Geen enkele stap uitvoerbaar: assignment aanmaken, activeren, scope beperken, of bestaande assignment beheren

## Stappen (theorie, volledige flow)

### Rol toewijzen als eligible
1. PIM > Microsoft Entra roles > Roles > + Add assignments
2. Membership tab: rol selecteren (Compliance Administrator), member selecteren (eigen account)
3. Settings tab: Assignment type, default op Eligible laten staan
   - Eligible; user moet eerst activeren (MFA, justification, of approval)
   - Active; permissies staan altijd aan, geen actie nodig
4. Assign

### Rol activeren
1. PIM > My roles
2. Eligible assignments bekijken
3. Bij Compliance Administrator: Activate
4. Additional verification required (MFA), eenmalig per sessie
5. Reason invullen
6. Activate

### Rol toewijzen met restricted scope (voorbeeld)
1. Roles > + Add assignments
2. Rol: User administrator
3. Scope type: Directory (of Administrative unit voor beperktere scope)
4. Members en settings zoals normaal

### Bestaande assignment updaten/verwijderen
1. PIM > Microsoft Entra roles > Assignments
2. Bij Compliance Administrator: Update (membership settings aanpassen) of Remove
3. Bij Remove: bevestigen met Yes

## Resultaat
Niet uitvoerbaar, consistent met de vorige PIM exercise. PIM voor Microsoft Entra roles blijft volledig geblokkeerd zonder P2 of Entra ID Governance licentie.

## Wat dit aantoont
- Begrip van het verschil tussen Eligible en Active role assignments
- Kennis van de activatie flow: MFA verificatie + justification vereist bij eligible roles
- Begrip van scope beperking bij role assignments (Directory vs Administrative unit)
- Herkenning van hetzelfde P2/Governance gated patroon door de hele PIM module heen
