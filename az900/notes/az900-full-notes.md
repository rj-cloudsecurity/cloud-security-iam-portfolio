# AZ-900 Study Notes

## Week 1: 23-2-2026

- **Learning path:** Part 1. Introduction to Cloud Infrastructure: Describe cloud concepts
   - **Module:** 1. Describe cloud computing
      - **Extra:** FreeCodeCamp AZ‑90

**What is cloud computing**
   - Leveren van computer services over internet, zoals: VM’s, storage, databases en networking

**Shared responsibility model**
   - Microsoft verantwoordlijk voor: alles wat fysiek is en beveiling van de cloud
   - Klant verantwoordelijk voor: data, indentiteiten en apparaten
   - Gedeelde verantwoordelijkeheid: afhankelijk van LaaS/PaaS/Saas

**Cloud Models:**
   - Private cloud: On premises met eigen datacentre, zelf beheer van hardware netwerk en beveiliging
   - Public cloud: Cloud die door meerdere organisaties wordt gebruikt. (Azure, AWS)
   - Hybrid cloud: Combinatie van private en public cloud
   - Multi cloud: meerdere cloud provides tegelijk met Azure Arc

**Consumption-based model**
   - CapEx: Eenmalige inverstering, vooraf betalen voor eigen datacenter en hardware
   - OpEx: Doorlopende kosten, betalen per maand of gebruik
   - Consumption-based model: Alleen betalen voor wat je gebruikt
   - 
---
   
- **Learning path:** Part 1. Introduction to Cloud Infrastructure: Describe cloud concepts
   - **Module:** 2. Describe the benefits of using cloud services
      - **Extra:** FreeCodeCamp AZ‑90
   
**Benefits of high availability and scalability in the cloud**
   - High availabilty: diensten blijven draaien doordat Azure meerdere datacenters gebruikt
   - Scalability: automatisch meer of midner capaciteit gebruiken wanneer de vraag stijgt of daalt
   - Vertical scaling: groter of kleiner maken van één machine
   - Horizontal scaling: meer of minder machines toevoegen

**Benefits of reliability and predictability in the cloud**
   - Reliability: cloud blijft werken, zelfs als er iets uitvalt
   - Predictability: vooraf goed te verwachten prestaties
   - Performance: autoscaling en load balancing houden je app snel
   - Cost: cloudkosten goed voorspellen en bijsturen met realtime inzicht en tools

**Benefits of security and governance in the cloud**
   - Governance: policies en audits zorgen dat alles aan de regels voldoet
   - Security: zelf de verantwoordelijkheid kiezen IaaS of PaaS/SaaS

**Benefits of manageability in the cloud**
   - Of the cloud: Automatically scale resources, templates, health alerts
   - In the cloud: webportal, CLI, API, Powershell

---
   
- **Learning path:** Part 1. Introduction to Cloud Infrastructure: Describe cloud concepts
   - **Module:** 3. Describe cloud service types
      - **Extra:** FreeCodeCamp AZ‑90

**IaaS - Infrastructure as a Service**
   - Definitie: de infrastructuur (servers, storage, netwerk).
   - Microsoft beheert: hardware, datacenter, netwerk, fysieke beveiliging.
   - Klant beheert: OS, updates, apps, data, configuratie.
   - Voorbeelden: Azure VM, Azure Storage, Azure Virtual Network.
      
**PaaS - Platform as a Service**
   - Definitie: compleet platform (infrastructuur + OS + runtime)
   - Microsoft beheert: hardware, netwerk, OS, updates, runtime
   - Klant beheert: applicatie en data
   - Voorbeelden: Azure App Service, Azure SQL Database, Azure Functions
      
**SaaS - Software as a Service**
   - Definitie: kant‑en‑klare app via internet.
   - Microsoft beheert: alles (infrastructuur, OS, app, updates).
   - Klant beheert: instellingen en data.
   - Voorbeelden: Microsoft 365, Outlook, Teams.

**Summary:**

   Cloud computing draait om het leveren van IT‑diensten via het internet, zoals virtuele machines, opslag, databases en complete applicaties. Je werkt daarbij met een shared responsibility‑model: Microsoft beheert de fysieke infrastructuur en beveiliging van de cloud, terwijl jij verantwoordelijk bent voor je eigen data, identiteiten en apparaten. Je kunt kiezen uit verschillende cloudmodellen zoals private, public, hybrid en multicloud, afhankelijk van hoeveel controle of flexibiliteit je nodig hebt. De cloud rekent meestal via een consumption‑based model, waarbij je alleen betaalt voor wat je gebruikt in plaats van grote investeringen vooraf. Het biedt daarnaast voordelen zoals hoge beschikbaarheid, automatische schaalbaarheid, betrouwbaarheid, voorspelbare kosten en sterke beveiliging en governance. Tot slot kun je kiezen uit IaaS, PaaS of SaaS, afhankelijk van hoeveel je zelf wilt beheren en hoeveel je door de provider laat doen.

---

## Compute

| Service                     | Wat doet het?                          | Type   | Wie beheert wat? |
|-----------------------------|-----------------------------------------|--------|------------------|
| Azure Virtual Machines      | Virtuele computers draaien              | IaaS   | Microsoft: hardware, netwerk — Jij: OS, updates, apps, data |
| Azure App Service           | Webapps hosten zonder servers           | PaaS   | Microsoft: OS, runtime, scaling — Jij: code, configuratie |
| Azure Functions             | Code uitvoeren zonder servers           | Serverless / PaaS | Microsoft: infra, scaling — Jij: functie‑code |
| Azure Kubernetes Service    | Kubernetes clusters draaien             | PaaS   | Microsoft: control plane — Jij: nodes, containers |
| Azure Container Instances   | Containers draaien zonder VM’s          | PaaS   | Microsoft: infra — Jij: container‑image |

## Storage

| Service               | Wat doet het?                               | Type | Wie beheert wat? |
|-----------------------|----------------------------------------------|------|------------------|
| Azure Storage Account | Blobs, files, queues, tables opslaan         | PaaS | Microsoft: platform — Jij: data, toegangsrechten |
| Azure Disk Storage    | Virtuele harde schijven voor VM’s            | IaaS | Microsoft: fysieke disks — Jij: data |
| Azure Backup          | Automatische back‑ups                        | SaaS | Microsoft: service — Jij: wat & hoe lang je back‑upt |

## Databases

| Service                          | Wat doet het?                        | Type | Wie beheert wat? |
|----------------------------------|---------------------------------------|------|------------------|
| Azure SQL Database               | Volledig beheerde SQL‑database        | PaaS | Microsoft: engine, updates — Jij: data & schema |
| SQL Server op VM                 | SQL Server op jouw VM                 | IaaS | Microsoft: hardware — Jij: OS, SQL‑engine, updates |
| Azure SQL Managed Instance       | Bijna volledige SQL Server, beheerd   | PaaS | Microsoft: engine, patches — Jij: data |
| Cosmos DB                        | Wereldwijde NoSQL database            | PaaS | Microsoft: platform — Jij: data & queries |
| Azure Database for MySQL/PostgreSQL | Beheerde MySQL/Postgres           | PaaS | Microsoft: engine — Jij: data |

## Networking

| Service            | Wat doet het?                         | Type | Wie beheert wat? |
|--------------------|----------------------------------------|------|------------------|
| Virtual Network    | Je eigen netwerk in Azure              | IaaS | Microsoft: fysieke infra — Jij: IP’s, subnets, NSG’s |
| VPN Gateway        | On‑prem verbinden met Azure            | PaaS | Microsoft: appliance — Jij: configuratie |
| Azure Firewall     | Beheerde firewall                      | PaaS | Microsoft: service — Jij: regels & policies |
| Load Balancer      | Verkeer verdelen over VM’s             | IaaS | Microsoft: infra — Jij: LB‑regels |
| Application Gateway| Webverkeer routeren (Layer 7)          | PaaS | Microsoft: platform — Jij: routing & regels |

## Identity

| Service                     | Wat doet het?                     | Type | Wie beheert wat? |
|-----------------------------|------------------------------------|------|------------------|
| Microsoft Entra ID          | Identity & access management       | SaaS | Microsoft: service — Jij: gebruikers, rollen, policies |
| MFA / Conditional Access    | Extra beveiliging                  | SaaS | Microsoft: platform — Jij: instellingen |

## Monitoring & Management

| Service                  | Wat doet het?                       | Type | Wie beheert wat? |
|--------------------------|--------------------------------------|------|------------------|
| Azure Monitor            | Monitoring van resources             | SaaS | Microsoft: platform — Jij: alerts & dashboards |
| Log Analytics Workspace  | Opslag + query’s voor logs           | PaaS | Microsoft: platform — Jij: data & queries |
| Azure Policy             | Governance & regels afdwingen        | SaaS | Microsoft: service — Jij: policies maken |

---

Scenario‑oefeningen
   - Wie is verantwoordelijk voor het patchen van een VM?		   Customer
   - Wie beheert de fysieke beveiliging van het datacenter?	      Microsoft
   - Wie bepaalt wie toegang heeft tot een Azure Storage Account?	Customer
   - Wie beheert de OS‑updates in PaaS?					            Microsoft
   - Wie beheert de data in SaaS?						               Customer		
   - Wie beheert de firewallregels in een VNET?			            Customer
   - Wie beheert de hypervisor?						                  Microsoft
   - Wie beheert MFA‑instellingen?					                  Customer
   - Wie beheert encryptie van data at rest?				            Microsoft/Customer
   - Wie beheert de applicatiecode in App Service?		            Customer

---
   
- **Learning path:** Part 2. Introduction to Cloud Infrastructure: Azure architecture & services
   - **Module:** 1. Describe the core architectural components of Azure
      - **Extra:** FreeCodeCamp AZ‑90

**What is Microsoft Azure**
   - CSP Cloud Service Provider met een wereldwijd netwerk van datacentres
   - Honderden services om apps te bouwen
   - Compute, storage, networking, databases, AI, security en identity services
   - IaaS, PaaS, SaaS en serverless

**Azure accounts**
   - Om Azure-services te gebruiken heb je een Azure account nodig met subscriptions
   - Een account kan meerdere subscriptions hebben. Dev, test, marketing etc.
   - Resources worden altijd binnen een subscription gemaakt.

**Interacting with Azure**
   - http://portal.azure.com
   - CLI: Cloud Shell Interface that can be in PowerShell of BASH
   - PowerShell: begint met PS
   - BASH: begint met username@azure
   - Interactive mode: Enter "az interactive"
   - Auto-completion: "a"

**Azure physical infrastructure**
   - Physical infrastructure: Datacenters with racks, power, cooling, network
   - Regions: Een geografisch gebied met minstens 1 maar vaak meerdere Availability Zones
   - Availability Zones: 1 of meer datacenters, altijd onafhankelijk
   - Availability Zones: VM's, managed disks, load balancers, SQL databases
     **3 catogorieen** 
      - Zonal services: Kiest een specific zone
      - Zone-redundant services: Automatisch copy over verschillende zones
      - Non-Regional services: Global services zonder region, geen impact van zone-wide of region uitval
   - **Region pairs**
        - Meeste regions zijn verbonden met een region minstens 300 mile er vandaan.
        - Doel: Bescherming tegen grootschalige uitval; natuurramp, onrust, stroomuitval, physieke netwerk uitval
        - Niet alle Azure services zijn automatisch, kopie en herstel is dan de verandwoordelijkheid van gebruiker
        - Updates worden nooit tegelijk uitgevoerd in beide regions van een region pair
        - Data blijft in de zelfde geography als zijn pair voor voor belasting- en wetshandhaving. ex Brazil
     - **Sovereign Regions**
        - Gescheiden van de publieke Azure cloud
        - US DoD central, US Gov Virginia, US Gov Iowa. China East, China North van 21Vianet

**Azure management infrastructure**
   - **Resources and resource groups**
      - Resources, resource groups, subscriptions and account
      - Resource: alles wat je creëert, configureert of uitrolt (VM, VNet, database, storage, function)
      - Resource group: group van resources. een resource kan maar van 1 group deel uitmaken
      - Resource group: bepalen toegang, lifecycle en beheeracties
   - **Subscriptions**
      - Een subscription = eenheden voor beheer, billing en schaal
      - Nodig om Azure‑services te gebruiken (authenticatie + autorisatie)
      - Gelinkt aan een Azure account (Entra ID‑identiteit)
      - Eén account kan meerdere subscriptions hebben
   - **Subscription boundaries**
      - Billing boundary: elke subscription heeft eigen kosten, facturen en rapporten
      - Access control boundary: RBAC‑toegang wordt toegepast op subscription‑niveau
   - **Waarom extra subscriptions maken**
      - Environments: dev / test / prod scheiden
      - Organisatie: teams of afdelingen isoleren
      - Kostenbeheer: kosten per workload of afdeling scheiden
   - **Azure Management Groups**
      - Laag boven subscriptions voor governance op grote schaal
      - Subscriptions worden gegroepeerd in management groups.
      - Policies en RBAC op een management group worden geërfd door:
           - onderliggende management groups
           - subscriptions
           - resource groups
           - resources
      - **Gebruiksscenario's**
           - Policies centraal afdwingen (bijv. VM’s alleen in West US)
           - Toegang verlenen aan meerdere subscriptions tegelijk
      - **Belangrijke feiten**
           - Maximaal 10.000 management groups per directory
           - Maximaal 6 niveaus diep (root en subscriptions niet meegerekend)
           - Elke subscription of management group heeft slechts één parent
      - **Create an Azure resource**
           - [Exercise 1 Create a resource exercise](/az900/exercises/1-create-azure-resource.md)
                    
**Summary:**
   - Azure bestaat uit een wereldwijd netwerk van datacenters waar Microsoft honderden cloudservices aanbiedt voor compute, storage, networking, databases, AI, security en identity, beschikbaar in IaaS, PaaS, SaaS en serverless.
   - Je gebruikt Azure via een Azure account met 1 of meerdere subscriptions, waarin alle resources worden aangemaakt en beheerd. Je kunt met Azure werken via het Portal, PowerShell, Bash/CLI en interactieve command modi.
   - De fysieke infrastructuur bestaat uit datacenters die zijn georganiseerd in regions, availability zones en region pairs voor hoge beschikbaarheid, herstel bij rampen en naleving van regionale regelgeving en wetgeving. Er zijn ook Sovereign Regions die volledig gescheiden zijn van de publieke cloud.
   - Voor beheer gebruik je resources, resource groups, subscriptions en management groups. Recources zitten in 1 resource group, subscriptions bepalen kosten en toegang en management groups zorgen voor centraal beleid en governance over meerdere subscriptions heen.

---

- **Learning path:** Part 2. Introduction to Cloud Infrastructure: Azure architecture & services
   - **Module:** 2. Describe Azure compute and networking services
      - **Extra:** FreeCodeCamp AZ‑90

**Azure virtual machines**
   - Create VMs in de cloud. IaaS zodat je totale controle hebt over de 'computer'. Het OS, custom software en custom hosting configs en daar verantwoordelijk voor bent
   - Kopen van hardware is niet nodig
   - Gebruik van een image om meerdere VMs te configureren
   - **Scale VMs in Azure**
      - Single VMs voor testing, dev of kleine taken
      - Group VMs voor high availability, scalability and redundancy. Of scale sets en availability sets
   - **Virtual machine scale sets**
      - Maak en manage een group van identieke, load-balanced VMs
      - Manage, configure en update grote hoeveelheiden van VM's
      - Gebruik van load balancers
      - Automatisch schalen op basis van CPU, RAM, tijdschema’s
   - **Virtual machine availability sets**
      - altijd binnen 1 datacenter
      - Update domain: Niet alle VMs worden tegelijk geupdatet, 30 min tussen updates
      - Fault domain: Verdeeld VMs over 3 fault domain. Elk heeft zijn eigen power source en network switch
   - **Examples of when to use VMs**
      - Testing en Development: snel een OS en apps maken en verwijderen
      - Running applications in the cloud: voor applicaties die grote fluctuaties hebben, starten en sluiten van VMs bespaard kosten
      - Extending datacenter to the cloud: Vergroten van het on-premises netwerk
      - Disaster recovery: wanneer je primaire datacenter niet werk kan een VM het werk tijdelijk overnemen
      - Applicaties die niet geschikt zijn voor containers of PaaS‑diensten.
   - **Move to the cloud with VMs**
      - Lift and shift: Maken van een VM die identiek is aan the on-premises server. 
   - **VM Resources**
      - Size: doel, processor cores en RAM
      - Storage disks: HDD of SSD etc
      - Networking: virtual netwerk, public ip en port configuratie

 - **Create an Azure resource**
   - Merged with the later exercise in this module.

**Azure virtual desktop**
   - Toegang vanaf elk OS, device en meeste browsers
   - Alles op cloud, geen gegevens op personlijke devices
   - Microsoft Entra ID, MFA en RBAC's Role-Based Access Control.
   - Multi-session Windows 10/11: Met Enterprise multi-session, meerdere gebruikers tegelijk op 1 Virtual Desktop

**Azure containers**
   - ACI Azure Container Instances: snelste manier om één container te draaien zonder VM’s of clusterbeheer. PaaS.
        - Korte workloads zoals scrips, API, batchjobs
        - upload en direct runnen.
   - ACA Azure Container Apps: PaaS‑oplossing zonder containerbeheer, met load balancing, autoscaling en ondersteuning voor microservices.
     
De fysieke infrastructuur bestaat uit datacenters die zijn georganiseerd in regions, availability aS‑oplossing zonder containerbeheer, met load balancing, autoscaling en ondersteuning voor microservices.
   - AKS Azure Kubernetes Services: Kubernetes‑gebaseerde container orchestration voor grote containerplatformen en complexe workloads.
   - Voorbeeld: Website, front end, back end, storage in 3 containers, afzonderlijk te schalen of updaten

**Azure functions**
   - Event-driven
   - Serverless compute option
   - Geen virtual machine of container
   - Wordt gebruikt als reactie op een event. REST request, timer of bericht van een azure servcie.
   - Taken van een paar seconde of minder
   - Scale automatisch op basis van vraag
   - Kosten alleen tijdens uitvoering voor CPU time
   - Stateless (default) geen state, elke run start opnieuw
   - Stateful: (Durable Function) bewaart state en kan voortgang onthouden   

**Application hosting options**
   - Azure App Service: PaaS voor de volgende types of app services. Bied auto scalling, high availability, load balacing, Github of Azure DevOps Integratie
   
   - Types of app services
      - Web apps: ASP.NET, ASP.NET COre, Java, Ruby, Node.js, PHP of Python. Windows of Linux
      - API apps: REST‑API’s die je in elke gewenste taal kunt bouwen, met volledige ondersteuning voor Swagger/OpenAPI.
      - WebJobs: Run een program .exe, Java, PHP, Python or Node.js of een script .cmd, .bat, PowerShell or Bash. Ze kunnen gepland worden of reageren op triggers.
      - Mobile apps: Back end for iOS en Android apps.
           - Store data in cloud SQL database
           - Gebruikers laten inloggen via MSA, Google, X, Facebook
           - Push notifications
           - Custom back-end in C# or Node.js

**Azure virtual networking**
   - VMs, Web apps en databases met elkaar kunnen communiceren, over internet met on-premises netwerken
   - Isolation and segmentation: Meerdere geïsoleerde VNET maken. Zelf een prive IP-range defineren en opdelen in subnets. Voor DNS kan Azure DNS of eigen DNS server worden gebruikt.
   - Internet communications: Een public ip adress voor een Azure resource. of de resource achter een load balancer
   - Communicate betwween Azure resources
      - Virtual networks: VMs, App service environment, Kubernetes (AKS), virutal machine scale sets
      - Service endpoints: Azure SQL database and storage accounts
   - Communicate with on-premise resources:
      - Point-to-point: Encrypted VPN connection naar het Azure vitual network
      - Point-to-site: Individuele client maakt versleutelde verbinding naar azure VNET
      - Azure ExpressRoute: Prive dedicated verbinding die niet over het gewone internet gaat. Stabieler, voorspelbaarder en veiliger
   - Route network traffic
      - Route tables: Hoe verkeer tussen subnets wordt geleid. Custom routing afdwingen
      - Border Gateway Protocol BGP: Werkt met Azure VPN gateways, Azure Route Server en Azure ExpressRoute
   - Filter network traffic
      - Network security groups: Regels voor inbound en outbound connecties
      - Network virtual appliances: Network virtual appliances zijn gespecialiseerde VMs zoals firewalls of WAN-optimalisatie-apparaten
   - Connect virtual networks: VNet peering verbindt 2 VNets via het microsoft backbone-netwerk,  niet via internet. Ook cross-region
   - UDR User-Defined Routes: controle over de routing tussen subnets of VNets
   - Public en Private endpoints
   - Public endpoints hebben een public ip adres en zijn wereldwijd bereikbaar
   - Private endpoints bestaan alleen binnen het virtual network en hebben een private ip adres

**Exercise - Create an Azure Virtual Machine and Configure network access**
   - [Exercise 2 Create an Azure Virtual Machine and Configure Network Access](/az900/exercises/2-create-an-azure-virtual-machine-and-configure-network-access.md)

**Azure virtual private networks**
   - Een VPN maakt een versleutelde tunnel binnen een ander netwerk, meestal het internet. Meedere vertrouwde prive netwerken veilig met elkaar verbinden. Het is versleuteld waardoor er vertrouwelijke informatie veilig uitgewisselt kan worden
   - VPN Gateway: Speciale gateway in een Azure Virtual Network. Hij staat altijd in dedicated GatewaySubnet
     - Site-to-site: On-premises netwerk van/naar Azure VNet
     - Point-to-site: Individuele apparaten van/naar Azure Vnet
     - VNet-to-Vnet: Twee Azure VNet van/naar elkaar
   - Maar 1 VPN gateway per VNet, maar hij kan wel meerdere verbindigen tegelijk ondersteunen.
   - VPN-Gateway Policy-based: Vaste IP-regels. Oud en weinig flexibel
   - VPN-Gateway Route-based: Statisch of BGP routing; flexibel en aanbevolen voor bijna alle scenario's zoals multisite,P2S, VNet-Vnet en ExpressRoute-coexistence
   - High Availability:
        - Active/standby: standaard met automatische failover
        - Active/active: Twee active gateways met twee tunnels voor hogere beschikbaarheid
        - ExpressRoute-failover: VPN als back-up wanneer ExpressRoute uitvalt
        - Zone-redundant gateways: Gateways over meerdere availability zones
          
**Azure ExpressRoute**
   - 
   - Features and benefits of ExpressRoute
      - Priveconnectie naar microsoft cloudservices in je regio
      - Wereldwijde verbindingen tussen locaties via ExpressRoute Global Reach, ExpressRoute circuits koppelt
      - Dynamic routing via BGP, waardoor routes automatisch worden uitgewisseld tussen jouw netwerk en Azure
      - Ingebouwde redundantie bij elke peeringlocatie voor hoge beschikbaarheid
   - ExpressRoute connectivity models
      - CloudExchange colocation: Fysiek in dezelfde colocatie als de provider en maakt een viruele cross-connect
      - Point-to-point Ethernet connection: directe verbinding met jouw locatie en Microsoft
      - Any-to-any connection: WAN provider koppelt je netwerk aan Azure
      - Driect from ExpressRoute sites: Directe aansluiting op de Microsoft's backbone met 10 of 100 Gbps voor grootschalige active/active connectiviteit
   - Security considerations: ExpressRoute is een priveverbinding. data reist niet over het internet. sommige zaken zoals DNS-queries, CR: checks en CDN verkeer gaan wel over het internet

**Azure DNS**
   - Azure DNS verzorgt name resolution. Het omzetten van domeinnamen naar IP-adressen. Beheren van alle DNS records centraal via de Azure Portal, PowerShell, CLI of API's
   - Benefits:
        - Reliability and performance: Wereldwijde DNS server en anycast routing
        - Security: RBAC, activity logs en resource locks
        - Ease of use: Volledig geintegreerd in Azure
        - Customize VNets: voor je eigen domeinnamen in je VNets
        - Alias records: Automatisch verwijzen anar Azure resources zoals Public IPs, Traffic manager of CDN. Automatisch update als IP verandert
   - Azure verkooptg een domeinnamen

**Summary:**
   - Azure bestaat uit een wereldwijd netwerk van datacenters die zijn georganiseerd in regions en availability zones voor hoge beschikbaarheid en bescherming tegen uitval. 
   - Binnen Azure kun je applicaties hosten via containers (ACR, ACI, AKS), serverless functies met Azure Functions, of PaaS‑diensten zoals App Service voor webapps, API’s, mobile back‑ends en achtergrondtaken. 
   - Azure‑netwerken verbinden resources met elkaar en met on‑premises via VNet‑peering, VPN‑tunnels of ExpressRoute, met opties voor routing, filtering en private of public endpoints. VPN‑gateways maken versleutelde verbindingen over het internet, terwijl ExpressRoute een privé, dedicated verbinding biedt met hogere stabiliteit en voorspelbaarheid. 
   - Azure DNS beheert domeinnamen en DNS‑records via Microsoft’s wereldwijde infrastructuur, inclusief private zones en alias‑records die automatisch meeveranderen met Azure‑resources.

















