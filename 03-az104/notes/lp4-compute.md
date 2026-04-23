# AZ-104: Azure Administrator Associate
## Learning Path 4: Deploy and manage Azure compute resources

  - **AZ-104 Started:** 11-4-2026
  - **AZ-104 Exam passed:**

---

## Inhoudsopgave

### Learning Path 4: Deploy and manage Azure compute resources

- [Module 1: Introduction to Azure virtual machines](#module-1-introduction-to-azure-virtual-machines)

---

## Learning Path 4: Deploy and manage Azure compute resources
### Module 1: Introduction to Azure virtual machines


**Compile a checklist for creating an Azure Virtual Machine**
  - Bij het aanmaken van een VM moet je rekening houden met 6 onderdelen:
    - Network: VNet, subnest, IP-ranges (niet-overlappend), NSGs voor traffic controle
    - VM naam: Max 64 tekens (Linux) of 15 tekens (Windows), gebruik een naamconvente
    - Locatie: Dichtstbijzijnde regio voor gebruikers, let op prijsverschillende en beschikbare hardware
    - VM grootte: Kies op basis van workload type
    - Disks: OS disk + data disk (aparte aanbevolen
    - Operating system
   
  - VM naamconventie elementen:
    
| Element | Voorbeeld | Beschrijving |
|---|---|---|
| Environment | dev, prod, QA | Identificeert de omgeving |
| Location | eus, jw | Identificeert de regio |
| Instance | 01, 02 | Voor meerdere instanties |
| Product/Service | service | Identificeert de applicatie |
| Role | sql, web, messaging | Identificeert de rol |

  - VM grootte opties:
    
| Optie | Gebruik |
|---|---|
| General purpose | Balanced CPU/memory — dev/test, kleine databases, web servers |
| Compute optimized | Hoge CPU/memory ratio — web servers, batch processen |
| Memory optimized | Hoge memory/CPU ratio — databases, caches, in-memory analytics |
| Storage optimized | Hoge disk throughput — databases |
| GPU | Graphics rendering, video editing, deep learning |
| High performance compute | Snelste CPU, optioneel high-throughput netwerk |

  - Kostenmodel:
    
| Resource | Kosten |
|---|---|
| Virtual network | Ja |
| NIC | Geen aparte kosten |
| IP adres | Ja |
| NSG | Geen aparte kosten |
| OS disk | Ja (standaard ~127 GiB) |
| Local disk | Geen kosten |
| OS licentie | Varieert (Linux goedkoper dan Windows) |

  - Compute kosten: Per minuut gefactureerd, gestopt + gedealloceerde VM kost geen compute
  - Storage kosten: Aparte gefactuurd van compute
  - Azure Hybrid Benefit: Bestaande licenties hergebruiken voor korting

  - Betaalopties compute:

| Optie | Beschrijving |
|---|---|
| Pay as you go | Per seconde, geen commitment, flexibel — geschikt voor korte of onvoorspelbare workloads |
| Reserved VM Instances (RI) | 1 of 3 jaar vooraf betalen — tot 72% goedkoper dan pay-as-you-go, geschikt voor continue workloads |

  - Disk types:

| | Ultra disk | Premium SSD v2 | Premium SSD | Standard SSD | Standard HDD |
|---|---|---|---|---|---|
| Type | SSD | SSD | SSD | SSD | HDD |
| Scenario | IO-intensief (SAP HANA, SQL, Oracle) | Productie, lage latency, hoge IOPS | Productie, performance-gevoelig | Web servers, dev/test | Backup, niet-kritiek |
| Max disk size | 65.536 GiB | 65.536 GiB | 32.767 GiB | 32.767 GiB | 32.767 GiB |
| Max throughput | 4.000 MB/s | 1.200 MB/s | 900 MB/s | 750 MB/s | 500 MB/s |
| Max IOPS | 160.000 | 80.000 | 20.000 | 6.000 | 2.000 |
| OS disk | Nee | Nee | Ja | Ja | Ja |


- [Exercise 15 Create a VM using the Azure portal](/03-az104/exercises/15-create-a-vm-using-the-azure-portal.md)


**Describe the options available to create and manage an Azure Virtual Machine**
  - 7 manieren om VMs aan te maken en te beheren:

| Methode | Beschrijving |
|---|---|
| ARM templates | JSON-bestanden voor reproduceerbare deployments — exporteer vanuit bestaande VM via Automation > Export template |
| Azure CLI | Cross-platform command-line tool — `az vm create` |
| Azure PowerShell | PowerShell cmdlets — `New-AzVM` |
| Terraform | Infrastructure as Code via HCL syntax — Azure Terraform Provider |
| Azure REST API | HTTP-based API (GET, PUT, POST, DELETE, PATCH) voor programmatische toegang |
| Azure Client SDK | Wrapper rond REST API voor diverse talen (.NET, Java, Node.js, Python, Ruby, Go) |
| Azure VM Extensions | Kleine applicaties voor configuratie en automatisering na initiële deployment |


- Azure Automation services:
  - Process Automation: Automatiseer reacties op events via watcher tasks
  - Configuration Management: Track software updates via Microsoft Enpoint Configuration Manager
  - Update Management: Beheer updates en patches, plan installaties, controleer resultaten
 
- Auto=shutdown
  - Automatisch afsluiten van VMs op scheme (dagelijk of wekelijks)
  - Configureerbaar via VM > Operations > Auto-Shutdown
  - Bespaart kosten door VMs niet onnodig te laten draaien
    

**Manage the availability of your Azure VMs**
  - Availability: Percentage van de tijd dat een service beschikbaar is
  - Azure VMs draaien op fysieke servers: Bij een storing verplaatst Azure de VM automatisch naar een gezonde server maar dit kan enkele minuten duren

  - Availability opties:

| Optie | Beschrijving |
|---|---|
| Availability Zones | Fysiek gescheiden zones binnen een regio (3 per regio), elk met eigen power, netwerk en koeling |
| VM Scale Sets | Groep load-balanced VMs die automatisch schaalt op basis van vraag of schema. Geen kosten voor de scale set zelf |
| Azure Load Balancer | Verdeelt traffic over meerdere VMs — inbegrepen bij Standard tier VMs |
| Azure Storage redundancy | Meerdere kopieën van data voor bescherming tegen hardware-, netwerk- en stroomstoringen |
| Azure Site Recovery | Repliceert workloads van primaire naar secundaire locatie voor regionele failover — ondersteunt Azure, Hyper-V, VMware en fysieke servers |

  - Azure Site Recovery voordelen:
    - Geen secundair fysiek datacenter nodig: Azure als recovery bestemming
    - Eenvoudig failover testen zonder impact op productie
   
**Back up your virtual machines**
  - Azure Backup is een Backup-as-a-Service oplossing voor fysieke en virtuele machines. On-premises en in de cloud

  - Ondersteunde scenarios:
    - Files en folders op Windows (fysiek en virtueel)
    - Application-aware snapshots (VSS)
    - Microsoft server workloads: SQL Server, SharePoint, Exchange
    - Azure VMs (Windows en Linux)
    - Linux en Windows 10 client machines
   
  - Voordelen:
    - Automatic storage management: Pay-as-you-use, geef vooraf toegewezen storage
    - Unlimited scaling: Hoge beschikbaarheid via Azure platform
    - Multiple storage options: LRS (lokaal) of GRS (geo-redundant)
    - Unlimited data transfer: Geen kosten voor inbound/outbound data
    - Data encryption: veilige opslag en verzending
    - Application-consistent backup: Recovery point bevat alle benodigde data voor volledig herstel
    - Long-term retention: Geen tijdslimiet op bewaren van backups
   
  - Componenten:
    - Azure Backup agent
    - System Center Data Protection Manager
    - Azure Backup Server
    - Azure BAckup VM extension
   
  - Opslag: Recovery Services vault. Backed by Azure Storage blobs. Hier definieer je welke machines worden gebackupt en wanneer snapshots worden gemaakt


---


## Learning Path 4: Deploy and manage Azure compute resources
### Module 2: Configure virtual machine availability 

**Plan for maintenance and downtime**
  - 3 typen downtime waarvoor je moet plannen:

| Type | Oorzaak | Azure reactie |
|---|---|---|
| Unplanned hardware maintenance | Azure detecteert dreigend hardware falen | Live Migration naar gezonde server — korte pauze, geen reboot |
| Unexpected downtime | Onverwacht falen van hardware of infrastructuur (netwerk, disk, rack) | Automatische migratie naar gezonde server in hetzelfde datacenter — reboot, mogelijk verlies van temp drive |
| Planned maintenance | Periodieke updates door Microsoft voor betrouwbaarheid, performance en security | Gepland, minimale impact |

  - Microsoft update niet automatisch het VM OS of andere software. Dat is de verantwoordelijkheid van de administrator.


**Create availability sets**
  - Een availability set is een logische groepering van VMs die zorgt dat niet alle VMs tegelijk uitvallen bij hardware- of softwarestoringen
  - Azure verdeelt VMs in een availability set ovre meerdere fysieke server, copute racks, storage units en netwerkswitches
  - VMs in een availability set moeten dezelfde functionaliteit en software hebben
  - Een VM kan alleen bij aanmaken aan een availability set worden toegevoegd. Wijzigen vereist verwijderen en opnieuw aanmaken

  - Best practices:
    - Plaats meerdere VMs in een availability set voor redundantie
    - Elke applicatietier in een aparte availability set. Voorkomt single point of failure
    - Combineer met Azure Load Balancer voor high availability en netwerkperformance
    - Gebruik managed disks voor block-level storage
   
    - Availability sets beschermen niet tegn OS- of applicatiespecifieke fouten. Gebruik aanvullende backup en disaster recovery technieken


**Review update domains and fault domains**
  - Elke VM in een availability set wordt geplaatst in 1 update domain en 1 fault domain.
  - Update Domains:
    - Groep van nodes die tegelijk geupdated en herstart worden tijdesn planned maintenance
    - Slects 1 update domain tegelijk herstart. Zorgt voor rolling updates zonder volledige downtime
    - Instelbaar van 1 tot 20 bij aanmaken, standaard 5
    - Aantal is niet wijzigbaar na aanmaken. Verwijder en hermaak de availability set
   
  - Fault domains:
  - Groep van nodes die een fysieke eenheid van falen vertegenwoordigen. Denk aan een server rack met gedeelde power en netwerk
  - Standaard 2 fault domains per availability set
  - Beschermt tegen hardware failures, netwerkstoringen en stroomonderbrekingen door VMs over meerdere racks te spreiden

**Review availability zones**
  - Availability zones zijn fysiek gescheiden locaties binnen een Azure regio. Elk met eigen power, cooling en netwerk
  - Minimaal 3 zones per enabled regio
  - VMs verpreid over 3 zones = automatisch verspreid over 3 fault domains en 3 update domains

| Categorie | Beschrijving | Voorbeelden |
|---|---|---|
| Zonal services | Resource gepind aan een specifieke zone | Azure VMs, managed disks |
| Zone-redundant services | Platform repliceert automatisch over alle zones | Zone-redundant Storage, Azure SQL Database |

  - Voor optimale business continuity: combineer availability zones met Azure Regional pairs


**Compare vertical and horizontal scaling**
  
| | Vertical scaling (scale up/down) | Horizontal scaling (scale out/in) |
|---|---|---|
| Wat | VM grootte aanpassen | Aantal VMs aanpassen |
| Voordeel | Eenvoudig, geen extra VMs nodig | Flexibeler, tot duizenden VMs |
| Beperking | Afhankelijk van beschikbare hardware, regio-afhankelijk, vereist VM stop/herstart | Complexer te beheren |
| Gebruik | Onder-benutting verminderen of piekbelasting opvangen | Wisselende workloads op grote schaal |

  - Bij reprovisioning (VM vervangen door nieuwe). Plan voor service onderbreking en datamigratie.


**Implement Azure Virtual Machine Scale Sets**
  - VM Scale Sets deployen en beheren een set indentieke VMs met automatisch schalen op basis van vraag
  - Geen pre-provisioning nodig. VMs worden automatisch toegevoegd of verwijderd
  - Geschikt voor large-scale services, big data en containzerized workloads

  - Kenmerken:
    - Ondersteunt Azure Load Balancer (layer-4 traffic) en Azure Application Gateway (Layer-7, TLS/SSL termination)
    - Bij uitval van 1 VM blijven andere VMs de applicatie bedienen
    - Schalen kan handmatig, automatisch of een combinatie

   - 2 orchestration modes:

| Mode | Beschrijving |
|---|---|
| Uniform | Alle VMs aangemaakt vanuit dezelfde base OS image en configuratie |
| Flexible | VMs kunnen verschillende images, sizes of configuraties gebruiken binnen dezelfde scale set |

  - Orchestration mode moet worden gekozen bij aanmaken van de scale set. Niet wijzigbaar achteraf


**Create Virtual Machine Scale Sets**
  - Configuratie-instellingen bij aanmaken:
    - Orchestration mode: Flexible (standaard en aanbevolen) of Uniform
    - Image: Base OS of applicatie voor de VM
    - VM Architecture: x64 (meest software compatibiliteit) of Arm64 (tot 50% betere price-performance)
    - Size: Bepaalt CPU, memory en storage capaciteit
   
    - Advanced tab:
      - Spreading algorithm: hoe VMs verdeeld worden over fault domains:
        - Max spreading: VMs verspreid over zoveelmogelijk fault domains (aanbevolen)
        - Fixed spreading: Altijd exact 5 fault domains. faalt als minder dan 5 beschikbaar zijn


**Implement autoscale**
  - Autoscaling verhoogt of verlaagt automatisch het aantal VM instances op basis van vraag. Minimaliseert kosten bij lage vraag, handhaaft performance bij hoge vraag

  - Configuratieopties:
    - Scale out: meer VM instances toevoegen bij consistent hoge load
    - Scale in: VM instances verwijderen bij consistent lage load (bijv. 's avonds of weekenden), bespaart kosten
    - Scheduled events: Automatisch schalen op vaste tijdstippen
    - Threshold-based rules: autoscale regels op basis van performance drempelwaarden
   
  - Autoscaling vermindert managment overhead voor het monitoren en optimaliseren van applicatieprestaties

**Configure autoscale**
  - Scaling modes:
    - Manual: vaste instance count instellen (0-1000), inclusief scale-in policiy (volgorde van verwijdering)
    - Autoscalling: Automatisch schalen op schema of op basis van metrics

    - Autoscale configuratie-instellinge:

| Instelling | Beschrijving |
|---|---|
| Default instance count | Initieel aantal VMs bij deployment (0-1000) |
| Instance limit | Minimum en maximum aantal instances voor de scaling condition |
| Scale out | CPU drempel % voor scale-out + aantal instances om toe te voegen |
| Scale in | CPU drempel % voor scale-in + aantal instances om te verwijderen |
| Query duration | Tijdvenster waarin Autoscale terugkijkt voor gemiddeld metricgebruik |
| Schedule | Start- en einddatum, herhaling op specifieke dagen |




---


## Learning Path 4: Deploy and manage Azure compute resources
### Module 3: Configure Azure App Service plans




























  
