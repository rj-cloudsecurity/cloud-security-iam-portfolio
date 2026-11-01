# Sandbox: Adding a Graph Application Permission and Granting Admin Consent

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Een daemon app heeft rechten nodig op Microsoft Graph zonder dat er een user is die ze kan geven.

## Doel
Een application permission toevoegen aan Daemon App en er admin consent voor geven.

## Stappen
1. Entra admin center -> Entra ID -> App registrations -> **Daemon App** -> **API permissions**
2. Add a permission -> **Microsoft Graph** -> **Application permissions** (niet Delegated)
3. **User.Read.All** gekozen en toegevoegd
4. Als Global Administrator op **Grant admin consent for Oceanic Airlines** geklikt

## Resultaat
- User.Read.All is toegevoegd als application permission
- Na admin consent staat de status op Granted

## Wat dit aantoont
- Een daemon app gebruikt application permissions, geen delegated permissions
- Application permissions hebben altijd admin consent nodig
