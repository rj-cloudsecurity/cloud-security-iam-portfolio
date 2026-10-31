# Sandbox: Creating an Access Review for a Group

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Een access review echt aanmaken en doorlopen, niet alleen de schermen bekijken.

## Doel
Een review maken voor de group Island Resources met mijzelf als reviewer.

## Stappen
1. Entra admin center -> ID Governance -> **Access reviews** -> **New access review** -> **Resource review**
2. Select what to review: **Teams + Groups**, group **Island Resources**, scope **All users**
3. Reviewer: mijzelf
4. Review name: **Test review access**
5. **Create**

## Resultaat
- De review staat in de lijst met de status **Not started**, daarna **Initializing**
- Er kwam geen e-mail, want mijn tenant heeft geen mailbox (geen Microsoft 365-licentie)

## Wat dit aantoont
- Een review start niet direct: de status loopt van Not started via Initializing naar In progress
- Zonder mailbox krijgt een reviewer geen melding; de review is dan alleen te vinden via My Access
