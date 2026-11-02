# Sandbox: Restore a Deleted App Registration

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Een per ongeluk verwijderde app registration moet terug te halen zijn, en ik wilde weten hoe lang dat kan.

## Doel
Een app registration verwijderen, terugzetten en de tijdslimiet noteren.

## Stappen
1. **Entra ID** -> **App registrations** -> **All applications** -> **Calendar Reader App** -> **Delete**
2. Tabblad **Deleted applications** geopend
3. De app aangevinkt en op **Restore app registration** geklikt
4. Teruggegaan naar **All applications**, de API permissions van de app bekeken en bij **Enterprise apps** gekeken of de app er ook weer stond

## Resultaat
- Op het tabblad **Deleted applications** stond de app met de kolommen Display name, Application (client) ID, Object ID en Deleted date (2-11-2026)
- Boven de lijst staat de melding: "If deleted for more than 30 days, app registrations cannot be restored and may be automatically permanently deleted."
- Na **Restore app registration** stond de app weer onder All applications, met dezelfde API permissions als voor het verwijderen
- Ook bij Enterprise apps stond de app weer

## Wat dit aantoont
- Een verwijderde app registration staat op het tabblad **Deleted applications** en is daar terug te zetten met **Restore app registration**
- De tijdslimiet is **30 dagen**: daarna kan de app niet meer worden hersteld en kan hij automatisch definitief worden verwijderd
- Na het herstellen is ook de enterprise app weer aanwezig
