
# Create a Microsoft Azure resource 

- Learning path: Introduction to Cloud Infrastructure: Azure architecture & services
- Module: 1. Describe the core architectural components of Azure

Deze oefening voer ik twee keer uit:
  - Eerst via de Azure Portal (UI)
  - Daarna via de Azure CLI

In deze oefening heb ik via de Azure Portal en CLI een nieuwe resource group aangemaakt en daarin een virtuele machine gedeployed. Het doel was om te zien hoe Azure automatisch alle benodigde onderdelen aanmaakt en groepeert, zoals netwerkinterfaces, disks en een virtual network. Na de deployment heb ik gecontroleerd welke resources waren aangemaakt en hoe deze binnen dezelfde resource group werden georganiseerd. Tot slot heb ik de volledige resource group verwijderd om alle resources in één keer op te schonen.

## Task 1 Resource Group, create, name, location

```bash
[ ~ ]$ az group create \
  --name IntroAzureRG \
  --location "westeurope"
{
  "id": "/subscriptions/<subscription-id>/resourceGroups/IntroAzureRG",
  "location": "westeurope",
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
[ ~ ]$ az vm create \
  --resource-group IntroAzureRG \
  --name my-VM \
  --image Ubuntu2204 \
  --admin-username robert-jan \
  --admin-password <"password"> \
  --size Standard_D2s_v3 \
  --location westeurope \
  --public-ip-sku Standard \
  --nsg-rule NONE
The default value of '--size' will be changed to 'Standard_D2s_v5' from 'Standard_DS1_v2' in a future release.
Selecting "uksouth" may reduce your costs. The region you've selected may cost more for the same services. You can disable this message in the future with the command "az config set core.display_region_identified=false". Learn more at https://go.microsoft.com/fwlink/?linkid=222571 

{
  "fqdns": "",
  "id": "/subscriptions/<subscription-id>/resourceGroups/IntroAzureRG/providers/Microsoft.Compute/virtualMachines/my-VM",
  "location": "westeurope",
  "macAddress": "<mac-address>",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "<public-ip>",
  "resourceGroup": "IntroAzureRG"
}
```

## Task 3 Verify Created Resources

```bash
[ ~ ]$ az resource list --resource-group IntroAzureRG --output table
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
[ ~ ]$ az group delete \
  --name IntroAzureRG \
  --yes \
  --no-wait
```

## Task 5 Check 1
```bash
[ ~ ]$ az group show --name IntroAzureRG
{
  "id": "/subscriptions/<subscription-id>/resourceGroups/IntroAzureRG",
  "location": "westeurope",
  "managedBy": null,
  "name": "IntroAzureRG",
  "properties": {
    "provisioningState": "Deleting"
  },
```

## Task 6 Check 2
```bash
[ ~ ]$ az group show --name IntroAzureRG
(ResourceGroupNotFound) Resource group 'IntroAzureRG' could not be found.
Code: ResourceGroupNotFound
Message: Resource group 'IntroAzureRG' could not be found.
```
