# AZ-900 Study Notes

## 23-2-2026 t/m 9-3-2026

- **Learning path:** Part 1. Introduction to Cloud Infrastructure: Describe cloud concepts
   - **Module:** 1. Describe cloud computing
      - **Extra:** FreeCodeCamp AZ‑90

**What is cloud computing**
   - Leveren van computer services over internet, zoals: VM’s, storage, databases en networking

**Shared responsibility model**
   - Microsoft verantwoordlijk voor: alles wat fysiek is en beveiling van de cloud
   - Klant verantwoordelijk voor: data, indentiteiten en apparaten
   - Gedeelde verantwoordelijkeheid: afhankelijk van IaaS/PaaS/Saas

**Cloud Models:**
   - Private cloud: On premises met eigen datacenter, zelf beheer van hardware netwerk en beveiliging
   - Public cloud: Cloud die door meerdere organisaties wordt gebruikt. (Azure, AWS)
   - Hybrid cloud: Combinatie van private en public cloud
   - Multi cloud: meerdere cloud provides tegelijk met Azure Arc

**Consumption-based model**
   - CapEx: Eenmalige inverstering, vooraf betalen voor eigen datacenter en hardware
   - OpEx: Doorlopende kosten, betalen per maand of gebruik
   - Consumption-based model: Alleen betalen voor wat je gebruikt

---
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
   - Security: zelf de verantwoordelijkheid kiezen IaaS, PaaS of SaaS

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
---
   
- **Learning path:** Part 2. Introduction to Cloud Infrastructure: Azure architecture & services
   - **Module:** 1. Describe the core architectural components of Azure
      - **Extra:** FreeCodeCamp AZ‑90

**What is Microsoft Azure**
   - CSP Cloud Service Provider met een wereldwijd netwerk van datacenters
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
   - **3 catogorieen** 
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
   - Microsoft merged this exercise with the later exercise in this module.

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
   - Communicate between Azure resources
      - Virtual networks: VMs, App service environment, Kubernetes (AKS), virtual machine scale sets
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

---
---

- **Learning path:** Part 2. Introduction to Cloud Infrastructure: Azure architecture & services
   - **Module:** 3. Describe Azure storage services
      - **Extra:** FreeCodeCamp AZ‑90

**Azure storage accounts**
   - Toegankelijk wereldwijd over HTTP OF HTTPS
   - Blobs, files, queues en tables
   - Secure, highly available, durable en massively scalable
   - Redundancy
      - LRS       - Locally Redundant Storage
      - GRS       - Geo-Redundant Storage
      - RA-GRS    - Read-Acces Geo Redundant Storage
      - ZRS       - Zone-Redundant Storage
      - GZRS      - Geo-Zone-Redundant Storage 
      - RA-GZRS   - Read-Access Geo-Zone_redundant Storage

   - Standard general purpose v2: Ondersteut alle opslagdiensten en de meeste redundantieopties.Geschik voor de meeste workloads
   - Premium block blobs: Geoptimaliseerd voor hoge transactiesnelheid en lage latency voor blob opsloag
   - Premium file shares: bedoeld voor snelle Azure Files workloads, SMB NFS
   - Premium page blobs: Page blobs zoals VHD's
     
   - Blob storage             - https://<storage-account-name>.blob.core.windows.net
   - Data lake storage gen2   - https://<storage-account-name>.dfs.core.windows.net
   - Azure files              - https://<storage-account-name>.file.core.windows.net
   - Queue storage            - https://<storage-account-name>.queue.core.windows.net
   - Table storage            - https://<storage-account-name>.table.core.windows.net

**Azure storage redundancy**
   - Azure slaat data altijd meerdere keren op zodat deze beschermd is tegen hardwarefoute, stroomstoringen of zelfs grote regionale uitval
   - Redundantie bepaalt hoe vaak en waar je data wordt gekopieerd, daarmee ook de beschikbaarheid, duurzaamheid en kosten

   - Redundatie binnen de primaire regio. Altijd 3 kopieen in de primaire regio met 2 keuzes:
        - LRS Locally Redundant Storage: 3 kopieen in 1 datacenter, goedkoop maar kwetsbaar bij datacenter ramp
        - ZRS Zone Redundant Storage: 3 Kopieen verspreid over 3 AZs
   - Redundatie naar secundaire regio. Extra bescherming omdat data ook in een 2e regio staat
        - GRS Geo Redundant Storage: LRSi n primaire regio, LRS in secundaire regio
        - GZRS Geo Zone Redundant Storage: ZRS in primaire regio, LRS in de secundaire regio. Max Beschikbaarheid en duurzaamheid
        - Replicatie naar secundaire regio is asynchroon, bij ramp een klein stuk data verloren RPO <15min
   
**Azure storage services**
   - Azure Blobs: schaalbare object opslag voor tekst en binary data, incl big data analyse door Data Lake Storage Gen2
   - Azure Files: beheerde file shares die je kunt gebruiken vanuit de cloud of on-premises
   - Azure Queues: eenvoudige berichtenopslag voor communicatie tussen applicatieonderdelen
   - Azure Disks: block-level opslag voor VMs
   - Azure Tables: NoSQL opslag voor gestructureerde, niet relationele data
     
   - Benefits of Azure Storage
        - Durable and highly available: Redundancy zodat data veilig is bij hardware- of regiostoringen. Kopieen tussen verschillende datacenters of geographical regions.
        - Secure: data versleuteld met gedetailleerde toegang
        - Scalable: voor grote hoeveelheden data en hoge performance
        - Managed: Azure verzorgt hardware maintenance, updates en critical issues
        - Accessible: Accessible wereldwijd over HTTP of HTTPS. .NET, Java, Node.js, Python, PHP, Ruby, Go, REST API. Scripting in Azure PowerShell of CLI. Visual solutions with Azure Portal en Azure Storage Explorer

   - Azure Blobs
      - Grote hoeveelheden ongestructeerde data, tekst, afbeeldingen, video's of logbestanden. Werelwijd te bereiken via HTTP(S) met tools zoals REST API, Azure CLI, PowerShell of client-libraries voor o.a. .NET, Java Python en Node.js.
      - Verschillende tiers zodat je kosten kunt afstemmen op hoe vaak data wordt gebruikt:
      - Hot: data die vaak wordt gelezen
      - Cool: minder vaak gebruikt en minimaal 30 dagen blijft staan
      - Cold: zelden gebruikt en minimaal 90 dagen blijft staan
      - Archive: bijna nooit wordt gebruikt, minimaal 180 bewaart blijft. Goedkoop opslaag maar duur om terug te halen

   - Azure Files
      - Volledig beheerde files shares in de cloud via SMB of NFS. Tegelijk te gebruiken vanuit de cloud en on-premises.
      - MB shares werken op Windows, Linux en MacOS,
      - NFS shares op Linux en macOS.
      - Azure File Sync: SMB shares lokaal cachen voor snelle toegang
      - Voordelen: gedeelde toegang, geen serverbeheer, scripting via PowerShell/CLI, hoge beschikbaarheid en compatibiliteit met bestaande applicaties

   - Azure Queues
      - Opslaan van grote aantallen berichten (miljoenen). Berichten kunnen tot 64 KB groot zijn.
      - Wereldwijd te bereiken via HTTP(S)
      - Taken asynchroon te verwerken, bijvoorbeeld in combinatie met Azure Functions die automatisch reageren wanneer een nieuw bericht binnenkomt.

   - Azure Disks
      - Beheerde block level schijven voor VMs. Werken als fysieke disks, maar volledig door Azure beheerd
      - High availability, High reliability en eEasy provisioning.

   - Azure Tables
      - NoSQL opslag voor grote hoeveelheiden gestructureerde niet relationele data.
      - Toegang via Azure en externe omgevingen
      - Geschikt voor hybride of multicloud scenario's

**Exercise - Create a storage blob**
   - [Exercise 3 Create a storage blob](/az900/exercises/3-create-a-storage-blob.md)
   
**Identify Azure data migration options**
   - Azure Migrate: centrale platform om workloads van on-premises naar Azure te verplaatsen. De plek waar je migratie kunt discover, assess en Migrate. Het ondersteunt servers, applicaties en databases
      - Discovery and Assessment: analyseert VMware-, Hyper-V- en fysieke servers om te bepalen wat klaar is voor migrate
      - Server Migration: verplaatst VMs, fysieke servers en workloads van andere clouds naar Azure
      - Data Migration Assistand DMA: controleert SQL servers op compatibiliteit en mogeljke blokkades
      - Azure Database Migration Service DMS: migreert databases naar Azure SQL Database, SQL managed Instance of SQL server op Azure VMs
      - App Service Migration Assistant: beoordeelt en migreert .NET- en PHP-website naar Azure App Service.
   
   - Azure Data Box
   - Fysiek apparaat die je kan bestellen om grote hoeveelheden data tot 80 TB snel en veilig naar Azure te verplaatsen. Data gewist volgens NIST 800-88r1
   - Wanneer Azure Data Box gebruiken:
      - One-time migration: grote bulk data naar Azure
      - Meida libraries: offline tapes of grote mediacollecties digitaliseren
      - VM farms en SQL server migreren: de 1e grote datastap
      - Historical data: Grote datasets naar Azure brengen voor analytics.
      - Initial bulk transfer: 1e grote upload via Data Box, daarna incrementale uploads via het netwerk
      - Periodic uploads: wanneer je regelmatig grote hoeveelheden data genereert

   - Export Scenarios:
     - Disaster recovery: grote hoeveelheden Azure data terughalen naar on-premises
     - Security/Compliance: data fysiek exporteren vanwege regelgeving
     - Cloud-to-cloud of terug naar on-premises: workloads verplaatsen naar andere omgeving.
    
**Identify Azure file movement options**
   - AzCopy: command-line tool waarmee je bestanden en blobs kunt vreplaatsen naar, van of tussen Azure Storage accounts. Uploaden, downloaden, kopieren en zelfs eenrichtings-synchronisatie uitvoeren. Bij synchronisatie kies je altijd een soure en destination. AzCopy werkt nooit bi-directioneel
   
   - Azure Storage Explorer: een grafische applicatie (Windows, macOS, Linux) waarmee je eenvoudig bestanden en blobs kunt beheren in je Azure Storage account. Het gebruikt AzCopy op de achtergrond, maar biedt een visuele interface om te uploaden, downloaden en data tussen storage accounts te verplaatsen.

   - Azure File Sync: lokale windows file server koppelen aan Azure Files, zodat je 1 centrale file share in Azure hebt, terwijl je lokaal de performance en compatibiliteit van Windows Server behoudt. Het werkt bi-directioneel en houdt je lokale server en Azure Files automatisch synchroon.

   - Toegang via alle Windows Server-protocollen zoals SMB, NFS en FTPS
   - Meerdere loakel caches wereldwijd
   - Kapotte server vervangen door simpelwg Azure File Sync opnieuw te installeren
   - Cloud Tiering: veelgebruikte bestanden lokaal houden, minder gebruikte bestanden alleen in Azure totdat ze nodig zijn.

**Summary:**
   - Azure Storage biedt werelwijde, veilige en schaalbare opslag via 1 storage account dat verschillende diensten ondersteunt: Blobs, Files, Queues en Tables, elk bereikbaar via HTTP(S) en specifieke service-endpoints
   - Beschikbaarheid en duurzaamheid worden bepaald door redundancy options zoals LRS, ZRS, GRS, GZRS  en hun read-access varianten. Data wordt altijd minimaal 3 keer opgeslagen, en kan optioneel naar een tweede regio worden gerepliceerd.
   - Azure Storage services omvatten Blob Storage voor ongestructureerde data met hot/cool/cold/archive tiers, Azure File Sync, Queues voor asynchrone messaging, Disks voor VM-block storage en Tables voor NoSQL-data
   - Storage accounts bestaan in verschillende performance types zoals Standard, GPv2, Premium Block Blobs, Premium File Shares en Premium Page Blobs, afgestemd op workload vereisten zoals throughput, latency of VM gebruik
   - Voor data migratie beidt Azure zowel online als offline opties: Azure Migrate voor discover/assess/migrate van servers, databases en apps. Azure Data Box voor fysieke bulk overdracht tot 80 TB per device, geschikt voor one-time, periodic of DR-scenarios.
   - Voor het verplaatsen van individuele bestanden zijn er tools zoals AzCopy (CLI voor kopie and sync), Azure Storage Explorer (GUI voor blob/filemanagement) en Azure File Sync (bi-directionele sync tussen Windows file servers en Azure Files met cloud tiering).
     
---
---

- **Learning path:** Part 2. Introduction to Cloud Infrastructure: Azure architecture & services
   - **Module:** 4. Describe Azure identity, access, and security
      - **Extra:** FreeCodeCamp AZ‑90

**Azure directory services**
   - Microsoft Entra ID
      - Directory service voor toegang tot Microsoft cloud applicaties en zelf ontwikkelde applicaties
      - On-premises gebruik je Active Directory op Windows Server, beheerd door jouw organisatie
      - In de cloud, Microsoft Entra ID, beheerd door Microsoft maar jij beheert de identity accounts
      - On-premises Active Directory koppelen aan Microsoft Entra ID, detecteert Microsoft automatisch suspicious sing-in attemps zoals logins vanaf unexpected locations of unknow devices (gratis)

   - Who uses Microsoft Entra ID?
      - IT administrators: toegangsbeheer tot applicaties en resources
      - App developers: SSO en authenticatie toevoegen aan applicaties
      - Users: eigen identiteit beheren en self-service password reset
      - Online service subscribers: Microsfot 365, Azure en dynamics CRM Online gebruiken Microsoft Entra ID automatisch voor authenticatie
    
   - What does Microsoft Entra ID do?
      - Authentication: identity verifieren voor toegang to applicaties en resources, inclusief self-service password reset, multifacotr authentication, banned passwords lijst en smart lockout
      - Single sign-on: 1 username en wachtwoord voor toegang to meerder applicaties. Als een gebruiker van rol wisselt of de organisatie verlaat hoef je maar 1 identity aan te passen
      - Application management: cloud en on=premises apps beheren via Application Proxy, SaaS apps en de My Apps portal
      - Device management: apparaten registreren en beheren via Microsoft Intune. Hiermee kun je Conditional Acces policies instellen die alleen toegang geven vanaf known devices.

   - Can I connect my on-premises AD with Microsoft Entra ID?
      - Zonder koppeling heb je twee losse identity sets: 1 on -premises en 1 in de cloud
      - Met Microsoft Entra Connect koppel je beide systemen en synchroniseer je user identities tussen on-premises Active Directory en Microsoft Entra ID
      - Hierdoor werken SSO, multifactor authentication en self-service passwords reset in beide omgevingen

   - What is Microsfot Entra Domain Services?
      - Managed domain services die klassieke functies biedt zoals domain join, group policy, LDAP en Kerberos/NTLM authentication
      - Je hoeft zelf geen domain controllers te deployen, beheren of patchen, Microsoft regelt dat
      - Handig voor legacy applications die geen moderne authentication methoden ondersteunen
      - Maakt lift-and-shift van on-premises applicaties naar de cloud mogelijk zonder AD DS zelf te beheren
      - Integreert met je bestaande Microsoft Entra tenant zodat gebruikers hun bestaande credentials kunnen blijven gebruiken

   - How does Microsoft Entra Domain Services work?
      - Definieert een unique namespace, dit is je domain name
      - Azure deployed automatisch twee Windows Server domain controllers in jouw Azure region, dit heet een replica set
      - Domain controllers hoef je niet te beheren, configureren of updaten, Azure regelt alles inclusief backups en encryption at rest via Azure Disk Encryption

   - Is information synchronized?
      - Synchronization is one-way: van Microsoft Entra ID naar Microsoft Entra Domain Services, niet andersom
      - Resources die je direct in de managed domain aanmaakt worden niet teruggesynchroniseerd naar Microsoft Entra ID
      - In een hybrid environment synchroniseert Microsoft Entra Connect eerst naar Microsoft Entra ID, Daaran wordt dat doorgesynchroniseerd naar de managed domain
      - Applications, services en VMs in Azure die verbonden zijn met de managed domain kunnen gebruik maken van domain join, group policy, LDAP en Kerberos/NTLM authentication

**Azure authentication methods**
   - Authentication is het proces van het vaststellen van de indentity van een persoon, service of device
   - Je bewijst wie je bent door credentials te verstrekken, vergelijkbaar met een ID tonen op reis
   - Azure ondersteunt meerdere authentication methoden: passwords, SSO, Multifactor authentication (MFA) en passwordless
   - Passwordless is zowel high security as high convenience
   - Een los opassword is high convernience maar low security

   - What's single sign-on?
      - SSO betekent 1 keer inloggen met credential voor toegang tot meerdere applicaties en provides
      - Zonder SSO heeft elke gebruiker meerdere passwords met verschillende policies, wat leidt tot meer security risico's en meer druk op de helpdesk
      - Als een gebruiker de organisatie verlaat is het met meerdere identities lastig om alle accounts te vinden en te disablen, met SSO hoef je maar 1 identity te disablen
      - SSO vereenvoudigt het security model: 1 identity per gebruiker, gekoppeld aan hun rol
      - Belangrijk: SSO is alleen zo veilig als de initial authenticator, alle volgende verbindengen zijn gebaseerd op de beveiliging van die eerste login

   - What’s multifactor authentication?
      - MFA vereist twee of meer verificatiemethoden tijdens het inloggen
      - 3 categorieen:
         - Something the user knows: bijvoorbeeld een challenge question of password
         - Something the user has: bijvoorbeeld een code op je telefoon
         - Something the user is: biometric zoals fingerprint of face scan
      - Als een attacker alleen je password heeft, kan hij nog steeds niet inloggen zonder de tweede factor
      - MFA moet overal worden ingeschakeld waar mogelijk vanwege de enorme security voordelen
     
   - What's Microsoft Entra multifactor authentication?
      - Microsoft service die de MFA mogelijk maakt
      - Gebruikers kiezen een extra authentication methode tijdens het inloggen, zoals een phone call of mobile app notification
     
   - What’s passwordless authentication?
      - Passwordless vervangt het password door something you have + something you are of something you know
      - Gebruikers zijn meer geneigd zich aan security regels te houden als het makkelijk en convenient is
      - Je device moet eerst geregistreerd worden voordat passwordless werkt, daarna weet Azure dat het device bij jou hoort
      - voorbeeld: je laptop is something you have, je PIN of fingerprint is something you know of something you are, samen authenticeer je zonder password
      - Microsfot biedt 3 passwordless opties die integreren met Microsoft Entra ID
         - Windows Hello for Business
         - Microsoft Authenticator app
         - FIDO2 security keys
     
   - Windows Hello for Business
      - Ideaal voor gebrukers met een eigen vaste Windows PC
      - Biometric en PIN credentials zijn direct gekoppeld aan de PC van de gebruiker, niemand anders kan inloggen
      - Heeft PKI integratie en ingebouwde SSO ondersteuning voor toegang tot corporate resources on-premises en in de cloud
     
   - Microsoft Authenticator App
      - Maakt van elke iOS of Android phone een passwordless credential
      - Werkt op elk platform en elke browser via een notification op je phone
      - Je bevestigt je login door een nummer op je scherm te matchen met je phone en daarna je biometric (touch of face) of PIN te gebruiken
      - Kan ook worden gebruikt als MFA optie naast een password
     
   - FIDO2 security keys
      - FIDO Fast Identity Online is een open standard voor passwordless authentication zonder username of password
      - FIDO2 is de nieuwste standaard en bouwt voort de WebAuthn standard
      - FIDO2 security keys zijn unphishable, er is geen password dat gestolen of geraden kan worden
      - Typisch een USB device maar Bluetooth of NFC is mogelijk
      - Gebruikers registeren hun security key eenmalig en gebruiken die daarna als authentication methode

**Azure external identities**
   - External identity is een persoon, device of service buiten jouw organisatie
   - Microsoft Entra External ID regelt hoe je veilig samenwerkt met gebruikers buiten je organisatie
   - External users kunnen hun eigen bestaande identity gebruiken om in te loggen, zoals een corporate account, Google of Facebook. Jij beheert alleen de toegang via Microsoft Entra ID
   - Drie mogelijkheden
      - B2B collaboration: externe gebruikers loggen in met hun eigen identity op jouw Microsoft of enterprise applicaties. Ze worden in jouw directory opgeslagen als guest users
      - B2B direct connect: twee-weg vertrouwensrelatie met een andere Microsoft Entra organisatie, Gebruikers zijn niet zichtbaar in jouw directory maar wel in Teams shared channels
      - Azure AD B2C: identity en access management voor consumers en customers van jouw eigen SaaS of custom apps
   - Microsoft Entra B2B kun je guest users uitnodigen vanuit een andere tenants of social identities zoals Microsoft accounts
   - Via Access Review kun je periodiek controleren of guest users nog steeds toegang nodig hebben en indien nodig toegang intrekken

**Azure conditional access**
   - Conditional Access i seen tool in Microsoft Entra ID die toegang toestaat of blokkeert op basis van identity signals
   - Signals zijn: wie de gebruiker is, waar de gebruiker is en vanaf welk device de gebruiker inlogt
   - 3 stappen
      - Signal: verzamelen van informatie over de gebruiker,locatie en device
      - Decision: beslissing nemen op basis van signals
      - Enforcement: de beslissing uitvoeren, toegang verlenen, blokkeren of MFA vereisen
   - Voorbeeld: een gebruiker op een bekende locatie krijg direct toegang, maar vanaf een unknown of high risk locatie wordt toegang geblokkeeerd of MFA vereist
   
   - When can I use Conditional Access?
      - MFA vereisen op basis van rol, locatie of netwerk
      - Toegang alleen toestaan via approved client applications
      - Toegang alleen toestaan vanaf managed devices
      - Toegang blokkeren vanaf untrusted of unknown locations


**Azure role-based access control**
   - RBAC: gebaseerd op het principe van least privilege; alleen toegang geven die nodig is voor een taak
   - In plaats van per persoon toegang te beheren, wijs je mensen toe aan een role met bijbehorende permissions
   - Nieuwe teamleden krijgen automatisch de juiste toegang door ze aan de juiste RBAC group toe te voegen
   - RBAC wordt toegepast op een scope:
      - Management group
      - Subscription
      - Resource group
      - Single resource
   - RBAC is hierarchaish: permissions op een parent scope worden geerfd door alle child scopes
      - Voorbeeld: owner rol op management group niveau geeft toegang tot alle subscriptions daaronder
      - Voorbeeld: Reader rol op subscription niveau geeft leestoegang tot alle resource groups en resources daarbinnen
   - RBAC wordt gehandhaafd via Azure Resource Manager, toegankelijk via de Azure Portal, Cloud Shell, PowerShell en CLI
   - RBAC regelt geen toegang op applicatie of data niveau, dat is de verantwoordelijkheid van de applicatie zelf
   - RBAC gebruikt een allow model: als twee rollen elkaar overlappen krijg je beide permissions gecombineerd
    
**Azure Zero Trust model**
   - Zero Trust is een security model dat atlijd uitgaat van het worst case scenario, assume breach
   - Elk request wordt geverifieerd alsof het afkomstig is van een uncontrolled network, ongeacht de locatie
   - Drie guiding pinciples
      - Verify explicitly: altijd authenticeren en autoriseren op basis van alle beschikbare data points
      - Use least privilege access: toegang beperken via Just-In-Time en Just-Enough-Access (JIT/JEA) en risk-based adaptive polices
      - Assume breach: toegang segmenteren, end-to-end encryption verfieren en analytics gebruiken voor threat detection
   - Traditioneel werd een corporate network als veilig beschouwd, managed devices konden joinen, VPN was tightly controlled
   - Zero Trust draait dat om: niet de locatie maar de authentication bepaalt de toegang
   
**Defense-in-depth**
   - Beschermt data door meerdere lagen van beveiliging te gebruiken
   - Als 1 laag wordt doorbroken, is er altijd een volgende laag die verdere schade beperkt
   - Het vertraagt een aanval en geeft security teams de tijd om te reageren
   - De 7 lagen van buiten naar binnen:
      - Physical security: bescherming van de fysieke hardware in het datacenter
      - Identity and access: toegangsbeheer tot infrastructure en cahnge control
      - Permimeter: DDoS protection om grootschalige aanvallen te filteren
      - Network: communicatie beperken via segmentation en access controls
      - Compute: toegang beveiligen tot virtual machines
      - Application: applicaties beveiligingen en vrij houden van security vulnerabilities
      - Data: toegang beheren tot business en customer data
        
   - Physical security
      - Eerste verdedigingslinie: fysieke toegang tot gebouwen en hardware in het datacenter beveiligen
      - Zorgt ervoor dat andere lagen niet omzeild kunnen worden via fysieke toegang
      
   - Identity and access
     - Identities beveiligen en toegang alleen verlenen aan wat nodig is
     - Belangrijke maatregelen:
         - Access control to infrastructure en change control
         - SSO en multifactor authentication gebruiken
         - Events en changes auditen en loggen
              
   - Perimeter
     - Beschermt tegen network-based attacks
     - Belangrijke maatregelen
         - DDoS protection om grootschalige aanvallen te filteren voordat ze de availability beinvloeden
         - Perimeter firewalls gebruiken om malicious attacks te identificeren en te melden
              
   - Network
     - Communicatie beperken tot alleen wat noodzakelijk is om verspreiding van aanvallen te verkomen
     - Belangrijke maatregelen
         - Deny by default
         - Inbound internet access beperken en outbound access waar nodig limiteren
         - Secure connectivity naar on-premises networks implementeren
     
   - Compute
     - Malware, unpatched systems en slecht beveiligde systemen openen de deur voor aanvallen
     - Belangrijke maatregelen
          - Secure access tot virtual machines
          - Endpoint protection implementeren en systemen up-to-date houden
     
   - Application
     - Security intergreren in de application development lifecycle om vulnerabilities te verminderen
     - Belangrijke maatregelen
          - Applicaties beveiligen en vrij houden van vulnerabilities
          - Sensitive secrets opslaan in een secure storage medium
          - Security als design requirement meenemen in alle application development
     
   - Data
     - Degene die data opslaat en beheert is verantwoordelijk voor de beveiliging ervan
     - Aanvallers zijn bijna altijd op oek naar data, in databases, op VM disks, in SaaS applications of in de cloud storage
     - Regelgeving dicteert vaak de controls die nodig zijn voor confidentiality, integrity en availability van data
     
**Microsoft Defender for Cloud**
   - Defender for cloud is een monitoring tool voor security posture management en threat protection
   - Monitort cloud, on-premises, hybrid en multicloud omgevingen
   - Is natively geintegreerd in Azure, geen deployment nodig voor Azure services

   - Protection everywhere
      - Voor hybrid en multicloud omgevingen wordt Azure Arc gebruikt om non-Azure machines te beschermen
      - Cloud Security Posture Management (CSPM) werkt op multicloud zonder agents

   - Azure-native protections
      - Detecteert threats op Azure PaaS services zoals App Service, Azure SQL en Storage
      - Classificeert automatisch data in Azure SQL en geeft vulnerability assessments
      - Beschermt tegen brute force attacks via just-in-time VM access op geselecteerde ports

   - Hybrid en multicloud
      - On-premises machines beschermen via Azure Arc
      - AWS en GCP worden ook ondersteund:
         - CSPM features voor AWS resources inclusief secure score
         - Microsoft Defender for Containers voor Amazon EKS Clusters
         - Microsoft Defender foor Server voor Windows en Linux EC2 instances
       
   - Drie kernfucnties, Assess, Secure, Defend
        - Continuously assess: security posture kennen, vulnerabilities identificeren via scans op VMs, container registries en SQL server
        - Secure: resources hardenen via security policies gebouwd op Azure Policy controls. Nieuwe resources worden automatisch gecontroleerd op security best practices en krijgen een priotized lijst van aanbevelingen. Een secure score geeft een overzicht van de gezondheid van je security posture
        - Defend: security alerts genereren bij gedetecteerde threats met details, remediation steps en optioneel een logic app trigger. Fusion kill-chain analysis correleert alerts automatisch om het volledige verhaal van een aanval te begrijpen. Advanced threat protection voor VMs, SQL databases, containers, web applications en networks
          

**Summary:**
   - Microsoft Entra ID is de cloud-based identity and access management service van Microsoft die authentication, SSO, application management en device management biedt. On-premises Active Directory kan worden gekoppeld via Microsoft Entra Connect voor een consistente identity experience. Microsoft Entra Domain Services biedt managed domain services zoals domain join, group policy en LDAP zonder zelf domain controllers te beheren
   - Azure ondersteunt meerdere authentication methoden van zwak naar sterk: passwords (low security), SSO (1 identity voor meerdere applicaties) MFA (iets wat je weet + hebt + bent) en passwordless via Windows Hello for Business, Microsoft Authenticator App of FIDO2 security keys.
   - External identities maken samenwerking buiten je organisatie mogelijk via B2B collaboration (guest users), B2B direct connect (Teams shared channels) of Azure AD B2C (consumers en custumers). External users brengen hun eigen identity mee, jij beheert alleen de toegang
   - Conditional Access verleent of blokkeert toegang op basis van identity signals zoals gebruiker, locatie en device, en kan MFA vereisen bij suspicious of high risk situaties.
   - Azure RBAC regelt toegang via roles en scopes op basis van least privilege. Permissions zijn hierarchisch en worden geerfd van parent naar child scopes. RBAC wordt gehandhaafd via Azure Resource Manager.
   - Zero Trust gaat altijd uit van assume breach en vereist verify explicitly, least privilege access en end-to-end encryption, ongeacht de locatie van de gebruiker.
   - Defense-in-depth beschermt data via zeven lagen: physical security, identity and access, perimeter, network, compute, application en data. Elke laag vertraagt een aanval en beperkt schade als een vorige laag wordt doorbroken.
   - Microsoft Defender for Cloud monitort cloud, on-premises, hybrid en multicloud omgevingen via drie kernfuncties: continuously assess (vulnerabilities identificeren), Secure (resources hardenen via security policies en secure score) en defend (threats detecteren via security alerts en fusion kill-chain analysis)

         
---
---


- **Learning path:** Part 3. Describe Azure management and governance
   - **Module:** 1. Describe cost management in Azure
      - **Extra:** FreeCodeCamp AZ‑90


**Describe factors that can affect costs in Azure**
   - Azure werkt met OpEx in plaats van CapEx, je betaald voor wat je gebruikt in plaats van vooraf te investeren in infrastructure
   - Factoren die kosten beïnvloeden:
      - Resource type: het type resource, de instellingen en de Azure region bepalen de kosten. Azure maakt metered instances aan die gebruik bijhouden en de factuur berekenen
        - Storage account: kosten verschillen per type, performance tier, access tier, redundancy settings en region
        - Virtual machines: kosten verschillen per OS licentie, processor, cores, storage en network interface, en per region

   - Consumption: pay-as-you-go betekent betalen voor wat je gebruikt. Azure biedt ook reserved capacity met kortingen tot 72% bij commitment van 1 of 3 jaar. Bij een surge boven je reservering betaal je alleen het verschil vie pay-as-you-go

   - Maintainance: recourses opruimen die niet meer nodig zijn. Als je een VM verwijdert worden bijbehorende recources zoals storage en networking niet automatisch verwijderd, dit kost onnodig geld

   - Geography: kosten verschillen per region door verschillen in energie, arbeid en belastingen. Netwerkverkeer binnen Europa is goedkoper dan tussen continenten

   - Network traffic: inbound data naar Azure datacenters is gratis. Outbound data wordt berekend op basis van billing zones, geografische groeperingen van Azure regions

   - Subscribtion Type: type beinvloedt kosten. Een free trail van 12 maanden gratis toegang tot bepaalde services en credit voor de eerste 30 dagen

   - Azure Marketplace: Third-party oplossingen en services kopen via Azure. Je betaalt zowel voor Azure services als voor third-party vendor. Alle oplossingen zijn gecertificieerd en compliant met Azure polices

**Explore the pricing calculator**
   - De pricing calculator geeft een geschatte kostprijs voor resources in Azure
   - Je kunt individuele resources, complete oplossingen of voorbeeldscenario's doorrekenen
   - De calculator is alleen informatief, er wordt niet aangemaakt en je wordt nergens voor gefactureerd
   - Je kunt kosten berekenen voor compute, storage en networking inclusief storage type, access tier en redundancy

**Explore the pricing calculator**
   - [Exercise 4 Estimate workload costs by using the Pricing calculator](/az900/exercises/4-estimate-workload-costs-by-using-the-pricing-calculator.md)

**Describe the Microsoft Cost Management tool**
   - Cost Management helpt onverwachte Azure kosten te voorkomen en te beheren
   - Functionaliteiten: kosten bekijken, alerts instellen en budgets maken
   - Cost analysis: visueel overzicht van kosten per billing cylce, region of resource. Helpt spending trends te identificeren en maandelijkse, kwartaal of jaarlijkse kostentrends te schatten
  
   - Cost alerts: drie typen alerts:
     - Budget alerts: melding wanneer spending de ingestelde limiet bereikt of overschrijdt, op basis van kosten of verbruik
     - Credits alerts: melding bij 90% en 100% verbruik van Azure credit, alleen voor Enterprise Agreement klanten.
      - Department spending quota alerts: melding wanneer een afdeling een ingesteld percentage van het quota bereikt, bijvoorbeeld 50% of 75%
   
   - Budgets: spending limiet instellen op basis van subscription, resource group of service type. Als de limiet bereikt wordt, wordt een alert getriggerd.
  
   - Geavanceerd gebruik: automatisch resources pauzeren of aanpassen wanneer het budget wordt overschreden

**Describe the purpose of tags**
   - Tags zijn metadata die je toevoegt aan Azure resources om ze te organiseren en te beheren
   - Een tag bestaat uit een naam en een waarde, bijvoorbeeld Environment: Production
   
   - Waarvoor gebruik je tags voor:
      - Resource management: resources vinden en beheren per workload, omgeving, afdeling of eigenaar
      - Cost management: kosten rapporteren en toewijzen aan interne cost centers
      - Operations management: resources groeperen op beschikbaarheidskritikaliteit voor SLA's
      - Security: data classificeren op beveilingsniveau zoals public of confidential
      - Governance en compliance: resources identificeren die voldoen aan regelgeving zoals ISO 27001
      - Workload automatisering: resources taggen voor gebruik met tools zoals Azure DevOps

   - Beheer van tags:
      - Tags toevoegen via PowerShell, Azure CLI, ARM templates, REST API of de Portal
      - Azure Policy gebruiken om tagging regels af te dwingen
      - Resources erven tags niet automatisch van subscriptions of resource groups, elke laag heeft eigen tags

   - Voorbeeld tag structuur:
      - AppName, Costcenter, Owner, Environment, Impact

**Summary**
   - Azure kosten worden bepaald door resource type, consumption, maintenance, geography, network traffic, subscription type en Azure Marketplace. Pay-as-you-go is het standaard model, maar reserved capacity biedt kortingen tot 72% bij commitment van 1 of 3 jaar.
   - De pricing calculator geeft een kostenschatting voor resources zonder iets aan te maken of te factureren. Cost Management helpt onverwachte kosten te voorkomen via cost analysis, budget alerts, credit alerts en department spending quota alerts.
   - Tags zijn metadata op Azure resources bestaande uit een naam en waarde. Ze worden gebruikt voor resource management, cost management, security, governance en workload automatisering. Tags worden niet automatisch geërfd tussen lagen.


---
---


- **Learning path:** Part 3. Describe Azure management and governance
   - **Module:** 2. Describe features and tools in Azure for governance and compliance
      - **Extra:** FreeCodeCamp AZ‑90

**Describe the purpose of Microsoft Purview**
   - Microsoft Purview is een familie van data governance, risk en compliance oplossingen
   - Geeft één unified view over on-premises, multicloud en SaaS data
   - Drie kernfuncties: automated data discovery, sensitive data classification en end-to-end data lineage

   - Risk and compliance:
      - Gebouwd op Microsoft 365 services zoals Teams, OneDrive en Exchange
      - Beschermt sensitive data across clouds, apps en devices
      - Identificeert data risico's en beheert regulatory compliance vereisten

   - Unified data governance:
     - Beheert data in Azure, SQL, Hive databases, on-premises en andere clouds zoals Amazon S3
     - Maakt een actuele map van je volledige data estate inclusief classificatie en lineage
     - Identificeert waar sensitive data is opgeslagen
     - Beheert toegang tot data veilig en op schaal

**Describe the purpose of Azure Policy**
   - Azure Policy is een service waarmee je regels instelt die bepalen wat er wel en niet mag in je Azure omgeving
   - Policies evalueren resources op compliance en markeren resources die niet voldoen
   - Noncompliant resources kunnen worden geblokkeerd voordat ze aangemaakt worden

   - Hoe werkt het:
      - Policies stel je in op resource, resource group, subscription of management group niveau
      - Policies zijn hierarchisch — een policy op een hogere laag wordt automatisch geërfd door alle onderliggende resources
      - Azure Policy kan noncompliant resources automatisch herstellen, bijvoorbeeld een ontbrekende tag automatisch toevoegen
      - Resources kunnen als exception worden gemarkeerd zodat ze niet automatisch worden aangepast

   - Initiatives:
      - Een initiative is een groep van gerelateerde policies samen voor een groter doel
      - Voorbeeld: het initiative "Enable Monitoring in Azure Security Center" bevat meer dan 100 policy definitions die samen alle security aanbevelingen monitoren

   - Azure Policy integreert met Azure DevOps voor compliance checks in CI/CD pipelines

**Describe the purpose of resource locks**
   - Resource locks voorkomen dat resources per ongeluk worden verwijderd of gewijzigd
   - Locks werken onafhankelijk van RBAC, zelfs een owner moet eerst de lock verwijderen
   - 2 types locks:
      - Delete: lezen en wijzigen mag, verwijderen niet
      - ReadOnly: alleen lezen mag, wijzigen en verwijderen niet
   - Locks zijn hierarchisch, een lock op een resource group geldt automatisch voor alle resources daarbinnen
   - Locks beheren via de Azure Portal, PowerShell, Azure CLI of ARM templates
   - Om een locked resource te wijzigen: eerst de lock verwijderen dan de wijziging doorvoeren, daarna optioneel de lock terugzetten.

**Exercise 5.  Configure a resource lock**
  - [Exercise 5 Configure a resource lock](/az900/exercises/5-configure-a-resource-lock.md)

**Describe the purpose of the Service Trust portal**
   - De Service Trust Portal is een portal van Microsoft met informatie over security, privacy en compliance practices
   - Bevat details over hoe Microsoft zijn cloud services en klantdata beschermt
   - Toegankelijk via servicetrust.microsoft.com/
   - Voor sommige content moet je inloggen met een Microsoft Entra account en de non-disclosure agreement accepteren
   - Hoofdonderdelen:
      - My Library: documenten opslaan en notificaties instellen bij updates
      - All Documents: centrale plek voor alle beschikbare documenten, minimaal 12 maanden beschikbaar na publicatie


---
---


- **Learning path:** Part 3. Describe Azure management and governance
   - **Module:** 3. Describe features and tools for managing and deploying Azure resources 
      - **Extra:** FreeCodeCamp AZ‑90

**Describe tools for interacting with Azure**
   - Azure biedt drie hoofdtools voor het beheren van je omgeving:
      - Azure Portal
      - Azure PowerShell
      - Azure CLI

   - What is the Azure portal?
      - Web-based grafische interface voor het beheren van Azure subscriptions
         - Dashboards aanmaken, resources beheren en deployements monitoren
         - Resilient, aanwezig in elk Azure datacenter, geen downtime voor onderhoud
           
   - Azure Cloud Shell
      - Browser-based shell zonder lokale installatie
         - Automatisch geauthenticeerd via je Azure credentials
         - Toegankelijk via Azure Portal
           
   - What is Azure PowerShell?
      - Shell voor het uivoeren van cmdlets die de Auzre REST API aanroepen
         - Geschikt voor losse taken en complexe geautomatiseerde workflows
         - Scripts maken processen herhaalbaar en automatiseerbaar
         - Beschikbaar op Windows, Linux en Mac

   - What is the Azure CLI?
      - Functioneel equivalent aan Azure PowerShell maar met Bash syntax
           - Zelfde mogelijkheden als PowerShell, keuze hangt af van voorkeur voor syntax
           - Beschikbaar op Windows, Linux en Mac

**Describe the purpose of Azure Arc**
   - Azure Arc breidt Azure beheer uit naar hybrid en multicloud omgevingen
   - Maakt het mogelijk om non-Azure resources te beheren via Azure Resource Manager (ARM) alsof ze in Azure draaien
     
   - Wat kan Azure ARC:
      - Servers, Kubernetes clusters, Azure data services, SQL Server en virtual machines buiten Azure centraal beheren
      - Governance en compliance toepassen op on-premises en multicloud resources
      - Bekende Azure services en tools gebruiken ongeacht waar de resources zich bevinden
      - Traditioneel ITOps combineren met DevOps Practices

**Describe Azure Resource Manager and Azure ARM templates**
   - Azure Resource Manager (ARM) is de deployment en management service van Azure
      - alle requests via Portal, CLI, Powershell of API gaan altijd via ARM
   - ARM authenticeert en autoriseert elk request voordat het wordt uitgevoerd
   
   - ARM voordelen
      - Infrastructure beheren via declarative JSON templates in plaats van scripts
      - Resources als groep deployen, beheren en monitoren
      - RBAC is natively geintegreerd
      - Tags toepassen voor organisatie en kostenbeheer

   - Infrastructure as Code (IaC): infrastructure beheren als code via herbruikbare templates en configuraties. ARM templates en Bicep zijn hier voorbeelden van

   - Arm Templates
      - JSON bestanden die declaratief beschrijven welke resources je wilt deployen
      - Template wordt eerst geverifieerd voordat er iets wordt aangemaakt
      - Resources worden parallel aangemaakt, 50 instances tegelijk in plaats van 1 voor 1
      - Voordelen: declarative syntax, repeatable results, orchestration, modulaire bestanden en uitbreidbaar met PowerShell of Bash scripts

   - Bicep:
      - Alternatief voor ARM templates met eenvoudigere en beknoptere syntax
      - Werkt ook declaratief en wordt door ARM gedeployed
      - Idempotent, hetzelfde bestand meerdere keren deployen geeft altijd hetzelfde resultaat
      - Ondersteunt direct alle nieuwe Azure resource types en API versies
      - Modulair, code opsplitsen in herbruikbare modules

**Summary**
   - Azure biedt drie tools voor interactie met de omgeving: Azure Portal, Azure PowerShell (cmdlets via REST API) en Azure CLI( Bash syntax). Azure Cloud Shell is een browser-based shell die beide ondersteunt en automatisch is geauthenticeerd via je Azure credentials
   - Azure Arc breidt Azure governance en beheer uit naar hybrid en multicloud omgevingen door non-Azure resources zoals servers, Kubernetes clusters en SQL Server te beheren via ARM alsof ze in Azure draaien.
   - Azure Resource Manager (ARM) is de centrale management laag van Azure, alle requests via Portal, CLI, PowerShell of API gaan altijd via ARM. ARM authenticeert, autoriseert en voert requests uit. Infrastructure as Code via ARM templates (JSON) of Bicep maakt deployements declaratief, herhaalbaar en parallel. Bicep heeft eenvoudigere syntax en is idempotent, in de praktijk de voorkeurskeuze boven ARM templates


---
---


- **Learning path:** Part 3. Describe Azure management and governance
   - **Module:** 4. Describe monitoring tools in Azure 
      - **Extra:** FreeCodeCamp AZ‑90


**Describe the purpose of Azure Advisor**
   - Analyseert je Azure resources en geeft gepersonaliseerde aanbevelingen om je omgeving te verbeteren
   - Aanbevelingen zijn beschikbaar via de Azure Portal en API, met optionele notificaties
   - Aanbevelingen kun je direct uitvoeren, uitstellen of negeren
   - 5 categorieen:
      - Reliability: continuiteit van business-critical applicaties verbeteren
      - Security: threats en vulnerabilities detecteren
      - Performance: snelheid van applicaties verbeteren
      - Operational Excellence: proces- en workflow efficientie en deployment best practices
      - Cost: Azure kosten optimaliseren en verlagen

**Describe Azure Service Health**
   - Azure Service Health houdt de status bij van zowel de globale Azure infrastructure als je eigen resources
   - Combineert 3 services:
      - Azure Status: globaal overzicht van alle Azure services en regio's, voor incidenten met brede impact
      - Service Health: gefocust op de Azure services en regio's die jij gebruikt. Toont outages, planned maintenance en health advisories. Ondersteunt alerts op maat
      - Resource Health: status van je individuele resources zoals een specifieke VM. Configureerbaar via Azure Monitor
   - Historische alerts worden opgeslagen voor later onderzoek
   - Bij een incident biedt Azure Service Health directe links naar support

**Describe Azure Monitor**
   - Azure Monitor is een platform voor het verzamelen, analyseren, visualiseren en reageren op data van Azure, on-premises en multicloud resources

   - Azure Log Analytics:
      - Tool in de Azure Portoal voor het schrijven en uitvoeren van log queries op Azure Monitor data
      - Ondersteunt eenvoudige en complexe queries inclusief statistische analyse en visualisatie
   - Azure Monitor Alerts:
      - Automatische notificaties wanneer een ingestelde threshold wordt overschreden
      - 2 types:
         - metric-based alerts (numerieke waarden, near real time)
         - Log-based alerts (complexe logica over meerdere bronner)
      - Gebruikt action groups om te bepalen wie wordt genotificeerd en welke actie wordt ondernomen
      - Azure Monitor, Service Health en Azure Advisor gebruiken alle drie action groups
   - Application Insights:
      - Azure Monitor feature voor het monitoren van web applicaties in Azure, on-premises of andere clouds
      - Installatie van SDK of Application Insight agent
      - Monitort: request rates, response times, failure rates, page views, user counts en performance counters
      - Kan periodiek synthetic request sturen om de applicatie te monitoren tijdens periodes van lage activiteit

**Summary**
   - Azure Advisor analyseert je resources en geeft gepersonaliseerde aanbevelingen in 5 categorieën: Reliability, Security, Performance, Operational Excellence en Cost. Aanbevelingen zijn direct uitvoerbaar, uitgesteld of negeren
   - Azure Service Health combineert 3 services: Azure status (global overzicht), Service Health (jouw services en regio's) en Resource Health (individuele resources). Historische alerts worden opgeslagen en bij incidenten zijn er directe links naar support
   - Azure Monitor verzamelt en analyseert data van Azure, on-premises en multicloud resources. Log Analytics biedt query mogelijkheden op die data. Monitor Alerts sturen notificaties via action groups bij overschreden thresholds, Metric-based voor near real time en log-based voor complexe logica. Application Insights monitort web applicaties inclusief request rates, response times en performance counters.

---
---
