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
| Tutorials Dojo Timed Mode Set 4 | 73% | 61/83. Weakest: Networking 63%, Storage 71%, Governance 76%. |
| Tutorials Dojo Timed Mode Set 2 | 79% | 54/68. Weakest: Compute 64%, Networking 64%. Fouten: proximity placement group regio, Bicep scope, DSC vs Custom Script, ACR Tasks. |
| Tutorials Dojo Timed Mode Set 3 | 86% | 63/73. Weakest: Monitor 75%, Governance 81%, Compute 80%. Fouten: P2S VPN gateway type, policy exclusion, Logic App Operator rol, ConvertTo-Json, managed identities ontvangen geen email. |

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
Answers tend to be confused between two options that look similar. Modify vs Append. Network Watcher vs Azure Monitor. ACA vs App Service. Session persistence vs five-tuple hash. The pattern is always two answers that both sound logical but differ on one specific detail.
**Strongest areas:**
Storage is now solid — Exam 5 had zero storage errors. Identity fundamentals are also strong: SSPR, RBAC roles, groups, and licensing are consistently correct.
**Recurring weak areas to focus on:**
Containers (ACI vs ACA vs App Service) and Networking are the two domains costing the most points and are heavily represented on the real exam.

## Next Focus Areas after Exam 6
  - LP1 M2 — ARM templates: subscription scope for multi-resource group deployments (recurring third time)
  - LP4 M2 — Availability: availability zone for datacenter failure protection; availability set for rack failure only

## Recurring Patterns and Observations after Exam 6
**Improvements since Exam 5:**
Containers (ACI vs ACA vs App Service) fully resolved — zero errors in Exam 6. Networking errors eliminated. Monitor & Backup zero errors. Storage zero errors for second consecutive exam.
**Consistent error pattern:**
ARM template deployment scope remains the single most persistent gap. Availability zone vs availability set is a second recurring gap.
**Progress trend:**
46% (baseline) → 73–94% (custom exams).

## Next Focus Areas after Exam 7
  - LP4 M3 — App Service: scale up to Standard/Premium before autoscale can be configured
  - LP4 M4 — App Service: Publish → Docker Container for container images, not Runtime stack
  - LP4 M5 — Containers: event-driven trigger for Service Bus scaling in ACA, not HTTP (recurring)
  - LP5 M1 — Networking: NSG must be in same region as the subnet it is associated with
  - LP5 M2 — DNS: Azure Private DNS zone for multiple VNets with custom domain; Azure-provided only supports single VNet
  - LP6 M2 — Monitoring: summarize operator for aggregation in KQL; alert state is always manually set

## Recurring Patterns and Observations after Exam 7
**Improvements since Exam 6:**
Identity & Governance zero errors. Storage improving. ARM template scope no longer an issue.
**Consistent error pattern:**
Compute (LP4) is now the single weakest domain — errors concentrated in UI/configuration details rather than deep technical concepts.
**Progress trend:**
46% → 60% → 70% on official Microsoft assessments.

## Next Focus Areas after Exam 8
  - LP4 M2 — Compute: VM Scale Set configured under Availability options, not Management
  - LP4 M3 — App Service: scale up = bigger tier; scale out = more instances; Basic does not support autoscale
  - LP4 M4 — App Service: Application Logging Blob for retention over 7 days; Warning severity includes Warning/Error/Critical only; Verbose = most detailed level
  - LP4 M5 — Containers: ACI for short isolated tasks (recurring fourth time)
  - LP5 M2 — DNS: virtual network link required for private DNS zone registration (recurring)
  - LP6 M3 — Backup: Site Recovery failover status must be Failover committed before reprotection

## Recurring Patterns and Observations after Exam 8
**Improvements since Exam 7:**
Networking DNS improving. Storage zero errors. Identity zero errors consistently.
**Consistent error pattern:**
LP4 Compute remains the most persistent weak domain across all exams.
**Progress trend:**
46% → 60% → 70% on official Microsoft assessments.

## Next Focus Areas after Exam 9
  - LP5 M1 — Networking: effective routes on NIC to verify peering routing path, not Network Watcher next hop (recurring)
  - LP5 M1 — Networking: NSG associates with subnets and NICs only — not VNets; NSG must be same region as subnet
  - LP6 M2 — Monitoring: action group must be created first before alert processing rules; action group defines notification target
  - LP6 M3 — Backup: vault credentials must be downloaded and server registered before backup policy can be configured
  - LP6 M3 — Backup: Site Recovery failover status must be Failover committed before reprotection (recurring)

## Recurring Patterns and Observations after Exam 9
**Improvements since Exam 8:**
Compute errors significantly reduced. Containers correct. Identity & Governance zero errors. Storage zero errors.
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
**Improvements since Exam 9:**
Monitor & Backup significantly improved. Identity & Governance zero errors. Storage zero errors. Networking routing diagnostics now correct.
**Consistent error pattern:**
LP4 M5 Containers remains the single most persistent error across all exams.
**Progress trend:**
46% → 60% → 70% → 80% → 88% on official Microsoft assessments.

## Next Focus Areas after Exam 11
  - LP3 M2 — Storage: Data Lake Gen2 requires premium block blobs or standard GPv2 — premium file shares not supported (recurring)
  - LP4 M4 — App Service: Application Logging Blob required for warnings or higher — not Detailed Error Message (recurring)
  - LP5 M3 — Load balancer: session persistence requires Client IP AND Protocol together; IP flow verify for NSG troubleshooting, not VNet flow logs
  - LP6 M2 — Monitoring: alert rule detects event + action group sends notification; alert processing rule is not a notification mechanism; budget settings must be modified to link action group to cost threshold

## Recurring Patterns and Observations after Exam 11
**Improvements since Exam 10:**
Containers resolved — App Service vs ACI now consistently correct. Networking port numbers correct. MARS vs MABS correct. NSG region constraints correct.
**Consistent error pattern:**
Errors now concentrated in subtle configuration details: which specific logging type to enable, when to use IP flow verify vs flow logs, and the distinction between alert rule, action group, and alert processing rule.
**Progress trend:**
46% → 60% → 70% → 80% → 88% → 90% on official Microsoft assessments.

## Next Focus Areas — Tutorials Dojo Timed Mode
  - Networking: P2S VPN vereist route-based gateway — policy-based wordt niet ondersteund; delete policy-based en deploy route-based
  - Governance: Azure policy exclusion — uitgesloten resource group is toegestaan, niet geblokkeerd
  - Governance: Logic App Operator rol = alleen lezen/inschakelen, niet aanmaken; gebruik Contributor
  - Governance: Get-AzRoleDefinition | ConvertTo-Json voor custom role definitie ophalen
  - Monitor: Email Azure Resource Manager Role — alleen users ontvangen email, managed identities niet
  - Compute: Proximity placement group + scale set moeten in dezelfde regio zitten
  - Compute: Bicep scope = waar resources worden gedeployed (resource group); niet location
  - Compute: DSC extension = consistent + compliance; Custom Script Extension = eenmalig bij deployment
  - Compute: ACR Tasks = automatisch rebuilden bij base image update; niet multi-step tasks
  - Backup: RSV verwijderen = eerst backup stoppen per item, dan pas data verwijderen

## Recurring Patterns and Observations — Tutorials Dojo
**Scores:**
Section-based scores hoog (83–100%). Timed mode scores lager (73–86%) deels door herkende vragen.
**Consistent error pattern:**
Volgordevragen en "welk tool voor welk doel" blijven moeilijk. Specifieke PowerShell cmdlets (ConvertTo-Json vs ConvertFrom-Json, Get-AzRoleDefinition vs Get-AzRoleAssignment). Policy exclusion logica (uitgesloten = toegestaan, niet geblokkeerd).
**Progress trend:**
46% → 60% → 70% → 80% → 88% → 90% on official Microsoft assessments. Tutorials Dojo Timed Mode: 73% → 79% → 86%.# AZ-104 Exam Preparation
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
## Next Focus Areas after Exam 11
  - LP3 M2 — Storage: Data Lake Gen2 requires premium block blobs or standard GPv2 — premium file shares not supported (recurring)
  - LP4 M4 — App Service: Application Logging Blob required for warnings or higher — not Detailed Error Message (recurring)
  - LP5 M3 — Load balancer: session persistence requires Client IP AND Protocol together; IP flow verify for NSG troubleshooting, not VNet flow logs
  - LP6 M2 — Monitoring: alert rule detects event + action group sends notification; alert processing rule is not a notification mechanism; budget settings must be modified to link action group to cost threshold
## Recurring Patterns and Observations after Exam 11
**Improvements since Exam 10:**
Containers resolved — App Service vs ACI now consistently correct. Networking port numbers correct. MARS vs MABS correct. NSG region constraints correct.
**Consistent error pattern:**
Errors now concentrated in subtle configuration details: which specific logging type to enable, when to use IP flow verify vs flow logs, and the distinction between alert rule, action group, and alert processing rule.
**Tutorials Dojo Timed Mode observations:**
Veel vragen al eerder gezien — scores zijn hierdoor minder betrouwbaar als indicator. Nieuwe fouten: P2S vereist route-based gateway (policy-based werkt niet), Azure policy exclusion (uitgesloten RG = wel toegestaan), managed identities ontvangen geen email notificaties, ConvertTo-Json voor custom role definitie ophalen.
**Progress trend:**
46% → 60% → 70% → 80% → 88% → 90% on official Microsoft assessments.
