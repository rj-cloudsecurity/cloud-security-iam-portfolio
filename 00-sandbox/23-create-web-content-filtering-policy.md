# Sandbox: Creating a Web Content Filtering Policy

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Praktisch ervaren hoe je websitecategorieën blokkeert met Global Secure Access.

## Doel
Een web content filtering policy maken die social media blokkeert.

## Stappen
1. Entra admin center -> Global Secure Access -> **Secure** -> **Web content filtering policies** -> Create
2. Naam: **Block social media**
3. Rule toegevoegd: **Social Media**, actie **Block**
4. Web category: **Social Networking**
5. Create

## Resultaat
- Web content filtering policy "Block social media" aangemaakt
- De policy doet nog niets totdat hij aan een security profile is gekoppeld

## Wat dit aantoont
- De web content filtering policy is de eerste stap, vóór het security profile en de Conditional Access policy
- Je blokkeert op categorie (zoals Social Networking) en niet op losse websites
