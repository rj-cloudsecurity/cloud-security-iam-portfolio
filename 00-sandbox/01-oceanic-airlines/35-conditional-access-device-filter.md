# Sandbox: Restricting an App to Entra-joined Devices with Conditional Access

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Een app mag alleen bereikbaar zijn vanaf Entra-joined devices.

## Doel
Een Conditional Access policy maken die de app Box blokkeert voor alle devices die niet Entra-joined zijn.

## Stappen
1. Entra admin center -> Entra ID -> **Conditional Access** -> Policies -> **New policy**
2. Naam: **Gallery app - Entra joined only**
3. Users: group **Jacobs Security Group** included, mijzelf excluded
4. Target resources: **Select resources** -> **Box**
5. Conditions -> **Filter for devices**: Configure **Yes**, **Exclude filtered devices from policy**, regel `device.trustType -eq "AzureAD"` (trustType Equals Microsoft Entra joined)
6. Grant: **Block access**
7. Enable policy: **Report-only**
8. Create

## Resultaat
- Policy aangemaakt in Report-only: 1 group included, 1 resource included, filter for devices 1 included, requirements for access Block access
- Bij het aanmaken meldde het portal dat Users nog een group moest bevatten; daarna lukte Create

## Wat dit aantoont
- Met een device filter op trustType blokkeer je alle devices behalve Entra-joined devices
- Bij Exclude filtered devices geldt de policy voor alle devices die niet aan de regel voldoen
- Niet getest: het effect met de What If-tool of op een echt device
