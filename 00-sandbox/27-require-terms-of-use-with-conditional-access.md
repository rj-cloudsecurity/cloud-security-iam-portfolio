# Sandbox: Requiring Terms of Use with Conditional Access

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Een terms of use moet gebruikers daadwerkelijk bereiken; dat regel je via Conditional Access.

## Doel
Een Conditional Access policy maken die de terms of use verplicht stelt voor een groep users.

## Stappen
1. Entra admin center -> Entra ID -> Conditional Access -> Policies -> **New policy**
2. Naam: **Require terms of use**
3. Users: group **DharmaInitiative** included, mijzelf excluded
4. Target resources: **All resources**
5. Grant: **Require terms of use** -> **Oceanic Airlines Terms of Use**
6. Enable policy: **Report-only**
7. Create

## Resultaat
- Conditional Access policy "Require terms of use" aangemaakt in Report-only
- Niet getest: het accepteren of weigeren door een gebruiker, omdat daarvoor iemand uit de groep moet inloggen

## Wat dit aantoont
- Een terms of use verplicht je via de Grant-controls van een Conditional Access policy
- Accepteren en weigeren vind je terug onder Conditional Access -> Terms of use (aantallen en View audit logs) en in de audit logs
