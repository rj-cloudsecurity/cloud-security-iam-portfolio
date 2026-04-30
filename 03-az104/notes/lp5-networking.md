# AZ-104: Azure Administrator Associate
## Learning Path 5: Configure and manage virtual networks for Azure administrators

  - **AZ-104 Started:** 11-4-2026
  - **AZ-104 Exam passed:**

---

## Inhoudsopgave

### Learning Path 4: Configure and manage virtual networks for Azure administrators


---

## Learning Path 5: Configure and manage virtual networks for Azure administrators
### Module 1: Configure virtual networks 

**Configure virtual networks**
  - Een Azure Virtual Network (VNet) is een logische isolatie van Azure cloud resources, je kunt er VPNs mee inrichten en resources veilig met elkaar verbinden
  - Elk VNet heeft een eigen CIDR block en kan gekoppeld worden aan andere VNets of on-premises netwerken (mits geen overlappende CIDR blocks)
  - Je beheert DNS instellingen en subnet segmentatie zelf

  - Gebruik scenario's:

| Scenario | Beschrijving |
|---|---|
| Private cloud-only VNet | Services en VMs communiceren direct en veilig binnen het VNet — geen cross-premises verbinding nodig |
| Datacenter uitbreiding | Site-to-site VPN via IPSEC voor veilige verbinding tussen on-premises VPN gateway en Azure |
| Hybrid cloud | VNet verbindt cloud applicaties met on-premises systemen zoals mainframes en Unix |

**Create subnets**
  - Subnets segmenteren een VNet voor betere security, performance en beheer.
  - Elk subnet heeft een uniek IP-bereik binnen de VNet adresruimte. Geen overlap met andere subnets. CIRD notatie vereist

  - Gereserveerde adressen per subnet (5 stuks):

| Adres | Reden |
|---|---|
| x.x.x.0 | VNet adres |
| x.x.x.1 | Default gateway |
| x.x.x.2 en x.x.x.3 | Azure DNS |
| x.x.x.255 | Broadcast adres |

  - Ovewegingen:
    - Service requirements: Sommige services vereisen een eigen subnet (bv. Azure VPN Gateway vereist een dedicated subnet)
    - Network virtual appliances: Standaard routeert Azure traffic tussen subnets; overschrijft dit om traffic via een network virtual appliance te sturen
    - NSGs: 0 of 1 NSG per subnet voor inbound/outbound traffic controle
    - Azure Private Link: Private connectivity van VNet naar PaaS services zonder public internet


















    
