# AZ-104: Azure Administrator Associate
## Learning Path 3: Implement and manage storage in Azure

  - **AZ-104 Started:** 11-4-2026
  - **AZ-104 Exam passed:** 

  ---
  
## Inhoudsopgave

### Learning Path 3: Implement and manage storage in Azure

- [Module 1: Configure storage accounts ](#module-1-Configure-storage-accounts)

   ---

## Learning Path 3: Implement and manage storage in Azure
### Module 1: Configure storage accounts 

**Implement Azure Storage**
  - Azure Storage ondersteunt 3 categorieen data:
    - Virtual machine data: Disks en files via Azure managed disks
    - Unstructured data: Blob Storage en Data Lake Storage
    - Structured data: Table Storage, Cosmos DB, Azure SQL Database
  - Kenmerken: Duurzaan, veilig, massaal schaalbaar, wereldwijd toegankelijk via HTTP/HTTPS
  - Ondersteunt SFTP (vereist hierarchical namespace), NFSv3, en Microsoft Entra autorisatie als standaard


**Explore Azure Storage services**
  - Blob (Binary Large Object) Storage: Object storage voor ongestructeerde data (tekst, Binair). Ideaal voor: Afbeeldingen/documenten naar browsers serveren, streaming video/aduio, backup en archivering. Toegankeljk via HTTP/HTTPS, REST API, PowerShell, CLI of client libraries
  - Azure Files: Highly available network file shares via SMB of NFS protocol. Meerdere VMs kunnen dezelfde bestanden lezen en schrijven. Geschikt voor migratie van on-premises apps die file shares gebruiken.
  - Queue Storage: Berichten opslaan voor asynchrone verwerking. Max 64 KB per bericht, een queue kan miljoenen berichten bevatten.
  - Table Storage: Schemaless NoSQL key/attribute store voor gestructureerde, niet-relationele data. Goedkoper dan traditionele SQL voor vergelijkbare datavolumes. Maakt deel uit van Azure Cosmos DB


**Determine storage account types**
  - Standard: Backed by HDD, laagste kosten per GB, geschikt voor bulk storage of infrequent access
  - Premium: Backed by SSD, consistent lage latency, geschikt voor I/O intensieve workloads zoals databases

  - Conversie tussen Standard en Premium is niet mogelijk. Je moet een nieuw account aanmaken en data kopieren. Alle storage accounts zijn versleuteld via Storage Service Engryption (SSE)

| Account type | Ondersteunde services | Redundancy | Gebruik |
|---|---|---|---|
| Standard general-purpose v2 | Blob, Queue, Table, Azure Files | LRS, GRS, RA-GRS, ZRS, GZRS, RA-GZRS | Standaard voor de meeste scenario's |
| Premium block blobs | Blob (incl. Data Lake Storage) | LRS, ZRS | Hoge transactiesnelheid, kleine objecten, lage latency |
| Premium file shares | Azure Files | LRS, ZRS | Enterprise file shares, SMB én NFS ondersteuning |
| Premium page blobs | Page blobs only | LRS only | OS disks, VM data disks, databases |

  - Legacy account types GPv1, BlobStorage) worden niet meer aanbevolen. Upgrade naar General-purpose v2 via portal, CLI of PowerShell
      

**Determine replication strategies**

| Strategie | Beschrijving | Durability | Lezen tijdens regio-uitval |
|---|---|---|---|
| **LRS** (Locally Redundant Storage) | 3 kopieën binnen 1 datacenter | Laagste | Nee |
| **ZRS** (Zone Redundant Storage) | 3 kopieën over 3 availability zones binnen 1 regio | Hoog | Nee |
| **GRS** (Geo Redundant Storage) | LRS + async replicatie naar secundaire regio | 16 negens | Nee (alleen bij failover door Microsoft) |
| **RA-GRS** (Read-Access GRS) | GRS + leestoegang tot secundaire regio altijd beschikbaar | 16 negens | Ja |
| **GZRS** (Geo Zone Redundant Storage) | ZRS + replicatie naar secundaire regio | 16 negens | Nee |
| **RA-GZRS** (Read-Access GZRS) | GZRS + leestoegang tot secundaire regio | 16 negens | Ja |

| Scenario | Minimale strategie |
|---|---|
| Node in datacenter unavailable | LRS |
| Heel datacenter unavailable | ZRS |
| Regio-uitval | GRS |
| Lezen tijdens regio-uitval | RA-GRS of RA-GZRS |

  - Microsoft adviseert GZRS voor productie workloads die hoge beschikbaarheid én disaster recovery vereisen.

  
**Access storage**
  - Elk object in Azure Storage heeft een unieke URL: `//<storage-account-name>.<service>.core.windows.net/<container>/<object>`
  - Standaard endpoints per service:

| Service | Endpoint |
|---|---|
| Blob | `//mystorageaccount.blob.core.windows.net` |
| Table | `//mystorageaccount.table.core.windows.net` |
| Queue | `//mystorageaccount.queue.core.windows.net` |
| File | `//mystorageaccount.file.core.windows.net` |


  - Custom Domain:
    - Je kunt een custom domain koppelen aan je blob endpoint via een CNAME record in DNS
    - Voorbeeld `blobs.contoso.com` - `contosoblobs.blob.core.windows.net`


**Secure storage endpoints**
  - Configureer via Firewalls and virtual networks in de Azure portal
  - Service endpoints: publiek endpoint blijft actief, toegang beperkt to specifieke VNets
  - Private endpoints: private IP uit VNET, verkeer via Microsoft backbone; aanbevolen voor productie


---

## Learning Path 3: Implement and manage storage in Azure
### Module 2: Configure Azure Blob Storage

  - 
  -  
  -  
  -  
  -  
  -  
  -  
  -  
  -  
  -  
  -  


  ---


## Learning Path 3: Implement and manage storage in Azure
### Module 3: Configure Azure Storage security

  - 
  -  
  -  
  -  
  -  
  -  
  -  
  -  
  -  
  -  
  -  



  ---



## Learning Path 3: Implement and manage storage in Azure
### Module 4: Configure Azure Files 


  - 
  -  
  -  
  -  
  -  
  -  
  -  
  -  
  -  
  -  
  -  

