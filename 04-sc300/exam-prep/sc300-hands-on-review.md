# SC-300 Hands-on Review

Focus: not "which feature", but where and how it is configured. For every mistake from the practice exams: perform it in the portal (Microsoft Entra admin center, Microsoft Defender portal, PowerShell), write down the menu path, and mark it Done.

The Dojo column shows the question number within its category in Tutorials Dojo Practice Exam 1 (Test 7), under Your Progress. The order follows that page. A dash means the topic comes from a custom exam.

## Implement and Manage User Identities
| Topic | Dojo question | Where in the portal | Status |
|-------|---------------|---------------------|--------|
| Password Administrator scoped to an administrative unit | Q1 | | |
| Bulk remove direct license assignments (Licenses blade) | Q2 | | |
| Cross-tenant app-to-app access: certificate and secret | Q3 | | |
| Invite a guest with PowerShell (`New-AzureADMSInvitation`) | Q4 | | |
| Application Developer role: register apps when users cannot | Q9 | | |
| Connect Sync: exclude users by attribute (inbound rule on the AD DS connector) | Q11 | | |
| Daemon app to Microsoft Graph: register app, assign permissions, grant admin consent | Q12 | | |
| Restrict self-service sign-up to verified domains (`Set-MsolCompanySettings`) | Q13 | PowerShell only: `Set-MsolCompanySettings` (geen portal-instelling) | |

## Implement Authentication and Access Management
| Topic | Dojo question | Where in the portal | Status |
|-------|---------------|---------------------|--------|
| Pass-through authentication: on-premises lockout policy applies to cloud sign-ins | Q1 | | |
| Enterprise application SSO plus Conditional Access on device state | Q2 | | |
| SSPR: authentication methods and number of methods required | Q5 | | |
| App governance dashboard (role and portal) | Q9 | | |
| Conditional Access: Client apps (block legacy authentication) | Q11 | | |
| Global Secure Access: Conditional Access signaling and compliant network location | — | | |

## Plan and Automate Identity Governance
| Topic | Dojo question | Where in the portal | Status |
|-------|---------------|---------------------|--------|
| Group-based licensing: license assigned to a group, old license removed (`Set-MgGroupLicense`) | Q1 | M365 admin center > Billing > Licenses > [licentie] > Groups (of Set-MgGroupLicense) | |
| Restore a deleted user (30 days) | Q5 | | |
| Diagnostic settings: Entra audit logs to a Log Analytics workspace | Q7 | | |
| User provisioning to a SaaS app (SCIM) | Q8 | Entra ID > Enterprise applications > [app] > Provisioning > Automatic (Tenant URL + Secret token) | |
| Entitlement management settings: automatic removal of external users | Q9 | Identity Governance > Entitlement management > Control configurations | |
| SaaS app with Defender for Cloud Apps session control: SSO first | Q12 | | |
| Admin consent workflow: reviewers and approval | Q13 | | |
| Access package with expiration in the policy | Q14 | | |
| Access review of a group with guests (twijfelachtige Dojo-key: bij "blokkeren" past guest review met auto-apply Block sign-in) | Q15 | Identity Governance > Access reviews > New access review > Teams + Groups > Upon completion settings | |

## Plan and Implement Workload Identities
| Topic | Dojo question | Where in the portal | Status |
|-------|---------------|---------------------|--------|
| Defender for Cloud Apps: activity policy | Q4 | | |
| User consent settings (verified publishers, selected permissions) | — | | |
