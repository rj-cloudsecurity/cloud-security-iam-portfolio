# Sandbox: Showing a French Sign-in Page for French Browsers

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Gebruikers met een Franse browser moeten een Franstalige inlogpagina zien.

## Doel
Een sign-in pagina per browsertaal instellen en testen.

## Stappen
1. Entra admin center -> **Entra ID** -> **Custom branding**
2. **Add** en bij **Browser language** gekozen voor **French**
3. De Franse variant van de inlogpagina ingevuld (tekst en layout)
4. **Create**
5. In Firefox de taal Frans bovenaan gezet (Settings -> General -> Language) en de inlogpagina geopend in een privévenster

## Resultaat
- Met de browser op Frans zag ik de Franse inlogpagina met de layout die ik had ingesteld

## Wat dit aantoont
- Een aparte sign-in pagina per taal stel je in bij Custom branding, met een browser language
- De pagina wordt getoond op basis van de taalinstelling van de browser
- Edge en Defender for Cloud Apps spelen hierbij geen rol
