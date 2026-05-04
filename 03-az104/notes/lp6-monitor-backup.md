# AZ-104: Azure Administrator Associate
## Learning Path 6: Monitor and back up Azure resources
  - **AZ-104 Started:** 11-4-2026
  - **AZ-104 Exam passed:**

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













