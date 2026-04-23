# AZ-104: Azure Administrator Associate
## Learning Path 4: Deploy and manage Azure compute resources

  - **AZ-104 Started:** 11-4-2026
  - **AZ-104 Exam passed:**

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

