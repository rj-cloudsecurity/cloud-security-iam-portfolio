# Exercise: Configure Microsoft Entra Multifactor Authentication Registration Policy

**Bron:** SC-300 Learning Path; Implement an authentication and access management solution

## Doel
Een policy inschakelen die users verplicht om te registreren voor multi factor authentication (MFA), voordat ze op MFA prompts kunnen reageren.

## Wat wel kan (zonder P2)
- Identity Protection > Multifactor authentication registration policy pagina openen en bekijken
- Assignments sectie bekijken: Users > All users, met opties All users of Select individuals and groups (0 users and groups selected getoond)

## Wat niet kan (vereist Entra ID P2)
- Controls: "Require Microsoft Entra ID multifactor authentication registration" staat grijs/disabled, kan niet aan of uit gezet worden
- Expliciete melding op de pagina: "This view is for Microsoft Entra ID P2 customers to setup multifactor authentication registration policy. Other customers can only disable policies here."
- Enforce Policy daadwerkelijk op Enabled zetten en opslaan

## Extra info gezien op de pagina
- Info box: "Multifactor authentication registration policy only affects cloud-based Azure multifactor authentication. If you have multifactor authentication server it will not be affected." Dit betekent dat deze policy niet van toepassing is op een eventuele on premises MFA server oplossing, alleen op de cloud based Entra MFA.

## Stappen (theorie, volledige flow)
1. Microsoft Entra admin center > Identity > Protection > Identity protection > Multifactor authentication registration policy
2. Assignments: All users, of Select individuals and groups voor beperkte rollout, exclusions mogelijk
3. Controls: Require Microsoft Entra ID multifactor authentication registration staat al vast geselecteerd, niet aanpasbaar
4. Enforce Policy: Enabled > Save

## Resultaat
Niet uitvoerbaar. De policy pagina en Assignments sectie zijn te bekijken, maar de control zelf staat grijs/disabled en de policy kan niet daadwerkelijk enabled worden zonder Entra ID Premium P2.

## Wat dit aantoont
- Begrip van het doel van de MFA registration policy: users verplichten te registreren voordat ze MFA kunnen gebruiken
- Herkenning van hetzelfde P2 gated patroon als bij de user risk en sign in risk policies
- Kennis van de scope beperking: deze policy geldt alleen voor cloud based MFA, niet voor een eventuele on premises MFA server
