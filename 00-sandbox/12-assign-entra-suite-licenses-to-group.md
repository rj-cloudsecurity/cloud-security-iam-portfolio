# Sandbox: Assigning Entra Suite Licenses to a Group

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Praktisch ervaren hoe group-based licensing werkt en waar je dit instelt.

## Doel
Een security group aanmaken en de Microsoft Entra Suite-licentie aan die group toewijzen, zodat de members de licentie overnemen.

## Stappen
1. Entra admin center -> Groups -> New group
2. Group type: Security, naam **The Looking Glass Licences**, Role assignment niet aangevinkt
3. Bonnie en Greta toegevoegd als members, mijzelf als owner
4. Entra admin center -> Groups -> The Looking Glass Licences -> Licenses: het portal verwijst voor het toewijzen door naar het Microsoft 365 admin center
5. Microsoft 365 admin center -> Groups -> Active groups -> The Looking Glass Licences -> Licenses and apps -> **Microsoft Entra Suite** aangevinkt en opgeslagen
6. Controle: Entra admin center -> Users -> Bonnie en Greta -> Licenses toonde Assignment paths **Direct, Inherited (The Looking Glass Licences)**

## Resultaat
- Bonnie en Greta hebben Microsoft Entra Suite nu zowel direct als via de group
- Het Entra admin center toont de licenties van de group, maar het toewijzen gebeurt in het Microsoft 365 admin center
- In het Microsoft 365 admin center zie je bij een user alleen de overgenomen licentie; de Assignment paths zie je in het Entra admin center

## Wat dit aantoont
- Praktisch begrip van group-based licensing en waar je het instelt
- Een licentie kan op dezelfde user zowel direct als via een group staan, en dat zie je aan de Assignment paths
