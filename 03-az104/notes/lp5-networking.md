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


**Create virtual networks**
  - Defineer bij aanmaken een IP adresruimte die nog niet in gebruik is in je organisatie, of on-premises of in de cloud, niet beide
  - Minimaal 1 subnet vereist. Elk subnet heeft een unieke, niet overlappend IP bereik binnen de VNet adresruimte
  - Aanmaken via Azure portal: Subscription, resource group, naam en regio opgeven

    
**Plan IP addressing**
  - Private IP: Communicatie binnen VNet en on-premises netwerk (via VPN Gateway of ExpressRoute)
  - Public IP: Communicatie met internet en Azure publieke services

  - Statisch vs dynamisch:
    - Statisch: IP wijzigt niet, aanbevolen voor: DNS name resolution, IP-gebaseerde security modellen, TLS/SSL certificaten, firewall regels, Domain Controllers en DNS server
    - Dynamishc: IP kan wijzigen, geschikt voor resources zonder vaste IP vereisting
   
    - Statisch en dynamisch toegewezen resources kunnen in aparte subnets worden geplaatst.


**Create public IP addressing**
  - Public IP adressen worden aangemaakt via de Azure portal en worden vaak gebruikt met load balancers

  - Configuratie-instellingen:
| Instelling | Beschrijving |
|---|---|
| IP Version | IPv4 of IPv6 — zelfde tarief |
| SKU | Moet overeenkomen met de SKU van de Load Balancer |
| Tier | Regional (traffic binnen VNet) of Cross-region (traffic over regionale backends) |
| IP address assignment | Statisch — toegewezen bij aanmaken, vrijgegeven pas bij verwijderen van het resource |


**Associate public IP addresses**
  - Public IP adressen kunnen worden gekoppeld aan:

| Resource | IP configuratie |
|---|---|
| Virtual machine | Network interface configuratie |
| VPN Gateway, ExpressRoute Gateway, NAT Gateway | Gateway IP configuratie |
| Public Load Balancer, Application Gateway, Azure Firewall, Route Server, API Management | Front-end configuratie |
| Bastion host | Public IP configuratie |    

  - Standard SKU kenmerken:
    - Allocation: Statisch
    - Security: Secure by default
    - Zones: Nonzonal, zonal of zone-reduntant


**Allocate or assign private IP addresses**
  - Private IP adressen kunnen worden gekoppeld aan:

| Resource | Private IP associatie | Dynamic | Static |
|---|---|---|---|
|Virtual machine|NIC|Ja|Ja|
|Internal load balancer|Front-end configuratie|Ja|Ja|
|Application gateway|Front-end configuratie|Ja|Ja|

  - Dynamic: Azure wijst het eerstvolgende beschikbare IP toe. Standaard methode
  - Static: Je kiest zelf een beschikbaar IP uit het subnet bereik


- [Lab 18 Create and Configure Virtual Networks](/03-az104/labs/18-create-and-configure-virtual-networks.md)


    
