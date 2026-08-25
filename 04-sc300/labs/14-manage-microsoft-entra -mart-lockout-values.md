# Exercise: Manage Microsoft Entra Smart Lockout Values

**Bron:** SC-300 Learning Path; Implement an authentication and access management solution

## Doel
Smart lockout waarden aanpassen (lockout duration en mode) volgens organisatie vereisten.

## Wat wel kan (zonder P1)
- Zoeken naar Password protection
- De pagina zelf bekijken

## Wat niet kan (vereist Entra ID P1 of hoger)
- Velden invullen/aanpassen op de Password protection pagina; melding: "Some features on this page require a Microsoft Entra ID Premium license. Click here to upgrade."
- Lockout duration wijzigen naar een custom waarde (bv. 120 seconden)
- Mode wijzigen naar Enforced
- Wijzigingen opslaan

## Stappen (theorie, volledige flow)
1. Microsoft Entra admin center > Protection > Authentication Methods > Password protection
2. Lockout duration in seconds: instellen op 120
3. Mode: Enforced
4. Save

## Resultaat
Niet uitvoerbaar. De Password protection pagina is toegankelijk om te bekijken, maar velden zijn niet invulbaar zonder Entra ID Premium P1 of hoger.

## Wat dit aantoont
- Begrip van welke smart lockout waarden aanpasbaar zijn (lockout duration, mode) en waarom dit customization vereist P1
- Kennis van het onderscheid tussen de default smart lockout instellingen (altijd actief, gratis) en custom waarden (premium vereist)
- Herkenning van hetzelfde premium gated patroon als bij eerdere labs (MFA, Conditional Access, SSPR)
