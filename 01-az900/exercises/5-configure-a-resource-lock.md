## Exercise 5. Configure resource locks

  - Learning Path: Describe Azure management and governance 
  - Module: 2. Describe features and tools in Azure for governance and compliance

---

Doel: Een resource lock aanmaken, het effect ervan testen en de lock verwijderen.

Deze oefening voer ik drie keer uit:
- Eerst via de Azure Portal (UI)
- Daarna via de Azure CLI (Bash)
- Tot slot via PowerShell

Hoewel de originele opdracht alleen via de Azure Portal wordt uitgevoerd, heb ik ervoor gekozen om de oefening ook via de Azure CLI (Bash) en PowerShell uit te voeren om extra ervaring op te doen met beide omgevingen.

---

## Via de Azure Portal (UI)

## Task 1: Create a resource group

Resource group IntroAzureRG aangemaakt in region West Europe via de Azure Portal.

## Task 2: Create a storage account

Storage account aangemaakt in resource group IntroAzureRG met de volgende instellingen:
    - tempstoragerj123
    - Performance: Standard
    - Redundancy: Locally redundant storage (LRS)

## Task 3: Apply a read-only resource lock
Read-only lock toegevoegd aan het storage account via Settings, Locks, +Add.

## Task 4: Try to add a container (blocked by lock)
Geprobeerd een container aan te maken via Data storage, Container, + Container.
Foutmelding ontvangen:
Failed to create storage container.
De read-only lock voorkomt alle create en update operaties op het storage account.

## Task 5: Change lock type to Delete and create container
Lock type gewijzigd van Read-only naar Delete via Settings, Locks.
Daarna container succesvol aangemaakt, de container verschijnt in de lijst.

## Task 6: Try to delete the storage account (blocked by lock)
Geprobeerd het storage account te verwijderen via Overview, Delete.
Foutmelding ontvangen:
Cannot delete resource because it has a delete lock.

## Task 7: Remove the delete lock and delete the storage account
Delete lock verwijderd via Settings, Locks, Delete.
Daarna storage account verwijderd, Azure vraagt om de naam te bevestigen ter verificatie.

## Task 8: Clean up
Resource group IntroAzureRG verwijderd via Resource groups, Delete resource group.

---

## Via de Azure CLI (Bash)

## Task 1: Create a resource group
```bash
az group create \
> --name IntroAzureRG \
> --location westeurope
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
  
## Task 2: Create a storage account
```bash
[ ~ ]$ az storage account create \
> --name tempstoragerj123 \
> --resource-group IntroAzureRG \
> --location westeurope \
> --sku Standard_LRS \
> --kind Storagev2
{
  "accessTier": "Hot",
  "accountMigrationInProgress": null,
  "allowBlobPublicAccess": false,
  "allowCrossTenantReplication": false,
  "allowSharedKeyAccess": null,
  "allowedCopyScope": null,
  "azureFilesIdentityBasedAuthentication": null,
  "blobRestoreStatus": null,
  "creationTime": "2026-03-08T19:34:30.113909+00:00",
  "customDomain": null,
  "defaultToOAuthAuthentication": null,
  "dnsEndpointType": null,
  "dualStackEndpointPreference": null,
  "enableExtendedGroups": null,
  "enableHttpsTrafficOnly": true,
  "enableNfsV3": null,
  "encryption": {
    "encryptionIdentity": null,
    "keySource": "Microsoft.Storage",
    "keyVaultProperties": null,
    "requireInfrastructureEncryption": null,
    "services": {
      "blob": {
        "enabled": true,
        "keyType": "Account",
        "lastEnabledTime": "2026-03-08T19:34:30.504538+00:00"
      },
      "file": {
        "enabled": true,
        "keyType": "Account",
        "lastEnabledTime": "2026-03-08T19:34:30.504538+00:00"
      },
      "queue": null,
      "table": null
    }
  },
  "extendedLocation": null,
  "failoverInProgress": null,
  "geoPriorityReplicationStatus": null,
  "geoReplicationStats": null,
  "id": "/subscriptions/<subscription-id>/resourceGroups/IntroAzureRG/providers/Microsoft.Storage/storageAccounts/tempstoragerj123",
  "identity": null,
  "immutableStorageWithVersioning": null,
  "isHnsEnabled": null,
  "isLocalUserEnabled": null,
  "isSftpEnabled": null,
  "isSkuConversionBlocked": null,
  "keyCreationTime": {
    "key1": "2026-03-08T19:34:30.504538+00:00",
    "key2": "2026-03-08T19:34:30.504538+00:00"
  },
  "keyPolicy": null,
  "kind": "StorageV2",
  "largeFileSharesState": null,
  "lastGeoFailoverTime": null,
  "location": "westeurope",
  "minimumTlsVersion": "TLS1_0",
  "name": "tempstoragerj123",
  "networkRuleSet": {
    "bypass": "AzureServices",
    "defaultAction": "Allow",
    "ipRules": [],
    "ipv6Rules": [],
    "resourceAccessRules": null,
    "virtualNetworkRules": []
  },
  "placement": null,
  "primaryEndpoints": {
    "blob": "https://tempstoragerj123.blob.core.windows.net/",
    "dfs": "https://tempstoragerj123.dfs.core.windows.net/",
    "file": "https://tempstoragerj123.file.core.windows.net/",
    "internetEndpoints": null,
    "ipv6Endpoints": null,
    "microsoftEndpoints": null,
    "queue": "https://tempstoragerj123.queue.core.windows.net/",
    "table": "https://tempstoragerj123.table.core.windows.net/",
    "web": "https://tempstoragerj123.z6.web.core.windows.net/"
  },
  "primaryLocation": "westeurope",
  "privateEndpointConnections": [],
  "provisioningState": "Succeeded",
  "publicNetworkAccess": null,
  "resourceGroup": "IntroAzureRG",
  "routingPreference": null,
  "sasPolicy": null,
  "secondaryEndpoints": null,
  "secondaryLocation": null,
  "sku": {
    "name": "Standard_LRS",
    "tier": "Standard"
  },
  "statusOfPrimary": "available",
  "statusOfSecondary": null,
  "storageAccountSkuConversionStatus": null,
  "tags": {},
  "type": "Microsoft.Storage/storageAccounts",
  "zones": null
}
  ```

## Task 3: Apply a read-only resource lock
```bash
az lock create \
  --name ReadOnlyLock \
  --resource-group IntroAzureRG \
  --resource-name tempstoragerj123 \
  --resource-type Microsoft.Storage/storageAccounts \
  --lock-type ReadOnly
{
  "id": "/subscriptions/6<subscription-id>/resourcegroups/IntroAzureRG/providers/Microsoft.Storage/storageAccounts/tempstoragerj123/providers/Microsoft.Authorization/locks/ReadOnlyLock",
  "level": "ReadOnly",
  "name": "ReadOnlyLock",
  "notes": null,
  "owners": null,
  "resourceGroup": "IntroAzureRG",
  "type": "Microsoft.Authorization/locks"
}
```
  
## Task 4: Try to add a container (blocked by lock)
```bash
az storage container create \
> --name mycontainer \
> --account-name tempstoragerj123 \
> --auth-mode key

There are no credentials provided in your command and environment, we will query for account key for your storage account.
It is recommended to provide --connection-string, --account-key or --sas-token in your command as credentials.

You also can add `--auth-mode login` in your command to use Azure Active Directory (Azure AD) for authorization if your login account is assigned required RBAC roles.
For more information about RBAC roles in storage, visit https://learn.microsoft.com/azure/storage/common/storage-auth-aad-rbac-cli.

In addition, setting the corresponding environment variables can avoid inputting credentials in your command. Please use --help to get more information about environment variable usage.

Skip querying account key due to failure: (ScopeLocked) The scope '/subscriptions/<subscription-id>/resourceGroups/IntroAzureRG/providers/Microsoft.Storage/storageAccounts/tempstoragerj123' cannot perform write operation because following scope(s) are locked: '/subscriptions/<subscription-id>/resourcegroups/IntroAzureRG/providers/Microsoft.Storage/storageAccounts/tempstoragerj123'. Please remove the lock and try again.
Code: ScopeLocked
Message: The scope '/subscriptions/<subscription-id>/resourceGroups/IntroAzureRG/providers/Microsoft.Storage/storageAccounts/tempstoragerj123' cannot perform write operation because following scope(s) are locked: '/subscriptions/<subscription-id>/resourcegroups/IntroAzureRG/providers/Microsoft.Storage/storageAccounts/tempstoragerj123'. Please remove the lock and try again.
Server failed to authenticate the request. Please refer to the information in the www-authenticate header.
RequestId:cd4c80b5-001e-0007-7633-af1b56000000
Time:2026-03-08T19:43:06.2865794Z
ErrorCode:NoAuthenticationInformation
```

Foutmelding ontvangen:
The scope is locked for 'ReadOnly' by lock 'ReadOnlyLock'.
De read-only lock voorkomt alle create en update operaties.

## Task 5: Change lock type to Delete and create container
Lock type wijzigen naar Delete:
```bash
az lock update \
> --name ReadOnlyLock \
> --resource-group IntroAzureRG \
> --resource-name tempstoragerj123 \
> --resource-type Microsoft.Storage/storageAccounts \
> --lock-type CanNotDelete
{
  "id": "/subscriptions/<subscription-id>/resourcegroups/IntroAzureRG/providers/Microsoft.Storage/storageAccounts/tempstoragerj123/providers/Microsoft.Authorization/locks/ReadOnlyLock",
  "level": "CanNotDelete",
  "name": "ReadOnlyLock",
  "notes": null,
  "owners": null,
  "resourceGroup": "IntroAzureRG",
  "type": "Microsoft.Authorization/locks"
}
```

Container aanmaken:
```bash
az storage container create \                                             --name mycontainer \
  --account-name tempstoragerj123 \
  --auth-mode key

There are no credentials provided in your command and environment, we will query for account key for your storage account.
It is recommended to provide --connection-string, --account-key or --sas-token in your command as credentials.

You also can add `--auth-mode login` in your command to use Azure Active Directory (Azure AD) for authorization if your login account is assigned required RBAC roles.
For more information about RBAC roles in storage, visit https://learn.microsoft.com/azure/storage/common/storage-auth-aad-rbac-cli.

In addition, setting the corresponding environment variables can avoid inputting credentials in your command. Please use --help to get more information about environment variable usage.
{
  "created": true
}
```
  
## Task 6: Try to delete the storage account (blocked by lock)
```bash
az storage account delete \
  --name tempstoragerj123 \
  --resource-group IntroAzureRG
Are you sure you want to perform this operation? (y/n): y
(ScopeLocked) The scope '/subscriptions/<subscription-id>/resourceGroups/IntroAzureRG/providers/Microsoft.Storage/storageAccounts/tempstoragerj123' cannot perform delete operation because following scope(s) are locked: '/subscriptions/<subscription-id>/resourcegroups/IntroAzureRG/providers/Microsoft.Storage/storageAccounts/tempstoragerj123'. Please remove the lock and try again.
Code: ScopeLocked
Message: The scope '/subscriptions/<subscription-id>/resourceGroups/IntroAzureRG/providers/Microsoft.Storage/storageAccounts/tempstoragerj123' cannot perform delete operation because following scope(s) are locked: '/subscriptions/<subscription-id>/resourcegroups/IntroAzureRG/providers/Microsoft.Storage/storageAccounts/tempstoragerj123'. Please remove the lock and try again.
```

Foutmelding ontvangen:
The scope is locked for 'CanNotDelete' by lock 'ReadOnlyLock'.

## Task 7: Remove the delete lock and delete the storage account
Lock verwijderen:
```bash
az lock delete \
  --name ReadOnlyLock \
  --resource-group IntroAzureRG \
  --resource-name tempstoragerj123 \
  --resource-type Microsoft.Storage/storageAccounts
  ```

Storage account verwijderen:
```bash
az storage account delete \
  --name tempstoragerj123 \
  --resource-group IntroAzureRG \
  --yes
  ```

## Task 8: Clean up
```bash
az group delete \
  --name IntroAzureRG \
  --yes \
  --no-wait
```

---

## Via PowerShell

## Task 1: Create a resource group
```powershell 
New-AzResourceGroup `                                      
>>   -Name IntroAzureRG `
>>   -Location westeurope

ResourceGroupName : IntroAzureRG
Location          : westeurope
ProvisioningState : Succeeded
Tags              : 
ResourceId        : /subscriptions/<subscription-id>/resourceGroups/Int
                    roAzureRG

```

## Task 2: Create a storage account
```powershell
New-AzStorageAccount `                                                
>>   -ResourceGroupName IntroAzureRG `                                            
>>   -Name tempstoragerj123 `
>>   -Location westeurope `
>>   -SkuName Standard_LRS `
>>   -Kind StorageV2

StorageAccountName ResourceGroupName PrimaryLocation SkuName      Kind      AccessTier Cre
                                                                                       ati
                                                                                       onT
                                                                                       ime
------------------ ----------------- --------------- -------      ----      ---------- ---
tempstoragerj123   IntroAzureRG      westeurope      Standard_LRS StorageV2 Hot        3/…

  ```

## Task 3: Apply a read-only resource lock
```powershell
New-AzResourceLock `                                       
>>   -LockName ReadOnlyLock `
>>   -LockLevel ReadOnly `
>>   -ResourceGroupName IntroAzureRG `
>>   -ResourceName tempstoragerj123 `
>>   -ResourceType Microsoft.Storage/storageAccounts `
>>   -Force
                                                                                           
Name                  : ReadOnlyLock
ResourceId            : /subscriptions/69799361-14fa-4e9b-8b7f-e48e93f9e422/resourceGroups
                        /IntroAzureRG/providers/Microsoft.Storage/storageAccounts/tempstor
                        agerj123/providers/Microsoft.Authorization/locks/ReadOnlyLock
ResourceName          : tempstoragerj123
ResourceType          : Microsoft.Storage/storageAccounts
ExtensionResourceName : ReadOnlyLock
ExtensionResourceType : Microsoft.Authorization/locks
ResourceGroupName     : IntroAzureRG
SubscriptionId        : 69799361-14fa-4e9b-8b7f-e48e93f9e422
Properties            : @{level=ReadOnly}
LockId                : /subscriptions/69799361-14fa-4e9b-8b7f-e48e93f9e422/resourceGroups
                        /IntroAzureRG/providers/Microsoft.Storage/storageAccounts/tempstor
                        agerj123/providers/Microsoft.Authorization/locks/ReadOnlyLock

```

## Task 4: Try to add a container (blocked by lock)
```powershell
$ctx = (Get-AzStorageAccount `
  -ResourceGroupName IntroAzureRG `
  -Name tempstoragerj123).Context

New-AzStorageContainer `
  -Name mycontainer `
  -Context $ctx
```

Foutmelding ontvangen:
```powershell
New-AzStorageContainer: Operation returned an invalid status code 'Conflict'
```
De read-only lock blokkeert alle write operaties op het storage account.

## Task 5: Change lock type to Delete and create container
Lock type wijzigen naar Delete:
```powershell
et-AzResourceLock `                      
>>   -LockName ReadOnlyLock `
>>   -LockLevel CanNotDelete `
>>   -ResourceGroupName IntroAzureRG `
>>   -ResourceName tempstoragerj123 `
>>   -ResourceType Microsoft.Storage/storageAccounts `
>>   -Force
                                                                                           
Name                  : ReadOnlyLock
ResourceId            : /subscriptions/<subscription-id>/resourceGroups
                        /IntroAzureRG/providers/Microsoft.Storage/storageAccounts/tempstor
                        agerj123/providers/Microsoft.Authorization/locks/ReadOnlyLock
ResourceName          : tempstoragerj123
ResourceType          : Microsoft.Storage/storageAccounts
ExtensionResourceName : ReadOnlyLock
ExtensionResourceType : Microsoft.Authorization/locks
ResourceGroupName     : IntroAzureRG
SubscriptionId        : <subscription-id>
Properties            : @{level=CanNotDelete}
LockId                : /subscriptions/<subscription-id>/resourceGroups
                        /IntroAzureRG/providers/Microsoft.Storage/storageAccounts/tempstor
                        agerj123/providers/Microsoft.Authorization/locks/ReadOnlyLock
```

Container aanmaken:
```powershell
New-AzStorageContainer `                                              
>>   -Name mycontainer `                                                              
>>   -Context $ctx
                                                                                           
   Storage Account Name: tempstoragerj123

Name                 PublicAccess         LastModified                   IsDeleted  Versio
                                                                                    nId
----                 ------------         ------------                   ---------  ------
mycontainer          Off                  3/8/2026 8:13:09 PM +00:00                

```

## Task 6: Try to delete the storage account (blocked by lock)
```powershell
Remove-AzStorageAccount `                                         
>>   -ResourceGroupName IntroAzureRG `
>>   -Name tempstoragerj123 `
>>   -Force
Remove-AzStorageAccount: Operation returned an invalid status code 'Conflict'
```

Foutmelding ontvangen:
The scope is locked for 'CanNotDelete' by lock 'ReadOnlyLock'.

## Task 7: Remove the delete lock and delete the storage account
Lock verwijderen:
```powershell
Remove-AzResourceLock `                                               
>>   -LockName ReadOnlyLock `
>>   -ResourceGroupName IntroAzureRG `
>>   -ResourceName tempstoragerj123 `
>>   -ResourceType Microsoft.Storage/storageAccounts `
>>   -Force
True       
```

Storage account verwijderen:
```powershell
Remove-AzStorageAccount `
  -ResourceGroupName IntroAzureRG `
  -Name tempstoragerj123 `
  -Force
```

## Task 8: Clean up
```powershell
Remove-AzResourceGroup `
  -Name IntroAzureRG `
  -Force
```
