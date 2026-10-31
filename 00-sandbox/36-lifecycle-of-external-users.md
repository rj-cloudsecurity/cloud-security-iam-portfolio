# Sandbox: Configuring the Lifecycle of External Users

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Uitzoeken wat er met externe gebruikers gebeurt als ze via een access package zijn toegevoegd en hun toegang verliezen.

## Doel
Instellen dat externe gebruikers automatisch worden verwijderd na 90 dagen.

## Stappen
1. Entra admin center -> ID Governance -> **Entitlement management** -> **Control configurations**
2. Bij **Lifecycle of external users** (Enabled) op **View settings** geklikt
3. Gezien: **Remove external user** en **Block external user from signing in to directory** stonden aan, het aantal dagen stond op **30**
4. Het aantal dagen veranderd naar **90**
5. **Save**

## Resultaat
- Externe gebruikers worden na 90 dagen verwijderd uit de directory, nadat ze hun laatste access package-toewijzing hebben verloren
- Eerst worden ze geblokkeerd bij het inloggen, daarna verwijderd

## Wat dit aantoont
- De standaardwaarde is 30 dagen; de waarde stel je in bij Control configurations
- De instelling geldt voor gasten die via een access package zijn toegevoegd en geen enkele toewijzing meer hebben
- Niet getest: het daadwerkelijk verwijderen van een gast, want dat vraagt 90 dagen wachten
