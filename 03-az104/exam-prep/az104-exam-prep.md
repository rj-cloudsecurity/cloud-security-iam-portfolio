# AZ-104 Exam Preparation
## Certification
  - Microsoft Certified: Microsoft Azure Administrator (AZ-104)
  - Result: In preparation
  - Date:
## Study Method
  - Completing all Microsoft Learn modules
  - Watching John Savill's Technical Training AZ-104
  - Creating detailed notes in [Learn Notes](/03-az104/notes/)
  - Practicing with custom AI-generated exams (claude.ai) based on official AZ-104 exam objectives
  - Practicing with the Official Microsoft Practice Assessment
  - Practicing with the tutorialsdojo.com
## Practice Assessment Progression
| Platform | Score | Notes |
|----------|-------|-------|
| | | *Baseline, no prior study* |
| Exam 1 — Official Microsoft Practice Assessment | 46% | 23/50. Weakest: LP2 M1, LP2 M2, LP2 M4, LP3 M1, LP3 M2, LP4 M1, LP5 M1.|
| | | *Progress checks — taken during study to track progress per learning path* |
| Exam 2 — Custom LP1 & LP2 | 70% | 14/20. Weakest: LP1 M2, LP2 M2, LP2 M3, LP2 M6.|
| Exam 3 — Custom LP1 & LP2 (mixed question types) | 90% | 37/41. Weakest: LP2 M2, LP2 M4, LP3 M2.|
| | | *From this point: full exam coverage across all learning paths, multiple choice only* |
| Exam 4 — Custom full exam (LP1–LP6) | 73% | 22/30. Weakest: LP3 M2, LP4 M5, LP5 M1, LP6 M3.|
| Exam 5 — Custom full exam (LP1–LP6) | 87% | 27/31. Weakest: LP2 M3, LP4 M5, LP5 M3, LP6 M2.|
| Exam 6 — Custom full exam (LP1–LP6), harder difficulty | 94% | 34/36. Weakest: LP1 M2, LP4 M2.|
| | | *Official Microsoft assessments* |
| Exam 7 — Official Microsoft Practice Assessment | 60% | 30/50. Weakest: LP4 M3, LP4 M4, LP4 M5, LP5 M1, LP5 M2, LP6 M2.|
| Exam 8 — Official Microsoft Practice Assessment | 70% | 35/50. Weakest: LP4 M2, LP4 M3, LP4 M4, LP5 M1, LP5 M2, LP6 M2, LP6 M3.|
| Exam 9 — Official Microsoft Practice Assessment | 80% | 40/50. Weakest: LP5 M1, LP6 M2, LP6 M3.|
| Exam 10 — Official Microsoft Practice Assessment | 88% | 44/50. Weakest: LP4 M5, LP5 M1, LP6 M3.|
| Exam 11 — Official Microsoft Practice Assessment | 90% | 45/50. Weakest: LP3 M2, LP4 M4, LP5 M3, LP6 M2.|
| | | *2 week holiday break — resuming preparation* |
| Exam 12 — Official Microsoft Practice Assessment | 83% | Weakest: Implement and manage virtual networking, Monitor and maintain Azure resources.|
| | | *Tutorials Dojo Section-Based Mode* |
| Tutorials Dojo Section-Based — Manage Azure Identities and Governance | 100% | 17/17. Perfect score. |
| Tutorials Dojo Section-Based — Implement and Manage Storage | 85% | 17/20. Fouten: GRS copies (3 ipv 6), AzCopy blob vs file, Import/Export vs Storage Explorer. |
| Tutorials Dojo Section-Based — Deploy and Manage Azure Compute Resources | 95% | 20/21. |
| Tutorials Dojo Section-Based — Implement and Manage Virtual Networking | 83% | 24/29. |
| Tutorials Dojo Section-Based — Monitor and Maintain Azure Resources | 87% | 13/15. |
| | | *Tutorials Dojo Timed Mode* |
| Tutorials Dojo Timed Mode Set 4 | 73% | 61/83. Weakest: Networking 63%, Storage 71%, Governance 76%. Veel herkende vragen. |
| Tutorials Dojo Timed Mode Set 2 | 79% | 54/68. Weakest: Compute 64%, Networking 64%. Fouten: proximity placement group regio, Bicep scope, DSC vs Custom Script, ACR Tasks. |
| Tutorials Dojo Timed Mode Set 3 | 86% | 63/73. Weakest: Governance 81%, Compute 80%, Monitor 75%. Fouten: P2S VPN gateway type, policy exclusion, Logic App Operator rol, ConvertTo-Json, managed identities ontvangen geen email. |
| | | *DNS oefensessies — gericht op zwakke punten* |
| DNS oefensessie 1 | 75% | 15/20. Fouten: CNAME vs A op apex, auto-registration limiet per VNet, regio private DNS zone, zone niet gelinkt als oorzaak publiek IP, A record vs MX. |
| DNS oefensessie 2 | 85% | 17/20. Fouten: apex zonder ALIAS/ANAME, regio private DNS zone, custom DNS server als oorzaak publiek IP. |
| DNS oefensessie 3 | 90% | 18/20. Fouten: auto-registration meerdere VNets, VNet niet gelinkt aan zone. |
| | | *Network Watcher oefensessies* |
| Network Watcher oefensessie 1 | 85% | 17/20. Fouten: NSG flow logs vs Effective security rules, Network topology vs Traffic Analytics. |
| Network Watcher oefensessie 2 | 85% | 17/20. Fouten: Connection troubleshoot vs IP flow verify, Traffic Analytics vs Network topology. |
| Network Watcher oefensessie 3 | 80% | 16/20. Fouten: Effective routes vs Traffic Analytics, Connection monitor vs NSG flow logs, Traffic Analytics resources, VPN troubleshoot vs Connection troubleshoot. |
| | | *DNS + Network Watcher gecombineerde sessie* |
| DNS oefensessie 4 | 85% | 17/20. Fouten: CNAME vs A op apex (subdomein www), auto-registration richting (zone vs VNet) — beide hardnekkig terugkerend. |

## Next Focus Areas after Exam 2
  - LP1 M2 — ARM templates: subscription scope for multi-resource group deployments
  - LP2 M2 — Device registration: Entra Registered (BYOD) vs Entra Joined (org-owned)
  - LP2 M2 — Custom security attributes: assignable to users and service principals only
  - LP2 M3 — RBAC: synced users cannot have passwords reset directly in Entra ID
  - LP2 M6 — SSPR: guests not supported; synced users require password writeback

## Next Focus Areas after Exam 3
  - LP2 M2 — Dynamic group membership: Dynamic Device not supported in Microsoft 365 groups
  - LP2 M4 — Group-based licensing: duplicate licenses deduplicated automatically; restored users do not regain group memberships automatically
  - LP3 M2 — Object replication: change feed required on source only; hierarchical namespace not related

## Next Focus Areas after Exam 4
  - LP2 M4 — Azure Policy: Modify effect for automatic tagging, not Append
  - LP1 M2 — ARM templates: subscription scope for multi-resource group deployments (recurring)
  - LP3 M1 — Storage replication: GZRS combines ZRS in primary region with secondary region replication
  - LP3 M3 — Storage security: NFS v3 is an access protocol, not related to POSIX ACLs; hierarchical namespace enables POSIX ACLs
  - LP4 M5 — Containers: ACI for short isolated tasks; App Service for Docker with autoscaling
  - LP5 M1 — Networking: P2S VPN client must be reinstalled after VNet peering is configured
  - LP5 M2 — DNS: virtual network link with auto-registration enabled for automatic hostname registration in private DNS zones
  - LP6 M3 — Backup: default VM backup retention is 30 days; soft delete retention is 14 days

## Next Focus Areas after Exam 5
  - LP2 M3 — RBAC: deny assignments always override allow assignments, even Owner role
  - LP4 M5 — Containers: ACA for scale-to-zero and event-driven microservices, not App Service (recurring)
  - LP5 M3 — Load balancer: five-tuple hash for even traffic distribution; session persistence causes uneven distribution
  - LP6 M2 — Monitoring: Azure Network Watcher for network health, not Azure Monitor

## Recurring Patterns and Observations after Exam 5
**Consistent error pattern:**
Answers tend to be confused between two options that look similar. Modify vs Append. Network Watcher vs Azure Monitor. ACA vs App Service. Session persistence vs five-tuple hash.
**Strongest areas:**
Storage is now solid. Identity fundamentals are also strong.
**Recurring weak areas:**
Containers (ACI vs ACA vs App Service) and Networking.

## Next Focus Areas after Exam 6
  - LP1 M2 — ARM templates: subscription scope for multi-resource group deployments (recurring third time)
  - LP4 M2 — Availability: availability zone for datacenter failure protection; availability set for rack failure only

## Recurring Patterns and Observations after Exam 6
**Improvements since Exam 5:**
Containers fully resolved. Networking errors eliminated. Monitor & Backup zero errors. Storage zero errors.
**Consistent error pattern:**
ARM template deployment scope remains the single most persistent gap.
**Progress trend:**
46% (baseline) → 73–94% (custom exams).

## Next Focus Areas after Exam 7
  - LP4 M3 — App Service: scale up to Standard/Premium before autoscale can be configured
  - LP4 M4 — App Service: Publish → Docker Container for container images, not Runtime stack
  - LP4 M5 — Containers: event-driven trigger for Service Bus scaling in ACA, not HTTP (recurring)
  - LP5 M1 — Networking: NSG must be in same region as the subnet it is associated with
  - LP5 M2 — DNS: Azure Private DNS zone for multiple VNets with custom domain
  - LP6 M2 — Monitoring: summarize operator for aggregation in KQL; alert state is always manually set

## Recurring Patterns and Observations after Exam 7
**Consistent error pattern:**
Compute (LP4) is now the single weakest domain.
**Progress trend:**
46% → 60% → 70% on official Microsoft assessments.

## Next Focus Areas after Exam 8
  - LP4 M2 — Compute: VM Scale Set configured under Availability options, not Management
  - LP4 M3 — App Service: scale up = bigger tier; scale out = more instances; Basic does not support autoscale
  - LP4 M4 — App Service: Application Logging Blob for retention over 7 days; Warning severity includes Warning/Error/Critical only
  - LP4 M5 — Containers: ACI for short isolated tasks (recurring fourth time)
  - LP5 M2 — DNS: virtual network link required for private DNS zone registration (recurring)
  - LP6 M3 — Backup: Site Recovery failover status must be Failover committed before reprotection

## Recurring Patterns and Observations after Exam 8
**Consistent error pattern:**
LP4 Compute remains the most persistent weak domain.
**Progress trend:**
46% → 60% → 70% on official Microsoft assessments.

## Next Focus Areas after Exam 9
  - LP5 M1 — Networking: effective routes on NIC to verify peering routing path, not Network Watcher next hop (recurring)
  - LP5 M1 — Networking: NSG associates with subnets and NICs only — not VNets; NSG must be same region as subnet
  - LP6 M2 — Monitoring: action group must be created first before alert processing rules
  - LP6 M3 — Backup: vault credentials must be downloaded and server registered before backup policy can be configured
  - LP6 M3 — Backup: Site Recovery failover status must be Failover committed before reprotection (recurring)

## Recurring Patterns and Observations after Exam 9
**Consistent error pattern:**
Networking and Monitor & Backup remain the two weak domains.
**Progress trend:**
46% → 60% → 70% → 80% on official Microsoft assessments.

## Next Focus Areas after Exam 10
  - LP4 M5 — Containers: App Service for Docker with custom domain + autoscale, not ACI (recurring fifth time)
  - LP5 M1 — Networking: VPN gateway for encrypted on-premises connection, not private endpoint (recurring)
  - LP5 M1 — Networking: port 443 = HTTPS, port 3389 = RDP, port 587 = SMTP relay
  - LP5 M1 — Networking: netstat -an to check listening ports, not Test-NetConnection
  - LP6 M3 — Backup: MARS agent for files/folders on individual server; MABS for central workload backup
  - LP6 M3 — Backup: three steps required before deleting Recovery Services vault

## Recurring Patterns and Observations after Exam 10
**Consistent error pattern:**
LP4 M5 Containers remains the single most persistent error across all exams.
**Progress trend:**
46% → 60% → 70% → 80% → 88% on official Microsoft assessments.

## Next Focus Areas after Exam 11
  - LP3 M2 — Storage: Data Lake Gen2 requires premium block blobs or standard GPv2 — premium file shares not supported (recurring)
  - LP4 M4 — App Service: Application Logging Blob required for warnings or higher — not Detailed Error Message (recurring)
  - LP5 M3 — Load balancer: session persistence requires Client IP AND Protocol together; IP flow verify for NSG troubleshooting, not VNet flow logs
  - LP6 M2 — Monitoring: alert rule detects event + action group sends notification; alert processing rule is not a notification mechanism

## Recurring Patterns and Observations after Exam 11
**Improvements since Exam 10:**
Containers resolved. Networking port numbers correct. MARS vs MABS correct. NSG region constraints correct.
**Consistent error pattern:**
Errors now concentrated in subtle configuration details.
**Progress trend:**
46% → 60% → 70% → 80% → 88% → 90% on official Microsoft assessments.

## Next Focus Areas — Tutorials Dojo Timed Mode
  - Networking: P2S VPN vereist route-based gateway — policy-based wordt niet ondersteund
  - Governance: Azure policy exclusion — uitgesloten resource group is toegestaan, niet geblokkeerd
  - Governance: Logic App Operator rol = alleen lezen/inschakelen, niet aanmaken; gebruik Contributor
  - Governance: Get-AzRoleDefinition | ConvertTo-Json voor custom role definitie ophalen
  - Monitor: Email Azure Resource Manager Role — alleen users ontvangen email, managed identities niet
  - Compute: Proximity placement group + scale set moeten in dezelfde regio zitten
  - Compute: Bicep scope = waar resources worden gedeployed; niet location
  - Compute: DSC extension = consistent + compliance; Custom Script Extension = eenmalig bij deployment
  - Compute: ACR Tasks = automatisch rebuilden bij base image update
  - Backup: RSV verwijderen = eerst backup stoppen per item, dan pas data verwijderen

## Recurring Patterns and Observations — Tutorials Dojo
**Scores:**
Section-based scores hoog (83–100%). Timed mode scores lager (73–86%) deels door herkende vragen.
**Consistent error pattern:**
Volgordevragen en "welk tool voor welk doel" blijven moeilijk. PowerShell cmdlets. Policy exclusion logica.
**Progress trend:**
46% → 60% → 70% → 80% → 88% → 90% on official Microsoft assessments. Tutorials Dojo Timed Mode: 73% → 79% → 86%.

## Next Focus Areas — DNS
  - Private DNS zone linken aan VNet verplicht voor resolution; VNet peering is niet genoeg
  - Apex zonder ALIAS/ANAME = A record + TXT; CNAME nooit op apex
  - Subdomein (www) = CNAME + TXT; apex (zonder www) = A record + TXT — blijft hardnekkig door elkaar gehaald
  - Custom domain verificatie = altijd TXT record asuid als eerste stap
  - Auto-registration: VNet kan maar één zone hebben; één zone mag meerdere VNets hebben — richting blijft hardnekkig door elkaar gehaald
  - Regio maakt niet uit bij private DNS zones
  - DNS Private Resolver voor on-premises → Azure private zone resolution
  - Custom DNS server moet forwarden naar 168.63.129.16 voor Azure private DNS
  - Public DNS zone kan nooit gelinkt worden aan VNet

## DNS Oefensessie Voortgang
| Sessie | Score | Fouten |
|---|---|---|
| Sessie 1 | 75% | Apex, auto-registration, regio, zone niet gelinkt, A vs MX |
| Sessie 2 | 85% | Apex, regio, custom DNS server |
| Sessie 3 | 90% | Auto-registration meerdere VNets, VNet niet gelinkt |
| Sessie 4 | 85% | Apex/subdomein records (CNAME vs A), auto-registration richting |

## Next Focus Areas — Network Watcher
  - NSG flow logs vs Effective security rules: NSG staat wel in flow logs naam maar toont geen regels; effective security rules toont geen "NSG" maar wél alle regels
  - Connection troubleshoot vs IP flow verify: "kan VM bereiken" = Connection troubleshoot, "wordt pakket geblokkeerd + welke regel" = IP flow verify
  - Traffic Analytics vs Network topology: Traffic Analytics = verkeersanalyse/geografisch, Network topology = visuele kaart van resources
  - Traffic Analytics vereist storage account + Log Analytics workspace (niet Application Insights)
  - Effective routes vs Next hop: effective routes = compleet overzicht, next hop = één destination
  - Connection monitor vs NSG flow logs: connection monitor = doorlopend + Log Analytics, NSG flow logs = historisch naar storage account
  - VPN troubleshoot vs Connection troubleshoot: VPN troubleshoot = gateway problemen, Connection troubleshoot = VM bereikbaarheid
  - Diagnosevolgorde: Connection troubleshoot → Next hop → IP flow verify (DNS → Route → Security)

## Network Watcher Oefensessie Voortgang
| Sessie | Score | Fouten |
|---|---|---|
| Sessie 1 | 85% | NSG flow logs vs Effective security rules, Network topology vs Traffic Analytics |
| Sessie 2 | 85% | Connection troubleshoot vs IP flow verify, Traffic Analytics vs Network topology |
| Sessie 3 | 80% | Effective routes vs Traffic Analytics, Connection monitor vs NSG flow logs, Traffic Analytics resources, VPN troubleshoot vs Connection troubleshoot |
