# SC-900 Exam Preparation
## Certification
  - Microsoft Certified: Security, Compliance, and Identity Fundamentals (SC‑900)
  - Result: Passed
  - Date: April 8, 2026

## Study Method
  - Completing all Microsoft Learn modules
  - Watching the FreeCodeCamp SC‑900 course
  - Watching John Savill's Technical Training SC‑900
  - Creating detailed notes in [Learn Notes](/02-sc900/notes/sc900-learn-notes.md)
  - Building a product‑cluster overview in [Identity & Security Clusters](/02-sc900/notes/sc900-identity-security-clusters.md)
  - Practicing with custom AI-generated exams (claude.ai) based on official SC-900 exam objectives
  - Practicing with the Official Microsoft Practice Assessment

## Practice Assessment Progression
| Platform | Score | Notes |
|----------|-------|-------|
| Exam 1 — Custom (Parts 1 & 2 — mid‑way baseline) | 82% | Parts 3 & 4 not yet studied. Triggered creation of the [Identity & Security Clusters](/02-sc900/notes/sc900-identity-security-clusters.md)|
| Exam 2 — Custom (Parts 1 & 2 — post study) | 90% | Retaken after creation of the clusters.|
| | | *Previous exams felt too easy. From this point: exam-level difficulty with harder questions and mixed question types.* |
| Exam 3 — Custom (All parts) | 85% | 34/40. Weakest: LP3 M5, LP2 M3.|
| Exam 4 — Custom (All parts) | 85% | 34/40. Correct topic distribution from this point. Weakest: LP2 M3, LP2 M4, LP4 M3.|
| Exam 5 — Custom targeted retake (weak areas only, 40 questions) | 92.5% | 37/40. Weakest: LP3 M3, LP3 M4, LP4 M3.|
| Exam 6 — Custom (mixed question types & extra hard) | 90% | 72/80. First exam with all four question types: multiple choice, true/false, matching, drop-down. 3 lost points due to careless reading; morning exams recommended over late evening. Only real knowledge gap: FIDO2 vs OATH hardware token distinction. Weakest: LP2 M1, LP3 M5, LP1 M1.|
| Exam 7 — Custom (Microsoft-style, mixed question types) | 90% | 47/52. Drop-down answers pre-filled due to widget issue — excluded from score. Weakest: LP2 M1 — SCIM, Verified ID; LP3 M4 — Sentinel automation rules vs playbooks; LP3 M5 — Defender Vulnerability Management vs Defender for Endpoint.|
| | | *Switching to the official Microsoft Learn practice assessment. After 1st attempt, incorrect answers were studied and weak areas retested with custom AI-generated Exam 9.* |
| Exam 8 — Microsoft Learn official practice assessment (1st attempt) | 82% | Gaps: LP2 M1, LP1 M1, LP3 M5, LP4 M1, LP4 M2.|
| Exam 9 — Custom targeted retake on exam 8 gaps | 88% | Focused on weak areas from exam 8. Remaining gaps: LP3 M2 — NSG priority order, LP1 M1 — SOAR characteristics, LP3 M5 — CASB four pillars, LP2 M4 — user risk vs sign-in risk.|
| Exam 10 — Microsoft Learn official practice assessment (2nd attempt) | 98% | 49/50. Only gap: LP4 M3 — Audit Premium vs eDiscovery (investigate based on records = Audit Premium).|

## Study Approach
  - Reviewed incorrect answers and grouped them by topic
  - Developed identity and security clusters to better distinguish similar products
  - Focused on risk‑based access, identity governance, and product comparisons

## Next Focus Areas after exam 3
  - LP2 M3 — Azure RBAC vs Microsoft Entra roles: when each applies
  - LP3 M5 — Defender product line distinctions (scenario-based questions)
  - LP3 M5 — Defender for Identity vs Defender for Cloud Apps vs Defender for Endpoint
  - LP3 M5 — Defender for Endpoint Plan 1 vs Plan 2 feature differences

## Next Focus Areas after exam 4
  - LP2 M2 — Password Protection: on-premises hybrid deployment with proxy and DC agents
  - LP2 M3 — Conditional Access: break-glass account exclusions and workload identity scope
  - LP2 M4 — PIM for Groups: just-in-time access to non-Microsoft applications via group membership
  - LP4 M3 — eDiscovery: Standard vs Premium feature boundaries (review sets are Premium-only)

## Next Focus Areas after exam 5
  - LP3 M3 — CSPM vs CWPP: misconfigurations and Secure Score = CSPM; active runtime threats = CWPP
  - LP3 M4 — Sentinel: analytics rule detects → automation rule triggers → playbook executes (all three required)
  - LP4 M2 — DLP vs Communication Compliance: DLP blocks data; Communication Compliance routes to human reviewer

## Next Focus Areas after exam 6
  - LP2 M1 — Authentication methods: FIDO2 = phishing-resistant hardware key (USB/NFC); OATH hardware token = physical device generating time-based OTP every 30-60 seconds

## Next Focus Areas after exam 7
  - LP2 M1 — Microsoft Entra Verified ID: cryptographically signed credentials stored in digital wallet using did:web trust system
  - LP2 M1 — SCIM: standard protocol for automated identity provisioning and deprovisioning across systems
  - LP3 M4 — Sentinel: automation rules trigger playbooks; playbooks execute the actual response actions — "execute" always = playbook
  - LP3 M5 — Defender Vulnerability Management = CVEs and misconfigurations; Defender for Endpoint = EDR for active threats

## Next Focus Areas after exam 8
  - LP2 M1 — Service principal vs managed identity: service principal = identity for any registered application; managed identity = credential-free service principal for Azure resources only
  - LP1 M1 — SIEM vs SOAR: SIEM = collect and correlate data; SOAR = action-driven workflows and issue mitigation
  - LP3 M5 — ASR vs AIR: ASR = blocks malicious URLs and IPs before execution; AIR = automatically investigates after detection
  - LP3 M5 — Defender XDR = unified detection across endpoints, identities, email AND applications; single Defender products cover only one domain
  - LP4 M1 — Microsoft privacy principles: security principle = encryption and key management; control principle = customer owns their data
  - LP4 M2 — Microsoft Purview portal = home for all compliance solutions: Communication Compliance, eDiscovery, Audit, DLP, Insider Risk Management, Compliance Manager
  - LP4 M3 — Audit Premium vs eDiscovery: investigate breaches based on records = Audit Premium; collect documents as evidence = eDiscovery
