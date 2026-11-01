# Sandbox: Creating a Dynamic Group for Guest Users

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Een Conditional Access-policy voor externe gebruikers wil ik aan één group koppelen, in plaats van aan elke gast apart.

## Doel
Een dynamic group maken die automatisch alle gasten bevat, behalve mijn eigen gastaccount met de rol Global Administrator.

## Stappen
1. Entra admin center -> **Entra ID** -> **Groups** -> **New group**
2. Group type **Security**, naam **External User Group**, Membership type **Dynamic User**
3. Bij **Dynamic membership rules** de regel ingevuld:
   `(user.userType -eq "Guest") and (user.userPrincipalName -ne "<UPN van mijn gast-admin>")`
4. **Create**
5. Na een paar minuten bij **Members** gecontroleerd

## Resultaat
- In de group staan de drie nieuwe gasten (Hawking, Abaddon en Widmore) en een eerder uitgenodigde gast
- Mijn eigen gast-admin zit er niet in

## Wat dit aantoont
- Een dynamic group vult zichzelf aan de hand van een regel op een attribuut, hier userType
- Dynamic groups vragen Entra ID P1; de leden verschijnen pas na enkele minuten
- Met een tweede voorwaarde in de regel kun je een account uitsluiten, zodat een beheerder niet onder een beperkende policy valt
