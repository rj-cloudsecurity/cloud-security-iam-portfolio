# Sandbox: Self-service Access to an Enterprise App With Approval

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Gebruikers moeten toestemming vragen voordat ze toegang krijgen tot een enterprise app.

## Doel
Self-service toegang aanzetten voor een enterprise app, een approver kiezen en het verzoek testen in het My Apps-portaal.

## Stappen
1. Een security group `swan station` gemaakt (Assigned membership, ik als owner, geen leden)
2. **Entra ID** -> **Enterprise apps** -> **Swan Station App** -> **Self-service**
3. **Allow users to request access to this application?** op **Yes**, groep `swan station`, **Require approval before granting access** op **Yes**, ikzelf als approver, **Save**
4. Als Frank Lapidus in een privévenster ingelogd. In het Entra admin center is er geen plek om toegang te vragen; de app stond ook niet bij My Apps
5. Bij **Properties** van de app stond **Visible to users?** op **No**. Die op **Yes** gezet en opgeslagen
6. Als Frank bij **myapps.microsoft.com**: **Apps dashboard** -> **Add apps** -> **Request new apps** -> **Swan Station App** -> **Request**
7. Als beheerder naar **myaccess.microsoft.com** -> **My Groups** -> **Requests**. Het verzoek van Frank Lapidus voor Swan Station gevonden en op **Approve** geklikt

## Resultaat
- Zonder **Visible to users?** op Yes kon Frank de app niet vinden in My Apps
- Frank kon de app daarna aanvragen via Add apps -> Request new apps
- Het verzoek verscheen bij mij in My Access en ik heb het goedgekeurd
- Frank werd lid van de groep: swan station

## Wat dit aantoont
- Self-service toegang stel je in bij de enterprise app onder **Self-service**: groep, goedkeuring en approver
- Gebruikers vragen toegang aan in My Apps (**Add apps** -> **Request new apps**), niet in het admin center
- **Visible to users?** moet op Yes staan, anders zie je de app niet in My Apps
- De approver keurt goed in My Access
