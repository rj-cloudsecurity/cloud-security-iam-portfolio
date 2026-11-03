# SC-300 Exam Preparation

## Certification
  - Microsoft Certified: Identity and Access Administrator Associate (SC-300)
  - Result: In preparation
  - Date:

## Study Method
  - Completing all Microsoft Learn modules
  - Creating detailed notes in [Key Concepts](/04-sc300/notes/)
  - Practicing with custom AI-generated exams (claude.ai) based on official SC-300 exam objectives
  - Practicing with the Official Microsoft Practice Assessment
  - Practicing with Tutorials Dojo practice exams
  - Redoing every mistake hands-on in the portal to see the correct configuration and where it is located in [Hands-on Review](/04-sc300/exam-prep/sc300-hands-on-review.md)

## Domains
  - Domain 1 — Implement and manage user identities
  - Domain 2 — Implement authentication and access management
  - Domain 3 — Plan and implement workload identities
  - Domain 4 — Plan and automate identity governance

## Practice Assessment Progression
| Platform | Score | Notes |
|----------|-------|-------|
| Test 1 — Official Microsoft Practice Assessment 1 | 54% | 27/50. Weakest: D1 (administrative units, dynamic groups, WS-Fed, PTA vs PHS), D2 (Identity Protection, CBA, Global Secure Access), D3 (App Proxy, scope, Cloud Discovery), D4 (entitlement management, PIM for Groups, audit logs). |
| **Custom exams** | | |
| Test 2 — Custom Exam Domain 1 | 85% | 17/20. Mistakes: B2B direct connect vs collaboration, license for dynamic groups (P1), directory extensions for custom attributes. |
| Test 3 — Custom Exam Domain 2 | 80% | 16/20. Mistakes: security defaults block Conditional Access, MFA fraud alert (automatically block), Global Secure Access compliant network, Identity Protection requires P2. |
| Test 4 — Custom Exam Domain 3 | 70% | 14/20. Mistakes: Enterprise applications vs App registrations, delegated vs application permissions, client credentials flow, snapshot report vs app connector, federated identity credential (GitHub Actions), Application Developer role. |
| Test 5 — Custom Exam Domain 4 | 95% | 19/20. Mistake: Lifecycle Workflows requires Entra ID Governance. |
| Test 6 — Custom Exam Mixed Domains | 80% | 24/30. Mistakes: App registrations vs Enterprise applications, Lifecycle Workflows license, B2B collaboration vs direct connect, Application Proxy connectivity, compliant network vs compliant device, Sentinel data connector + analytics rule. |
| **Tutorials Dojo practice exams** | | |
| Test 7 — Tutorials Dojo Practice Exam 1 | 55% | 26/50 questions (31/56 points). D1 50%, D2 59%, D3 86%, D4 44%. Mistakes: PowerShell cmdlets (licenses, sign-up, invitations), Connect Sync inbound rules, entitlement management settings and access packages, access reviews, Defender for Cloud Apps policies, admin consent, SCIM. |
| Test 8 — Tutorials Dojo Randomized Test | 75% | 37/50 questions (42/56 points). Users 79%, Authentication 81%, Governance 60%, Workload 83%. Mistakes: Defender for Cloud Apps session control (first step), diagnostic settings (2x), Application Developer, Terms of use (audit logs, PDF), PIM scope, Key Vault RBAC, custom security attributes, access review scope, SSPR method. |
| Test 9 — Tutorials Dojo Diagnostic Test | 90% | 9/10 questions. Users 100%, Authentication 100%, Governance 100%, Workload 0% (1 question). Mistake: Defender for Cloud Apps activity policy. |
| Test 10 — Tutorials Dojo Timed Mode Set 1 | 67% | 33/50 questions (36/54 points). Users 60%, Authentication 74%, Governance 56%, Workload 78%. Mistakes: administrative unit (Password Administrator), cross-tenant credentials, Application Developer, role for a helpdesk, Sentinel data connector, MFA without mobile signal, App governance, sign-in risk policy, Set-MgGroupLicense, PIM, diagnostic settings (2x), Terms of use (audit logs), entitlement management (catalog and settings), OAuth app policy, session policy. |
| Test 11 — Tutorials Dojo Timed Mode Set 1 (second attempt) | 89% | 44/50 questions (48/54 points, 88.89%). Same questions as Test 10. Users 100%, Authentication 84%, Governance 88%, Workload 89%. Mistakes: Usage & insights (app sign-in success rate), access policy, Azure Monitor action group, App governance console (Microsoft Defender portal), Cloud Discovery, entitlement management catalog as first step. |
| Test 12 — Tutorials Dojo Review Mode Set 1 (apparently, same as test 10 and 11) | 96% | 48/50 questions (52/54 points, 96.30%). Users 100%, Authentication 100%, Governance 88%, Workload 100%. Mistakes: diagnostic settings (sign-in and activity logs are both needed), Azure Monitor action group. |
| Test 13 — Tutorials Dojo Review Mode Set 2 | 73% | 35/50 questions (40/55 points, 72.73%). Users 71%, Authentication 71%, Governance 56%, Workload 100%. Mistakes: access review scope (groups, apps, Entra roles, service principals), "Upon completion" setting of an access review, app governance (Microsoft Defender portal), modern authentication before tenant restrictions, ABAC (Azure Storage with blob index tags), Connect Sync inbound rule for extensionAttribute value, password writeback (not Conditional Access), PIM-manageable roles, Defender for Cloud Apps session control (SSO first), admin consent reviewer needs a role with consent rights, ABAC role conditions, access package for 90-day access, Identity Governance Administrator, collaboration restrictions, Application Proxy connector and Application Developer. |

## Next Focus Areas after Test 1

**Domain 1 — Implement and manage user identities**
  - Administrative units: a group in the AU gives management of the group and its membership, not of the members; a user who is in the AU itself can be managed
  - Dynamic groups: created in the Entra admin center and the Intune admin center, not in the Microsoft 365 admin center
  - WS-Fed federation: required claims in the token are ImmutableID and emailaddress
  - PTA vs PHS: PTA enforces user-level AD policies, PHS does not
  - Connect Health: Duplicate Attribute report for sync errors with self-service remediation

**Domain 2 — Implement authentication and access management**
  - Certificate-based authentication: high-affinity bindings are X509SKI, SHA1PublicKey and IssuerAndSerialNumber
  - Identity Protection: Block access is the only control that is in both the sign-in risk and the user risk policy
  - The Risk detections report keeps data for 90 days, Risky sign-ins for 30 days
  - Global Secure Access: web content filtering (e.g. gambling) = security profile linked to a Conditional Access policy
  - Global Secure Access client: Windows must be Entra joined or hybrid joined, macOS may be registered via Company Portal
  - License: Private Access and Internet Access together = Microsoft Entra Suite

**Domain 3 — Plan and implement workload identities**
  - Federation SSO methods: SAML, OpenID Connect and OAuth
  - Publishing a legacy on-prem web app with MFA: the first step is Application Proxy
  - Scope for application permissions: `https://graph.microsoft.com/.default`
  - Registering apps when "Users can register applications = No": Application Developer
  - Filling the Cloud Discovery dashboard: snapshot report (log upload), not an app connector
  - Blocking downloads on unmanaged devices in third-party apps: Conditional Access App Control (session policy)

**Domain 4 — Plan and automate identity governance**
  - Connected organization: federation and one-time passcode as authentication methods
  - External users who are not yet in the tenant: request access via a My Access portal link
  - Just-in-time access for a member/owner of a security group: PIM for Groups
  - All PIM activity for a group: Resource audit; My audit only shows your own actions
  - Entra logs to Azure Monitor require an Entra ID P1 or P2 license

## Next Focus Areas after Test 2
  - Domain 1 — B2B direct connect = Teams shared channels without a guest account; B2B collaboration = guest users
  - Domain 1 — Dynamic groups require Entra ID P1; the Intune admin center is a portal, not a license
  - Domain 1 — Synchronizing a custom attribute from on-prem AD to Entra: directory extensions (cloudFiltered is an exclusion marker, not a sync)

## Next Focus Areas after Test 3
  - Domain 2 — Security defaults are on by default in a new tenant and block Conditional Access; turn them off first, even with P1
  - Domain 2 — Fraud alert: the user reports an unrequested MFA prompt; the option "Automatically block users who report fraud" blocks the account
  - Domain 2 — Global Secure Access: Compliant network (under Conditions > Locations) recognizes traffic through GSA; a named location with IP ranges cannot do that
  - Domain 2 — Identity Protection (sign-in and user risk policies) requires Entra ID P2; P1 only gives Conditional Access
  - Domain 2 — PTA smart lockout: Entra threshold lower than the AD threshold, so Entra blocks before AD does

## Next Focus Areas after Test 4
  - Domain 3 — You configure SSO (SAML) in Enterprise applications; App registrations is for your own apps and APIs
  - Domain 3 — Delegated permissions: on behalf of a signed-in user; application permissions: without a user, always admin consent
  - Domain 3 — Daemon without a user: client credentials flow; with a user: authorization code flow
  - Domain 3 — Cloud Discovery: snapshot report = upload a log file once; continuous report = automatic; app connector = connect a SaaS app via API
  - Domain 3 — Workload identity federation (e.g. GitHub Actions without secrets): federated identity credential on the app registration; managed identities only exist for Azure resources
  - Domain 3 — Registering apps when "Users can register applications = No": Application Developer (least privilege)
  - Domain 3 — Consent: configure user consent via verified publishers + selected permissions; admin consent workflow for requests

## Next Focus Areas after Test 5
  - Domain 4 — Lifecycle Workflows requires Microsoft Entra ID Governance (or Entra Suite); Workload ID Premium is only for workload identities

## Next Focus Areas after Test 6
  - Domain 3 — App registrations: your own app or API (app roles, API scopes, secrets); Enterprise applications: SSO, assignment and Conditional Access for an existing app
  - Domain 4 — Lifecycle Workflows (joiner, mover, leaver) require Microsoft Entra ID Governance, not P2
  - Domain 1 — B2B collaboration: guest object in the directory (SharePoint, apps, files); B2B direct connect: Teams shared channels only, no object
  - Domain 3 — Application Proxy connector: outbound traffic only on ports 80 and 443, no inbound ports
  - Domain 2 — Compliant network (Conditions > Locations, requires CA signaling in Global Secure Access) checks the traffic; compliant device (Intune) checks the device
  - Domain 4 — Sentinel detection: data connector for the logs plus a scheduled analytics rule; a playbook is only the response

## Next Focus Areas after Test 7

**Domain 1 — Implement and manage user identities**
  - Group-based licensing: assign the new license to the group and remove the old one with `Set-MgGroupLicense`; remove direct licenses in bulk via the Licenses blade
  - Restrict self-service sign-up to verified SMTP domains: `Set-MsolCompanySettings`
  - Invite a guest with PowerShell: `New-AzureADMSInvitation`
  - Connect Sync: exclude users by attribute value (e.g. extensionAttribute15 = NoSync): inbound synchronization rule on the AD DS connector (scoping filter in the Synchronization Rules Editor); inbound = source to metaverse, outbound = to the Entra ID connector
  - Connect Sync: OU filtering (Domain and OU filtering in the wizard) is for a location or a whole OU; an attribute value needs an inbound rule
  - Restore a deleted user: within 30 days, minimum role User Administrator
  - Password Administrator can only reset passwords within the scope the role is assigned at (organization or administrative unit)
  - SCIM 2.0: the standard for automatic provisioning to SaaS apps; SAML, OIDC and OAuth are for sign-in and authorization

**Domain 2 — Implement authentication and access management**
  - PTA enforces on-prem account lockout for cloud sign-ins; smart lockout does not
  - SSPR with 1 required method: mobile app code (the notification only works if 2 methods are required)
  - Block legacy authentication: Conditional Access, condition Client apps
  - SSO via Enterprise application; restrict access to Entra-joined devices with a Conditional Access policy

**Domain 3 — Plan and implement workload identities**
  - Defender for Cloud Apps session control for a third-party SaaS app: the first step is to set up SSO in the Entra admin center
  - Activity policy: alerts on risky actions in SaaS apps (mass downloads, repeated deletions); session policy: real-time control
  - App governance dashboard: role Cloud Application Administrator, via the Microsoft Defender portal
  - Daemon app to Graph: register the app, assign Graph permissions, give tenant-wide admin consent
  - App in tenant A to app in tenant B: certificate or secret; a managed identity does not work across tenants
  - Admin consent requests can only be approved by a designated reviewer who also has a role with consent rights (e.g. Cloud Application Administrator)
  - Registering apps when "Users can register applications = No": Application Developer

**Domain 4 — Plan and automate identity governance**
  - Entitlement management settings: automatically remove external users after a period (e.g. 90 days)
  - Temporary access to a group and SharePoint site (e.g. 90 days): access package with expiration in the policy
  - Periodic review of guest access that comes through a group: access review of that group
  - Entra audit logs to Azure Monitor: diagnostic settings to a Log Analytics workspace

## Next Focus Areas after Test 8

**Recurring mistakes (multiple tests)**
  - Diagnostic settings: the first step to send Entra audit/sign-in logs to Log Analytics (mistake in Test 7 and 2x in Test 8)
  - Application Developer: registering apps when "Users can register applications = No" (mistake in Test 4, 7 and 8)
  - Defender for Cloud Apps session control (mistake in Test 7 and 3x in Test 8): see Domain 3

**Domain 1 — Implement and manage user identities**
  - Terms of use: who accepted or declined is shown in the audit logs (kept for 30 days); you upload the ToU document as a PDF
  - Custom security attributes: Global Administrator has no rights on them by default; first assign the role Attribute Definition/Assignment Administrator or Reader, per attribute set

**Domain 2 — Implement authentication and access management**
  - SSPR with 1 required method: a verification code to an external email address is valid (besides mobile app code); smartcard and Windows Hello for Business are not SSPR methods
  - PIM manages Entra roles (e.g. SharePoint Administrator) and Azure resource roles; not classic administrator roles (Account Administrator) and not billing account roles (Billing Account Owner)

**Domain 3 — Plan and implement workload identities**
  - Defender for Cloud Apps session control: if the app is not yet set up via Entra, SSO first; if the app is already in Entra, first a Conditional Access policy with Session > Use Conditional Access App Control; only then the session policy in Defender
  - Key Vault with Azure RBAC: Key Vault Administrator and Key Vault Secrets User read secret values, Key Vault Reader only metadata; a role at subscription level applies to all vaults below it, a role on a single vault only to that vault

**Domain 4 — Plan and automate identity governance**
  - Access reviews can target groups, enterprise applications, Entra roles (via PIM) and service principals (requires Workload ID Premium plus P2 or Governance)

## Next Focus Areas after Test 9
  - Domain 3 — Activity policy: alert on a threshold of activity in a SaaS app (e.g. more than 100 downloads in a minute); session policy is real-time control, anomaly detection is machine learning without a fixed threshold

## Next Focus Areas after Test 10

**Recurring mistakes (multiple tests)**
  - Application Developer: registering apps when "Users can register applications = No" (mistake in Test 4, 7, 8 and 10)
  - Diagnostic settings: the first step to send Entra logs to Log Analytics (mistake in Test 7, 8 and 10)
  - Defender for Cloud Apps session policy and session control (mistake in Test 7, 8 and 10): see Domain 3
  - Terms of use: who accepted or declined is shown in the audit logs (mistake in Test 8 and 10)
  - `Set-MgGroupLicense` for licenses per group (mistake in Test 7 and 10)
  - Entitlement management settings: remove external users after 90 days (mistake in Test 7 and 10)
  - App governance dashboard: Cloud Application Administrator via the Microsoft Defender portal (mistake in Test 7 and 10)
  - Password Administrator and scope: administrative unit (mistake in Test 7 and 10)

**Domain 1 — Implement and manage user identities**
  - Password Administrator can reset passwords of users without an admin role, Directory Readers, Guest Inviter and other Password Administrators; with organization scope for everyone under it, with administrative unit scope only for members of that AU
  - App in tenant A to app in tenant B: two valid credentials, secret and certificate; an API key and a token are not credentials for this
  - A helpdesk that assigns licenses, creates and deletes users and groups and resets passwords of non-admins: User Administrator; Helpdesk Administrator may only reset passwords

**Domain 2 — Implement authentication and access management**
  - Sentinel data connector for Entra ID: the connector in Sentinel brings in the logs; diagnostic settings only routes logs and a user risk policy connects nothing
  - MFA without mobile signal or wifi: Windows Hello for Business works on the device, also offline; Windows Hello for Business is not an SSPR method
  - A sign-in risk policy that does not block: first the MFA registration policy in ID Protection, so users can register for MFA and answer the MFA prompt of a risky sign-in. You now create the sign-in risk policy itself in Conditional Access (condition Sign-in risk); the legacy sign-in risk policy in ID Protection has been retired

**Domain 3 — Plan and implement workload identities**
  - OAuth app policy (Defender for Cloud Apps): alert when more than a number of users authorize a third-party app with high permissions
  - Session policy: real-time restriction during the session, for example blocking printing or downloading in SharePoint; file policy and access policy do not do that

**Domain 4 — Plan and automate identity governance**
  - PIM: for administrators with broad rights across multiple subscriptions: just-in-time access, monitoring and access reviews
  - Entra sign-in and activity logs to Azure Monitor: diagnostic settings; a data collection rule alone is not enough because it does not export logs from Entra
  - Entitlement management starts with a catalog; you add the resources to it (SharePoint site, team), then you create the access packages

## Next Focus Areas after Test 13

**Recurring mistakes (multiple tests)**
  - App governance: activate and manage it in the Microsoft Defender portal (mistake in Test 7, 10, 11 and 13)
  - Defender for Cloud Apps session control: for an app that is not yet in Entra, the first step is SSO in the Entra admin center (mistake in Test 7, 8, 10 and 13)
  - Application Developer vs Application Administrator: registering a new app = Application Developer; installing the Application Proxy connector or managing all apps = Application Administrator
  - Admin consent reviewers: a designated reviewer can only approve with a role that has consent rights (e.g. Cloud Application Administrator); Authentication Administrator and a user without a role cannot (mistake in Test 7 and 13)

**Domain 1 — Implement and manage user identities**
  - Connect Sync: excluding users by attribute value (e.g. extensionAttribute15 = NoSync) = inbound synchronization rule on the AD DS connector; OU filtering is for locations (mistake in Test 7 and 13)
  - Collaboration restrictions (External collaboration settings): allow or deny list of domains for B2B invitations; this is what blocks guests from a specific partner domain
  - Identity Governance Administrator: creates and manages access packages, lifecycle policies and access reviews for entitlement management without global permissions

**Domain 2 — Implement authentication and access management**
  - Tenant restrictions only work with modern authentication (OAuth tokens); legacy clients such as Outlook 2013 need modern authentication enabled first
  - Password writeback is configured in Microsoft Entra Connect; a Conditional Access policy does not write passwords back on-premises
  - ABAC role assignment conditions: in the exam questions the answer is Azure Storage (blob data roles with blob index tags), and the role that supports conditions is Storage Blob Data Reader (Carlos), not Monitoring Reader, Contributor or Virtual Machine Contributor

**Domain 3 — Plan and implement workload identities**
  - Defender for Cloud Apps session control for a new SaaS app: SSO first, then Conditional Access with Conditional Access App Control, then the session policy

**Domain 4 — Plan and automate identity governance**
  - Access reviews can cover groups, enterprise applications, Entra roles and Azure resource roles (via PIM) and service principals (Workload ID Premium plus P2 or Governance)
  - Access review: what happens when reviewers do not respond is set under Upon completion settings ("If reviewers don't respond")
  - 90-day access to a group and SharePoint site: an access package with an expiration in the policy, not a group expiration policy or lifecycle workflow
  - PIM manages Entra roles, Azure resource roles and groups; not the classic roles (Account Administrator, Service Administrator, Co-Administrator) and not billing roles. PIM can manage any Entra role; the Privileged label only marks the most sensitive roles
