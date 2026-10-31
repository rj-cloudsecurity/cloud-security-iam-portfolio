# Sandbox: Assigning an Access Package to a User

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Controleren dat een access package de toegang echt na 90 dagen laat verlopen.

## Doel
De access package Island Access als admin direct aan een user toewijzen en de einddatum controleren.

## Stappen
1. Entra admin center -> ID Governance -> Entitlement management -> Access packages -> **Island Access** -> **Assignments** -> **New assignment**
2. Policy: **Initial Policy**, identiteit **Benjamin Linus** (Identities in my directory)
3. Assignment ends on: veranderd van de voorgestelde 11/15/2026 naar **1/29/2027**, 90 dagen na de start op 10/31/2026
4. Business justification ingevuld en **Add**

## Resultaat
- De toewijzing staat op status **Delivered** met de einddatum **1/29/2027**
- Bevestigd: dat Benjamin nu lid is van de group Island Resources

## Wat dit aantoont
- Een admin kan een access package direct toewijzen zonder dat de user hem hoeft aan te vragen
- Bij een toewijzing zie je de einddatum; op die datum verliest de user de toegang automatisch
