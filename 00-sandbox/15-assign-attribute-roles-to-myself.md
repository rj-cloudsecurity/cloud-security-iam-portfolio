# Sandbox: Assigning Attribute Roles to Myself

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Uitzoeken wat een Global Administrator standaard kan met custom security attributes.

## Doel
Controleren of een Global Administrator custom security attributes kan beheren, en mijzelf de benodigde rollen geven.

## Stappen
1. Entra admin center -> Entra ID -> **Custom security attributes**: de pagina meldde dat de Global Administrator en Privileged Role Administrator standaard geen rechten hebben om custom security attributes te lezen of toe te voegen
2. Entra ID -> Users -> [eigen user] -> **Assigned roles** -> Add assignment
3. **Attribute Definition Administrator** en **Attribute Assignment Administrator** aangevinkt en toegewezen

## Resultaat
- Beide rollen staan bij mijn user als Active en Permanent, met als scope Oceanic Airlines
- Pas na een nieuwe sessie kon ik attribute sets beheren

## Wat dit aantoont
- Een Global Administrator heeft standaard geen toegang tot custom security attributes; je moet jezelf eerst een attribute-rol geven
- Praktische bevestiging dat deze attributen bewust van de gewone beheerdersrollen zijn afgeschermd
