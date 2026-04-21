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

**Implement Azure Blob Storage**
  - Blob Storage slaat ongestructureerde data op als object/blobs in de cloud. Tekst, afbeeldingen, video, binaire bestanden.
  - 3 resources: Storage account -> Containers -> Blobs
  - Configuratie-instellingen: container options, Blob types en upload opties, access tiers, lifecycle rules, object replicatie

  - Gebruik:
    - Browser uploads, distributed access, streaming, backup/archivering, data-analyese

**Create blob containers**
  - Elke blob moet in een container zitten. Een blob kan niet zelfstandig bestaan
  - Een Container kan onbeperkte blobs bevatten, een storage account kan onbeperkt containers bevatten

  - Container naam vereisten:
    - Alleen lowercase letters, cijfers en hyphens
    - Begint met een letter of cijfer
    - Minimal 3, maximaal 63 tekens

  - Public access levels:
    - Private (standaar): Geen anonieme toegang
    - Blob: Anonieme leestoegang tot blobs alleen
    - Container: anonieme lees- en lijsttoegang tot de hele container

  - Blob en Container access levels hebben geen effect tenzij Allow Blob Anonymous Access is ingeschakeld op het storage account. Microsoft adviseert dit uitgeschakeld te laten tenzij je publieke content serveert.

**Assign blob access tiers**

| Tier | Gebruik | Storage kosten | Access kosten | Min. opslag | Latency | Availability |
|---|---|---|---|---|---|---|
| **Hot** | Frequent gelezen/geschreven data | Hoogste | Laagste | Geen | Milliseconden | 99,9% |
| **Cool** | Infrequent, min 30 dagen | Lager dan Hot | Hoger dan Hot | 30 dagen | Milliseconden | 99% |
| **Cold** | Infrequent, min 90 dagen | Lager dan Cool | Hoger dan Cool | 90 dagen | Milliseconden | 99% |
| **Archive** | Offline, zelden nodig | Laagste | Hoogste | 180 dagen | Uren | 99% |

  - Rehydratie vanuit Archive:
    - Copy Blob (aanbevolen): Maakt nieuwe blob in online tier
    - Set Blob Tier: Wijzigt tier in place
    - Standard priority: tot 15 uur
    - High priority: binnen 1 uur voor objecten onder 10 GB (hogere kosten


| Comparison | Hot | Cool | Cold | Archive |
|---|---|---|---|---|
| Availability | 99,9% | 99% | 99% | 99% |
| Availability (RA-GRS reads) | 99,99% | 99,9% | 99,9% | 99,9% |
| Latency (time to first byte) | Milliseconds | Milliseconds | Milliseconds | Hours |
| Minimum storage duration | N/A | 30 days | 90 days | 180 days |


   
**Add blob lifecycle management rules**
  - Lifecycle management stelt je in staat blobs automatisch te verplaatsen naar goedkopere tiers of te verwijderen op basis van leeftijd of toegangspatroon
  - Ondersteund voor GPv2 en Premium block blobs accoutns

  - Mogelijke acties:
    - Blob transitie naar cooler tier: Hot -> Cool -> Cold -> Archive
    - Blob verwijderen aan het einde van de lifecycle
    - Automatisch terugzetten van Cool naar Hot bij onverwachte toegang
    - Regels toepassen op hele storage account, specifieke containers, of subsets via naam prefix of blob index tags
   
  - Lifecycle policy regel structuur (If -> Then):
    - If: Conditie op basis van aantal dagen sinds laatste toegang of wijziging
    - Then: Actie: Verplaats naar Cool, Cold, Archive of verwijder
  - Voorbeeld
    - Dag 0-14: Hot
    - Dag 14-30: Cool
    - Na dag 30: Archive

  **Determine blob object replication**
  - Object replication kopieert blobs asynchroon tussen storage accounts op basis van policy rules. Inclusief blob content, metadata en versies

  - Vereisten:
    - Blok versioning moet ingeschakeld zijn op zowel source als destination account
    - Ondersteund voor Hot, Cool en Cold tier. Source en destination mogen verschillende tiers hebben
    - Blob snapshots worden niet gerepliceerd
   
  - Configuratie:
    - Replication policy: specificeert source en destination storage account
    - Policy bevat 1 of meer rules: per rule een source container en destination container

  - Voordelen:
    - Lagere latency voor read requests: Client lezen vanuit dichtstbijzijnde regio
    - Efficiente compute workloads: Zelfde blobs beschikbaar in meerdere regio's
    - Data distributie: verwerkt data op 1 locatie, repliceer alleen resultaten
    - Kosten optimalisatie: gerepliceerde data verplaatsen naar Archive tier via lifecylce management
   
  **Manage blobs**
    - 3 blob types:
      - Block blob: Standaard type, opgebouwd uit blokken data. Ideaal voor tekst, afbeeldingen, video's
      - Append blob: Vergelijkbaar met block blob maar geoptimaliseerd voor append operaties. Ideaal voor logging.
      - Page blob: Tot 8 GB, geoptimaliseerd voor frequent lezen/schrijven. Gebruikt door Azure VMs voor OS disks en data disks.

  - Na aanmaken kun je het blob type niet meer wijzigen

  - Tools voor blob beheer:
    - Azure portal: Geschikt voor kleine aantallen bestanden
    - Azure Storage Explorer: GUI tool voor upload, download, beheer van blobs, files, queues, tables en Data Lake Storage
    - AzCopy: Command-line tool voor Windows en Linux, kopieren van/naar Blob Storage en tussen storage accounts
    - Azure Data Box Disk: Fysieke SSDs van Microsoft voor grote datasets of wanneer netwerk upload niet realistisch is


**Determine Blob Storage pricing**
  - Kosten van Blob Storage worden bepaald door:
    - Volume data opgeslagen per maand
    - Aantal en type operaties + data transfer kosten
    - Gekozen redundancy opties
   
  - Kostenfactoren:
    - Performance tier: Hoe koeler de tier, hoe lager de kosten per GB opslag
    - Data access kosten: Hoe koeler de tier, hoe hoger de kosten per GB bij lezen (Cool, Cold, Archive)
    - Transaction kosten: Per transactie, neemt toe bij koelere tiers
    - Geo-replication transfer: Per GB, alleen bij accounts met geo-replicatie
    - Outbound data transfer: Per GB bandwidth
    - Tier wijzigen: Cool -> Hot kost zoveel als alle data lezen. Hot -> Cool kost zoveel als alle data schrijven (alleen GPv2)

  - Gebruik de Azure Pricing Calculator voor kostenramingen



**Exercise - Provide storage for the public website**

- [Exercise 13 Provide storage for the public website](/03-az104/exercises/13-provide-storage-for-the public-website.md)


  ---


## Learning Path 3: Implement and manage storage in Azure
### Module 3: Configure Azure Storage security

 **Review Azure Storage security strategies**
   - Securty lagen:
     - Encryption at rest: SSE met 256-bit AES, automiatisch voor alle data. VHDs versleuteld via Azure Disk Encryption (BitLocker voor Windows, dm-crypt voor Linux)
     - Encryption in transit: Secure transfer required instelling, TLS 1.0 en 1.1 uitschakelen
     - Encryption models: Server-side (service-managed keys, customer-managed keys via Key Vault, of customer-controlled hardware), of client-side encryptie
     - RBAC: Toegang tot storage resources via role assignments
     - Storage analytics: Logging voor tracing, gebruikerstrends en diagnose

  - Autorisatiestrategieen:

| Strategie | Beschrijving |
|---|---|
| Microsoft Entra ID | Aanbevolen — fine-grained access via RBAC voor blob, queue en table data |
| Shared Key | Autorisatie via account access key (primary of secondary). Uitschakelen om Entra ID te verplichten |
| Shared Access Signatures (SAS) | Tijdelijke gedelegeerde toegang tot specifieke resources met specifieke permissies |
| Anonymous access | Standaard uitgeschakeld — aanbevolen uitgeschakeld te laten voor gevoelige data |


**Create shared access signatures**
  - SAS (shared access signature) is een URI (uniform resource identifier) die tijdelijke, beperkte toegang verleent tot Azure Storage resources zonder de account key te delen

  - 3 typen SAS:
    - User delegation SAS: Beveiligd met Microsoft Entra credentials, ondersteund voor Blob Storage en Data Lake Storage
    - Account-level SAS: Toegang tot alles wat een service-level SAS kan, plus extra resources zoals file systems aanmaken
    - Service-level SAS: Toegang tot specifieke resources in een storage account

  - Stored access policy: Extra controlelaag bovenop service-level SAS, maakt het mogelijk permissies in te trekken zonder account keys te regenereren

  - Best Practices
    - Altijd HTTPS gebruiken voor aanmaken en distribueren
    - Refereer waar mogelijk naar stored access policies
    - Stel korte vervaltijden in voor ongeplande SAS
    - Clients moeten SAS ruim voor vervaldatum vernieuwen
    - Stel starttijd minimaal 15 minuten in het verleden vanwege clock skew
    - Geef minimale permissies, alleen wat nodig is
    - Valideer data geschreven via SAS voor gebruik
    - SAS is niet altijd de juiste keuze. Overweeg een middle-tier service voor complexe scenario's

   
**Identify URI and SAS parameters**
  - Een SAS URI bestaat uit de Azure Storage resource URI + een SAS token met parameters

| Parameter | Voorbeeld | Beschrijving |
|---|---|---|
| Resource URI | `https://myaccount.blob.core.windows.net/` | Azure Storage endpoint |
| Storage version | `sv=2015-04-05` | API versie die gebruikt wordt |
| Storage service | `ss=bf` | Service waarop SAS van toepassing is (b=Blob, f=Files) |
| Start time | `st=2015-04-29T22:18:26Z` | Optioneel — starttijd in UTC |
| Expiry time | `se=2015-04-30T02:23:26Z` | Vervaltijd in UTC |
| Resource | `sr=b` | Welke resource toegankelijk is |
| Permissions | `sp=rw` | Permissies (r=read, w=write) |
| IP range | `sip=168.1.5.60-168.1.5.70` | Toegestaan IP-bereik |
| Protocol | `spr=https` | Toegestane protocollen |
| Signature | `sig=...` | HMAC handtekening via SHA256, Base64 gecodeerd |


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

