# Sandbox: Group Enterprise Apps in a My Apps Collection

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Gebruikers moeten bij elkaar horende enterprise apps in het My Apps-portaal gegroepeerd zien.

## Doel
Een collection maken met meerdere enterprise apps en die toewijzen aan gebruikers.

## Stappen
1. Er was alleen de enterprise app **Swan Station App**, dus ik heb een tweede app gemaakt: **The Looking Glass App**
2. **Collections** stond niet in het menu van mijn portal. Via de zoekbalk bovenin op "collections" gezocht en de pagina **Enterprise applications** met de collections geopend
3. **New collection**, naam `Island Apps`, beschrijving "all apps on the island"
4. Tab **Applications** -> **Add application**: Swan Station App en The Looking Glass App
5. Tab **Owners**: mijzelf toegevoegd
6. Tab **Users and groups**: de groepen `swan station` en `the looking glass licences` toegevoegd
7. **Create**

## Resultaat
- De pagina met collections toont twee collections: de standaardcollection **Apps** ("All apps") en **Island Apps** ("all apps on the island")
- In My Apps van Frank Lapidus (lid van de groep `swan station`) staan twee tabs: **Island Apps** en **Apps**. De tab Island Apps toonde op het moment van kijken "There are no apps to show", terwijl Swan Station App wel in de sectie Apps stond. Frank was nog niet toegewezen aan The Looking Glass App; ik heb hem daaraan toegevoegd. Na verversen en opnieuw inloggen bleef de tab leeg
- Bij het terugkijken in de collection (tab **Applications**) stonden de twee apps er niet meer in, ook al had ik ze bij het aanmaken toegevoegd. Waarom is mij niet duidelijk. Ik heb ze opnieuw toegevoegd en opgeslagen. Direct daarna zag Frank in My Apps nog steeds "There are no apps to show" in Island Apps
- Na een paar minuten en opnieuw inloggen stonden beide apps (Swan Station App en The Looking Glass App) wel in de tab **Island Apps** van Frank.

## Wat dit aantoont
- Een collection maak je in het Entra admin center onder Enterprise applications -> Collections. Je kiest de apps en wijst de collection toe aan gebruikers en groepen
- Collections groeperen apps in het My Apps-portaal van de toegewezen gebruikers, als aparte tab naast Apps
- Je kunt een collection aan een groep toewijzen in plaats van aan één gebruiker
