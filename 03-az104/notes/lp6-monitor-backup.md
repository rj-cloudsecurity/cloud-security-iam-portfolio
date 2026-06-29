# AZ-104: Azure Administrator Associate
## Learning Path 6: Monitor and back up Azure resources

  - **AZ-104 Started:** 11 April, 2026
  - **AZ-104 Exam passed:** 29 June, 2026

---


## Inhoudsopgave

### Learning Path 6: Monitor and back up Azure resources


---

## Learning Path 6: Monitor and back up Azure resources
### Module 1: Introduction to Azure Backup 


**What is Azure Backup?**
  - Azure Back up is een Azure service voor veilige, kosteneffectieve backup van data assets. Geen eigen backup-infrastructuur nodig

  - Wat kan worden gebackupt
    - On-premises files/folders/system state, Azure VMs, MAnaged Disks, File Shares, SQL Server in VMs, SAP HANA, PostgreSQL, MySQL, Blobs, AKS clusters
   
  - Key features
    - Zero-infrastructure: Geen backup server of storage nodig. Azure beheert en schaalt automatisch
    - Centraal beheer: Via Backup Center, PowerShell, CLI en APIs
    - Security: Encryptie in transit en at rest, private endpoints, bescherming tegen ransomware en accidentele verwijdering
   
  - RTO en RPO
  - RTO (Recovery Time Objective): Maximale tijd die een systeem down mag zijn na een incident. Voorbeeld RTO = 3 uur -> systeem moet binnen 3 uur hersteld zijn
  - RPO (Recovery Point Objective): Maximaal dataverlies gemeten in tijd. Voorbeeld: RPO = 1 uur -> backup elk uur, max 1 uur data verlies bij incident



**How Azure Backup works**
  - Opslaglagen (Access Tiers)
    - Snapshot tier: Snelle eerste laag, snapshot opgeslagen bij de bron in de subscription van de klant. Snelte retore
    - Vault-standard tier: Geisoleerde kopie in Microsoft-managed storage. Beschikbaar ook als de brondata verwijderd of gecompromitteerd is
    - Archive tier: Voor long-term retention (LTR), zelden geraadpleegde data voor compliance. Goedkoopst, langzaamste RTO
   
  - Backup types:
    - full: Volledige backup van database/VM
    - Incremental: Alleen gewijzigde blokken sinds vorige backup
    - Differential: Gewijzigde data sinds laatste full backup
    - Transaction log: Point-in-Time tot op de seconde, elke 15 min
    - Selective Disk: Subset van VM-schijven backuppen
   
  - Redundantie opties:
    - LRS (lokaal)
    - GRS (geo-redundant)
    - ZRS (zone-redundant)
   
  - Security
    - Encryptie in transit en at rest
    - RBAC voor toegangsbeheer
    - Soft delete: Verwijderde backup bewaard voor 14 dagen gratis
   
  - Vaults
    - Recovery Service Vault: Voor Azure VMs, on-premises, SQL etc.
    - Backup vault: Voor nieuwere workloads (Managed Disks, PostgreSQL, Blobs)
    - Backup Center: Centraal beheer over alle vaults, subscriptions en regio via 1 console


**When to use Azure Backup**
  - Gebruik Azure Backup voor
    - Azure workloads: VMs, Managed Disks, SQL Server in VMs, SAP HANA, Blobs, File Shares, PostgreSQL
    - Compilance: Lange retentie (wekelijks, maandelijks, jaarlijks) via backup policies per vault. Short-term = minuten/dagelijks, Long-term = wekelijks t/m jaren
    - Operationele recovery: Self-service backup en restore voor applicatiebeheerders bij accidentele verwijdering of datacorruptie.
   
  - SQL Server specifiek
    - Full, differential en log backups ondersteund
    - RPO van 15 minuten via frequente log backups
    - Point-in-time restore tot op de seconde
    - Backup op individueel database-niveau
   
  - Compliance en retentie
    - Planned: Van te voren bekende retentievereisten (bv. 10 jaar)
    - Unplanned: On-demand backup met custom retentie
    - On-demand: Buiten het geplande schema, eigen retentie-instellingen (Policy-shcema geldt niet)
   
  - Monitoring
    - Backup Explorer: Centraal overzicht over alle vaults, subscriptions en regio's
    - Log Analytics: Integratie voor monitoring en rapportage via Workbooks
    - RBAC voor toegangsbeheer tot backup-operaties
   
  - Beperking
    - Cross-region backup wordt voor de meeste workloads niet ondersteund. Cross-region restore naar een paired secondary region wel


---


## Learning Path 6: Monitor and back up Azure resources
### Module 2: Protect your virtual machines by using Azure Backup 

**Azure Backup features and scenarios**
  - Azure Backup is een ingebouwde Azure service voor veilige backup van Azure en on-premises data zonder eigen backup infrastructuur te hoeven deployen

  - Azure Backup vs Azure Site Recovery
    - Azure Backup: Bewaart kopieen van data, terug in de tijd. Voor accidenteel dataveries, corruptie, ransomware
    - Azure Site Recovery: Real-time replicatie en failover. Voor regio brede disaster

  - Voordelen
    - Zero-infrastructure: Geen backup server of storage beheer nodig
    - Long-term retention: Jaren bewaren met automatische lifecycle management
    - RBAC: Toegansbeheer per rol
    - Encryptie: Automatisch met Microsoft-managed of customer-manager keys
    - Geen internetverbinding vereist: Dataverkeer via Azure Backbone
    - Soft Delete: 14 dagen extra bewaard na verwijdering
   
  - Replicatie opties:
    - LRS: Noncritical scenarios
    - GRS: Aanbevolen voor backup scenarios
    - ZRS: High-availability scenarios
   
  - Ondersteunde scenarios
    - Azure VMs: Windows en Linux
    - On-premises: via MARS agent, MABS of DPM server
    - Azure Files shares: Via snapshot management
    - SQL Server en SAP HANA in Azure VMs: 15 minuten RPO, Point-in-Time recorvery


**Back up an Azure virtual machine by using Azure Backup**
  - Recovery Sevices Vault
    - Beheert en slaat backup data op. Geen eigen storage account nodig. Azure regelt dit automatisch. Fungeert ook als RBAC-grens voor toegangscontrole

  - Snapshot consistentieniveaus
    - Application consistent. Volledige VM inclusief geheugen en I/O via VSS. Hoogste niveau, Linux vereist custom pre/post scripts
    - File system consistent: Snapshot zonder geheugeninhoud. Apps doen eigen cleanup bij opstart. Fallback als VSS faalt
    - Crash consistent: VM was uit tijdens backup. Geen geheugen of I/O vastgelegd, geen garantie voor data-integriteit

  - Backup process
    - Backup gestart op basis van policy
    - Backup extension geinstalleerd op VM (windows: VM Snapshot via VSS, Linux: VM SnapshotLInux)
    - Snapshot gemaakt -> lokaal opgeslagen -> overgedragen naar vault
    - Alleen gewijzigde blokken (delta) worden overgedragen
    - Totale backup tijd < 24 uur voor dagelijkse policy
   
  - Extra opties
    - Selective disk backup: Alleen subset van schijven backuppen
    - CMK: Vault encryptie met customer-managed keys
    - Einhanced soft delete: Beschermt tegen accidentele verwijdering en malware


**Exercise: Create and configure virtual networks**
  - [Lab 26 Create and configure virtual networks](/03-az104/labs/26-create-and-configure-virtual-networks.md)



**Restore virtual machine data**
  - Restore opties
    - Create a new VM: Nieuwe VM aanmaken vanuit restore point.Moet in dezelfde regio als bron-VM
    - Restore Disk: Schijf herstellen en gebruiken voor nieuwe VM of koppelen aan bestaande VM. Handig voor custom configuraties via template of PowerShell
    - Replace existing: Schijf van bestaande VM vervangen. Azure maakt eerst snapshot van huidige staat. VM moet nog bestaan. Werkt niet als VM verwijderd is.
    - Cross region restore: Restore naar paired secondary regio. Ondersteunt Create VM en REstore Disk, niet replace existing
    - Cross Subscription Restore: Restore naar andere subscription binnen dezelfde tenant. Alleen voor managed VMs, niet voor snapshots of ADE-versleutelde VMs
    - Cross Zonal Restore: Restore naar andere availability zone. Alleen voor managed VMs, vereist ZRS-enabled vault
    - Selective disk restore: Subste van VM schijven herstellen
   
  - Individuele bestanden herstellen
    - Mogelijk via iSCI initiator. Snapshot mounten op doelmachine en individuele bestanden kopieren
   
  - Encrypted VMs
    - Werkt met Azure Disk Encryption + Key Vault
    - Beperkingen: Geen file/folder-level restore (hele VM moet hersteld worden), geen Replace existing optie, geen certificate-based keys 



**Exercise: Restore Azure virtual machine data**
  - [Lab 27 Restore Azure virtual machine data](/03-az104/labs/27-restore-azure-virtual-machine-data.md)

---


## Learning Path 6: Monitor and back up Azure resources
### Module 3: Monitor your Azure virtual machines with Azure Monitor 

**Monitoring for Azure VMs**
  - Azure monitor. 2 hoofdfuncties:
    - Metrics: Numerieke waarden op vaste intervallen. Automatisch verzameld voor elke Azure VM, bewaard 93 dagen
    - Logs: Vastgelegde systeemgebeurtenissen met timestamp. Niet standaard verzameld, moet geconfigureerd worden. Opgeslagen in Log Analytics workspace, query's via KQL (Kusto Query Language)
   
  - VM monitoring lagen
    - Host VM -> Guest OS -> Client workloads -> Applicaties

  - Host VM metrics
    - Automatisch verzameld via Azure portal (Overview pagina): VM availability, CPU%, OS disk usage, Network operations, Disk operations/sec
    - Metrics Explorer: Meer metrics plotten, trends vergelijken, alerts instellen, pinnen aan dashboards
    - Recommended alert rules: Voorgedefinieerde alerts op CPU, geheugen, schijf, netwerk en VM availability. Instelbaar bij aanmaken of achteraf
    - Activity logs: Automatisch bijgehouden (VM start, wijzigingen). Doorsturen mogelijk naar Log analystics (max 2 jaar), Azure Storage (goedkoop archief) of Event Hubs (buiten Azure)
    - Boot Diagnostics: Screenshot en serial console logs voor troubleshooting van bootproblemen. Opgeslagen in managed storage account
   
    - Guest OS/client monitoring
      - Vereist Azure Monitor Agent + DCR (Data Collection Rule). DCR bepaalt welke data verzameld wordt en waar het naartoe gaat
    - VM insights
      - Vereenvoudigt onboarding van Azure Monitor Agent. Biedt preconfigured DCR, trending, performance charts en workbooks voor Windows en Linux. Optioneel: process monitoring en dependency map


**Monitor VM host data**
  - Zodra een VM aangemaakt wordt, begint Azure automatisch met verzamelen van basis metrics en activity logs

  - Bij aanmaken VM instellen
    - Recommended alert rules: Inschakelen via Monitoring tab bij aanmaken. Alert op CPU, geheugen, schijf, netwerk en VM availability. Notificaties via email
    - Boot diagnostics: Inschakelen via "Enable with managed storage account (recommended)". Niet verwarren met OS guest diagnostics (LAD is geprecated)
   
  - Beschikbare monitoring na aanmaken
    - Platform metrics (Monitoring tab -> Overview) VM availability, CPU%, Disk bytes, Network, Disk operations/sec automatisch verzameld, Direct beschikbaar
   
    - Activity log: Via linker navigatiemenu -> Activity log. Ook opvraagbaar via PowerShell of CLI

  - Boot diagnostics: Via Help -> Boot diagnostics:
    - Screenshot: Startup screenshot van de hypervisor
    - Serial log: Log van de bootsequentie
   
  - Guest OS metrics worden nog niet verzameld, doorvoor is VM insights + DCR nodig


**Use Metrics Explorer to view detailed host metrics**
  - Metrics Explorer maakt aangepaste metics-grafieken voor VM host metrics, meer detail dan de ingebouwde grafieken

  - Openen via
    - VM -> linker menu -> Metrics
    - VM -> Overview -> Monitoring tab -> See all Metrics
    - Azure Monitor -> linker menu -> Metrics

  - Configuratie-opties
    - Scope: VM naam (vooringevuld), uitbreidbaar met andere VMs van hetzelfde type en locatie
    - Metric Namespace: Meestal 1 namespace per resource type. Storage accounts hebben aparte namespaces per service (files, tables, blobs queues)
    - Metric: Keuze uit alle beschikbare metrics binnen de namespace
    - Aggregation: Count, Average, Maximum, Minimum, Sum
    - Tijdsbereik: 30 minuten t/m 30 dagen of custom. Granulariteit: 1 minuut t/m 1 maand
   
    - Voorbeeld: CPU + Inbound Flows grafiek
      - Open Metrics Explorer
      - Metric: Percentage CPU -> Aggregations: Max
      - Add metric -> Inbound Flows -> Aggregation: avg
      - Tijdsbereik: Last 30 mins
    - Resultaat: Gecombineerde grafiek die toont hoe inkomend verkeer de CPU beinvloedt



**Collect client performance counters by using VM insights**
  - VM Insights
    - VM insights is een Azure Monitor feature die client-monitoring van een VM snel inschakelt, geen handmatige configuratie van agent, DCR of workbooks nodig
   
  - Wat VM insights doet
    - Installeert Azure Monitor Agent op de VM
    - Maakt een DCR aan die client performance data verzamelt en naar Log Analytics workspace stuurt
    - Presenteert data in voorgeconfigureerde workbooks

  - Inschakelen
    - Portal -> VM -> Monitoring -> Insights -> Enable -> Configure. Duurt 5-10 min voor installatie, daarna nog 5-10 min voor data beschikbaar is
   
    - Na installatie verificeren via VM -> Overview -> Properties tab -> Extensions + applications
   
  - Data bekijken
    - VM insights stuurt metrics naar Azure Monitor Logs. Niet naar Metrics Explorer. Bekijken via VM -> Monitoring -> Insights:
      - Performance tab: Prebuilt workbook met performance charts. Aanpasbaar via Time range en aggregaties
      - Map tab (optioneel: Visualiseert VM-dependencies: Actieve processen en netwerkverbingen over een tijdsperiode
     
  - Processes and dependencies (ap) staan standaard op disabled, handmatig in te schakelen bij het aanmaken van de DCR



**Collect VM client event logs**
  - VM insights verzamelt performance data, maar voor root cause analyse heb je log data nodig. Hiervoor maak je een eigen DCR aan

  - Benodigdheden
    - Data Collection Endpoint: Ontvangt de log data
    - Data Collection Rule (DCR): Bepaalt welke data verzameld wordt en waar het naartoe gaat
    - Log Analytics workspace: Opslag en query's via KQL

  - DCR aanmaken, stappen
     - Azure Monitor -> Settings -> Data Collection Endpoints -> Create `linux-logs-endpoint`
     - Azure Monitor -> Settings -> Data Collection Rules -> Create
     - Basics: naam, subscription, resource group, regio, platform type (Linux)
     - Resources: VM toevoegen + data collection endpoint koppelen
     - Collect and deliver: data source type -> Linux Syslog -> destination -> Log Analytics workspace

  - Key points
    - 1 DCR kan gekoppeld worden aan meerdere VMs in een subscription
    - Meerdere DCRs mogelijk voor verschillende data types van verschillende VMs
    - VM insights DCR = performance counters; eigen DCR = log data
    - Log data bewaard in Log Analytics workspace, niet in Metrics Explorer
      



