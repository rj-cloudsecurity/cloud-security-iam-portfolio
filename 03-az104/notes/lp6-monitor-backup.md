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












---


## Learning Path 6: Monitor and back up Azure resources
### Module 3: Monitor your Azure virtual machines with Azure Monitor 













