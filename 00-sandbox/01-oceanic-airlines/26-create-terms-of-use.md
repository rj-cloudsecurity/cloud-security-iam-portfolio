# Sandbox: Creating Terms of Use

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Praktisch ervaren hoe je gebruikers voorwaarden laat accepteren voordat ze bij resources komen.

## Doel
Een terms of use-document aanmaken met een PDF.

## Stappen
1. Entra admin center -> Entra ID -> **Conditional Access** -> **Terms of use** -> **New terms**
2. Naam: **Oceanic Airlines Terms of Use**
3. Terms of use document: PDF **oceanic-airlines-terms-of-use.pdf**, taal **English**, met een display name
4. Require users to expand the terms of use: **Off**
5. Require users to consent on every device: **Off**
6. Expire consents: **Off**
7. Conditional access: **Create conditional access policy later**
8. Create

## Resultaat
- Terms of use "Oceanic Airlines Terms of Use" aangemaakt
- De Create-knop bleef grijs totdat het veld **Display name** was ingevuld
- Het document verschijnt in de Grant-controls van Conditional Access

## Wat dit aantoont
- Een terms of use heeft een PDF, een taal en een display name nodig
- Het document doet pas iets als je het via Conditional Access verplicht stelt
