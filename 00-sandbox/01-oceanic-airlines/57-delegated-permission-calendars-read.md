# Sandbox: Delegated Permission Calendars.Read Compared With an Application Permission

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Een app moet de agenda van de ingelogde gebruiker lezen. Ik wilde zien hoe een delegated permission zich verhoudt tot de application permission van mijn daemon app: wie geeft consent en van wie worden de gegevens gelezen.

## Doel
De delegated permission Calendars.Read toevoegen aan een app registration en vergelijken met de application permission van de Daemon App.

## Stappen
1. **Entra ID** -> **App registrations** -> **New registration**, naam `Calendar Reader App`, Supported account types: **My organization only**, geen redirect URI
2. **API permissions** -> **Add a permission** -> **Microsoft Graph** -> **Delegated permissions** -> **Calendars.Read** -> **Add permissions**
3. In de lijst met API permissions de kolommen Type en Admin consent required bekeken. Geen admin consent verleend
4. **Enterprise apps** -> **Calendar Reader App** -> **Permissions** geopend
5. Daarna **Enterprise apps** -> **Daemon App** -> **Permissions** (tab Admin consent) bekeken

## Resultaat
- Calendar Reader App heeft twee Microsoft Graph permissions: **Calendars.Read** (Delegated, "Read user calendars") en **User.Read** (Delegated, "Sign in and read user profile"). Bij beide staat Admin consent required op **No**
- Bij Enterprise apps -> Calendar Reader App -> Permissions staat Calendars.Read niet in de lijst. Die pagina toont alleen permissions waarvoor consent is verleend; Calendars.Read is alleen aangevraagd en nog niet verleend
- De Daemon App heeft bij Permissions: **User.Read.All** (Application, "Read all users' full profiles", Granted through Admin consent, Granted by An administrator) en **User.Read** (Delegated, Admin consent)
- Niet getest: of Calendars.Read echt een agenda teruggeeft. Mijn tenant heeft geen mailbox, dus ik kon geen agenda lezen

## Wat dit aantoont
- Een delegated permission werkt namens een ingelogde gebruiker; een application permission werkt zonder gebruiker, als de app zelf (zoals bij de daemon app)
- Bij Calendars.Read staat Admin consent required op No: een gebruiker kan zelf consent geven bij de eerste keer inloggen. Een application permission zoals User.Read.All wordt door een beheerder verleend, zoals de Daemon App laat zien
- Een delegated permission leest de gegevens van de ingelogde gebruiker. Een application permission geldt voor alle gebruikers in de tenant. Dat laatste heb ik hier niet getest, het volgt uit de werking van de permissions
- API permissions bij de app registration laten zien wat een app **aanvraagt**; Permissions bij de enterprise app laat zien wat er **verleend** is
