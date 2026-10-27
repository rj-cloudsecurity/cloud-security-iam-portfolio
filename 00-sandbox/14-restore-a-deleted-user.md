# Sandbox: Restoring a Deleted User

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Praktisch ervaren wat er gebeurt met een verwijderde user en hoe je die terugzet.

## Doel
Een testuser aanmaken, verwijderen en herstellen via Deleted users.

## Stappen
1. Entra ID -> Users -> New user -> Create new user: **Michael Dawson**
2. Michael Dawson verwijderd
3. Entra ID -> Users -> **Deleted users**: de melding toonde dat users 30 dagen na verwijdering automatisch definitief worden verwijderd
4. Michael Dawson aangevinkt -> **Restore user**
5. Controle: Michael Dawson staat weer in de lijst met users

## Resultaat
- Michael Dawson is hersteld en staat weer bij All users
- Een verwijderde user blijft 30 dagen in Deleted users staan voordat hij definitief wordt verwijderd

## Wat dit aantoont
- Praktisch begrip van soft delete: een verwijderde user is binnen 30 dagen terug te zetten
- Waar je verwijderde users vindt en hoe je ze herstelt
