# Sandbox: Calling Microsoft Graph with the Client Credentials Flow

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Controleren of de daemon app met een secret en application permissions echt Microsoft Graph kan aanroepen.

## Doel
Met een client secret een token ophalen en daarmee Microsoft Graph aanroepen, zonder ingelogde user.

## Stappen
1. Entra admin center -> Entra ID -> App registrations -> Daemon App -> **Certificates & secrets** -> New client secret; de **Value** gekopieerd (niet de Secret ID)
2. Application (client) ID gekopieerd van de Overview-pagina
3. In een terminal een token opgevraagd bij het token-endpoint van de tenant (`login.microsoftonline.com/<tenant-id>/oauth2/v2.0/token`) met `client_id`, `client_secret`, `scope=https://graph.microsoft.com/.default` en `grant_type=client_credentials`
4. Met die token `https://graph.microsoft.com/v1.0/users?$top=3` aangeroepen

## Resultaat
- Eerste pogingen mislukten: de opdracht stond over twee regels, waardoor `grant_type` ontbrak, en daarna was de token leeg
- Daarna lukte het: Graph gaf drie users terug (Benjamin Linus, Bonnie en Charles Widmore)

## Wat dit aantoont
- Een daemon app haalt zelf een token op met de client credentials flow, zonder user
- Het scope-formaat `https://graph.microsoft.com/.default` geeft de rechten die via admin consent zijn toegekend
- Het secret is de Value, niet de Secret ID
