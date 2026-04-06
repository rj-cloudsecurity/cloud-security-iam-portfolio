# SC-900 Exam Preparation
## Certification
  - Microsoft Certified: Security, Compliance, and Identity Fundamentals (SC‑900)
  - Result: In preparation
  - Date: TBD

## Study Method
  - Completing all Microsoft Learn modules
  - Watching the FreeCodeCamp SC‑900 course
  - Watching John Savill's Technical Training SC‑900
  - Creating detailed notes in [Full Notes](/02-sc900/notes/sc900-full-notes.md)
  - Building a product‑cluster overview in [Identity & Security Clusters](/02-sc900/notes/sc900-identity-security-clusters.md)
  - Practicing with custom AI-generated exams (claude.ai) based on official SC-900 exam objectives

## Practice Assessment Progression
| Platform | Score | Notes |
|----------|-------|-------|
| Custom practice exam 1 (Parts 1 & 2 — mid‑way baseline) | 82% | Parts 3 & 4 not yet studied. Triggered creation of the [Identity & Security Clusters](/02-sc900/notes/sc900-identity-security-clusters.md)|
| Custom practice exam 2 (Parts 1 & 2 — post study) | 90% | Retaken after creation of the clusters.|
| | | *Previous exams felt too easy. From this point: exam-level difficulty with harder questions and mixed question types.* |
| Custom practice exam 3 (All parts) | 85% | 34/40. Weakest: LP3 M5, LP2 M3.|
| Custom practice exam 4 (All parts) | 85% | 34/40. Correct topic distribution from this point. Weakest: LP2 M3, LP2 M4, LP4 M3.|
| Targeted retake — weak areas only (40 questions) | 92.5% | 37/40. Weakest: LP3 M3, LP3 M4, LP4 M3.|
| open-exam-prep.com (35 questions) | 96% | Questions significantly easier and more conceptual than custom exams. Exam appears outdated — several questions outside current SC-900 objectives.|
| Custom practice exam 6 (mixed question types & extra hard) | 90% | 72/80. First exam with all four question types: multiple choice, true/false, matching, drop-down. 3 lost points due to careless reading; morning exams recommended over late evening. Only real knowledge gap: FIDO2 vs OATH hardware token distinction. Weakest: LP2 M1, LP3 M5, LP1 M1.|
| Custom practice exam 7 (Microsoft-style, mixed question types) | 92% | 59/64. Weakest: LP2 M1 — SCIM, Verified ID; LP3 M4 — Sentinel automation rules vs playbooks; LP3 M5 — Defender Vulnerability Management vs Defender for Endpoint.|

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

## Next Focus Areas after targeted retake
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
