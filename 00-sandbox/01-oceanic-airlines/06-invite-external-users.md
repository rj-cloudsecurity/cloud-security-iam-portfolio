# Sandbox: Inviting an External User

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Geïnspireerd op de Microsoft Learn oefening **"Invite external users - individually and in bulk"**, onderdeel van de SC-300 Learning Path *Implement an identity management solution using Microsoft Entra ID*.

## Aanleiding
Praktisch ervaren hoe de B2B invitation en redemption flow werkt, na eerder de theorie hierover te hebben doorlopen.

## Doel
Een externe user individueel uitnodigen als guest, en de volledige redemption flow doorlopen.

## Stappen
1. Identity -> Users -> + New user -> Invite external user
2. Guest uitgenodigd: **Desmond Hume**
3. Invitation email verstuurd naar het externe emailadres
4. Redemption link geopend en geaccepteerd door Desmond (via het externe account)
5. Consent-scherm doorlopen

## Resultaat
- Invite succesvol verstuurd en geredeemed
- Desmond Hume verschijnt in All Users met User Type **Guest** en `#EXT#` in de UPN

## Wat dit aantoont
- Praktische ervaring met de volledige B2B invitation en redemption flow, van beide kanten (als inviting admin én als de guest zelf)
- Bevestiging van eerder geleerde theorie: guest users zijn herkenbaar aan het `#EXT#`-patroon in hun UPN
