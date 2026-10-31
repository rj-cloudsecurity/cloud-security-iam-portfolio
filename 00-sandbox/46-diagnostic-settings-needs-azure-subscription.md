# Sandbox: Looking for Diagnostic Settings to Send Entra Logs to Log Analytics

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Entra-logs (zoals audit logs) langer bewaren of analyseren kan door ze naar een Log Analytics workspace te sturen.

## Doel
Nagaan waar je dit instelt en wat je daarvoor nodig hebt.

## Stappen
1. Entra admin center -> **Entra ID** -> **Monitoring & health** -> **Diagnostic settings**
2. Gekeken naar het scherm **Diagnostic settings | General**

## Resultaat
- Het scherm toonde alleen de melding: "An Azure subscription is required to use this capability", met een link om een subscription aan te maken
- Een knop om een diagnostic setting toe te voegen was er niet
- In hetzelfde menu staan ook **Sign-in logs**, **Audit logs**, **Provisioning logs**, **Log Analytics** en **Workbooks**

## Wat dit aantoont
- Logs naar Log Analytics sturen vraagt een Azure-subscription, omdat de workspace een Azure-resource is
- De eerste stap is daarom het aanmaken van een Log Analytics workspace in een subscription; pas daarna maak je de diagnostic setting
- Niet getest: het aanmaken van de workspace en de diagnostic setting zelf, want mijn tenant heeft geen subscription
