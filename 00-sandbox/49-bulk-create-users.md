# Sandbox: Creating Users in Bulk with a CSV File

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Bij een bulk-onboarding van veel medewerkers wil je users niet één voor één aanmaken. Uitzoeken hoe de CSV-template werkt en welke kolommen verplicht zijn.

## Doel
Drie users aanmaken met de bulk create-functie.

## Stappen
1. Entra admin center -> **Entra ID** -> **Users** -> **Bulk operations** -> **Bulk create**
2. De CSV-template gedownload
3. Drie users ingevuld: James Ford, Kate Austen en Sayid Jarrah
4. Het bestand geüpload bij **Upload your csv file** en **Submit**
5. Gecontroleerd onder **Users** -> **Bulk operation results**

## Resultaat
- De eerste upload gaf een foutmelding. Ik had het bestand in OpenOffice opgeslagen; de oorzaak heb ik niet vastgesteld
- Daarna het bestand opnieuw in Numbers ingevuld en als CSV geëxporteerd: die upload werkte
- Alle drie de users staan in de tenant
- De template markeert vier kolommen als verplicht: Name, User name, Initial password.

## Wat dit aantoont
- Bulk create vraagt een CSV in het formaat van de template; de kolomnamen en de eerste regels moeten blijven staan
- Het programma waarin je het bestand opslaat kan het CSV-formaat veranderen, waardoor de upload faalt
- Het resultaat van een bulkbewerking zie je onder Bulk operation results
