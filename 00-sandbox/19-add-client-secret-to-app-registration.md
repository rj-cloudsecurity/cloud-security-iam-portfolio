# Sandbox: Adding a Client Secret to an App Registration

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Uitzoeken hoe een app zich authenticeert bij een andere tenant, en waarom een managed identity daarvoor niet werkt.

## Doel
Een credential aanmaken op een app registration en zien waar je een secret en een certificaat toevoegt.

## Stappen
1. Entra admin center -> Entra ID -> App registrations -> **Swan Station App** -> **Certificates & secrets**
2. Client secrets -> **New client secret**
3. Description ingevuld: Sandbox secret for Swan Station App
4. **Add**
5. De **Value** gekopieerd; de Secret ID is alleen een intern kenmerk en heeft de app niet nodig

## Resultaat
- Client secret aangemaakt op Swan Station App
- De Value is maar één keer zichtbaar, direct na het aanmaken

## Wat dit aantoont
- Een app authenticeert zich met een credential (secret of certificaat) uit zijn app registration
- Theorie, niet getest: een managed identity werkt niet over tenants heen, omdat hij bij één Azure-resource in één tenant hoort. Voor cross-tenant toegang gebruik je daarom een app registration met secret of certificaat.
