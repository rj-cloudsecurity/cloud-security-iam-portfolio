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


**Exercise: Create and configure virtual networks**
  - [Lab 18 Create and Configure Virtual Networks](/03-az104/labs/18-create-and-configure-virtual-networks.md)



---

## Learning Path 5: Configure and manage virtual networks for Azure administrators
### Module 2: Configure network security groups 


**Implement network security groups**
  - NSG: set security rules (Allow/Deny, Inbound/Outbount)
  - Je koppelt een NSG aan 1 subnet of 1 NIC
  - Een NSG zelf kan aan meerdere resources gekoppeld worden
  - Subnet-NSG: Brede filtering bv. DMZ
  - NIC-NSG: specifieker filtering per VM
  - VM: Overview toont gekoppelde NSGs en regels


**Determine network security group rules**
  - NSG's filteren inbound/outbound verkeer op subnets en entwork interaces
  - Default rules (automatisch aangemaakt, niet verwijderbaar)

  - Inbound:
    
| Priority | Naam                            | Actie |
|----------|---------------------------------|-------|
| 65000    | AllowVnetInBound                | Allow |
| 65001    | AllowAzureLoadBalancerInBound   | Allow |
| 65500    | DenyAllInBound                  | Deny  |    


  - Outbound:
    
| Priority | Naam                    | Actie |
|----------|-------------------------|-------|
| 65000    | AllowVnetOutBound       | Allow |
| 65001    | AllowInternetOutBound   | Allow |
| 65500    | DenyAllOutBound         | Deny  |


  - Custom rules:
    
| Setting             | Opties                                  |
|---------------------|-----------------------------------------|
| Source/Destination  | Any, IP, Service Tag, ASG               |
| Protocol            | TCP, UDP, ICMP, ESP, AH, Any            |
| Action              | Allow / Deny                            |
| Priority            | 100 – 4096 (lager = hogere prioriteit)  |


  - Key points:
    - Lage priority-waarde = hogere voorrang
    - Default rules niet verwijderbaar, wel overriden met hogere priority
    - ESP/AH alleen via JSON/PowerShel
   
  
**Determine network security group effective rules**
  - Verwerkingsvolgorde

| Richting | Stap 1     | Stap 2     |
|----------|------------|------------|
| Inbound  | Subnet NSG | NIC NSG    |
| Outbound | NIC NSG    | Subnet NSG |

  - Elke NSG wordt onafhankelijk geevalueerd. Regels van subnet NSG en NIC NSG worden niet samengevoegd. Azure controleer ook intra-subnet traffic (verkeer tussen VM's binnen hetzelfde subnet)

  - Overwegingen bij het maken van effective rules
    - Geen NSG koppelen: Als je geen NSG koppelt aan een subnet of NIC, geldt de Azure default, all traffic allowed. Gebruik dit alleen als je geen controle nodig hebt op dat niveau
    - Allow Rules op beide niveaus: Heb je een NSG op zowel subnet als NIC? Dan moet op BEIDE niveaus een allow rule aanwezig zijn. Ontbreekt de allow rule op 1 niveau -> traffic wordt denied, ook al staat het andere niveau open
    - Intra-subnet traffic: Standaard kunnen VM's in hetzelfde subnet met elkaar communiceren. Wil je dit blokkeren? Maak een regel in de subnet NSG die all inbound en outbound traffic deniet
    - Priority gaps: Gebruik stappen van 100. Zo kun je later regels tussenvoegen zonder bestaande regels te hernoemen of opnieuw te nummeren

  - Troubleshooting / inzicht:
    
| Tool                              | Functie                                                                                   |
|-----------------------------------|-------------------------------------------------------------------------------------------|
| Effective security rules (Portal) | Toont welke NSG-regels actief zijn per VM, subnet of NIC                                  |
| Network Watcher                   | Gecombineerd overzicht van NSG rules én Virtual Network Manager security admin rules       |
| IP flow verify                    | Test of specifiek verkeer allowed of denied wordt, gebaseerd op NSG én security admin rules |


**Create network security group rules**
  - Configuratie-instellingen

| Setting         | Beschrijving                                                        |
|-----------------|---------------------------------------------------------------------|
| **Source**      | Inbound traffic filter: Any, IP range, ASG, of Service Tag          |
| **Destination** | Outbound traffic filter: Any, IP range, ASG, of Service Tag         |
| **Service**     | Protocol + poort(bereik): voorgedefinieerd (RDP, SSH, HTTPS) of custom |
| **Priority**    | 100–4096 — lager = hogere prioriteit                                |
| **Action**      | Allow of Deny                                                       |

  - Augmented security rules
    - 1 regel met meerdere waarden in Source, Destination of Service. Minder regels, minder beheer
   
| Mogelijkheid          | Voorbeeld                                      |
|-----------------------|------------------------------------------------|
| Meerdere IP-adressen  | 10.0.0.1, 10.0.0.5, 10.1.0.0/24 in één rule   |
| Meerdere poorten      | 80, 443, 8080, 8090 in één Service-veld        |
| Mix van types         | Service Tag + ASG + IP in dezelfde regel       |

  - Voordeel: voorkomt rule sprawl in enterprise-omgevingen met veel IP-ranges of services

**Implement application security groups (ASGs)**
  - ASG groeperen VM's logisch per workload/applicatielaag. Je gebruikt de ASG als source of destination in NSG-regels. Geen specifieke IP-adressen nodig

  - Voordelen:

  | Voordeel                    | Uitleg                                                        |
|-----------------------------|---------------------------------------------------------------|
| Geen IP-beheer              | Regels op groepsnaam, niet op IP — schaalt automatisch mee    |
| Geen subnet-indeling vereist| VM's groeperen op functie, niet op netwerklocatie             |
| Vereenvoudigde rules        | Één regel per ASG i.p.v. per VM                               |
| Dynamisch                   | Nieuwe VM in ASG → regels gelden direct                       |
| Workload-gebaseerd          | Logische indeling op applicatie, service of datalaag          |


  - Praktijkvoorbeeld, online retailer:

| Rule | Priority | Van                | Naar               | Poort      | Actie |
|------|----------|--------------------|--------------------|------------|-------|
| 1    | 100      | Internet           | Web servers (ASG)  | 80, 443    | Allow |
| 2    | 110      | Web servers (ASG)  | App servers (ASG)  | 1433 (SQL) | Allow |
| 3    | 120      | Any                | App servers (ASG)  | 80, 443    | Deny  |


  - Rule 2 + 3 samen: alleen web server mogen de database bereiken
  - ASG vs Service Tag
    - ASG -> groepeert eigen VMs, beheert security policies per groep
    - Service Tag -> vertegenwoordigt IP-prefixes van Azure-service (bv. AzureCloud), vereenvoudigt beheer van Azure-service adressen


**Exercise - Implement virtual networking**
  - [Lab 19 Implement virtual networking](/03-az104/labs/19-implement-virtual-networking.md)




---

## Learning Path 5: Configure and manage virtual networks for Azure administrators
### Module 3: Host your domain on Azure DNS


**What is Azure DNS?**
  - Azure DNS is een hosting service voor DNS-domeinen, gebouwd op Azure Resource Manager

  - DNS record types
    
| Type  | Naam             | Gebruik                                          |
|-------|------------------|--------------------------------------------------|
| A     | Host record      | Domein/hostnaam → IPv4 adres                     |
| AAAA  | Host record      | Domein/hostnaam → IPv6 adres                     |
| CNAME | Canonical Name   | Alias van één domein naar ander domein           |
| MX    | Mail exchange    | Mailverzoeken → mailserver                       |
| TXT   | Text record      | Tekst koppelen aan domein (bijv. Microsoft 365)  |
| NS    | Name server      | Automatisch aangemaakt bij nieuwe DNS zone       |
| SOA   | Start of authority | Automatisch aangemaakt bij nieuwe DNS zone     |


  - Azure DNS kenmerken
    
| Eigenschap        | Detail                                      |
|-------------------|---------------------------------------------|
| Domein registreren| ❌ Niet mogelijk — via third-party registrar |
| SOA               | Azure DNS fungeert als SOA voor het domein  |
| DNSSEC            | ❌ Niet ondersteund                          |
| Beheer            | Portal, PowerShell, CLI, REST API           |


  - Public vs Private DNS
    
| Eigenschap  | Public                  | Private                            |
|-------------|-------------------------|------------------------------------|
| Bereikbaar  | Vanaf internet          | Alleen vanuit gelinkte VNets       |
| Gebruik     | Externe naamresolutie   | VM-naamresolutie binnen VNet       |
| Split-horizon | —                     | ✅ Zelfde naam in public én private |


  - Key points
    - SOA + NS records worden automatisch aangemaakt bij nieuwe zone
    - SOA en CNAME ondersteunen geen record sets
    - Alias records sets verwijzen naar Azure-resources (Public IP, Traffic Manager, CDN(Content Delivery Network))



**Configure Azure DNS to host your domain**
  - Public DNS zone steps:
    - Maak DNS zone aan in Azure (subcription, resource group, domeinnaam)
    - Haal de 4 Azure DNS name server op uit het NS-record
    - Update NS-records bij domain registrat -> Domain delegation (alle 4 name server verplicht, kan 10+ min duren)
    - Verifieer via nslookup -type=SOA wideworldimports.com
    - Voeg custom records toe. A-records (hostnaam -> IP) en CNAMEs (alias -> A-record
   
  - TTL = Tijd in seconden dat een record gecached blijft in DNS

  - Private DNS zone steps:
    - Maak private DNS zone aan (bv private.wideworldimports.com)
    - Identificeer VNets waarvan VM's naamresolutie nodig hebben
    - Koppel elk VNet via een Virtual network link
   
  - Niet zichtbaar op internet, geen domain registrat nodig. Puur voor interne VM-naamresolutie binnen VNets



**Exercise - Create a DNS zone and an A record by using Azure DNS**
  - [Lab 20 Create a DNS zone and an A record by using Azure DNS](/03-az104/labs/20-create-a-dns-zone-and-an-a-record-by-using-azure-dns.md)



**Dynamically resolve resource name by using alias record**
  - Alias Records in Azure DNS
    - Een alias record koppelt een zone apex domein direct aan een Azure resource. Geen hardcoded IP nodig
    - Zone APEX = hoogste niveau van je domein (bv wideworldimports.com), ook wel root apex of @. CNAME records worden niet ondersteund op zone apex niveau. Alias records wel
    - Alias records kunnen verwijzen naar:
      - Traffic Manager profile
      - Azure CDN endpoints
      - Public IP resource
      - Front-door profile
     
    - Ondersteunde record types
      - A, AAAAA, CNAME
     
    - Voordelen
     - Geen dangling DNS records: Alias is gekoppeld aan lifecycle van Azure resource. Wijzigt het IP -> record wordt automatisch bijgewerkt
     - Zone apex load balacing: Normaal niet mogelijk met A/CNAME, wel met alias records via Traffic Manager
     - Automatische updates: IP-wijziging van de onderliggende resource wordt direct doorgevoerd in de DNS zone



**Exercise - Create alias records for Azure DNS**
  - [Lab 21 Create alias records for Azure DNS](/03-az104/labs/21-create-alias-records-for-azure-dns.md)




---

## Learning Path 5: Configure and manage virtual networks for Azure administrators
### Module 4: Configure Azure Virtual Network peering 


**Determine Azure Virtual Network peering uses**
  - VNet peering verbindt 2 VNets zodat ze als 1 netwerk functioneren. Verkeer blijft op de Azure Backbone. Geen publiek internet, gateway of encrypte vereist

  - 2 types:
    - Regional peering: VNets in dezelfde regio.
    - Global peering: VNets in verschillende regio's. Global peering tussen verschillende Azure Governemnt cloud regio's is niet toegestaan
   
  - Peering is mogelijk over subscriptions en tenats heen. VNets blijven na peering gewoon separate resources

  - Voordelen:
    - Prive verbinden via Azure Backbone met lage latency en hoge bandbreedte. Geen downtime vereist bij aanmaken of verwijderen van peering. Data transfer mogelijk cross-subscription, cross-regio en cross-deployment model
   
  - Beperkingen:
    - Overlappende address spaces: Peering mislukt; address spaces mogen niet overlappen
    - Address space wijzigen: Peering eerst verwijderen, dan aanpassen, dan opnieuw aanmaken
    - Basic Load Balancer: Werkt niet cross-region via peering; gebruik Standard Load Balancer
    - DNS: Ingebouwde Azure naamresolutie werkt niet cross-VNet; gebruik Private DNS zones of Custom DNS server


**Determine gateway transit and connectivity**
  - Concept
    - In een hub-en-spoke topologie kan 1 VPN gateway in het hub VNet gedeeld worden door alle gepeerde VNets. De spoke VNets gebruiken de gateway van het hub VNet als transit point. Geen eigen VPN gateway nodig
   
    - 4 peering-instellingen in de portal
      - Traffic to remote virtual network: Bepaalt of verkeer van dit VNet naar het remote VNet mag stromen.
      - Traffic forwarded from remote virtual network: Bepaalt of doorgestuurd verkeer (niet afkomstig van het remote VNet zelf) geaccepteerd wordt.
      - Virtual network gateway or Route Server: Laat dit VNet de gateway van het remote VNet gebruiken
     
      - VPN Gateway, belangrijke punten:
        - Een VNet kan maar 1 VPN gateway hebben
        - Gateway transit werkt voor zowel regional als global peering
        - Via gateway transit kan een spoke VNet communiceren met resources buiten de peering, zoals een on-premises netwerk (site-to-site), ander VNet (vnet-to-vnet) of VPN client (point-to-site)
        - NSG-regels tussen gepeerde VNets kun je open of dicht zetten bij het configureren van de peering
       
      

**Create virtual network peering**
  - Vereisten
    - Azure account moet de Network Contributor rol hebben (of custom rol met peering-rechten)
    - 2 VNets vereist; het 2e VNet heet het remote network
    - VM's kunnen pas communiseren nadat peering is ingesteld
   
  - Peering status
   
| Status    | Betekenis                                                              |
|-----------|------------------------------------------------------------------------|
| Initiated | Peering aangemaakt vanuit eerste VNet, tweede VNet nog niet geconfigureerd |
| Connected | Beide kanten geconfigureerd — peering actief                           |


  - Peering is pas succesvol als beide VNets de status Connected hebben

  - Aanmaken
    - Kan via Azure Portal, PowerShell of Azure CLI. In de portal: ga naar het VNet -> Settings -> Peering -> AD



**Extend peering with user-defined routes and service chaining**
  - VNet peering is non-transitief: Als A↔B en B↔C gepeerd zijn, kunnen A en C niet automatisch communiceren. Extra mechanismen zijn nodig

  - Oplossingen:
    - Hub-en-spoke: Hub VNet bevat centrale infrastructuur (NVA ofVPN gateway). Alle spoke VNets peeren met de hub; Verkeer loopt via de hub
    - User-defined route (UDR): Handmatige routeringsregel waarbij de next hop het IP-aderes is van een VM in een gepeerd VNet, of een VPN gateway
    - Service chaining: UDRs configureren die verkeer van het ene VNet via een virtual appliance of gateway in en een gepeerd VNet sturen. Combineert UDRs met hub-and-spoke
    - Azure Virtual Network Manager: Beheert hub-and-spoke of mesh peering topologieen op schaal; automatiseert peering zonder handmatige configuratie per VNet
   
    
**Exercise - Implement Intersite Connectivity**
  - [Lab 22 Implement Intersite Connectivity](/03-az104/labs/22-implement-intersite-connectivity.md)





