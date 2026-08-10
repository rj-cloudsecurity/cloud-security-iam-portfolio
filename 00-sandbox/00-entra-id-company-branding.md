# Sandbox: Entra ID Company Branding

**Type:** Eigen verkenning in persoonlijke test-tenant

## Aanleiding
Wilde zelf uitproberen hoe branding werkt in de praktijk binnen mijn eigen Entra ID omgeving.

## Doel
Custom branding (logo, achtergrond) configureren op de sign-in pagina van mijn eigen Entra ID tenant.

## Stappen
1. Azure Portal -> Microsoft Entra ID -> Manage -> Company branding
2. Logo (.png) geüpload via de branding-instellingen
3. Configuratie opgeslagen

## Resultaat
- Logo succesvol opgeslagen in de configuratie
- **Niet zichtbaar** op de daadwerkelijke sign-in pagina (`login.microsoftonline.com`)

## Root cause
Company branding op de sign-in vereist een **Entra ID P1, P2, of Office 365 licentie**. Mijn tenant draait op de gratis Entra ID Free tier; de configuratie-optie is toegankelijk en op te slaan, maar wordt niet gerenderd zonder premium licentie.

## Wat dit aantoont
- Eigen initiatief om theorie te testen in een echte omgeving
- Begrip van het licentiemodel achter Entra ID features
- Onderscheid tussen "feature toegankelijk in UI" vs "feature actief in productie"
