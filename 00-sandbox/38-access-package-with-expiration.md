# Sandbox: Creating an Access Package with Expiration

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Tijdelijke toegang geven die na 90 dagen automatisch verloopt.

## Doel
Een access package maken met een toewijzing die na 90 dagen afloopt.

## Stappen
1. Entra admin center -> ID Governance -> **Entitlement management** -> **Access packages** -> **New access package**
2. Basics: naam **Island Access**, catalog **General**
3. Resource roles: group **Island Resources** met de rol **Member**
4. Requests: *For users in your directory*, mijn testgroep als toegestane aanvragers, goedkeuring vereist met mijzelf als approver
5. Lifecycle: **Access package assignments expire: After 90 days**
6. Require access reviews: ingeschakeld met een maandelijkse self-review
7. Review + create -> **Create**

## Resultaat
- Access package "Island Access" met de policy *Initial Policy*
- Op het overzichtsscherm stond bij de resource eerst "No role selected" en bij de approver "None selected"; na het kiezen van de rol Member en mijzelf als approver kon ik het aanmaken

## Wat dit aantoont
- De tijdslimiet stel je in bij Lifecycle in de policy van de access package
- Een access package heeft een resource role nodig, anders geeft hij geen toegang
- Een verloopdatum (assignments expire) is iets anders dan een access review: het eerste is een harde einddatum, het tweede een controle tussendoor
