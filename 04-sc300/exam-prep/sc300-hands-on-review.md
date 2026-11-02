# SC-300 Hands-on Review

Each item comes from a practice exam question. The focus is not on which feature is the answer, but on where and how it is configured: I perform the scenario in the portal (Microsoft Entra admin center, Microsoft 365 admin center, Microsoft Defender portal or PowerShell) and write down the menu path.

The topics follow the SC-300 skills measured, not the order of an exam. The columns mean:

- **Dojo question:** where the item came from. Exam 1 = Tutorials Dojo Practice Exam 1 (category and question number), Random = Tutorials Dojo Randomized Test (question number), Random 16 = Randomized Test 16 (category and question number), Diagnostic = Tutorials Dojo Diagnostic Test (question number), Set 1 = Tutorials Dojo Timed Mode Set 1 (category and question number). A dash means the topic comes from a custom exam.
- **Scenario and task:** what the question asked and what to do in the portal.
- **Where in the portal:** the menu path.
- **Sandbox:** Done means I performed the scenario in my sandbox tenant, where every lab is documented as a numbered entry in the [sandbox](https://github.com/rj-cloudsecurity/cloud-security-iam-portfolio/tree/main/00-sandbox). Skipped means I only looked up where it is configured and did not perform it.

## 1. Tenant, roles, users and groups
| Topic | Dojo question | Scenario and task | Where in the portal | Sandbox |
|-------|---------------|-------------------|---------------------|---------|
| Role scoped to an administrative unit | Exam 1: Users #1, Diagnostic: #5, Set 1: Users #1 | Liza is Password Administrator for the whole organization, Ramon only for AU-HR. Create an AU, add users, assign the role scoped to the AU, and test who can reset which user's password. | Entra ID > Administrative units > [AU] > Roles and administrators > Password Administrator > Add assignments | Done |
| Group-based licensing | Exam 1: Governance #1, Set 1: Governance #1 | Assign E5 to a group of all employees and remove the old E3 licenses. Do it in the portal and with `Set-MgGroupLicense`. | M365 admin center > Billing > Licenses > [licentie] > Groups (of Set-MgGroupLicense) | Done |
| Bulk remove direct licenses | Exam 1: Users #2, Diagnostic: #6 | Users have E3 assigned directly while the group gives E5. Remove the direct E3 assignments in bulk. | M365 admin center > Billing > Licenses > [licentie] > Users > selecteer users > Unassign licenses | Done |
| Restore a deleted user | Exam 1: Governance #5 | A user was deleted. Restore the account. Note the time limit and the minimum role. | Entra ID > Users > Deleted users > selecteer user > Restore user | Done |
| Custom security attributes | Random: #38 | Create an attribute set and attributes, assign Attribute Definition Administrator on one set, and check what a Global Administrator can and cannot see. | Entra admin center > Entra ID > Custom security attributes | Done |
| Restrict self-service sign-up | Exam 1: Users #13 | Only allow accounts with the verified SMTP domains. | PowerShell only: `Set-MsolCompanySettings` (geen portal-instelling) | Done |
| Helpdesk Administrator or User Administrator | Set 1: Users #9 | The helpdesk must assign licenses, create and delete users and groups, and reset passwords of non-administrators, with the least privilege. Give a test user each role in turn and check what they can and cannot do. | Entra ID > Roles & admins > Helpdesk Administrator of User Administrator > Add assignments | Done |
| Bulk create users | Random 16: Users #2 | Create three users in bulk with the CSV template. Download the template and note which columns are required. | Entra ID > Users > Bulk operations > Bulk create | Done |
| Bulk invite guests | Random 16: Users #3, Diagnostic: #9 | Invite external users in bulk with a CSV file. Note which columns are required and what happens at sign-in when Conditional Access requires MFA for guests. | Entra ID > Users > Bulk operations > Bulk invite en Entra ID > Conditional Access > Policies > New policy > Users > Include (group) > Grant > Require multifactor authentication | Done |
| Sign-in page language | Random 16: Users #6 | Users whose browser is set to French must see a French sign-in page. Find where you add a language to the sign-in experience. | Entra ID > Custom branding > Add > Browser language | Done |

## 2. External identities and hybrid identity
| Topic | Dojo question | Scenario and task | Where in the portal | Sandbox |
|-------|---------------|-------------------|---------------------|---------|
| Cross-tenant app-to-app access | Exam 1: Users #3, Set 1: Users #2 | An app in one tenant must call an app in a partner tenant. Create a credential (certificate or secret) on the app registration and check why a managed identity doesn't work across tenants. | Entra admin center > Entra ID > App registrations > [app] > Certificates & secrets > New client secret | Done |
| Exclude users from Connect Sync by attribute | Exam 1: Users #11 | Do not sync users with `extensionAttribute15 = NoSync`. Create the inbound rule on the AD DS connector with a scoping filter. | | Skipped |
| Pass-through authentication and lockout | Exam 1: Auth #1 | On-prem lockout policy must apply to cloud sign-ins. Check the PTA setting and compare it with password hash sync and smart lockout. | | Skipped |

## 3. Authentication, Conditional Access and Global Secure Access
| Topic | Dojo question | Scenario and task | Where in the portal | Sandbox |
|-------|---------------|-------------------|---------------------|---------|
| SSPR authentication methods | Exam 1: Auth #5, Random: #50 | Require 1 method, then 2 methods. Check which methods are available each time (mobile app code, e-mail, notification). | Entra ID > Password reset > Authentication methods (aantal methoden) en Entra ID > Authentication methods > Policies (welke methoden) | Done |
| Block legacy authentication | Exam 1: Auth #11 | Create a Conditional Access policy that blocks legacy authentication clients. | Entra ID > Conditional Access > Policies > New policy > Conditions > Client apps | Done |
| Global Secure Access web filtering | Exam 1: Auth #3, Diagnostic: #4 | Block social media for the Marketing group during business hours. Find the first step before the Conditional Access policy. | Entra ID > Global Secure Access > Secure > Web content filtering policies > Create | Done |
| Global Secure Access: compliant network | — | Enable Conditional Access signaling and use the compliant network location in a policy. | | Skipped |
| Terms of use | Random: #12, #43, Diagnostic: #2, #3, #7, Set 1: Governance #10 | Create a ToU (PDF), require it through Conditional Access, and find who accepted or declined in the logs. | Entra ID > Conditional Access > Terms of use > New terms | Done |
| Sign-in risk policy | Set 1: Auth #13 | Create a sign-in risk policy that asks for MFA instead of blocking. Find which setting must be in place first so users can satisfy the MFA request, and use report-only mode. | Entra ID > ID Protection > Multifactor authentication registration policy (Enabled), then Entra ID > Conditional Access > Policies > New policy > Conditions > Sign-in risk > Grant > Require multifactor authentication > Report-only. The legacy ID Protection > Sign-in risk policy is retired | Done |
| Download audit logs of Conditional Access changes | Random 16: Auth #8 | Change a Conditional Access policy, filter the audit logs on that change and download them. Note which export formats exist. | Entra ID > Monitoring & health > Audit logs > filter Service: Conditional Access, Activity: Update conditional access policy > open the entry > Modified Properties; Download in the toolbar | Done |
| Sign-in success rate of an app | Random 16: Auth #2 | Find the number of failed sign-ins and the success rate of an app over the past 30 days with the least configuration. | Entra ID > Monitoring & health > Usage & insights > Microsoft Entra application activity > Date range: 30 days (columns Successful sign-ins, Failed sign-ins, Success rate)	| Done |

## 4. Applications and workload identities
| Topic | Dojo question | Scenario and task | Where in the portal | Sandbox |
|-------|---------------|-------------------|---------------------|---------|
| Application Developer role | Exam 1: Users #9, Random: #11, Set 1: Users #5 | A developer must register apps while "Users can register applications" is No. Assign the role and test what the developer can and cannot do. | Entra ID > Roles & admins > Application Developer > Add assignments (Active) en Entra ID > Users > User settings (Users can register applications) | Done |
| Daemon app to Microsoft Graph | Exam 1: Users #12 | Register the app, add Graph application permissions, grant admin consent. | Entra ID > App registrations > [app] > API permissions > Add a permission > Microsoft Graph > Application permissions > Grant admin consent | Done |
| Delegated permission on behalf of a user | Random 16: Workload #2 | An app must read the signed-in user's calendar. Add Calendars.Read as a delegated permission and compare it with the application permission of the daemon app: who consents and whose data is read. | Entra ID > App registrations > the app > API permissions > Add a permission > Microsoft Graph > Delegated permissions > Calendars.Read (column Admin consent required: No). Granted permissions: Enterprise apps > the app > Permissions | Done |
| Redirect URI of an app registration | Random 16: Auth #14 | After sign-in, users must be sent back to the app. Add a web redirect URI and note where the setting is. | | |
| Restore a deleted app registration | Random 16: Workload #1 | Delete an app registration and restore it. Note the time limit. | | |
| My Apps collections | Random 16: Workload #3 | Group related enterprise apps in the My Apps portal with a collection and assign it to a user. | | |
| Admin consent workflow | Exam 1: Governance #13 | Set reviewers and see who can approve a request. | Entra ID > Enterprise apps > Consent and permissions > Admin consent settings | Skipped |
| User consent settings | — | Allow consent only for verified publishers and selected permissions. | Entra ID > Enterprise apps > Consent and permissions > User consent settings | Skipped |
| Application Proxy connector group | Diagnostic: #1 | Publish an on-premises app for remote users. Create a connector group, see which role is needed, and find where Conditional Access is applied to the published app. | | |
| Self-service access to an enterprise app | Diagnostic: #10 | Users must request approval before they get access to an enterprise app. Turn on self-service access, choose an approver and test the request in the My Apps portal. | | |
| SSO plus Conditional Access on device state | Exam 1: Auth #2 | A gallery app must use SSO and only be reachable from Entra-joined devices. | Entra ID > Enterprise apps > New application > [app] > Single sign-on, en Entra ID > Conditional Access > New policy > Conditions > Filter for devices | Done |
| User provisioning to a SaaS app (SCIM) | Exam 1: Governance #8 | Set up automatic provisioning to a SaaS app. | Entra ID > Enterprise applications > [app] > Provisioning > Automatic (Tenant URL + Secret token) | Skipped |
| Defender for Cloud Apps session control: first steps | Exam 1: Governance #12, Random: #1, #42, #49, Set 1: Workload #7 | Third-party or SharePoint app, block downloads. Do the steps in order: SSO if needed, Conditional Access with Use Conditional Access App Control, then the session policy. | | Skipped |
| Activity policy | Exam 1: Workload #4, Diagnostic: #8 | Alert on mass downloads or repeated deletions in a sanctioned app. | | Skipped |
| OAuth app policy | Set 1: Workload #6 | Alert when more than 15 users authorize a third-party app with elevated permissions. Find which policy type does this in Defender for Cloud Apps. | | |
| App governance | Exam 1: Auth #9, Set 1: Auth #8 | Give a user access to the dashboard with the least privilege and find where it is. | | Skipped |
| Key Vault with Azure RBAC | Random: #26 | Check which role can read secret values at subscription, resource group or vault scope. | Azure portal > Key vaults > [vault] > Access control (IAM) > Add role assignment > Key Vault Secrets User | Skipped |

## 5. Identity governance and privileged access
| Topic | Dojo question | Scenario and task | Where in the portal | Sandbox |
|-------|---------------|-------------------|---------------------|---------|
| Entitlement management settings | Exam 1: Governance #9, Set 1: Governance #15 | Remove external users automatically after 90 days. | Identity Governance > Entitlement management > Control configurations > Lifecycle of external users > View settings | Done |
| Access package with expiration | Exam 1: Governance #14 | Give a group time-limited access (90 days) to a SharePoint site. | Identity Governance > Entitlement management > Access packages > New access package > Lifecycle > Access package assignments expire | Done |
| Catalog with resources | Set 1: Governance #12 | Before an access package for contractors can exist, create a catalog and add resources to it (group, app, SharePoint site or team). Find where you add resources and who may do it. | | |
| Access review of a group with guests | Exam 1: Governance #15 | Review guest access monthly. Check whether failed guests can be blocked from signing in. | Identity Governance > Access reviews > New access review > Teams + Groups > Upon completion settings | |
| What an access review can cover | Random: #48 | Create reviews for a group, an enterprise app, an Entra role and a service principal. Note the license needs. | Identity Governance > Access reviews > New access review > Resource review (group, app) en Identity Governance > Privileged Identity Management > Microsoft Entra roles > Access reviews > New (Entra role, service principal) | Done |
| Access review of inactive users | Random 16: Governance #10 | Remove access to an app automatically for users who have not used it in the past 30 days, with the least overhead. Find the inactive users option and the auto apply setting. | | |
| PIM scope | Random: #27 | Check which roles PIM can manage and which it cannot (classic administrator and billing roles). | Identity Governance > Privileged Identity Management > Microsoft Entra roles > Roles en Privileged Identity Management > Azure resources > Discover resources (subscription nodig) | Done |

## 6. Monitoring
| Topic | Dojo question | Scenario and task | Where in the portal | Sandbox |
|-------|---------------|-------------------|---------------------|---------|
| Diagnostic settings to Log Analytics | Exam 1: Governance #7, Random: #5, #16, Set 1: Governance #5, #11 | Send Entra audit logs to a Log Analytics workspace. This is always the first step. | Entra ID > Monitoring & health > Diagnostic settings > Add diagnostic setting (Azure-subscription en Log Analytics workspace nodig) | Done |
