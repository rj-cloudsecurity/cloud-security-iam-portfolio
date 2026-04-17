# Exercise 1. Create and deploy an Azure Resource Manager template

- Learning path 1.: AZ-104: Prerequisites for Azure administrators
- Module: 1. Deploy Azure infrastructure by using JSON ARM templates

In deze oefening maak ik een ARM template aan in VSCode, deploy ik deze naar Azure, en voeg ik een storage account toe als resource. Uitgevoerd met zowel **Azure PowerShell** (VSCode terminal) als **Azure CLI** (Konsole, KDE Neon Linux).

---

## Uitvoering 1 — Azure PowerShell (VSCode terminal)

### Task 1 Resource Group aanmaken

```powershell
New-AzResourceGroup -Name exercise1 -Location westeurope
```

### Task 2 Blank ARM template aanmaken en deployen

`azuredeploy.json` aangemaakt in VSCode met alle verplichte secties maar zonder resources.

```powershell
$templateFile="azuredeploy.json"
$today=Get-Date -Format "MM-dd-yyyy"
$deploymentName="blanktemplate-"+"$today"
New-AzResourceGroupDeployment -Name $deploymentName -ResourceGroupName exercise1 -TemplateFile $templateFile
```

```
DeploymentName          : blanktemplate-04-14-2026
ResourceGroupName       : exercise1
ProvisioningState       : Succeeded
Timestamp               : 4/14/2026 7:37:32 PM
Mode                    : Incremental
```

In de Azure portal gecontroleerd onder **Resource groups > exercise1 > Deployments**: 1 Succeeded.

### Task 3 Storage account toevoegen aan de ARM template

`azuredeploy.json` bijgewerkt met een `Microsoft.Storage/storageAccounts` resource met een globally unique naam.

```powershell
$templateFile="azuredeploy.json"
$today=Get-Date -Format "MM-dd-yyyy"
$deploymentName="addstorage-"+"$today"
New-AzResourceGroupDeployment -Name $deploymentName -ResourceGroupName exercise1 -TemplateFile $templateFile
```

```
DeploymentName          : addstorage-04-14-2026
ResourceGroupName       : exercise1
ProvisioningState       : Succeeded
Timestamp               : 4/14/2026 7:43:15 PM
Mode                    : Incremental
```

In de Azure portal gecontroleerd: 2 Succeeded deployments zichtbaar. Storage account succesvol aangemaakt.

### Task 4 Clean up

```powershell
Remove-AzResourceGroup -Name exercise1 -Force -AsJob
```

---

## Uitvoering 2 — Azure CLI (Konsole, KDE Neon Linux)

Voor deze uitvoering heb ik de blank template stap overgeslagen en direct de storage account template gedeployed. De `azuredeploy.json` bevatte al de `Microsoft.Storage/storageAccounts` resource.

### Task 1 Inloggen en Resource Group aanmaken

```bash
az login
az group create --name exercise1 --location westeurope
az configure --defaults group=exercise1
```

```json
{
  "id": "/subscriptions/69799361-14fa-4e9b-8b7f-e48e93f9e422/resourceGroups/exercise1",
  "location": "westeurope",
  "name": "exercise1",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "type": "Microsoft.Resources/resourceGroups"
}
```

### Task 2 ARM template deployen met storage account

Eerste poging mislukt: `date+"%d-%b-%Y"` zonder spatie geeft een fout (`date+%d-%b-%Y: command not found`), en het pad naar `azuredeploy.json` was niet gevonden omdat ik nog niet in de juiste map stond.

Oplossing: eerst naar de juiste map navigeren, en spatie toevoegen in het `date` commando.

```bash
cd "/mnt/data/RJ/All My Files/Documents/Studies/IT/Identity & Access Management IAM & Cloud Security/Learn Exercises/az-104/exercise-1/"
templateFile="azuredeploy.json"
today=$(date +"%d-%b-%Y")
DeploymentName="blanktemplate-"$today
az deployment group create --name $DeploymentName --template-file $templateFile
```

```json
{
  "name": "blanktemplate-15-apr-2026",
  "properties": {
    "duration": "PT23.7499549S",
    "mode": "Incremental",
    "outputResources": [
      {
        "id": "/subscriptions/69799361-14fa-4e9b-8b7f-e48e93f9e422/resourceGroups/exercise1/providers/Microsoft.Storage/storageAccounts/rjstorageaccount1",
        "resourceType": "Microsoft.Storage/storageAccounts"
      }
    ],
    "provisioningState": "Succeeded",
    "timestamp": "2026-04-15T08:51:48.757683+00:00"
  },
  "resourceGroup": "exercise1"
}
```

Storage account `rjstorageaccount1` succesvol aangemaakt in `westeurope`.

### Task 3 Clean up

```bash
az group delete --name exercise1 --yes --no-wait
```

---
