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
