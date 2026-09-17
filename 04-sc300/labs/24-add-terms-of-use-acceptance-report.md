# Exercise: Add Terms of Use Acceptance Report

**Bron:** SC-300 Learning Path; Plan and implement an identity governance strategy

## Doel
Terms of use (ToU) aanmaken op basis van een PDF document, afdwingen via een Conditional Access policy, en het acceptance report bekijken.

## Wat niet kan (vereist Entra ID P1, P2, EMS E3, of EMS E5; onderliggend gebruikt Conditional Access)
- ID Governance openen geeft direct een 401 error, zoals eerder al bevestigd
- Terms of use aanmaken vereist ID Governance zelf
- Afdwingen van de terms of use vereist een Conditional Access policy, wat ook al eerder geblokkeerd bleek zonder P1/P2

## Stappen (theorie, volledige flow)

### Terms of use aanmaken
1. Microsoft Entra admin center > ID Governance > Entitlement Management > Terms of use > + New terms
2. Name: interne naam (niet zichtbaar voor users)
3. Display name: naam die users zien
4. PDF document uploaden (aanbevolen fontgrootte 24pt voor mobiel)
5. Taal selecteren (meerdere talen mogelijk, browser voorkeur van de user bepaalt welke versie ze zien)
6. Require users to expand the terms of use: On, om te forceren dat users het document openen voor accepteren
7. Require users to consent on every device: On, indien gewenst (vereist device registratie in Entra ID)
8. Expire consents: On, met Expire starting on datum en Frequency, of Duration before reacceptance (dagen)
9. Conditional Access: Custom policy kiezen (users/groups/apps selecteren) of later een Conditional Access policy aanmaken
10. Create

### Conditional Access policy voor de terms of use
1. Naam: bv. Enforce ToU
2. Assignments > Users and groups > testaccount selecteren (nooit alleen het eigen admin account, altijd een tweede beheerdersaccount achter de hand houden)
3. Cloud apps or actions > All cloud apps
4. Access controls > Grant > Testing terms of use > Select
5. Enable policy: On > Create

### Acceptance report bekijken
1. ID Governance > Terms of use > eigen terms of use selecteren
2. Cijfers onder Accepted/Declined aanklikken voor de lijst van users
3. Ellipsis naast een user > View History voor een historie van accepts/declines/expirations

### Terms of use bewerken
- Name, Display name, Require users to expand, taal toevoegen, en andere instellingen aanpasbaar
- Bestaand document zelf kan niet gewijzigd worden, alleen vervangen via Update in de Language Options tabel
- Require reaccept toggle bepaalt of bestaande consents geldig blijven of dat iedereen opnieuw moet accepteren

### Hoe users hun eigen terms of use kunnen terugzien
- myaccount.microsoft.com > View settings and privacy > Privacy tab > Organization's notice

## Resultaat
Niet uitvoerbaar. Zowel Entitlement Management (voor het aanmaken van de terms of use) als Conditional Access (voor het afdwingen ervan) zijn al eerder bevestigd geblokkeerd zonder P1/P2 licentie in deze tenant.

## Wat dit aantoont
- Begrip van hoe terms of use zijn opgebouwd: PDF document, taalopties, expiration/reacceptance schema's, en afdwinging via Conditional Access
- Kennis van het verschil tussen een schema gebaseerde expiration (vaste datum + frequency) en een duration gebaseerde expiration (per user vanaf hun eigen accept datum)
- Herkenning dat terms of use twee losse premium features combineert (Entitlement Management + Conditional Access), beide al bevestigd geblokkeerd in deze sandbox







































