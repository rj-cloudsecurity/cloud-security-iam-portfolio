# Sandbox: Checking Which Entra Roles PIM Can Manage

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Uitzoeken welke rollen Privileged Identity Management (PIM) kan beheren en welke niet.

## Doel
In PIM kijken welke Entra-rollen te beheren zijn, met als voorbeeld de rollen Billing Administrator en Global Administrator.

## Stappen
1. Entra admin center -> ID Governance -> **Privileged Identity Management** -> **Microsoft Entra roles**
2. Links onder **Manage** -> **Roles**
3. In de lijst gezocht naar **Billing Administrator** en **Global Administrator**
4. Op **Global Administrator** geklikt en **Add assignments** geopend (niets toegewezen, **Cancel**)

## Resultaat
- Beide rollen staan in de PIM-lijst; Global Administrator had 2 en 0 in de twee aantalkolommen, Billing Administrator 0 en 0
- Bij Add assignments: Resource **Oceanic Airlines**, Resource type **Directory**, de gekozen rol en de keuze voor een member; ook groups zijn als member mogelijk

## Wat dit aantoont
- Billing Administrator is een Entra-rol en dus wel te beheren in PIM; dat is iets anders dan de billing-rollen van een Azure billing account
- PIM beheert Entra-rollen via Microsoft Entra roles, Azure RBAC-rollen via Azure resources en groups via Groups
- Niet getest: dat de klassieke subscription-beheerders (Service Administrator, Co-administrator) en de billing-rollen van een billing account niet in PIM staan; dat is theorie, want ik heb geen subscription of billing account
