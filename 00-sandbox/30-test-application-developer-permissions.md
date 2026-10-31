# Sandbox: Testing What an Application Developer Can Do

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Uitzoeken welke rechten de rol Application Developer wel en niet geeft.

## Doel
Als Frank Lapidus met de rol Application Developer een app registreren en admin consent proberen te geven.

## Stappen
1. Ingelogd als **Frank Lapidus** in een nieuw InPrivate-venster
2. Entra ID -> App registrations -> New registration: app **Frank Test App** aangemaakt
3. Frank Test App -> API permissions: de standaard **User.Read** stond er al; **User.Read.All** toegevoegd (bij *Admin consent required* staat Yes)
4. Op **Grant admin consent for Oceanic Airlines** geklikt
5. Daarna als Global Administrator ingelogd en bij de toestemmingsvraag voor Frank Test App op **Accept** geklikt

## Resultaat
- App registreren lukte: Frank Test App is aangemaakt
- Admin consent geven lukte niet: Frank kreeg "Need admin approval... needs permission to access resources in your organization that only an admin can grant"
- Alleen mijn Global Administrator-account kon de toestemming voor de organisatie geven

## Wat dit aantoont
- Application Developer maakt het mogelijk om apps te registreren terwijl de tenant-instelling op No staat
- De rol geeft geen recht om admin consent te geven; dat blijft voor een admin
- Niet getest: of Frank apps van andere users kan zien of wijzigen
