# Sandbox: Unassigning Entra Suite Licenses from Users

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Direct toegewezen licenties opruimen wanneer dezelfde licentie al via een group wordt toegewezen.

## Doel
De directe Microsoft Entra Suite-licenties van Bonnie en Greta in bulk verwijderen, zodat alleen de group-licentie overblijft.

## Stappen
1. Microsoft 365 admin center -> Billing -> Licenses -> **Microsoft Entra Suite** -> Users
2. Bonnie en Greta geselecteerd (mijzelf niet)
3. **Unassign licenses**
4. Controle: Entra admin center -> Users -> Bonnie en Greta -> Licenses toonde nu alleen **Inherited (The Looking Glass Licences)**

## Resultaat
- De directe toewijzingen van Bonnie en Greta zijn in bulk verwijderd
- De licentie blijft actief via de group

## Wat dit aantoont
- Praktisch begrip van het verschil tussen een directe en een overgenomen licentie
- Directe licenties kun je opschonen zonder dat de user de licentie kwijtraakt, zolang de group-licentie blijft staan
