# Sandbox: Assigning the Application Developer Role

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Frank moet apps kunnen registreren terwijl de instelling "Users can register applications" op No staat.

## Doel
De rol Application Developer aan Frank Lapidus toewijzen en het verschil tussen Eligible en Active ervaren.

## Stappen
1. Entra admin center -> Entra ID -> **Roles & admins** -> **Application Developer** -> **Add assignments** (opent Privileged Identity Management)
2. Frank Lapidus geselecteerd, Assignment type **Eligible** (de standaardkeuze), Permanently eligible
3. Als Frank opnieuw een app proberen te registreren: nog steeds geen toegang; ik kon de rol ook niet activeren
4. Eligible assignment van Frank verwijderd (tab Eligible assignments -> Remove)
5. Opnieuw **Add assignments**, nu met Assignment type **Active**
6. Opnieuw ingelogd als Frank in een nieuw InPrivate-venster

## Resultaat
- Een Eligible assignment geeft de rol pas na activatie; Frank had de rol dus nog niet
- Met een Active assignment werkt de rol direct

## Wat dit aantoont
- Een eligible rol moet eerst geactiveerd worden voordat hij rechten geeft
- Voor een vaste rol die direct werkt, kies je Active
