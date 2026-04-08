# SC-900 — Last Push Study Notes

This document summarizes the topics I got wrong most often, had recurring doubts about, or consistently second-guessed across all practice exams. Read this the morning before the real exam. Focus on the exam-style traps section; those cost the most points not because of missing knowledge but because of subtle wording.

---

## 1. Sentinel — three components, three roles

| Component | Role | Key word |
|---|---|---|
| Analytics rules | Detects threats and creates incidents | detect |
| Automation rules | Determines WHEN playbooks are triggered | orchestrate / trigger |
| Playbooks | EXECUTES response actions via Azure Logic Apps | execute / perform |

**Exam trap:** "execute the actual response actions" → always Playbooks, never Automation rules.

---

## 2. eDiscovery Standard vs Premium

| Feature | Standard | Premium |
|---|---|---|
| Search | ✓ | ✓ |
| Holds | ✓ | ✓ |
| Export | ✓ | ✓ |
| Review sets | ✗ | ✓ |
| Conversation threading | ✗ | ✓ |
| Near-duplicate detection | ✗ | ✓ |
| OCR | ✗ | ✓ |

**Remember:** If the question mentions review sets, threading, or analytics → always Premium.

---

## 3. Audit Standard vs Premium

| Feature | Standard | Premium |
|---|---|---|
| Retention | 180 days | 1 year (10 years with add-on) |
| MailItemsAccessed | ✗ | ✓ |
| SharePoint search query logging | ✗ | ✓ |
| Higher API bandwidth | ✗ | ✓ |

**Remember:** Forensic investigation into mailbox access or search queries → always Audit Premium.

**Remember:** "investigate possible security or compliance breaches based on records" → Audit Premium, not eDiscovery. eDiscovery collects documents. Audit Premium investigates activity via logs.

---

## 4. License tiers P1 vs P2

| Feature | License |
|---|---|
| Conditional Access | P1 |
| SSPR | P1 |
| Custom banned password list | P1 |
| Custom roles | P1 |
| PIM | **P2** |
| Identity Protection | **P2** |
| Entitlement Management / Access packages | **P2** |
| Access Reviews | **P2** |

**Rule of thumb:** Everything involving just-in-time access, risk detection, or governance = P2.

---

## 5. Purview solutions — choosing the right product

| Situation | Solution |
|---|---|
| Block data from leaving the organization | DLP |
| Route flagged messages to a human reviewer | Communication Compliance |
| Detect risky employee behavior | Insider Risk Management |
| Collect documents for a legal case or audit | eDiscovery |
| Investigate breaches based on activity records | Audit Premium |
| Improve compliance score | Compliance Manager |
| Classify and encrypt sensitive data | Sensitivity Labels |
| See where sensitive data is stored | Content Explorer |
| Retain mailbox and file data for a required period | Data Lifecycle Management |
| Identify invoice numbers or known data patterns | Sensitive Information Types (SITs) |

**Remember:** Microsoft Purview portal = home for ALL compliance solutions: Communication Compliance, eDiscovery, Audit, DLP, Insider Risk Management, Compliance Manager. Not Defender portal, not Entra admin center.

**Remember:** Compliance Manager = measures and improves compliance posture via score. eDiscovery = collects documents. Audit Premium = investigates activity via records/logs.

---

## 6. Defender products — what they protect

| Product | Scope | Key words |
|---|---|---|
| Defender for Identity | On-premises Active Directory | lateral movement, credential theft |
| Defender for Endpoint | Laptops, phones, servers | EDR, ASR |
| Defender Vulnerability Management | CVEs and misconfigurations | CVE, misconfiguration |
| Defender for Cloud | Azure workloads, AWS, GCP | CSPM, CWPP, Secure Score, multi-cloud |
| Defender for Cloud Apps | SaaS applications | CASB, shadow IT |
| Defender for Office 365 | Email and Teams | phishing, Safe Links, ZAP |
| **Defender XDR** | **Unified across endpoints, identities, email AND applications** | **unified, cross-domain** |

**Remember:** Misconfigurations are vulnerabilities → Vulnerability Management, not Endpoint.

**Remember:** If the question asks for unified detection across ALL domains (endpoints + identities + email + apps) → always Defender XDR, never a single Defender product.

**Remember:** Multi-cloud security management including AWS and GCP → Defender for Cloud, not Sentinel or Purview.

**Remember:** Enabling the Defender for Servers plan is done via Defender for Cloud — not Defender for Endpoint, even though servers are technically endpoints.

---

## 7. Azure network — key words

- **SNAT** → Azure Firewall
- **SSL termination** → WAF
- **Distributed filtering within VNet** → NSG
- **Network segmentation per department** → VNet (not VPN)
- **VPN** = connects two networks together, not segmentation within Azure
- **NSG rule processing** = lowest priority number processed first (65000 before 65001 before 65500); processing stops at first matching rule

---

## 8. Sentinel vs Defender for Cloud vs Defender XDR

- **Microsoft Sentinel** = SIEM + SOAR, collects from everywhere, cloud-native
- **Defender for Cloud** = CSPM (posture + Secure Score) + CWPP (runtime workload protection), focused on Azure and cloud
- **Defender XDR** = unified portal combining all Defender products

---

## 9. SIEM vs SOAR

| | SIEM | SOAR |
|---|---|---|
| Function | Collect and correlate security data | Action-driven workflows and issue mitigation |
| Key words | collection, correlation | automated response, remediation |

**Remember:** Collection and correlation = SIEM. Action-driven workflows and issue mitigation = SOAR.

---

## 10. Identity types — service principal vs managed identity

- **Service principal** = identity for any registered application in Entra ID; credentials must be managed manually
- **Managed identity** = credential-free service principal for Azure resources only; credentials managed automatically by Microsoft

"allow an Azure VM to access storage without handling credentials" → managed identity. "Identity for an application" → service principal.

---

## 11. Microsoft privacy principles — which principle covers what

| Principle | What it covers |
|---|---|
| Control | Customers are in control of their own data |
| Transparency | Microsoft informs how data is used and accessed |
| **Security** | **Encryption and key management** |
| Strong legal protections | Government data requests go to the customer, not Microsoft |
| No content-based targeting | Data is not used for advertising |
| Benefits to you | Data is used to improve your experience |

"defines use and management of encryption keys" → Security, not Control.

---

## 12. Sign-in risk vs user risk

| | Sign-in risk | User risk |
|---|---|---|
| What it flags | A specific authentication attempt looks suspicious | The identity itself may be compromised |
| Examples | Anonymous IP, atypical travel, unfamiliar sign-in properties | Leaked credentials, suspicious sending patterns, user reported activity |
| Key question | Is this login attempt suspicious? | Is this account compromised? |

**Remember:** Atypical travel = sign-in risk. Leaked credentials = user risk.

---

## 13. CASB — four pillars

The four pillars of a Cloud Access Security Broker are: **visibility, compliance, data security, and threat protection.**

**Exam trap:** "platform security" is NOT a CASB pillar — threat protection is.

---

## 14. Microsoft Entra RBAC vs Azure RBAC

| | Microsoft Entra RBAC | Azure RBAC |
|---|---|---|
| Controls access to | Entra ID resources: users, groups, applications | Azure resources: VMs, storage, databases |
| Example roles | Global Administrator, User Administrator | Owner, Contributor, Reader |

**Remember:** Users/groups/apps → Entra RBAC. VMs/storage/subscriptions → Azure RBAC.

---

## 15. Security baselines vs Azure Security Benchmark

- **Azure Security Benchmark** = the framework of security recommendations based on CIS and NIST
- **Security baselines** = apply Azure Security Benchmark guidance to a specific service such as Microsoft Entra or Azure Storage

"apply guidance from the Azure Security Benchmark to a specific service" → Security baselines, not Sentinel, not Purview.

---

## 16. Microsoft Defender for Cloud — enhanced security features

Enhanced security (paid tier) includes: EDR via Defender for Servers, vulnerability scanning for VMs and SQL resources, adaptive application controls, file integrity monitoring.

**Remember:** SIEM correlation = Microsoft Sentinel, not Defender for Cloud. Azure Security Benchmark recommendations = free CSPM tier, not enhanced security.

---

## 17. Edge knowledge Microsoft tests

- **Verified ID** → cryptographically signed credentials stored in a digital wallet (did:web trust system)
- **SCIM** → standard protocol for automated identity provisioning and deprovisioning
- **Honeytoken** → fake accounts used as bait in Defender for Identity to detect reconnaissance
- **ASR vs AIR** → ASR blocks malicious URLs and IPs before execution; AIR automatically investigates after detection
- **Defender for Office 365 Plan 2 only** → Attack simulation training, Threat Explorer, Campaign views
- **Microsoft Entra Password Protection** = covers both global and custom banned password lists; for org-specific names always answer "Microsoft Entra Password Protection"
- **Azure Security Benchmark frameworks** → CIS and NIST
- **Microsoft Secure Score** = provides recommendations for Microsoft 365, Microsoft Entra, Defender for Endpoint, Defender for Identity, Defender for Cloud Apps, and Teams — NOT Azure SQL Database or Cosmos DB

---

## 18. Exam-style traps — wording matters

| If you see this | Answer |
|---|---|
| "execute the actual response actions" | Playbooks — not automation rules |
| "guarantees legal compliance" | FALSE — a score is not a legal certification |
| "always", "never", "only", "guarantees" | Almost always signals a FALSE statement |
| "network segmentation per department" | VNet — not VPN |
| "container label protects all files inside" | FALSE — container labels do not propagate to files |
| "Security Reader can access Purview portal" | FALSE — Security Reader is a Defender portal role |
| "PIM is included in P1" | FALSE — PIM requires P2 |
| "SMS is the most secure MFA method" | FALSE — SMS is the least secure MFA method |
| "defines use of encryption keys" | Security principle — not Control |
| "unified detection across endpoints, identities, email and apps" | Defender XDR — not a single Defender product |
| "investigate breaches based on records" | Audit Premium — not eDiscovery |
| "identify documents for a compliance audit" | eDiscovery — not Compliance Manager |
| "platform security as a CASB pillar" | FALSE — the fourth pillar is threat protection |
| "atypical travel is a user risk" | FALSE — atypical travel is a sign-in risk |
| "NSG highest priority number processed first" | FALSE — lowest number is processed first |
| "enable Defender for Servers from Defender for Endpoint" | FALSE — enable from Defender for Cloud |
