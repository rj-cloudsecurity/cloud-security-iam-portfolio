# Exercise 8 List access using Azure RBAC and the Azure portal
- Learning path 2.: AZ-104: Manage identities and governance in Azure
- Module: 4. Secure your Azure resources with Azure role-based access control (Azure RBAC)

In deze oefening bekijk ik role assignments in de Azure portal via Access control (IAM).

---

## Task 1 Eigen permissions bekijken

Uitgevoerd via **Azure portal > Profile menu (...) > My permissions**

Toont de rollen die aan het eigen account zijn toegewezen en de bijbehorende scope.

---

## Task 2 Role assignments bekijken voor een resource group

Resource group aangemaakt: `example-group-for-exercise-8`

Uitgevoerd via **Azure portal > Resource groups > example-group-for-exercise-8 > Access control (IAM) > Role assignments**

Bij de Role assignments tab was alleen het eigen account zichtbaar. Sommige rollen zijn direct toegewezen op de resource group (This resource), andere worden geërfd van een hogere scope (Inherited).

---

## Task 3 Beschikbare roles bekijken

Uitgevoerd via **Access control (IAM) > Roles tab**

Resultaat: **889 roles** zichtbaar — een combinatie van built-in en custom roles. Via de Details kolom is per rol te zien hoeveel users en groups aan die rol zijn toegewezen.

---
