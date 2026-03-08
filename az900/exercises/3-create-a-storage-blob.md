## Exercise 3. Create a storage blob

  - Learning Path: Describe Azure architecture and services
  - Module: 3. Describe Azure storage services

Doel: Een storage account aanmaken, een blob container aanmaken, een bestand uploaden, de toegang wijzigen en daarna alles opschonen.
Deze oefening voer ik twee keer uit:
  - Eerst via de Azure Portal (UI)
  - Daarna via de Azure CLI

## Task 1 Create a storage account

```bash
[ ~ ]$ az group create \
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

```bash
[ ~ ]$ az storage account create \
  --name mijnaccountname \
  --resource-group IntroAzureRG \
  --location westeurope \
  --sku Standard_LRS \
  --kind StorageV2 \
  --allow-blob-public-access true
{
  "accessTier": "Hot",
  "accountMigrationInProgress": null,
  "allowBlobPublicAccess": true,
  "allowCrossTenantReplication": false,
  "allowSharedKeyAccess": null,
  "allowedCopyScope": null,
  "azureFilesIdentityBasedAuthentication": null,
  "blobRestoreStatus": null,
  "creationTime": "2026-03-04T20:34:05.686941+00:00",
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
        "lastEnabledTime": "2026-03-04T20:34:06.015056+00:00"
      },
      "file": {
        "enabled": true,
        "keyType": "Account",
        "lastEnabledTime": "2026-03-04T20:34:06.015056+00:00"
      },
      "queue": null,
      "table": null
    }
  },
  "extendedLocation": null,
  "failoverInProgress": null,
  "geoPriorityReplicationStatus": null,
  "geoReplicationStats": null,
  "id": "/subscriptions/<subscription-id>/resourceGroups/IntroAzureRG/providers/Microsoft.Storage/storageAccounts/mijnaccountname",
  "identity": null,
  "immutableStorageWithVersioning": null,
  "isHnsEnabled": null,
  "isLocalUserEnabled": null,
  "isSftpEnabled": null,
  "isSkuConversionBlocked": null,
  "keyCreationTime": {
    "key1": "2026-03-04T20:34:05.999430+00:00",
    "key2": "2026-03-04T20:34:05.999430+00:00"
  },
  "keyPolicy": null,
  "kind": "StorageV2",
  "largeFileSharesState": null,
  "lastGeoFailoverTime": null,
  "location": "westeurope",
  "minimumTlsVersion": "TLS1_0",
  "name": "mijnaccountname",
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
    "blob": "https://mijnaccountname.blob.core.windows.net/",
    "dfs": "https://mijnaccountname.dfs.core.windows.net/",
    "file": "https://mijnaccountname.file.core.windows.net/",
    "internetEndpoints": null,
    "ipv6Endpoints": null,
    "microsoftEndpoints": null,
    "queue": "https://mijnaccountname.queue.core.windows.net/",
    "table": "https://mijnaccountname.table.core.windows.net/",
    "web": "https://mijnaccountname.z6.web.core.windows.net/"
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

## Task 2 Create a blob container

```bash
az storage container create \
  --name mycontainer \
  --account-name mijnaccountname \
  --public-access off \
  --auth-mode login
{
  "created": true
}
```

## Task 3 Upload a file

```bash
echo "Hello from Azure Blob Storage" > testfile.txt
```

```bash
[ ~ ]$ az storage blob upload \
  --account-name mijnaccountname \
  --container-name mycontainer \
  --name testfile.txt \
  --file testfile.txt \
  --auth-mode login

You do not have the required permissions needed to perform this operation.
Depending on your operation, you may need to be assigned one of the following roles:
    "Storage Blob Data Owner"
    "Storage Blob Data Contributor"
    "Storage Blob Data Reader"
    "Storage Queue Data Contributor"
    "Storage Queue Data Reader"
    "Storage Table Data Contributor"
    "Storage Table Data Reader"

If you want to use the old authentication method and allow querying for the right account key, please use the "--auth-mode" parameter and "key" value.
```

In plaats van Entra ID rol voor authenticatie ga ik nu de storage account key gebruiken

```bash
[ ~ ]$ az storage blob upload \
  --account-name mijnaccountname \
  --container-name mycontainer \
  --name testfile.txt \
  --file testfile.txt \
  --auth-mode key
Finished[#############################################################]  100.0000%
{
  "client_request_id": "f455d0e8-180a-11f1-a77d-00155d6612fb",
  "content_md5": "5o+7WI49/Eda+aWnj8y1kA==",
  "date": "2026-03-04T20:44:35+00:00",
  "encryption_key_sha256": null,
  "encryption_scope": null,
  "etag": "\"0x8DE7A2ED88D11CD\"",
  "lastModified": "2026-03-04T20:44:35+00:00",
  "request_id": "a57d5276-001e-0075-7117-ac5a25000000",
  "request_server_encrypted": true,
  "structured_body": null,
  "version": "2026-02-06",
  "version_id": null
}
```

Get the URL:

```bash
[ ~ ]$ az storage blob url \
  --account-name mijnaccountname \
  --container-name mycontainer \
  --name testfile.txt \
  --auth-mode key
"https://mijnaccountname.blob.core.windows.net/mycontainer/testfile.txt"
```

De URL openen in de browser geeft een foutmelding omdat de container privé is:
ResourceNotFound - The specified resource does not exist.

## Task 4 Change the access level

```bash
az storage container set-permission \
  --name mycontainer \
  --account-name mijnaccountname \
  --public-access blob \
  --auth-mode key
{
  "client_request_id": "5b99fbc6-180b-11f1-9666-00155d6612fb",
  "date": "2026-03-04T20:47:28+00:00",
  "etag": "\"0x8DE7A2F3FCE8CDA\"",
  "last_modified": "2026-03-04T20:47:28+00:00",
  "request_id": "c4dfed44-401e-0029-3a18-ac0f7d000000",
  "version": "2026-02-06"
}
```

Na het wijzigen is de blob publiek bereikbaar. De inhoud is zichtbaar in de browser:
Hello from Azure Blob Storage

## Task 5 Verify blob list

```bash
az storage blob list \
  --account-name mijnaccountname \
  --container-name mycontainer \
  --output table \
  --auth-mode key

Name          Blob Type    Blob Tier    Length    Content Type    Last Modified              Snapshot
------------  -----------  -----------  --------  --------------  -------------------------  ----------
testfile.txt  BlockBlob    Hot          30        text/plain      2026-03-04T20:44:35+00:00
```

## Task 6 Clean up

```bash
az group delete \
  --name IntroAzureRG \
  --yes \
  --no-wait
```
