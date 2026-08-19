# Exercise: Invite External Users - Individually and in Bulk

**Bron:** SC-300 Learning Path; Implement an identity management solution using Microsoft Entra ID

## Doel
Begrijpen hoe individuele en bulk guest-invites werken in Microsoft Entra ID, en hoe self-service app management voor guests is opgezet.

## Individueel uitnodigen
- Vereist minimaal een limited administrator directory role
- Kan via: Azure portal, direct naar de directory, naar een group, of naar een applicatie
- Uitgenodigde user wordt toegevoegd als **Guest** user type
- Invitation verloopt niet — geen expiratie
- Guest moet de invite **redeemen** voordat ze toegang krijgen
- Na toevoegen: directe link naar een shared app versturen, of guest gebruikt de redemption URL uit de invitation email
- Vereist dat external collaboration settings dit toestaan (default: iedereen mag uitnodigen, tenzij aangepast — zie vorige oefening)

## Self-service app management (voor gallery/SAML-apps)
Laat application owners zelf guests beheren, ook als de guest nog niet in de directory staat.

Setup door admin (eenmalig):
1. Self-service group management inschakelen voor de tenant
2. Group aanmaken die aan de app wordt gekoppeld, user als owner instellen
3. App configureren voor self-service, group toewijzen aan de app

Daarna: app owner gebruikt eigen Access Panel om guests uit te nodigen of toe te voegen aan de group die toegang heeft tot de app.

## Bulk invite via CSV
1. Bulk invite users -> CSV-bestand voorbereiden met user info + invitation preferences
2. CSV uploaden in Entra ID
3. Verifiëren dat users zijn toegevoegd aan de directory

### CSV template structuur
- **Rij 1: version number** — verplicht, niet verwijderen/wijzigen
- **Rij 2: column headings** — format: `Item name [PropertyName] Required/blank`, bv. `Email address to invite [inviteeEmail] Required`
- **Rij 3: voorbeeldrij** — moet verwijderd en vervangen worden door eigen data

### Aandachtspunten
- Eerste twee rijen nooit verwijderen/aanpassen, anders faalt de upload
- Verplichte kolommen staan eerst
- Geen eigen kolommen toevoegen — worden genegeerd
- Download regelmatig de laatste versie van het template

## Resultaat
Niet uitgevoerd in de sandbox — vastgelegd als theorie/proces-kennis. Individuele invite wordt apart gedocumenteerd als sandbox-experiment.

## Wat dit aantoont
- Begrip van het verschil tussen individuele en bulk guest-invites
- Kennis van self-service app management als delegatie-mechanisme voor app owners
- Bewustzijn van de CSV-template vereisten voor bulk operations
