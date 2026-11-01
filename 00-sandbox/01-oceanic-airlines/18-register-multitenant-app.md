# Sandbox: Registering a Multitenant App

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Uitzoeken hoe een app in de ene tenant een app in een andere tenant kan aanroepen.

## Doel
Een app registration aanmaken die door meerdere tenants gebruikt kan worden.

## Stappen
1. Entra admin center -> Entra ID -> **App registrations** -> New registration
2. Naam: **Swan Station App**
3. Supported account types: **Multiple Entra ID tenants** met **Allow all tenants**
4. Redirect URI leeggelaten, omdat de app zelf tokens aanvraagt en geen gebruikers inlogt
5. Register

## Resultaat
- App registration "Swan Station App" is aangemaakt en geschikt voor meerdere tenants

## Wat dit aantoont
- Een app die in een andere tenant wordt gebruikt, heeft een multitenant app registration nodig
- Een redirect URI is niet verplicht voor een app die zich zelf authenticeert
