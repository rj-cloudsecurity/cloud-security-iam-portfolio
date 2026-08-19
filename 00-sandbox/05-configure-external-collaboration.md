# Sandbox: Configure External Collaboration

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Geïnspireerd op de Microsoft Learn oefening **"Exercise - configure external collaboration"**, onderdeel van de SC-300 Learning Path *Implement an identity management solution using Microsoft Entra ID*.

## Aanleiding
External collaboration settings aanscherpen in de Oceanic Airlines tenant, en een user aanwijzen die ondanks de striktere instelling nog wel guests mag uitnodigen.

## Doel
Guest access beperken tot least privilege, en via de Guest Inviter role gericht 1 user de mogelijkheid geven om guests uit te nodigen.

## Stappen
1. Nieuwe user aangemaakt: **Jacob Pellegrino**
2. Identity -> External Identities -> External collaboration settings
3. Guest user access: ingesteld op **most restrictive** (guests zien alleen hun eigen profiel)
4. Guest invite settings: ingesteld op **Only users assigned to specific admin roles can invite guest users**
5. Jacob Pellegrino toegewezen aan de **Guest Inviter** role, zodat hij ondanks de restrictie alsnog guests mag uitnodigen
6. Collaboration restrictions: default settings geaccepteerd
7. Save

## Resultaat
- Guest access beperkt tot eigen profiel voor alle guests in de tenant
- Standaard mag niemand meer guests uitnodigen, behalve admins en Jacob Pellegrino (via Guest Inviter role)

## Wat dit aantoont
- Praktische ervaring met het combineren van een tenant-brede restrictie met een gerichte uitzondering via role assignment
- Begrip van de Guest Inviter role als manier om invite-rechten te delegeren zonder volledige adminrechten te geven
- Toepassing van least privilege: standaard dicht, gericht open waar nodig
