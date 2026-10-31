# Sandbox: Restricting App Registration for Users

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Uitzoeken wat er gebeurt als gewone users geen apps meer mogen registreren.

## Doel
De tenant-instelling "Users can register applications" op No zetten en testen met een gewone user zonder rollen.

## Stappen
1. Entra admin center -> Entra ID -> Users -> **User settings** -> **Users can register applications**: **No**
2. Ingelogd als **Frank Lapidus**, een gewone user zonder rollen, in een InPrivate-venster
3. Entra ID -> App registrations -> New registration

## Resultaat
- Frank kreeg de melding "You don't have permission to register applications in the Oceanic Airlines directory", met error code 403

## Wat dit aantoont
- Met de instelling op No kunnen gewone users geen app registraties meer maken
- Praktische bevestiging van het probleem dat de rol Application Developer oplost
