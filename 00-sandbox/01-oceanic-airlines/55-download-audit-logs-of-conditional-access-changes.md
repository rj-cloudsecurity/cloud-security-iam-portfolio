# Sandbox: Download Audit Logs of Conditional Access Changes

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Een wijziging in een Conditional Access policy moet terug te vinden zijn in de audit logs, en de logs moeten te downloaden zijn.

## Doel
Een Conditional Access policy wijzigen, de audit logs op die wijziging filteren en bekijken welke exportformaten de portal biedt.

## Stappen
1. In **Entra ID** -> **Conditional Access** -> **Policies** de naam van het beleid `Sign-in risk: require MFA` gewijzigd in `Require MFA for Sign-in risk` (om 10:34) en opgeslagen
2. **Entra ID** -> **Monitoring & health** -> **Audit logs**
3. Date range op de laatste 24 uur, Service op **Conditional Access**, Activity op **Update conditional access policy**
4. De regel van 10:35:21 geopend en de tab **Modified Properties** bekeken
5. Op **Download** in de werkbalk geklikt

## Resultaat
- De wijziging verscheen in de audit logs om 10:35:21: Service Conditional Access, Category Policy, Activity **Update conditional access policy**, Status Success. Ongeveer een minuut na de wijziging
- Dezelfde wijziging staat ook als twee regels "Update policy" met Service Core Directory
- Onder **Modified Properties** staat de oude waarde (displayName `Sign-in risk: require MFA`) en de nieuwe waarde (`Require MFA for Sign-in risk`), elk als JSON van het hele beleid. Alleen displayName en modifiedDateTime verschillen; de rest (state, conditions, grantControls) is gelijk
- Exportformaten in het Download-menu: JSON of CSV

## Wat dit aantoont
- Wijzigingen aan Conditional Access staan in **Audit logs** met Service Conditional Access en Activity Update conditional access policy
- Een wijziging staat er na ongeveer een minuut, en onder Modified Properties zie je het beleid voor en na de wijziging
- De logs kun je vanuit de portal downloaden via de knop Download
