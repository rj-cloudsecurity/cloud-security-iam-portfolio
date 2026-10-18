# SC-300 Hands-on Review

Focus: not "which feature", but where and how it is configured. For every mistake from the practice exams: perform it in the portal (Microsoft Entra admin center, Microsoft Defender portal, PowerShell), write down the menu path, and mark it Done.

The Dojo column shows the question number in Tutorials Dojo Practice Exam 1 (Test 7). A dash means the topic comes from a custom exam.

## Domain 1 — Implement and manage user identities
| Topic | Dojo question | Where in the portal | Status |
|-------|---------------|---------------------|--------|
| Group-based licensing: license assigned to a group, old license removed (`Set-MgGroupLicense`) | Q1 | M365 admin center > Billing > Licenses > [licentie] > Groups (of Set-MgGroupLicense) | Done |
| Restrict self-service sign-up to verified domains (`Set-MsolCompanySettings`) | Q5 | PowerShell only: `Set-MsolCompanySettings` (geen portal-instelling) | Done |
| Connect Sync: exclude users by attribute (inbound rule on the AD DS connector) | Q14 | | Todo |
| Password Administrator scoped to an administrative unit | Q18 | | Todo |
| Bulk remove direct license assignments (Licenses blade) | Q35 | | Todo |
| Restore a deleted user (30 days) | Q37 | | Todo |
| Invite a guest with PowerShell (`New-AzureADMSInvitation`) | Q40 | | Todo |
| Pass-through authentication: on-premises lockout policy applies to cloud sign-ins | Q50 | | Todo |

## Domain 2 — Implement authentication and access management
| Topic | Dojo question | Where in the portal | Status |
|-------|---------------|---------------------|--------|
| SSPR: authentication methods and number of methods required | Q17 | | Todo |
| Conditional Access: Client apps (block legacy authentication) | Q41 | | Todo |
| Global Secure Access: Conditional Access signaling and compliant network location | — | | Todo |

## Domain 3 — Plan and implement workload identities
| Topic | Dojo question | Where in the portal | Status |
|-------|---------------|---------------------|--------|
| User provisioning to a SaaS app (SCIM) | Q10 | Entra ID > Enterprise applications > [app] > Provisioning > Automatic (Tenant URL + Secret token) | Todo |
| Application Developer role: register apps when users cannot | Q16 | | Todo |
| Daemon app to Microsoft Graph: register app, assign permissions, grant admin consent | Q20 | | Todo |
| Admin consent workflow: reviewers and approval | Q21 | | Todo |
| Enterprise application SSO plus Conditional Access on device state | Q22 | | Todo |
| Defender for Cloud Apps: activity policy | Q26 | | Todo |
| Cross-tenant app-to-app access: certificate and secret | Q27 | | Todo |
| App governance dashboard (role and portal) | Q34 | | Todo |
| SaaS app with Defender for Cloud Apps session control: SSO first | Q39 | | Todo |
| User consent settings (verified publishers, selected permissions) | — | | Todo |

## Domain 4 — Plan and automate identity governance
| Topic | Dojo question | Where in the portal | Status |
|-------|---------------|---------------------|--------|
| Entitlement management settings: automatic removal of external users | Q4 | Identity Governance > Entitlement management > Control configurations | Done |
| Access review of a group with guests (twijfelachtige Dojo-key: bij "blokkeren" past guest review met auto-apply Block sign-in) | Q8 | Identity Governance > Access reviews > New access review > Teams + Groups > Upon completion settings | Todo |
| Access package with expiration in the policy | Q33 | | Todo |
| Diagnostic settings: Entra audit logs to a Log Analytics workspace | Q48 | | Todo |
