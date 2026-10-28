# Sandbox: Blocking Legacy Authentication with Conditional Access

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Uitzoeken hoe je met Conditional Access oude inlogmethoden zonder moderne authenticatie blokkeert, en hoe je kunt testen of de policy alleen die clients raakt.

## Doel
Een Conditional Access policy maken die legacy authentication clients blokkeert, en met de What If-tool controleren dat moderne clients niet geraakt worden.

## Stappen
1. Entra admin center -> Entra ID -> **Conditional Access** -> Policies -> **New policy**
2. Naam: **Block legacy authentication**
3. Users: **All users** included, met specifieke users excluded
4. Target resources: **All resources (formerly 'All cloud apps')**; de waarschuwing over het Azure portal gezien en genegeerd, omdat de policy alleen legacy clients raakt
5. Conditions -> **Client apps** -> Configure **Yes**: alleen **Exchange ActiveSync clients** en **Other clients** aangevinkt; **Browser** en **Mobile apps and desktop clients** uit
6. Grant: **Block access**
7. Enable policy: **Report-only**, daarna Create
8. Conditional Access -> **What If** met Greta: Client app **Mobile apps and desktop clients - Other clients**
9. Opnieuw met Client app **Mobile apps and desktop clients - Modern authentication clients**

## Resultaat
- Bij Other clients staat onder *Policies that will apply* 1 policy: **Block legacy authentication**, Grant controls **Block access**, State **Report-only**
- Bij Modern authentication clients: **0 policies found**

## Wat dit aantoont
- Legacy authentication zit in twee client types: Exchange ActiveSync clients en Other clients
- De policy raakt alleen legacy clients; clients met moderne authenticatie vallen er niet onder
- Report-only laat je de werking zien zonder iemand te blokkeren
- De What If-tool vraagt altijd om een cloud app, ook als de policy op All resources staat
