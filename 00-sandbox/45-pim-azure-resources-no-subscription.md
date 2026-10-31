# Sandbox: Checking Azure Resources in PIM

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
PIM beheert naast Entra-rollen ook Azure-rollen. Nagaan of ik die kant in mijn tenant kan bekijken.

## Doel
Kijken of er een subscription is waarvoor PIM Azure-rollen kan beheren.

## Stappen
1. Entra admin center -> ID Governance -> **Privileged Identity Management**
2. Links onder **Manage** -> **Azure resources**
3. In de scope-kiezer op de dropdown **Subscriptions** geklikt

## Resultaat
- De scope-kiezer toonde Management groups, Subscriptions, Resource groups en Resources
- De lijst met subscriptions was leeg: mijn tenant heeft geen Azure-subscription
- Daardoor kon ik **Manage resource** niet gebruiken en geen Azure-rollen bekijken

## Wat dit aantoont
- Azure-rollen beheer je in PIM per scope: management group, subscription, resource group of resource
- Zonder subscription is dit deel van PIM niet te testen
- Niet getest: de klassieke beheerders en de billing-rollen van een billing account, want daarvoor is een subscription of billing account nodig
