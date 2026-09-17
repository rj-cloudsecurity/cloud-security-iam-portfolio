# Exercise: Create and Manage a Resource Catalog with Microsoft Entra Entitlement Management

**Bron:** SC-300 Learning Path; Plan and implement an identity governance strategy

## Doel
Een catalog aanmaken binnen Entitlement Management, resources toevoegen, catalog owners toevoegen, en de catalog bewerken/verwijderen.

## Wat niet kan (vereist Entra ID P1, P2, EMS E3, of EMS E5)
- Identity Governance openen geeft direct een 401 error: "No access"
- Geen enkele stap van de exercise is uitvoerbaar; zelfs de eerste navigatie naar ID Governance > Entitlement management > Catalogs is al geblokkeerd

## Stappen (theorie, volledige flow)

### Catalog aanmaken
1. Microsoft Entra admin center > ID Governance > Entitlement management > Catalogs
2. + New Catalog
3. Naam: Marketing
4. Description: For marketing department users
5. Enabled: No (voor deze exercise niet nodig)
6. Create

### Resources toevoegen aan de catalog
1. Catalogs > Marketing > Manage > Resources
2. + Add resources
3. Resource categorie kiezen (Groups and Teams, Applications, of SharePoint sites), resource selecteren
4. Add

### Extra catalog owners toevoegen
1. Marketing catalog > Roles and administrators
2. + Add owner
3. Administrator account selecteren, Select

### Catalog bewerken
1. Marketing > Overview > Edit
2. Enabled op Yes zetten
3. Save

### Catalog verwijderen
1. Marketing > Overview > Delete
2. Bevestigen met Yes

## Resultaat
Volledig niet uitvoerbaar in de sandbox. In tegenstelling tot eerdere premium gated features (die een landingspagina met upgrade optie toonden), geeft Identity Governance hier direct een harde 401 "No access" foutmelding, zonder enige UI te tonen.

## Wat dit aantoont
- Begrip van de opbouw van entitlement management: catalog als container, resources daarin, owners voor delegatie
- Herkenning dat Identity Governance features (entitlement management, catalogs, access packages) volledig P1/P2/EMS licentie vereisen, strenger afgeschermd dan sommige eerdere premium features
- Kennis van de catalog lifecycle: aanmaken, resources toevoegen, owners delegeren, bewerken, verwijderen (alleen mogelijk zonder gekoppelde access packages)
