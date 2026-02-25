
# Create a Microsoft Azure resource 

## Learning path: Introduction to Cloud Infrastructure: Azure architecture & services
  ## Module: 1. Describe the core architectural components of Azure

Note: De originele oefening wordt uitgevoerd via de Azure Portal, maar ik heb ervoor gekozen om alle opdrachten in PowerShell (Azure CLI) uit te voeren om mijn CLI‑vaardigheden te trainen.

In deze oefening heb ik via de Azure Portal een nieuwe resource group aangemaakt en daarin een virtuele machine gedeployed. Het doel was om te zien hoe Azure automatisch alle benodigde onderdelen aanmaakt en groepeert, zoals netwerkinterfaces, disks en een virtual network. Na de deployment heb ik gecontroleerd welke resources waren aangemaakt en hoe deze binnen dezelfde resource group werden georganiseerd. Tot slot heb ik de volledige resource group verwijderd om alle resources in één keer op te schonen.

## Task 1 Group, create, name, location

```bash
Requesting a Cloud Shell.Succeeded. 
Connecting terminal...

  Your Cloud Shell session will be ephemeral so no files or system changes will persist beyond your current session.
robert-jan [ ~ ]$ az group create \--name IntroAzureRG \--location "Central US"
{
  "id": "/subscriptions/69799361-14fa-4e9b-8b7f-e48e93f9e422/resourceGroups/IntroAzureRG",
  "location": "centralus",
  "managedBy": null,
  "name": "IntroAzureRG",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null,
  "type": "Microsoft.Resources/resourceGroups"
}
