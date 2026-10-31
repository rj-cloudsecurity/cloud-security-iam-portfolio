# Sandbox: Making a Decision as Reviewer in My Access

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Zien hoe een review er voor de reviewer uitziet.

## Doel
Als reviewer een beslissing nemen over de toegang van Benjamin Linus tot Island Resources.

## Stappen
1. Browser -> **myaccess.microsoft.com** (geen menu-item in het Entra admin center)
2. Links **Access reviews** -> **Test review access**
3. Benjamin Linus geselecteerd en **Deny** gekozen
4. Beslissing ingediend

## Resultaat
- Bij Benjamin stond de aanbeveling **Deny** met de reden **Inactive user**
- De kolom Decision toonde **Denied**, Reviewed by **Paulides**
- Benjamin bleef nog lid van de group zolang de review liep, tot de review werd afgerond en het resultaat werd toegepast (zie entry 43)

## Wat dit aantoont
- Een reviewer beslist in My Access en niet in het Entra admin center
- Een beslissing wordt pas toegepast als de review is afgerond
- De aanbeveling Inactive user komt uit de recommendations: de user had zich nog niet aangemeld
