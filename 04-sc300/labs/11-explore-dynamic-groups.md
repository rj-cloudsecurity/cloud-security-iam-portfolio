# Exercise: Explore Dynamic Groups

**Bron:** SC-300 Learning Path; Implement an identity management solution using Microsoft Entra ID

## Doel
Een dynamic security group aanmaken die automatisch alle users (members én guests) bevat, om te oefenen met dynamic membership rules.

## Wat wel kan (zonder P1)
- Group aanmaken met Group type: Security
- Group name invullen
- Bij Membership type de optie **Dynamic User** selecteren en zien hoe de UI eruitziet
- Bij Add dynamic query -> Edit rule syntax de rule `user.objectId -ne null` invoeren

## Wat niet kan (vereist Entra ID P1)
- De group daadwerkelijk **opslaan/aanmaken** met Dynamic User membership; dit faalt in de Free tier tenant met een licentie-foutmelding
- Members zien automatisch toegevoegd worden op basis van de rule

## Stappen (theorie, volledige flow)
1. Microsoft Entra admin center -> Identity -> Groups -> All Groups -> New group
2. Group type: Security
3. Group name: All company users dynamic group
4. Membership type: Dynamic User
5. Add dynamic query -> Edit rule syntax
6. Rule: `user.objectId -ne null`
7. Save
8. Create

## Resultaat
Niet volledig uitvoerbaar; Dynamic User membership vereist Entra ID P1, niet beschikbaar op de Free tier. UI tot en met het invoeren van de rule kan wel bekeken worden; het daadwerkelijk aanmaken van de group faalt.

## Wat dit aantoont
- Begrip van dynamic group membership en rule syntax
- Kennis van de `-ne null` rule als manier om letterlijk alle users (inclusief B2B guests) automatisch op te nemen in een group
- Bewustzijn van de licentie-vereisten en grenzen van een Free tier tenant
