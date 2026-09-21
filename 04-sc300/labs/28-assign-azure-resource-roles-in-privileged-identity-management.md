# Exercise: Assign Azure Resource Roles in Privileged Identity Management

**Bron:** SC-300 Learning Path; Plan and implement an identity governance strategy

## Doel
Een subscription discoveren en onder PIM management brengen, een user eligible maken voor een Azure resource role (API Management Service Contributor), en een bestaande assignment beheren.

## Wat wel kan (zonder P2)
- PIM > Azure resources openen
- De discovery UI zelf bekijken: Management groups, Subscriptions, Resource groups, en Resources dropdowns zijn zichtbaar en klikbaar
- Filters instellen (Resource type: Subscription, Directory: Oceanic Airlines)

## Wat niet kan (vereist Entra ID P2 of Entra ID Governance)
- Expliciete melding: "To use Microsoft Entra Privileged Identity Management, your organization needs Microsoft Entra ID P2 or Microsoft Entra ID Governance"
- Resultaten blijven leeg ("No results"), ook met filters ingesteld op de eigen subscription/directory
- Discover resources, Manage resource, en alle vervolgstappen (role assignment, activatie, update/remove) zijn niet uitvoerbaar

## Stappen (theorie, volledige flow)

### Resource onder PIM management brengen
1. PIM > Azure resources > Discover resources
2. Subscription selecteren > Manage resource
3. Onboarding bevestigen met OK

### Rol toewijzen als eligible
1. Toegevoegde resource selecteren > Manage > Roles
2. + Add assignments
3. Rol: API Management Service Contributor
4. Member selecteren
5. Settings: Assignment type = Eligible
6. Start/end datum instellen voor de assignment duur
7. Assign

### Bestaande assignment updaten/verwijderen
1. PIM > Azure resources > resource > Manage > Assignments
2. Eligible roles tab, Action kolom
3. Remove > bevestigen met Yes

## Resultaat
Niet uitvoerbaar. De discovery UI zelf is wel zichtbaar en interactief (in tegenstelling tot de Microsoft Entra roles pagina die meteen leeg was), maar levert geen resultaten op zonder P2 of Entra ID Governance, met een expliciete licentiemelding.

## Wat dit aantoont
- Begrip van het PIM voor Azure resources proces: eerst discovery/onboarding, dan pas role assignment mogelijk
- Herkenning van hetzelfde P2/Governance gated patroon, nu specifiek voor Azure resource roles i.p.v. Microsoft Entra roles
