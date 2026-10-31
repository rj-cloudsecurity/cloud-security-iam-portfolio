# Sandbox: Testing What a User Administrator Can Do

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Na de test met Helpdesk Administrator (entry 47) dezelfde tests doen met de rol User Administrator.

## Doel
Nagaan wat een User Administrator wel en niet kan, vergeleken met een Helpdesk Administrator.

## Stappen
1. Bij Frank Lapidus de rol Helpdesk Administrator weggehaald
2. Entra ID -> **Roles & admins** -> **User Administrator** -> **Add assignments** -> Frank, type **Active**
3. Opnieuw ingelogd als Frank in een privévenster en getest: wachtwoord resetten, user aanmaken, licentie toewijzen, group aanmaken

## Resultaat
- Wachtwoord resetten: niet gelukt bij Benjamin Linus, Charles Widmore en Jack Shephard (Application Administrator), ook na opnieuw inloggen. Michael Dawson heb ik in deze ronde niet getest
- Nieuwe user aanmaken: het scherm kon ik openen en invullen; niet opgeslagen
- Licentie toewijzen aan Jacob Pellegrino: het scherm kon ik openen en invullen; niet opgeslagen
- Group aanmaken: het scherm kon ik openen en invullen; niet opgeslagen
- Niet vastgesteld: waarom Benjamin en Charles niet te resetten waren

## Wat dit aantoont
- Een User Administrator kan, anders dan een Helpdesk Administrator, een user aanmaken en een licentie toewijzen
- Jack Shephard is niet te resetten met User Administrator, omdat hij zelf een beheerdersrol heeft (Application Administrator)
- Dezelfde users waren onder beide rollen niet te resetten; dat wijst op iets bij die accounts, niet op het verschil tussen de rollen
- Niet getest: dat het aanmaken, het toewijzen van de licentie en het aanmaken van de group echt zijn gelukt, want ik heb niets opgeslagen
