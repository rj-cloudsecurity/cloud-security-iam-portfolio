# Exercise 15 Create a VM using the Azure portal
- Learning path 4.: AZ-104: Deploy and manage Azure compute resources
- Module: 1. Introduction to Azure virtual machines

In deze oefening maak ik een Ubuntu VM aan via de Azure portal.

---

## Task 1 VM aanmaken

Uitgevoerd via **Azure portal > Create a resource > Virtual machine**

| Setting | Value |
|---|---|
| Resource group | exercise15 (nieuw) |
| Virtual machine name | test-ubuntu-cus-vm |
| Region | West Europe |
| Availability options | No infrastructure redundancy required |
| Security type | Standard |
| Image | Ubuntu Server 24.04 LTS - x64 Gen2 |
| VM architecture | x64 |
| Size | Standard_D2s_v3 (2 vCPUs, 8 GiB memory) |
| Authentication type | SSH public key |
| Username | azureuser |
| SSH public key source | Generate new key pair |
| Public inbound ports | SSH (22) |

VM succesvol gedeployed. Public IP: `51.136.106.58`

---

## Task 2 Clean up

Resource group `exercise15` verwijderd.

---
