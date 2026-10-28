# SC-300 Hands-on Review

Focus: not *which* feature, but *where* and *how* it is configured. Each item comes from a practice exam question: perform it in the portal (Microsoft Entra admin center, Microsoft 365 admin center, Microsoft Defender portal or PowerShell), write down the menu path, and mark it Done.

The topics follow the SC-300 skills measured, not the order of an exam. The "Scenario and task" column summarizes what the question asked and what to do in the portal. The Dojo column shows where it came from: Exam 1 = Tutorials Dojo Practice Exam 1 (category and question number), Random = Tutorials Dojo Randomized Test (question number). A dash means the topic comes from a custom exam.

## 1. Tenant, roles, users and groups
| Topic | Dojo question | Scenario and task | Where in the portal | Status |
|-------|---------------|-------------------|---------------------|--------|
| Role scoped to an administrative unit | Exam 1: Users #1 | Liza is Password Administrator for the whole organization, Ramon only for AU-HR. Create an AU, add users, assign the role scoped to the AU, and test who can reset which user's password. | Entra ID > Administrative units > [AU] > Roles and administrators > Password Administrator > Add assignments | Done |
| Group-based licensing | Exam 1: Governance #1 | Assign E5 to a group of all employees and remove the old E3 licenses. Do it in the portal and with `Set-MgGroupLicense`. | M365 admin center > Billing > Licenses > [licentie] > Groups (of Set-MgGroupLicense) | Done |
| Bulk remove direct licenses | Exam 1: Users #2 | Users have E3 assigned directly while the group gives E5. Remove the direct E3 assignments in bulk. | M365 admin center > Billing > Licenses > [licentie] > Users > selecteer users > Unassign licenses | Done |
| Restore a deleted user | Exam 1: Governance #5 | A user was deleted. Restore the account. Note the time limit and the minimum role. | Entra ID > Users > Deleted users > selecteer user > Restore user | Done |
| Custom security attributes | Random: #38 | Create an attribute set and attributes, assign Attribute Definition Administrator on one set, and check what a Global Administrator can and cannot see. | Entra admin center > Entra ID > Custom security attributes | Done |
| Restrict self-service sign-up | Exam 1: Users #13 | Only allow accounts with the verified SMTP domains. | PowerShell only: `Set-MsolCompanySettings` (geen portal-instelling) | Done |

## 2. External identities and hybrid identity
| Topic | Dojo question | Scenario and task | Where in the portal | Status |
|-------|---------------|-------------------|---------------------|--------|
| Invite a guest with PowerShell | Exam 1: Users #4 | A guest signs in with a personal address and must reach an enterprise app. Send the invitation with `New-AzureADMSInvitation`. | | |
| Cross-tenant app-to-app access | Exam 1: Users #3 | An app in one tenant must call an app in a partner tenant. Create a credential (certificate or secret) on the app registration and check why a managed identity doesn't work across tenants. | Entra admin center > Entra ID > App registrations > [app] > Certificates & secrets > New client secret | Done |
| Exclude users from Connect Sync by attribute | Exam 1: Users #11 | Do not sync users with `extensionAttribute15 = NoSync`. Create the inbound rule on the AD DS connector with a scoping filter. | | Skipped |
| Pass-through authentication and lockout | Exam 1: Auth #1 | On-prem lockout policy must apply to cloud sign-ins. Check the PTA setting and compare it with password hash sync and smart lockout. | | Skipped |

## 3. Authentication, Conditional Access and Global Secure Access
| Topic | Dojo question | Scenario and task | Where in the portal | Status |
|-------|---------------|-------------------|---------------------|--------|
| SSPR authentication methods | Exam 1: Auth #5, Random: #50 | Require 1 method, then 2 methods. Check which methods are available each time (mobile app code, e-mail, notification). | Entra ID > Password reset > Authentication methods (aantal methoden) en Entra ID > Authentication methods > Policies (welke methoden)	 | Done |
| Block legacy authentication | Exam 1: Auth #11 | Create a Conditional Access policy that blocks legacy authentication clients. | ntra ID > Conditional Access > Policies > New policy > Conditions > Client apps | Done |
| Global Secure Access web filtering | Exam 1: Auth #3 | Block social media for the Marketing group during business hours. Find the first step before the Conditional Access policy. | | |
| Global Secure Access: compliant network | — | Enable Conditional Access signaling and use the compliant network location in a policy. | | |
| Terms of use | Random: #12, #43 | Create a ToU (PDF), require it through Conditional Access, and find who accepted or declined in the logs. | | |

## 4. Applications and workload identities
| Topic | Dojo question | Scenario and task | Where in the portal | Status |
|-------|---------------|-------------------|---------------------|--------|
| Application Developer role | Exam 1: Users #9, Random: #11 | A developer must register apps while "Users can register applications" is No. Assign the role and test what the developer can and cannot do. | | |
| Daemon app to Microsoft Graph | Exam 1: Users #12 | Register the app, add Graph application permissions, grant admin consent. | | |
| Admin consent workflow | Exam 1: Governance #13 | Set reviewers and see who can approve a request. | | |
| User consent settings | — | Allow consent only for verified publishers and selected permissions. | | |
| SSO plus Conditional Access on device state | Exam 1: Auth #2 | A gallery app must use SSO and only be reachable from Entra-joined devices. | | |
| User provisioning to a SaaS app (SCIM) | Exam 1: Governance #8 | Set up automatic provisioning to a SaaS app. | Entra ID > Enterprise applications > [app] > Provisioning > Automatic (Tenant URL + Secret token) | |
| Defender for Cloud Apps session control: first steps | Exam 1: Governance #12, Random: #1, #42, #49 | Third-party or SharePoint app, block downloads. Do the steps in order: SSO if needed, Conditional Access with Use Conditional Access App Control, then the session policy. | | |
| Activity policy | Exam 1: Workload #4 | Alert on mass downloads or repeated deletions in a sanctioned app. | | |
| App governance | Exam 1: Auth #9 | Give a user access to the dashboard with the least privilege and find where it is. | | |
| Key Vault with Azure RBAC | Random: #26 | Check which role can read secret values at subscription, resource group or vault scope. | | |

## 5. Identity governance and privileged access
| Topic | Dojo question | Scenario and task | Where in the portal | Status |
|-------|---------------|-------------------|---------------------|--------|
| Entitlement management settings | Exam 1: Governance #9 | Remove external users automatically after 90 days. | Identity Governance > Entitlement management > Control configurations | |
| Access package with expiration | Exam 1: Governance #14 | Give a group time-limited access (90 days) to a SharePoint site. | | |
| Access review of a group with guests | Exam 1: Governance #15 | Review guest access monthly. Check whether failed guests can be blocked from signing in. | Identity Governance > Access reviews > New access review > Teams + Groups > Upon completion settings | |
| What an access review can cover | Random: #48 | Create reviews for a group, an enterprise app, an Entra role and a service principal. Note the license needs. | | |
| PIM scope | Random: #27 | Check which roles PIM can manage and which it cannot (classic administrator and billing roles). | | |

## 6. Monitoring
| Topic | Dojo question | Scenario and task | Where in the portal | Status |
|-------|---------------|-------------------|---------------------|--------|
| Diagnostic settings to Log Analytics | Exam 1: Governance #7, Random: #5, #16 | Send Entra audit logs to a Log Analytics workspace. This is always the first step. | | |
