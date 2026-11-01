# Sandbox: Stopping an Access Review and Applying the Results

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Na het Deny-besluit bleef Benjamin Linus in de group Island Resources staan.

## Doel
De review afronden en het resultaat laten toepassen.

## Stappen
1. Entra admin center -> ID Governance -> **Access reviews** -> **Test review access**
2. Bovenaan **Stop**
3. Op de lijst de status gevolgd; die stond op **Applying**
4. De ledenlijst van Island Resources ververst

## Resultaat
- Direct na Stop stond Benjamin nog in de group, en de review stond op **Applying**
- Na het toepassen van het resultaat is Benjamin Linus uit de group Island Resources verwijderd

## Wat dit aantoont
- Stop beëindigt de review vroegtijdig; daarna verwerkt Entra het resultaat (Applying)
- Het resultaat staat niet direct in de group: er zit vertraging tussen een beslissing, Stop en de verwijdering
- Pas na afronding wordt een Deny uitgevoerd: de user verliest dan de toegang tot de group
