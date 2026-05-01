# Exercise 18 Create and configure virtual networks
- Learning Path 5: Configure and manage virtual networks for Azure administrators  
- Module 1: Configure virtual networks

---

## Task 1 Create hub and spoke virtual networks

Uitgevoerd via **Azure portal > Virtual networks > + Create**

### app‑vnet configuratie

| Setting | Value |
|---|---|
| Resource group | lab18rg |
| Virtual network name | app-vnet |
| Region | West Europe |
| IPv4 address space | 10.1.0.0/16 |
| Subnet 1 name | frontend |
| Subnet 1 range | 10.1.0.0/24 |
| Subnet 2 name | backend |
| Subnet 2 range | 10.1.1.0/24 |

**Opmerking:** In eerste poging vergeten om het default address space aan te passen. Hierdoor kon de VNet niet peeren. Na correctie werkte het direct.

---

### hub‑vnet configuratie

| Setting | Value |
|---|---|
| Resource group | lab18rg |
| Virtual network name | hub-vnet |
| Region | West Europe |
| IPv4 address space | 10.0.0.0/16 |
| Subnet name | AzureFirewallSubnet |
| Subnet range | 10.0.0.0/26 |
| Subnet purpose | Azure Firewall |

---

### Validatie

- Beide VNets zichtbaar in **Virtual networks** overzicht  
- Subnets correct aangemaakt  
- Address spaces overlappen niet  

---

## Task 2 Configure VNet peering

Uitgevoerd via **app‑vnet > Settings > Peerings > + Add**

| Setting | Value |
|---|---|
| Remote peering link name | app-vnet-to-hub |
| Virtual network | hub-vnet |
| Local peering link name | hub-to-app-vnet |
| Other settings | Default |

**Resultaat:**  
- Peering status: **Connected**  
- Beide VNets tonen **Fully synced**

---

## Task 3 Clean up

```bash
az group delete --resource-group lab18rg --yes
