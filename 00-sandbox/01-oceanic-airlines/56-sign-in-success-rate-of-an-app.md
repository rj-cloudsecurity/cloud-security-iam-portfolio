# Sandbox: Sign-in Success Rate of an App Over 30 Days

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Het aantal mislukte inlogs en het slagingspercentage van een app over de afgelopen 30 dagen moeten te vinden zijn, met zo weinig mogelijk configuratie.

## Doel
Uitzoeken waar je deze cijfers ziet zonder iets in te stellen, zoals diagnostic settings of een Log Analytics workspace.

## Stappen
1. **Entra ID** -> **Monitoring & health** -> **Usage & insights** -> **Microsoft Entra application activity (Preview)**
2. Date range op **30 days** (stond al zo)
3. De kolommen Successful sign-ins, Failed sign-ins en Success rate per app bekeken
4. Op de app **Frank Test App** geklikt: een detailpagina met Sign-in activity (grafiek) en Sign-in failures
5. Ter vergelijking via **Entra ID** -> **Enterprise apps** -> **Frank Test App** -> **Sign-in logs** gekeken. De standaardperiode was 24 uur; ik heb die op **Last 1 month** gezet

## Resultaat
- In de lijst staat per app: Frank Test App 2 successful, 1 failed, success rate **66,67%**; Azure Portal 77 successful, 1 failed, **98,72%**. De meeste andere apps hebben 0 failed en 100%
- De detailpagina van Frank Test App toont Success 2 en Failure 1, en onder **Sign-in failures** de fout "Admin consent is required for the permissions requested by this application", error code 90094, 1 keer, laatst gezien op 31-10-2026
- De sign-in logs van de app tonen drie inlogs: Success, Interrupted en Failure (Frank Lapidus). Usage & insights telt 2 successful en 1 failed; dat past erbij als de inlog met status Interrupted als succes meetelt. Dat heb ik niet apart gecontroleerd

## Wat dit aantoont
- Het aantal mislukte inlogs en het slagingspercentage per app staan in **Usage & insights** -> **Microsoft Entra application activity**, zonder dat je iets hoeft te configureren
- De date range kun je daar op 30 dagen zetten; de sign-in logs van een enterprise app staan standaard op 24 uur
- Per app zie je de fouten en error codes, zodat je kunt zien waarom inlogs mislukken
