# Exercise: Enable Sign-in Risk Policy

**Bron:** SC-300 Learning Path; Implement an authentication and access management solution

## Doel
User risk policy en sign in risk policy inschakelen en configureren via Identity Protection.

## Belangrijke waarschuwing gezien in de UI
Bij User risk policy staat een melding: "This risk policy is now read only and will be retired on October 1 2026. To manage or modify it, migrate it to Conditional Access." Dit betekent dat de legacy Identity Protection risk policies worden uitgefaseerd ten gunste van risk based Conditional Access policies.

## Wat wel kan (zonder P2)
- Identity Protection > User risk policy pagina openen en bekijken
- Assignments sectie bekijken (All users optie zichtbaar)

## Wat niet kan (vereist Entra ID P2)
- Onder Assignments: "Select individuals and groups" optie is niet aanklikbaar
- Onder User risk: threshold instellen op High (of andere waarde) is geblokkeerd, met melding: "This view is for Microsoft Entra ID P2 customers to setup user risk policy. Other customers can only disable policies here."
- Onder Controls > Access > Block access: eveneens grijs/disabled, zelfde P2 melding
- Sign-in risk policy configureren zal waarschijnlijk hetzelfde patroon volgen (niet apart getest, zelfde onderliggende licentie beperking)

## Stappen (theorie, volledige flow)

### Enable user risk policy
1. Microsoft Entra admin center > Identity > Protection > Identity protection > User risk policy
2. Assignments: All users, of Select individuals and groups voor beperkte rollout, exclusions mogelijk
3. User risk: Low and above (of hoger, bv. High)
4. Controls > Access > Block access, of aanbevolen: Allow access + Require password change
5. Enforce Policy: On > Save

### Enable sign-in risk policy
1. Identity protection > Sign-in risk policy
2. Assignments: zelfde opties als user risk policy
3. Sign-in risk: Medium and above (of hoger, bv. High)
4. Controls > Access > Block access, of Require multifactor authentication
5. Enforce Policy: On > Save

## Resultaat
Niet uitvoerbaar. De policy pagina's zijn te bekijken, maar alle configuratie opties (assignments beperken, risk threshold instellen, access controls kiezen) zijn geblokkeerd zonder Entra ID Premium P2. Daarnaast toont Microsoft zelf dat deze legacy risk policies worden uitgefaseerd per 1 oktober 2026, ten gunste van Conditional Access.

## Wat dit aantoont
- Begrip van de opbouw van user risk en sign in risk policies (assignments, risk threshold, access controls)
- Herkenning van hetzelfde P2 gated patroon als bij eerdere Identity Protection gerelateerde features
- Bewustzijn dat deze specifieke legacy policy interface wordt uitgefaseerd, en dat de toekomstige aanpak via Conditional Access loopt
