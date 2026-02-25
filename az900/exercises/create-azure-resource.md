
# Create a Microsoft Azure resource 

- Learning path: Introduction to Cloud Infrastructure: Azure architecture & services
- Module: 1. Describe the core architectural components of Azure

- Note: De originele oefening wordt uitgevoerd via de Azure Portal, maar ik heb ervoor gekozen om alle opdrachten in PowerShell (Azure CLI) uit te voeren om mijn CLI‑vaardigheden te trainen.

In deze oefening heb ik via de Azure Portal een nieuwe resource group aangemaakt en daarin een virtuele machine gedeployed. Het doel was om te zien hoe Azure automatisch alle benodigde onderdelen aanmaakt en groepeert, zoals netwerkinterfaces, disks en een virtual network. Na de deployment heb ik gecontroleerd welke resources waren aangemaakt en hoe deze binnen dezelfde resource group werden georganiseerd. Tot slot heb ik de volledige resource group verwijderd om alle resources in één keer op te schonen.

## Task 1 Resource Group, create, name, location

```bash
Requesting a Cloud Shell.Succeeded. 
Connecting terminal...

  Your Cloud Shell session will be ephemeral so no files or system changes will persist beyond your current session.
robert-jan [ ~ ]$ az group create \
  --name IntroAzureRG \
  --location "Central US"
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
```

## Task 2 Deploy Virtual Machine

```bash
Requesting a Cloud Shell.Succeeded. 
Connecting terminal...

Your Cloud Shell session will be ephemeral so no files or system changes will persist beyond your current session.
robert-jan [ ~ ]$ az vm create \
  --resource-group IntroAzureRG \
  --name my-VM \
  --image Ubuntu2204 \
  --admin-username robert-jan \
  --admin-password Abc123456789! \
  --size Standard_D2s_v3 \
  --location westeurope \
  --public-ip-sku Standard \
  --nsg-rule NONE
The default value of '--size' will be changed to 'Standard_D2s_v5' from 'Standard_DS1_v2' in a future release.
Selecting "uksouth" may reduce your costs. The region you've selected may cost more for the same services. You can disable this message in the future with the command "az config set core.display_region_identified=false". Learn more at https://go.microsoft.com/fwlink/?linkid=222571 

{
  "fqdns": "",
  "id": "/subscriptions/69799361-14fa-4e9b-8b7f-e48e93f9e422/resourceGroups/IntroAzureRG/providers/Microsoft.Compute/virtualMachines/my-VM",
  "location": "westeurope",
  "macAddress": "00-0D-3A-BE-54-93",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "20.229.41.188",
  "resourceGroup": "IntroAzureRG"
}
```

## Task 3 Verify Created Resources

```bash
robert-jan [ ~ ]$ az resource list --resource-group IntroAzureRG --output table
Name                                          ResourceGroup    Location    Type                                     Status
--------------------------------------------  ---------------  ----------  ---------------------------------------  ---------
my-VMNSG                                      IntroAzureRG     westeurope  Microsoft.Network/networkSecurityGroups  Succeeded
my-VMPublicIP                                 IntroAzureRG     westeurope  Microsoft.Network/publicIPAddresses      Succeeded
my-VMVNET                                     IntroAzureRG     westeurope  Microsoft.Network/virtualNetworks        Succeeded
my-VMVMNic                                    IntroAzureRG     westeurope  Microsoft.Network/networkInterfaces      Succeeded
my-VM                                         IntroAzureRG     westeurope  Microsoft.Compute/virtualMachines        Succeeded
my-VM_disk1_15de01512b074201903571c3a95155cc  INTROAZURERG     westeurope  Microsoft.Compute/disks                  Succeeded
```

## Task 4 Cleanup

```bash
robert-jan [ ~ ]$ az group delete \
--name IntroAzureRG \
--yes \
--no-wait
```

## Taks 5 Check 1
```bash
robert-jan [ ~ ]$ az group show --name IntroAzureRG
{
  "id": "/subscriptions/69799361-14fa-4e9b-8b7f-e48e93f9e422/resourceGroups/IntroAzureRG",
  "location": "centralus",
  "managedBy": null,
  "name": "IntroAzureRG",
  "properties": {
    "provisioningState": "Deleting"
  },
```

## Taks 6 Check 2
```bash
robert-jan [ ~ ]$ az group show --name IntroAzureRG
(ResourceGroupNotFound) Resource group 'IntroAzureRG' could not be found.
Code: ResourceGroupNotFound
Message: Resource group 'IntroAzureRG' could not be found.
```
