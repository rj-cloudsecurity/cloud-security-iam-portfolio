# Exercise 2. Create a Microsoft Azure Virtual Machine

- Learning path: Introduction to Cloud Infrastructure: Azure architecture & services
- Module: 2. Describe Azure Virtual Machine and Configure network access

In deze oefening maak ik een Azure VM aan. Installeer een web server (Nginx) en update de configuratie van het netwerk zodat deze toegang heeft vanaf het internet. Tot slot controleer ik de NSG regels en test ik de webserver.

Voor deze oefening gebruik ik de Azure CLI in az interactive‑modus bij het eerste gedeelte. Dit maakt het mogelijk om sneller opdrachten uit te voeren, inline suggesties te krijgen en mijn command‑linevaardigheden verder te ontwikkelen.

## Task 1 Resource Group, create, name, location

```bash
az interactive
```

```bash
az>> az group create --name IntroAzureRG --location centralus
{
  "id": "/subscriptions/<subscription-id>/resourceGroups/IntroAzureRG",
  "location": "centralus",
  "managedBy": null,
  "name": "IntroAzureRG",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null,
  "type": "Microsoft.Resources/resourceGroups"
}
az>> 
```

## Task 2 Create a Linux virtual machine

```bash
vm create --name my-vm --size Standard_D2s_v5 --public-ip-sku Standard --image Ubuntu2204 --admin-username azureuser --generate-ssh-keys

``` 
Deze opdracht gaf een foutmelding omdat de VM‑size Standard_D2s_v5 momenteel niet beschikbaar is in de regio centralus. Dit komt door regionale capaciteit‑restricties binnen Azure. Daarom heb ik ervoor gekozen om de VM te deployen in een Europese regio (westeurope) waar deze SKU wél beschikbaar is.

## Task 0 Remove the existing resource group (centralus) and prepare for a new deployment in Europe

```bash
az>> group delete --name IntroAzureRG --yes --no-wait
```

## Task 1 Resource Group, create, name, location (westeurope)

```bash
az>> group create --name IntroAzureRG --location westeurope 
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


## Task 2 Create a Linux virtual machine

```bash
az vm create --rescource-group "IntroAzureRG" --name my-vm --size Standard_D2s_v5 --public-ip-sku Standard --image Ubuntu2204 --admin-username azureuser --generate-ssh-keys 
Selecting "uksouth" may reduce your costs. The region you've selected may cost more for the same services. You can disable this message in the future with the command "az config set core.display_region_identified=false". Learn more at https://go.microsoft.com/fwlink/?linkid=222571 

{
  "fqdns": "",
  "id": "/subscriptions/<subscription-id>/resourceGroups/IntroAzureRG/providers/Microsoft.Compute/virtualMachines/my-vm",
  "location": "westeurope",
  "macAddress": "<mac-address>",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "<public-ip>",
  "resourceGroup": "IntroAzureRG"
}
```

## Task 3 Install Nginx

```bash
 az vm extension set --resource-group "IntroAzureRG" --vm-name my-vm -name customScript --publisher Microsoft.Azure.Extensions --version 2.1 --settings '{"fileUris":["https://raw.githubusercontent.com/MicrosoftDocs/mslearn-welcome-to-azure/master/configure-nginx.sh"]}' --protected-settings '{"commandToExecute": "./configure-nginx.sh"}'

{               
  "autoUpgradeMinorVersion": true,
  "id": "/subscriptions/<subscription-id>/resourceGroups/IntroAzureRG/providers/Microsoft.Compute/virtualMachines/my-vm/extensions/customScript",
  "location": "westeurope",
  "name": "customScript",
  "provisioningState": "Succeeded",
  "publisher": "Microsoft.Azure.Extensions",
  "resourceGroup": "IntroAzureRG",
  "settings": {
    "fileUris": [
      "https://raw.githubusercontent.com/MicrosoftDocs/mslearn-welcome-to-azure/master/configure-nginx.sh"
    ]
  },
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "typeHandlerVersion": "2.1",
  "typePropertiesType": "customScript"
}
```

## Task 4 Access your web server (exiting interactive) 

```bash
[ ~ ]$ IPADDRESS="$(az vm list-ip-addresses \
> --resource-group "IntroAzureRG" \
> --name my-vm \
> --query "[].virtualMachine.network.publicIpAddresses[*].ipAddress" \
> --output tsv)"
robert-jan [ ~ ]$ curl --connect-timeout 5 http://$IPADDRESS
curl: (28) Connection timed out after 5002 milliseconds
robert-jan [ ~ ]$ echo $IPADDRESS
<public-ip>
```

## Task 5 List the current network security group rules

```bash
[ ~ ]$ az network nsg list \
> --resource-group "IntroAzureRG" \
> --query '[].name' \
> --output tsv
my-vmNSG
```

```bash
[ ~ ]$ az network nsg rule list \
> --resource-group 'IntroAzureRG' \
> --nsg-name my-vmNSG
[
  {
    "access": "Allow",
    "destinationAddressPrefix": "*",
    "destinationAddressPrefixes": [],
    "destinationPortRange": "22",
    "destinationPortRanges": [],
    "direction": "Inbound",
    "etag": "W/\"33ca56c4-d4c2-4ad4-9b03-b9ce0d902682\"",
    "id": "/subscriptions/<subscription-id>/resourceGroups/IntroAzureRG/providers/Microsoft.Network/networkSecurityGroups/my-vmNSG/securityRules/default-allow-ssh",
    "name": "default-allow-ssh",
    "priority": 1000,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "IntroAzureRG",
    "sourceAddressPrefix": "*",
    "sourceAddressPrefixes": [],
    "sourcePortRange": "*",
    "sourcePortRanges": [],
    "type": "Microsoft.Network/networkSecurityGroups/securityRules"
  }
]
```

```bash
[ ~ ]$ az network nsg rule list \
  --resource-group "IntroAzureRG" \
  --nsg-name my-vmNSG \
  --query '[].{Name:name, Priority:priority, Port:destinationPortRange, Access:access}' \
  --output table    
Name               Priority    Port    Access
-----------------  ----------  ------  --------
default-allow-ssh  1000        22      Allow
```

## Task 6 Create the network security rule

```bash
[ ~ ]$ az network nsg rule create \
  --resource-group "IntroAzureRG" \
  --nsg-name my-vmNSG \
  --name allow-http \
  --protocol tcp \
  --priority 100 \
  --destination-port-range 80 \
  --access Allow    
{
  "access": "Allow",
  "destinationAddressPrefix": "*",
  "destinationAddressPrefixes": [],
  "destinationPortRange": "80",
  "destinationPortRanges": [],
  "direction": "Inbound",
  "etag": "W/\"2ff2fcac-0960-42a8-89c6-a06c4e9702e3\"",
  "id": "/subscriptions/<subscription-id>/resourceGroups/IntroAzureRG/providers/Microsoft.Network/networkSecurityGroups/my-vmNSG/securityRules/allow-http",
  "name": "allow-http",
  "priority": 100,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "IntroAzureRG",
  "sourceAddressPrefix": "*",
  "sourceAddressPrefixes": [],
  "sourcePortRange": "*",
  "sourcePortRanges": [],
  "type": "Microsoft.Network/networkSecurityGroups/securityRules"
}
```

```bash
[ ~ ]$ az network nsg rule list \
  --resource-group "IntroAzureRG" \
  --nsg-name my-vmNSG \
  --query '[].{Name:name, Priority:priority, Port:destinationPortRange, Access:access}' \
  --output table    
Name               Priority    Port    Access
-----------------  ----------  ------  --------
default-allow-ssh  1000        22      Allow
allow-http         100         80      Allow
```

## Task 7 Access your web server again

```bash
[ ~ ]$ curl --connect-timeout 5 http://$IPADDRESS
<html><body><h2>Welcome to Azure! My name is my-vm.</h2></body></html>
```

Ik heb de browserpagina vernieuwd en kreeg direct toegang tot de webpagina.


## Task 8 Clean up

```bash
[ ~ ]$ az group delete \
> --name IntroAzureRG \
> --yes \
> --no-wait
```

Ik heb een Linux VM uitgerold, Nginx automatisch geinstalleerd, netwerktoegang ingericht met NSG regels en webserver succesvol vanaf het internet benaderd. Daarna heb ik de hele omgeving opgeschoond door de resource group te verwijderen.

