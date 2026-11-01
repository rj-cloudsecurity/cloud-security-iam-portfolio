# Sandbox: Inviting Guests in Bulk with a CSV File

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Bij een samenwerking met partnerorganisaties moeten veel externe gebruikers tegelijk worden uitgenodigd. Uitzoeken hoe de CSV-template voor B2B-uitnodigingen werkt.

## Doel
Drie externe gasten tegelijk uitnodigen met een CSV-bestand.

## Stappen
1. Entra admin center -> **Entra ID** -> **Users** -> **Bulk operations** -> **Bulk invite**
2. De CSV-template gedownload
3. Drie externe adressen ingevuld die ik zelf beheer, voor de gasten Eloise Hawking, Matthew Abaddon en Penny Widmore
4. In de kolom met de redirect-URL ingevuld: `https://myapps.microsoft.com`
5. Het bestand opgeslagen als CSV via Numbers en geüpload bij **Upload your csv file** -> **Submit**
6. Gecontroleerd onder **Users** -> **All users** (filter op gasten)

## Resultaat
- De drie gasten staan in de tenant, met een gebruikersnaam in het formaat `naam_domein#EXT#@rjpaulidesoutlook.onmicrosoft.com`
- De template markeert twee kolommen als verplicht: het e-mailadres van de genodigde en de redirect-URL
- De template heeft geen kolom voor een naam: die komt uit het account of pas je daarna aan

## Wat dit aantoont
- Een bulk-uitnodiging vraagt alleen een e-mailadres en een redirect-URL; de gast komt na accepteren op die URL terecht
- Gasten krijgen een eigen gebruikersnaam met #EXT# in de tenant
- Een gast kan niets doen voordat hij de uitnodiging heeft geaccepteerd
