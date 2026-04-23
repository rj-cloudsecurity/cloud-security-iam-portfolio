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





