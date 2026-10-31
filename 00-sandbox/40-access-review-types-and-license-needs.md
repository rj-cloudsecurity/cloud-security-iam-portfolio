# Sandbox: What an Access Review Can Cover and Which License It Needs

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Uitzoeken voor welke soorten toegang je een access review kunt maken en welke licentie daarbij hoort.

## Doel
In de wizards nagaan welke resource types ik kan kiezen: een group, een enterprise app, een Entra-rol en een service principal.

## Stappen
1. Entra admin center -> ID Governance -> **Access reviews** -> **New access review** -> template **Resource review**
2. Bij **Select what to review**: de keuzes bekeken. Ik kon **Teams + Groups** en **Applications** kiezen
3. Bij Teams + Groups: scope **All Microsoft 365 groups with guest users** of **Select Teams + groups**; daarna voor de group Island Resources de scope **Guest users only** of **All users**
4. Bij Applications: de app Box gekozen; scope **Guest users only** of **All users**
5. Entra-rollen en service principals: ID Governance -> **Privileged Identity Management** -> **Microsoft Entra roles** -> **Access reviews** -> **New**
6. Daar: scope **All users and groups** of **Service Principals**, plus **Select privileged role(s)**

## Resultaat
- Group, enterprise app en Entra-rol: te kiezen in mijn tenant
- Service Principals: grijs, niet te kiezen. Dat past bij de licentie Microsoft Entra Workload ID Premium, die niet in mijn Entra Suite-trial zit
- Op de Access reviews-pagina stond een banner: sinds 15 januari 2026 is een gekoppeld Azure-subscription nodig voor Entra ID Governance-functies met gasten, en de kosten zijn gebaseerd op unieke gasten per maand

## Wat dit aantoont
- Een access review kan groups, apps, Entra-rollen (via PIM) en access packages dekken
- Reviews van Entra-rollen en service principals zitten onder PIM, niet onder de gewone Access reviews
- Entra ID Governance (of P2) is nodig voor access reviews; service principals vragen daarbovenop Workload ID Premium
- Niet bevestigd: de exacte licentietekst voor service principals, want de optie was grijs zonder uitleg
