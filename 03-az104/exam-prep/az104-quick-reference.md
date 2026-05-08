## Recovery Services Vault Verwijderen — Vereiste Stappen
1. Stop backup van alle protected items
2. Disable soft delete feature
3. Permanently remove all items in soft delete state
4. Dan pas vault verwijderen
- VM verwijderen is niet vereist
- Read lock op vault blokkeert verwijdering — niet instellen

## Azure Backup Agents — Vergelijking
| Agent/Tool | Gebruik |
|---|---|
| MARS agent | Files, folders en system state op individuele Windows server |
| MABS | Centrale backup van workloads — SQL, SharePoint, Hyper-V, meerdere machines |
| Site Recovery Provider | Disaster recovery / replicatie via Azure Site Recovery |
| Azure Connected Machine agent | Azure Arc — on-premises servers via Azure beheren |

## Poorten — Aanvulling
| Poort | Protocol/Gebruik |
|---|---|
| 587 | SMTP relay — outbound email via authenticated SMTP |
| 25 | SMTP — mail traffic (niet authenticated) |

## Application Security Groups (ASG)
- Groepeert network interfaces van meerdere VMs
- Gebruik als bron of doel in NSG regel
- Alle NICs in de ASG moeten in hetzelfde VNet zitten
- Minimale NSG regels — één regel voor de groep i.p.v. één per VM
- Voor "fewest number of NSG rules" = altijd ASG

## Publiek IP Adres Types
| Type | Gedrag bij VM stop/deallocate |
|---|---|
| Dynamisch publiek IP | Wordt vrijgegeven — nieuw IP bij opnieuw starten |
| Statisch publiek IP | Blijft altijd hetzelfde — ook na stop/deallocate |

## Netwerk Diagnostiek Commands
| Command | Gebruik |
|---|---|
| `netstat -an` | Toont alle luisterende poorten en actieve verbindingen |
| `Test-NetConnection` | PowerShell — test TCP verbinding of ping naar host |
| `ping` | ICMP test — controleert bereikbaarheid |
| `tracert` / `traceroute` | Toont routing pad naar doel |
| `nslookup` | DNS lookup — naam naar IP resolutie |
| `nbtstat -c` | NetBIOS name cache — legacy Windows naming |
| `ipconfig` | IP configuratie van network interfaces |
