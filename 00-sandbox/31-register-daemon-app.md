# Sandbox: Registering a Daemon App

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Uitzoeken hoe een app zonder ingelogde user toegang krijgt tot Microsoft Graph.

## Doel
Een app registration maken voor een daemon app, een achtergrondapp die zelf een API aanroept.

## Stappen
1. Entra admin center -> Entra ID -> **App registrations** -> New registration
2. Naam: **Daemon App**
3. Supported account types: **Single tenant**
4. Redirect URI leeggelaten, omdat er geen user inlogt
5. Register

## Resultaat
- App registration "Daemon App" aangemaakt

## Wat dit aantoont
- Een daemon app heeft geen redirect URI nodig, omdat er geen user is die inlogt
- De app authenticeert zich zelf, met een secret of certificaat
