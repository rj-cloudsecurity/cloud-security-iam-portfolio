# Exercise: Create a Custom Role to Manage App Registration

**Bron:** SC-300 Learning Path; Implement access management for apps

## Doel
Een custom role aanmaken ("My custom app role") die specifiek toegang geeft om app registration credentials te beheren.

## Wat niet kan (vereist Entra ID P1 of P2)
- Direct bij het openen van New custom role: melding dat de organisatie Entra ID Premium P1 of P2 nodig heeft om custom roles aan te maken
- Geen enkele stap van de wizard (Basics, Permissions, Create) is uitvoerbaar

## Stappen (theorie, volledige flow)
1. Microsoft Entra admin center > Identity > Roles and admins > Roles and administrators
2. New custom role
3. Basics tab: naam = My custom app role, overige opties bekijken, Next
4. Permissions tab: zoeken op "credentials", Manage permissions selecteren, Next
5. Wijzigingen reviewen, Create

## Resultaat
Niet uitvoerbaar. Custom roles vereisen Entra ID Premium P1 of P2, direct geblokkeerd bij het starten van de wizard.

## Wat dit aantoont
- Begrip van de custom role creation flow (Basics, Permissions, Review + Create)
- Herkenning van hetzelfde P1/P2 gated patroon als bij eerdere premium features
- Bevestiging dat custom roles, in tegenstelling tot built-in roles, altijd een premium licentie vereisen

