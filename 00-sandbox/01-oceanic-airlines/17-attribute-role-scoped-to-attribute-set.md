# Sandbox: Assigning an Attribute Role Scoped to an Attribute Set

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Praktisch ervaren hoe je een attribute-rol beperkt tot één attribute set in plaats van tot de hele tenant.

## Doel
De rol Attribute Assignment Administrator aan Jacob Pellegrino toewijzen met de attribute set als scope.

## Stappen
1. Entra admin center -> Entra ID -> Custom security attributes -> [attribute set] -> **Roles and administrators**
2. **Attribute Assignment Administrator** -> Add assignments -> **Jacob Pellegrino**

## Resultaat
- Op de pagina Assignments staat Jacob Pellegrino met scope **This resource**
- Mijn eigen user staat er ook, met scope **Directory (Inherited)**

## Wat dit aantoont
- Een rol op set-niveau geeft rechten voor alleen die set, een rol op directory-niveau geldt voor alle sets
- Praktisch begrip van het verschil tussen een directe en een overgenomen scope
