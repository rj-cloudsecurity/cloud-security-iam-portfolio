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
ARM template deployment scope remains the single most persistent gap — appearing after Exams 2, 4, 5, and 6. Availability zone vs availability set is a second recurring gap. Both involve choosing between two options that are close but differ on one specific scope or protection level detail.


