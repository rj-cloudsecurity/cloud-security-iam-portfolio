# Sandbox: Testing What a Helpdesk Administrator Can Do

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Een helpdesk moet licenties toewijzen, users en groups aanmaken en verwijderen, en wachtwoorden van niet-beheerders resetten, met de minste rechten. Uitzoeken wat de rol Helpdesk Administrator hiervan toestaat.

## Doel
De rol Helpdesk Administrator toewijzen aan een testuser en nagaan wat die wel en niet kan.

## Stappen
1. Bij Frank Lapidus de rol Application Developer van een eerdere oefening verwijderd, zodat hij geen rollen had
2. Het wachtwoord van Frank als admin gereset (Entra ID -> Users -> Frank -> **Reset password**), omdat self-service password reset niet voor hem is ingesteld
3. Entra ID -> **Roles & admins** -> **Helpdesk Administrator** -> **Add assignments** -> Frank, type **Active**
4. In een privévenster als Frank ingelogd en getest: wachtwoord resetten, user aanmaken, licentie toewijzen, group aanmaken, gast uitnodigen

## Resultaat
- Wachtwoord resetten: gelukt bij Michael Dawson. Niet gelukt bij Bonnie, Charles Widmore en Benjamin Linus, met de melding "The password can not be reset. This may be due to an incorrect level of administrative privilege". Ook na opnieuw inloggen bleef dat zo
- Nieuwe user aanmaken: niet gelukt
- Licentie toewijzen in het Microsoft 365 admin center: de optie Microsoft Entra Suite was grijs
- Group aanmaken en verwijderen: gelukt
- Gast uitnodigen (Invite external user): gelukt
- Niet vastgesteld: waarom het resetten bij Bonnie, Charles en Benjamin niet lukte. In de PIM-lijst met actieve toewijzingen stond geen rol bij hen, en Restricted management stond bij de administrative unit op Nee

## Wat dit aantoont
- Helpdesk Administrator kan wachtwoorden resetten van users zonder beheerdersrol, maar geen users aanmaken en geen licenties toewijzen
- Een group aanmaken en een gast uitnodigen lukt ook zonder rol: dat staat standaard open voor leden. Die twee tests zeggen dus niets over de rol
- Een resetpoging kan stranden op de eigenschappen van de doel-user, niet alleen op de rol van de beheerder
