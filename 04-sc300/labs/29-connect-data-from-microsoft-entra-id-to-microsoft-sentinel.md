# Exercise: Connect Data from Microsoft Entra ID to Microsoft Sentinel

**Bron:** SC-300 Learning Path; Plan and implement an identity governance strategy

## Doel
Een Microsoft Sentinel workspace aanmaken en de Microsoft Entra ID connector configureren om sign-in logs en audit logs te streamen naar Sentinel.

## Wat ik heb gedaan
1. Log Analytics workspace aangemaakt: lab-workspace-ex29 (resource group lab-workspace-ex29-RG, regio West Europe, Pay-as-you-go)
2. Microsoft Sentinel toegevoegd aan de workspace; automatisch 31-dagen gratis trial geactiveerd (10 GB/dag gratis voor zowel Sentinel als Log Analytics)
3. Microsoft Entra ID solution geinstalleerd via Content Hub (89 content items: 74 analytics rules, 1 data connector, 11 playbooks, 3 workbooks, 1 watchlist), gratis in prijs
4. Data connector geopend via Content Hub > Microsoft Entra ID > Manage > "1 items" (Created content link) op de Data connector rij
5. Configuration scherm geopend met alle beschikbare log types
6. Sign-In Logs bewust NIET aangevinkt, om te voorkomen dat dit een P1/P2 zou triggeren
7. Audit Logs wel aangevinkt, Apply Changes geklikt: geen foutmelding, wijziging succesvol toegepast

## Resultaat
Deels uitgevoerd. Sentinel workspace, solution installatie, en Audit Logs connector configuratie zijn volledig gelukt zonder P2, via de losstaande Sentinel 31-dagen trial. Sign-In Logs is bevestigd premium gated: expliciete melding "In order to export Sign-in data, your organization needs Microsoft Entra ID P1 or P2 license" verscheen bij die specifieke checkbox, en is bewust niet geactiveerd.

## Wat dit aantoont
- Praktische ervaring met het opzetten van een Sentinel workspace en het installeren van een content hub solution
- Bevestiging van het specifieke licentieverschil: Sign-In Logs vereist P1/P2, Audit Logs en overige logtypes niet
- Begrip van de Content Hub structuur: solutions bevatten data connectors, analytics rules, workbooks, en playbooks als losse content items
- Bewuste, verantwoorde keuze om geen ongewenste licentiewijziging te triggeren tijdens het testen
