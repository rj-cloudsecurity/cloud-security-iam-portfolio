# Create a Microsoft Azure Virtual Machine

- Learning path: Introduction to Cloud Infrastructure: Azure architecture & services
- Module: 2. Describe Azure Virtual Machine and Configure network access

In deze oefening maak ik een Azure VM aan. Installeer een web server (Nginx) en update de configuratie van het netwerk zodat deze toegang heeft vanaf het internet. Tot slot controleer ik de NSG regels en test ik de webserver.

I'm using the CLI and this time using az interactive

## Task 1 Resource Group, create, name, location

```bash
az interactive
```

```bash
az>> az group create --name IntroAzureRG --location centralus
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
az>> 
```




