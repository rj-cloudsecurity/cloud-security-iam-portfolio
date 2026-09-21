# Exercise: Configure Privileged Identity Management for Microsoft Entra Roles

**Bron:** SC-300 Learning Path; Plan and implement an identity governance strategy

## Doel
Role settings voor de Compliance Administrator rol openen en "Require approval to activate" configureren met een eigen approver.

## Wat wel kan (zonder P2)
- Navigeren naar Privileged Identity Management > Microsoft Entra roles > Settings
- De Settings pagina zelf openen, incl. het linker menu (Tasks, Manage, Activity secties)

## Wat niet kan (vereist Entra ID P2 of Entra ID Governance)
- Expliciete melding: "The tenant needs to have Microsoft Entra ID P2 or Microsoft Entra ID Governance license"
- De rollenlijst zelf is leeg ("No results"), Compliance Administrator (of enige andere rol) is niet te vinden of te selecteren
- Role settings bewerken, approval vereisen, en approvers instellen is dus volledig niet uitvoerbaar

## Stappen (theorie, volledige flow)
1. Microsoft Entra admin center > Privileged Identity Management > Microsoft Entra roles > Settings
2. Search by role name: compliance
3. Compliance Administrator selecteren
4. Edit > Require approval to activate aanvinken
5. Select approvers > eigen account selecteren > Select
6. Update

## Resultaat
Niet uitvoerbaar. PIM voor Microsoft Entra roles toont direct een expliciete licentiemelding, en de rollenlijst zelf blijft leeg zonder P2 of Entra ID Governance.

## Wat dit aantoont
- Begrip van de PIM role settings structuur: require approval, approvers, activation duration, etc.
- Herkenning dat PIM (net als eerdere Identity Governance features) volledig geblokkeerd is zonder P2, met een expliciete license melding in plaats van een gedeeltelijk werkende UI
