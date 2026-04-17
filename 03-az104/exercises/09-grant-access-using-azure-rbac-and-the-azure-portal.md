# Exercise 9 Grant access using Azure RBAC and the Azure portal
- Learning path 2.: AZ-104: Manage identities and governance in Azure
- Module: 4. Secure your Azure resources with Azure role-based access control (Azure RBAC)

In deze oefening wijs ik een rol toe aan een gebruiker via Access control (IAM) en verwijder ik deze daarna.

---

## Task 1 Rol toewijzen

Uitgevoerd via **Azure portal > Resource groups > example-group-for-exercise-8 > Access control (IAM) > Add > Add role assignment**

| Setting | Value |
|---|---|
| Role | Virtual Machine Contributor |
| Member | Chris Green |
| Scope | example-group-for-exercise-8 |

Chris Green kan nu virtual machines aanmaken en beheren binnen deze resource group.

---

## Task 2 Toegang verwijderen

Uitgevoerd via **Access control (IAM) > Role assignments > Chris Green selecteren > Remove > Yes**

Role assignment succesvol verwijderd.

---
