# SC-300 Hands-on Review

Focus: not "which feature", but where and how it is configured. For every mistake from the practice exams: perform it in the portal (Microsoft Entra admin center, Microsoft Defender portal, PowerShell), write down the menu path, and mark it Done.

The Dojo column shows the question number in Tutorials Dojo Practice Exam 1 (Test 7), sorted by question number. A dash means the topic comes from a custom exam. Domains: D1 = Implement and manage user identities, D2 = Implement authentication and access management, D3 = Plan and implement workload identities, D4 = Plan and automate identity governance.

| Topic | Dojo question | Domain | Where in the portal | Status |
|-------|---------------|--------|---------------------|--------|
| Group-based licensing: license assigned to a group, old license removed (`Set-MgGroupLicense`) | Q1 | D1 | M365 admin center > Billing > Licenses > [licentie] > Groups (of Set-MgGroupLicense) | Done |
| Entitlement management settings: automatic removal of external users | Q4 | D4 | Identity Governance > Entitlement management > Control configurations | Done |
| Restrict self-service sign-up to verified domains (`Set-MsolCompanySettings`) | Q5 | D1 | PowerShell only: `Set-MsolCompanySettings` (geen portal-instelling) | Done |
| Access review of a group with guests (twijfelachtige Dojo-key: bij "blokkeren" past guest review met auto-apply Block sign-in) | Q8 | D4 | Identity Governance > Access reviews > New access review > Teams + Groups > Upon completion settings | Todo |
| User provisioning to a SaaS app (SCIM) | Q10 | D3 | Entra ID > Enterprise applications > [app] > Provisioning > Automatic (Tenant URL + Secret token) | Todo |
| Connect Sync: exclude users by attribute (inbound rule on the AD DS connector) | Q14 | D1 | | Todo |
| Application Developer role: register apps when users cannot | Q16 | D3 | | Todo |
| SSPR: authentication methods and number of methods required | Q17 | D2 | | Todo |
| Password Administrator scoped to an administrative unit | Q18 | D1 | | Todo |
| Daemon app to Microsoft Graph: register app, assign permissions, grant admin consent | Q20 | D3 | | Todo |
| Admin consent workflow: reviewers and approval | Q21 | D3 | | Todo |
| Enterprise application SSO plus Conditional Access on device state | Q22 | D3 | | Todo |
| Defender for Cloud Apps: activity policy | Q26 | D3 | | Todo |
| Cross-tenant app-to-app access: certificate and secret | Q27 | D3 | | Todo |
| Access package with expiration in the policy | Q33 | D4 | | Todo |
| App governance dashboard (role and portal) | Q34 | D3 | | Todo |
| Bulk remove direct license assignments (Licenses blade) | Q35 | D1 | | Todo |
| Restore a deleted user (30 days) | Q37 | D1 | | Todo |
| SaaS app with Defender for Cloud Apps session control: SSO first | Q39 | D3 | | Todo |
| Invite a guest with PowerShell (`New-AzureADMSInvitation`) | Q40 | D1 | | Todo |
| Conditional Access: Client apps (block legacy authentication) | Q41 | D2 | | Todo |
| Diagnostic settings: Entra audit logs to a Log Analytics workspace | Q48 | D4 | | Todo |
| Pass-through authentication: on-premises lockout policy applies to cloud sign-ins | Q50 | D1 | | Todo |
| Global Secure Access: Conditional Access signaling and compliant network location | — | D2 | | Todo |
| User consent settings (verified publishers, selected permissions) | — | D3 | | Todo |
