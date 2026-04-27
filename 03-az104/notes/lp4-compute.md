# AZ-104: Azure Administrator Associate
## Learning Path 4: Deploy and manage Azure compute resources

  - **AZ-104 Started:** 11-4-2026
  - **AZ-104 Exam passed:**

---

## Inhoudsopgave

### Learning Path 4: Deploy and manage Azure compute resources

- [Module 1: Introduction to Azure virtual machines](#module-1-introduction-to-azure-virtual-machines)

---

## Learning Path 4: Deploy and manage Azure compute resources
### Module 1: Introduction to Azure virtual machines


**Compile a checklist for creating an Azure Virtual Machine**
  - Bij het aanmaken van een VM moet je rekening houden met 6 onderdelen:
    - Network: VNet, subnest, IP-ranges (niet-overlappend), NSGs voor traffic controle
    - VM naam: Max 64 tekens (Linux) of 15 tekens (Windows), gebruik een naamconvente
    - Locatie: Dichtstbijzijnde regio voor gebruikers, let op prijsverschillende en beschikbare hardware
    - VM grootte: Kies op basis van workload type
    - Disks: OS disk + data disk (aparte aanbevolen
    - Operating system
   
  - VM naamconventie elementen:
    
| Element | Voorbeeld | Beschrijving |
|---|---|---|
| Environment | dev, prod, QA | Identificeert de omgeving |
| Location | eus, jw | Identificeert de regio |
| Instance | 01, 02 | Voor meerdere instanties |
| Product/Service | service | Identificeert de applicatie |
| Role | sql, web, messaging | Identificeert de rol |

  - VM grootte opties:
    
| Optie | Gebruik |
|---|---|
| General purpose | Balanced CPU/memory — dev/test, kleine databases, web servers |
| Compute optimized | Hoge CPU/memory ratio — web servers, batch processen |
| Memory optimized | Hoge memory/CPU ratio — databases, caches, in-memory analytics |
| Storage optimized | Hoge disk throughput — databases |
| GPU | Graphics rendering, video editing, deep learning |
| High performance compute | Snelste CPU, optioneel high-throughput netwerk |

  - Kostenmodel:
    
| Resource | Kosten |
|---|---|
| Virtual network | Ja |
| NIC | Geen aparte kosten |
| IP adres | Ja |
| NSG | Geen aparte kosten |
| OS disk | Ja (standaard ~127 GiB) |
| Local disk | Geen kosten |
| OS licentie | Varieert (Linux goedkoper dan Windows) |

  - Compute kosten: Per minuut gefactureerd, gestopt + gedealloceerde VM kost geen compute
  - Storage kosten: Aparte gefactuurd van compute
  - Azure Hybrid Benefit: Bestaande licenties hergebruiken voor korting

  - Betaalopties compute:

| Optie | Beschrijving |
|---|---|
| Pay as you go | Per seconde, geen commitment, flexibel — geschikt voor korte of onvoorspelbare workloads |
| Reserved VM Instances (RI) | 1 of 3 jaar vooraf betalen — tot 72% goedkoper dan pay-as-you-go, geschikt voor continue workloads |

  - Disk types:

| | Ultra disk | Premium SSD v2 | Premium SSD | Standard SSD | Standard HDD |
|---|---|---|---|---|---|
| Type | SSD | SSD | SSD | SSD | HDD |
| Scenario | IO-intensief (SAP HANA, SQL, Oracle) | Productie, lage latency, hoge IOPS | Productie, performance-gevoelig | Web servers, dev/test | Backup, niet-kritiek |
| Max disk size | 65.536 GiB | 65.536 GiB | 32.767 GiB | 32.767 GiB | 32.767 GiB |
| Max throughput | 4.000 MB/s | 1.200 MB/s | 900 MB/s | 750 MB/s | 500 MB/s |
| Max IOPS | 160.000 | 80.000 | 20.000 | 6.000 | 2.000 |
| OS disk | Nee | Nee | Ja | Ja | Ja |


- [Lab 15 Create a VM using the Azure portal](/03-az104/labs/15-create-a-vm-using-the-azure-portal.md)


**Describe the options available to create and manage an Azure Virtual Machine**
  - 7 manieren om VMs aan te maken en te beheren:

| Methode | Beschrijving |
|---|---|
| ARM templates | JSON-bestanden voor reproduceerbare deployments — exporteer vanuit bestaande VM via Automation > Export template |
| Azure CLI | Cross-platform command-line tool — `az vm create` |
| Azure PowerShell | PowerShell cmdlets — `New-AzVM` |
| Terraform | Infrastructure as Code via HCL syntax — Azure Terraform Provider |
| Azure REST API | HTTP-based API (GET, PUT, POST, DELETE, PATCH) voor programmatische toegang |
| Azure Client SDK | Wrapper rond REST API voor diverse talen (.NET, Java, Node.js, Python, Ruby, Go) |
| Azure VM Extensions | Kleine applicaties voor configuratie en automatisering na initiële deployment |


- Azure Automation services:
  - Process Automation: Automatiseer reacties op events via watcher tasks
  - Configuration Management: Track software updates via Microsoft Enpoint Configuration Manager
  - Update Management: Beheer updates en patches, plan installaties, controleer resultaten
 
- Auto=shutdown
  - Automatisch afsluiten van VMs op scheme (dagelijk of wekelijks)
  - Configureerbaar via VM > Operations > Auto-Shutdown
  - Bespaart kosten door VMs niet onnodig te laten draaien
    

**Manage the availability of your Azure VMs**
  - Availability: Percentage van de tijd dat een service beschikbaar is
  - Azure VMs draaien op fysieke servers: Bij een storing verplaatst Azure de VM automatisch naar een gezonde server maar dit kan enkele minuten duren

  - Availability opties:

| Optie | Beschrijving |
|---|---|
| Availability Zones | Fysiek gescheiden zones binnen een regio (3 per regio), elk met eigen power, netwerk en koeling |
| VM Scale Sets | Groep load-balanced VMs die automatisch schaalt op basis van vraag of schema. Geen kosten voor de scale set zelf |
| Azure Load Balancer | Verdeelt traffic over meerdere VMs — inbegrepen bij Standard tier VMs |
| Azure Storage redundancy | Meerdere kopieën van data voor bescherming tegen hardware-, netwerk- en stroomstoringen |
| Azure Site Recovery | Repliceert workloads van primaire naar secundaire locatie voor regionele failover — ondersteunt Azure, Hyper-V, VMware en fysieke servers |

  - Azure Site Recovery voordelen:
    - Geen secundair fysiek datacenter nodig: Azure als recovery bestemming
    - Eenvoudig failover testen zonder impact op productie
   
**Back up your virtual machines**
  - Azure Backup is een Backup-as-a-Service oplossing voor fysieke en virtuele machines. On-premises en in de cloud

  - Ondersteunde scenarios:
    - Files en folders op Windows (fysiek en virtueel)
    - Application-aware snapshots (VSS)
    - Microsoft server workloads: SQL Server, SharePoint, Exchange
    - Azure VMs (Windows en Linux)
    - Linux en Windows 10 client machines
   
  - Voordelen:
    - Automatic storage management: Pay-as-you-use, geef vooraf toegewezen storage
    - Unlimited scaling: Hoge beschikbaarheid via Azure platform
    - Multiple storage options: LRS (lokaal) of GRS (geo-redundant)
    - Unlimited data transfer: Geen kosten voor inbound/outbound data
    - Data encryption: veilige opslag en verzending
    - Application-consistent backup: Recovery point bevat alle benodigde data voor volledig herstel
    - Long-term retention: Geen tijdslimiet op bewaren van backups
   
  - Componenten:
    - Azure Backup agent
    - System Center Data Protection Manager
    - Azure Backup Server
    - Azure BAckup VM extension
   
  - Opslag: Recovery Services vault. Backed by Azure Storage blobs. Hier definieer je welke machines worden gebackupt en wanneer snapshots worden gemaakt

**Summary**
  - Bij het aanmaken van een VM plan je van tevoren: netwerk (VNet, NSGs), naam (max 64/15 tekens, locatie, grootte op basis van workload, disks en OS. Compute wordt per minuut gefactureerd. Gedealloceerde VMs kosten geen compute. Storage wordt apart gefactureerd

  - VM groottes: General purpose, Compute optimized, Memory optimized, Storage optimized, GPU, High performance compute
  - Disk types: Ultra disk -> Premium SSD v2 -> Premium SSD -> Standaard SSD -> Standaard HDD (Ultra en Premium SSD v2 niet bruikbaar als OS disk
  - Betaalopties: Pay-as-you-go of Reserverd VM Instances (1/3 jaar, tot 72% korting)
  - Availability: Availability Zones, VM Scale Sets, Load Balancer, Site Recovery
  - Backup: Azure Backup via Recorvery Services vault. LRS of GRS, geen data transfer kosten, geen tijdlimiet

    
---


## Learning Path 4: Deploy and manage Azure compute resources
### Module 2: Configure virtual machine availability 

**Plan for maintenance and downtime**
  - 3 typen downtime waarvoor je moet plannen:

| Type | Oorzaak | Azure reactie |
|---|---|---|
| Unplanned hardware maintenance | Azure detecteert dreigend hardware falen | Live Migration naar gezonde server — korte pauze, geen reboot |
| Unexpected downtime | Onverwacht falen van hardware of infrastructuur (netwerk, disk, rack) | Automatische migratie naar gezonde server in hetzelfde datacenter — reboot, mogelijk verlies van temp drive |
| Planned maintenance | Periodieke updates door Microsoft voor betrouwbaarheid, performance en security | Gepland, minimale impact |

  - Microsoft update niet automatisch het VM OS of andere software. Dat is de verantwoordelijkheid van de administrator.


**Create availability sets**
  - Een availability set is een logische groepering van VMs die zorgt dat niet alle VMs tegelijk uitvallen bij hardware- of softwarestoringen
  - Azure verdeelt VMs in een availability set ovre meerdere fysieke server, copute racks, storage units en netwerkswitches
  - VMs in een availability set moeten dezelfde functionaliteit en software hebben
  - Een VM kan alleen bij aanmaken aan een availability set worden toegevoegd. Wijzigen vereist verwijderen en opnieuw aanmaken

  - Best practices:
    - Plaats meerdere VMs in een availability set voor redundantie
    - Elke applicatietier in een aparte availability set. Voorkomt single point of failure
    - Combineer met Azure Load Balancer voor high availability en netwerkperformance
    - Gebruik managed disks voor block-level storage
   
    - Availability sets beschermen niet tegn OS- of applicatiespecifieke fouten. Gebruik aanvullende backup en disaster recovery technieken


**Review update domains and fault domains**
  - Elke VM in een availability set wordt geplaatst in 1 update domain en 1 fault domain.
  - Update Domains:
    - Groep van nodes die tegelijk geupdated en herstart worden tijdesn planned maintenance
    - Slects 1 update domain tegelijk herstart. Zorgt voor rolling updates zonder volledige downtime
    - Instelbaar van 1 tot 20 bij aanmaken, standaard 5
    - Aantal is niet wijzigbaar na aanmaken. Verwijder en hermaak de availability set
   
  - Fault domains:
  - Groep van nodes die een fysieke eenheid van falen vertegenwoordigen. Denk aan een server rack met gedeelde power en netwerk
  - Standaard 2 fault domains per availability set
  - Beschermt tegen hardware failures, netwerkstoringen en stroomonderbrekingen door VMs over meerdere racks te spreiden

**Review availability zones**
  - Availability zones zijn fysiek gescheiden locaties binnen een Azure regio. Elk met eigen power, cooling en netwerk
  - Minimaal 3 zones per enabled regio
  - VMs verpreid over 3 zones = automatisch verspreid over 3 fault domains en 3 update domains

| Categorie | Beschrijving | Voorbeelden |
|---|---|---|
| Zonal services | Resource gepind aan een specifieke zone | Azure VMs, managed disks |
| Zone-redundant services | Platform repliceert automatisch over alle zones | Zone-redundant Storage, Azure SQL Database |

  - Voor optimale business continuity: combineer availability zones met Azure Regional pairs


**Compare vertical and horizontal scaling**
  
| | Vertical scaling (scale up/down) | Horizontal scaling (scale out/in) |
|---|---|---|
| Wat | VM grootte aanpassen | Aantal VMs aanpassen |
| Voordeel | Eenvoudig, geen extra VMs nodig | Flexibeler, tot duizenden VMs |
| Beperking | Afhankelijk van beschikbare hardware, regio-afhankelijk, vereist VM stop/herstart | Complexer te beheren |
| Gebruik | Onder-benutting verminderen of piekbelasting opvangen | Wisselende workloads op grote schaal |

  - Bij reprovisioning (VM vervangen door nieuwe). Plan voor service onderbreking en datamigratie.


**Implement Azure Virtual Machine Scale Sets**
  - VM Scale Sets deployen en beheren een set indentieke VMs met automatisch schalen op basis van vraag
  - Geen pre-provisioning nodig. VMs worden automatisch toegevoegd of verwijderd
  - Geschikt voor large-scale services, big data en containzerized workloads

  - Kenmerken:
    - Ondersteunt Azure Load Balancer (layer-4 traffic) en Azure Application Gateway (Layer-7, TLS/SSL termination)
    - Bij uitval van 1 VM blijven andere VMs de applicatie bedienen
    - Schalen kan handmatig, automatisch of een combinatie

   - 2 orchestration modes:

| Mode | Beschrijving |
|---|---|
| Uniform | Alle VMs aangemaakt vanuit dezelfde base OS image en configuratie |
| Flexible | VMs kunnen verschillende images, sizes of configuraties gebruiken binnen dezelfde scale set |

  - Orchestration mode moet worden gekozen bij aanmaken van de scale set. Niet wijzigbaar achteraf


**Create Virtual Machine Scale Sets**
  - Configuratie-instellingen bij aanmaken:
    - Orchestration mode: Flexible (standaard en aanbevolen) of Uniform
    - Image: Base OS of applicatie voor de VM
    - VM Architecture: x64 (meest software compatibiliteit) of Arm64 (tot 50% betere price-performance)
    - Size: Bepaalt CPU, memory en storage capaciteit
   
    - Advanced tab:
      - Spreading algorithm: hoe VMs verdeeld worden over fault domains:
        - Max spreading: VMs verspreid over zoveelmogelijk fault domains (aanbevolen)
        - Fixed spreading: Altijd exact 5 fault domains. faalt als minder dan 5 beschikbaar zijn


**Implement autoscale**
  - Autoscaling verhoogt of verlaagt automatisch het aantal VM instances op basis van vraag. Minimaliseert kosten bij lage vraag, handhaaft performance bij hoge vraag

  - Configuratieopties:
    - Scale out: meer VM instances toevoegen bij consistent hoge load
    - Scale in: VM instances verwijderen bij consistent lage load (bijv. 's avonds of weekenden), bespaart kosten
    - Scheduled events: Automatisch schalen op vaste tijdstippen
    - Threshold-based rules: autoscale regels op basis van performance drempelwaarden
   
  - Autoscaling vermindert managment overhead voor het monitoren en optimaliseren van applicatieprestaties

**Configure autoscale**
  - Scaling modes:
    - Manual: vaste instance count instellen (0-1000), inclusief scale-in policiy (volgorde van verwijdering)
    - Autoscalling: Automatisch schalen op schema of op basis van metrics

    - Autoscale configuratie-instellinge:

| Instelling | Beschrijving |
|---|---|
| Default instance count | Initieel aantal VMs bij deployment (0-1000) |
| Instance limit | Minimum en maximum aantal instances voor de scaling condition |
| Scale out | CPU drempel % voor scale-out + aantal instances om toe te voegen |
| Scale in | CPU drempel % voor scale-in + aantal instances om te verwijderen |
| Query duration | Tijdvenster waarin Autoscale terugkijkt voor gemiddeld metricgebruik |
| Schedule | Start- en einddatum, herhaling op specifieke dagen |

**Summary**
  - Azure plant voor 3 typen downtime: Unplanned hardware maintenance (Live Migration), Unexpected downtime (automatische migratie, reboot) en planned maintenance (Microsoft updates, minimale impact)
      - Availability sets: Logische groepering van VMs over meerdere fysieke servers, racks en switches. Elke VM krijgt 1 update domain en 1 fault domain. Standaard 5 updates domains, 2 fault domains. Niet wijzigbaar na aanmaken
      - Availability zones: Fysiek gescheiden locaties binnen een regoi (minimaal 3). Zonal (gepind) of Zone-redundant ( automatisch gerepliceerd)
      - Scaling: Vertical (VM grootte aanpassen) vs Horizonal (aantal VMs aanpassen). Horizontal is flexibeler
      - VM Scale Sets: Identieke VMs met autoscaling. Uniform (zelfde image) of Flexible (verschillende images). Max spreading aanbevolen
      - Autoscale: Schalen op basis van CPU drempel, schema of metrics. Altijd scale-out en scale-in regel instellen


---


## Learning Path 4: Deploy and manage Azure compute resources
### Module 3: Configure Azure App Service plans

**Implement Azure App Service plans**
  - Een App Service plan definieert de compute resources waarop een of meerdere web applicaties draaien. Vergelijkbaar met een server farm
  - Meerdere applicaties kunnen dezelfde App Service plan delen

  - Instellingen per App Service plan:
    - OS: Linux of Windows
    - Region: Regio voor het plan
    - Pricing tier: Bepaalt beschikbare features en kosten
    - Aantal VM Instances: Bepaald door het plan
    - VM instance grootte: CPU, memory en remote storage
   
  - Overwegingen:
    - Meerdere apps in 1 plan bepaart kosten. Gedeelde VM instances
    - Monitor capaciteit voor het toevoegen van nieuwe apps. Overbeslasting kan downtime veroorzaken
    - Isoleer een app in een nieuw plan als de app resource-intensief is, onafhankelijk moet schalen, of resources in een andere regio nodig heeft
   
  **Determine Azure App Service plan pricing**
    - 3 compute categorieen:

| Categorie | Tiers | Beschrijving |
|---|---|---|
| Shared compute | Free, Shared | Gedeelde Azure VMs met andere klanten — alleen voor dev/test, geen SLA, kan niet uitschalen |
| Dedicated compute | Basic, Standard, Premium, PremiumV2, PremiumV3 | Dedicated VMs — alleen apps in hetzelfde plan delen resources |
| Isolated | Isolated, IsolatedV2 | Dedicated VMs op dedicated VNets — netwerk + compute isolatie, maximale uitschaal capaciteit |

| Feature | Free F1 | Basic B1 | Standard S1 | Premium P1V3 | Isolated V2 |
|---|---|---|---|---|---|
| Gebruik | Dev/Test | Dev/Test | Productie | Enhanced scale | Netwerk-isolatie |
| Staging slots | N/A | N/A | 5 | 20 | 20 |
| Auto scale | N/A | Handmatig | Rules | Rules + Elastic | Rules |
| Max instances | N/A | 3 | 10 | 30 | 200 |
| Daily backups | N/A | N/A | 10 | 50 | 50 |    

  - PremiumV3 en IsolatedV2 zijn de aanbevolen tiers voor nieuwe deployments.

**Scale up and scale out Azure App Service**

| Methode | Beschrijving |
|---|---|
| **Scale up** | Meer CPU, memory en disk — hogere pricing tier, extra features (staging slots, custom domains, autoscaling) |
| **Scale out** | Meer VM instances — handmatig of via autoscale op basis van regels en schema's. Max instances afhankelijk van pricing tier, tot 100 via App Service Environments (Isolated tier) |

  - Belangrijke punten:
    - Scale up en down door pricing tier te wijzigen: Geen redeployment nodig, wijzigingen binnen seconden actief
    - Autoscale vermindert kosten bij lage load door atuomatisch te schalen
    - Schaalwijzigen gelden voor alle apps in hetzelfde App Service plan
    - Afhankelijke Azure servicess zoals SQL Database of Storage worden apart geschaald


**Configure Azure App Service autoscale**
  - Autoscale past het aantal VM instances automatisch aan op basis van regels en condities
  - Autoscale settings worden gegroepeerd in profiles

  - Twee typen autoscale regels:

| Type | Beschrijving |
|---|---|
| Metric-based | Schaalt op basis van load (bijv. CPU > 50%, response time, requests) |
| Time-based (schedule) | Schaalt op basis van tijdpatronen (bijv. elke zaterdag 08:00) |

  - Best practices:
    - Stel altijd een minimum en maximum instance count in
    - Gebruik altijd een scale-out en scale-in regel combinatie
    - Kies de juiste metric statistiek (average, minimum, maximum, total)
    - Stel een veilige default instance count in voor als metrics niet beschikbaar zijn
    - Configureer altijd notificaties (email of webhook)
   
  - Autoscale vs Automatic scaling:

| | Autoscale | Automatic scaling |
|---|---|---|
| Configuratie | Regels handmatig instellen | Platform-managed, geen regels nodig |
| Basis | Metrics of schema | HTTP traffic |
| Beschikbaar | Alle tiers | Alleen PremiumV2 en PremiumV3 |
| Gebruik | Custom logica, meerdere metrics, schema | Minder beheer, onvoorspelbare load |
    
**Summary**
  - Een App Service plan definieert de compute resources voor web applicaties. Vergelijkbaar met een server farm. Meerdere apps kunnen hetzelfde plan delen, maar overbelasting veroorzaakt downtime
      - Pricing tiers: Shared (free/shared, dev/test, geen SLA) -> Dedicated (basic t/m premiumv3, productie) -> Isolated (VNet isolatie, max 200 instances. PremiumV3 en IsolatedV2 aanbevolen voor nieuwe deployements.
      - Scale up: Hogere pricing tier, meer CPU/memory/features, geen redeployment nodig
      - Scale out: Meer VM instances, handmatig of via autoscale, geldt voor alle apps in hetzelfde plan
      - Autoscale: Metric-based (CPU, response time) of time-based (schema). Altijd scale-out en scale-in regel instellen, altijd notificaties configureren
      - Automatisch scaling: Alleen PremiumV2/V3, platform-managed op basis van HTTP traffic, geen regels nodig
        

---


## Learning Path 4: Deploy and manage Azure compute resources
### Module 4: Configure Azure App Service

**Implement Azure App Service**
  - Azure App Service is een platform voor het hosten van websites, mobile backends en web APIs op Windows en Linux

  - Voordelen:

| Voordeel | Beschrijving |
|---|---|
| Multiple languages | ASP.NET, Java, Node.js, PHP, Python, PowerShell |
| DevOps optimization | CI/CD met Azure DevOps, GitHub, BitBucket, Docker Hub, Container Registry |
| Global scale | Handmatig of automatisch schalen, wereldwijd datacenter netwerk, hoge beschikbaarheid SLA |
| Security & compliance | ISO, SOC, PCI compliant — Entra ID, social logins, IP restricties |
| Application templates | Azure Marketplace templates: WordPress, Joomla, Drupal |
| Visual Studio integration | Dedicated tools voor aanmaken, deployen en debuggen |
| API & mobile features | CORS support, authenticatie, offline sync, push notifications |


**Create an app with App Service**
  - Basis configuratie-instellingen:

| Instelling | Beschrijving |
|---|---|
| Name | Unieke naam — identificeert de app (`webappces1.azurewebsites.net`) of custom domain |
| Publish | Code of Docker Container |
| Runtime stack | Software stack: .NET Core, .NET Framework, Node.js, PHP, Python |
| Operating system | Linux of Windows |
| Region | Bepaalt beschikbare App Service plans |
| Pricing plan | Koppelt app aan een App Service plan |

| Instelling | Beschrijving |
|---|---|
| Always On | App geladen houden zonder traffic — vereist voor continue WebJobs of CRON-triggered WebJobs |
| Session affinity | Client altijd naar dezelfde instance gerouteerd in multi-instance deployment |
| HTTPS Only | Alle HTTP traffic automatisch omgeleid naar HTTPS |


**Explore continuous integration and deployment**
  - App Service ondersteunt CI/CD via de Doployment Center. Code wijzigingen worden automatisch gesynchroniseerd

  - Continuous deployment (CI/CD) bronner:
    - Github: Via Github Actions (standaard) of App Service Build Service
    - Bitbucket: Vergelijkbaar met GitHub
    - Local Git: Locale URL toevoegen als repository
    - Azure Repos: Version control tools voor code beheer
   
  - Manual deployment
    - Remote Git: Git URL toevoegen als remote repository, pushen deployt de app


**Create deployment slots**
  - Deployment slots zijn live apps met hostnames. Je deployt naar een slot in plaats van direct naar productie
  - Beschikbaar in Standard, Premium en isoloted v2 tiers.

  - Voordelen
    - Validatie: Test wijzigingen in een staging slot voor je naar productie swapt
    - Geen downtime: Swap naar productie als alle instances klaar zijn, geen request woren gedropt
    - Rollback: Bij problemen direct terug naar vorige versie door dezelfde swap opnieuw te doen
    - Auto swap: Automatisch deployen naar productie na warmup in het staging slot. Geen cold starts, geen downtime
   

**Add deployment slots**
  - Nieuwe deployment slots kunnen leeg of gekloond zijn vanuit een bestaand slot
  - Slot settings vallen in 3 categorieen: slot-specific app settings/connection strings, continuous deployment settings, en App Service Authentications settings

  - Swapped vs slot-specific settings:

| Swapped (meegaan bij swap) | Slot-specific (blijven in source slot) |
|---|---|
| Language stack en versie | App settings* |
| 32/64-bit | Connection strings* |
| Public certificates | Mounted storage accounts* |
| WebJobs content | Custom domain names |
| Path mapping | Nonpublic certificates en TLS/SSL |
| Scale settings | IP restrictions |
| CORS | Virtual network integration |
| Always On | Managed identities |
| Diagnostic settings | WebJobs schedulers |

  - Kan geconfigureerd worden als slot-specific


**Secure your App Service app**
  - App Service biedt ingebouwde authenticatie en autorisatie. Geen SDK of code wijzigingen vereist
  - De security module draait in dezelfde omgeving als de app code maar apart daarvan
  - Taken van security module: Gebruikers authenticeren, tokens valideren/opslaan/vernieuwen, sessie beheren, identity informatie injecteren in request headers

  - Configuratieopties in de Azure portal:

| Optie | Beschrijving |
|---|---|
| Allow Anonymous requests | Unauthenticated traffic doorgeven aan app code — app beslist zelf wat te doen. Ondersteunt meerdere sign-in providers |
| Allow only authenticated requests | Alle anonieme requests omgeleid naar `/.auth/login/<provider>`. Native mobile apps krijgen HTTP 401. Geen authenticatiecode nodig in de app |
| Logging and tracing | Authenticatie en autorisatie traces in log files — zoek naar `EasyAuthModule_32/64` in trace logs |


**Create custom domain names**
  - Standaard krijgt elke App Service app een Azure domain: `appnaam.azurewebsites.net`
  - Een custom domain vervang dit door een eigen domeinnaam zoals `www.contoso.com`

  - 3 stappen
    - Domain reserveren: Koop direct via Azure portal of bij een externe registar
    - DNS records aanmaken: Wijs het domein naar je Azure app:
      - A record: mapt domeinnaam naar IP adres. Moet bijgewerkt worden als IP wijzigt
      - CNAME record: mapt domeinnaam naar een adere domeinnaam (bijv. `contoso.com` -> webapp.azurewebsites.net) Blijft geldig als IP wijzigt
      - Custom domain inschakelen: Valideer en voeg toe via Azure portal
     
    - App service biedt gratis managed TLS certificaten via Custom Domain -> Add binding -> App Service Managed Certificat - Automatisch vernieuwd 30 dagen voor vervaldatum
      

**Back up and restore your App Service app**
  - Backup beshcikbaar in Basic, Standard, Premium en Isolated tiers. Basic ondersteunt alleen productie slot
  - Vereist een Azure storage account en container in dezelfde subscription

  - Wat wordt gebackupt:
    - App configuratie settings
    - File content
    - Gekoppelde databases (SQL Database, MySQL, PostgreSQL, MySQL in-app)
   
  - Opslag formaat: ZIP bestand (data) + XML bestand (manifest)

  - Belangrijke punten:
    - Handmatig of op schema
    - Full backups zijn standaard: Alle content wordt overschreven bij herstel
    - Partial backups mogelijk: Specifieke bestanden/mappen uitsluiten
    - Max 10 GB per backup (app + database)
    - Storage account met firewall kan niet als backup bestemming gebruikt worden


**Use Azure Application Insights**
  - Application Insights is een feature van Azure Monitor voor het monitoren van live applicaties. Detecteert automatisch performance anomalieen
  - Werkt op .NET, Node.js, JAVA EE. On-premises, hybrid en cloud
  - Integreert met Azure Pipelines en development tools

  - Wat je kunt monitoren:

| Metric | Beschrijving |
|---|---|
| Request rates, response times, failure rates | Populaire pagina's, piekmomenten, performance problemen |
| Dependency rates | Externe services die app performance beïnvloeden |
| Exceptions | Server én browser exceptions met stack trace |
| Page views en load performance | Browsergebaseerde paginaweergaven en laadtijden |
| User en session counts | Aantal actieve gebruikers en sessies |
| Performance counters | CPU, memory, network op Windows of Linux servers |
| Host diagnostics | Docker of Azure diagnostics integratie |
| Diagnostic trace logs | Trace events koppelen aan requests |
| Custom events en metrics | Eigen tracking algoritmes voor business events |


- [Lab 16 Implement Web Apps](/03-az104/labs/16-implement-web-apps.md)


**Summary**
  - Azure App Service host websites, mobile backends en web APIs op Windows of Linux, met CI/CD, global scale, ingebouwde security en Application Insights monitoring.
    - App aanmakenL: Naam, runtime stack, OS, regio, pricing plan. Extra: Always On, Session affinity, HTTPS Only
    - CI/CD: GitHub, Bitbucket, Local Git, Azure Repos of handmatig via Remote Git
    - Deployment slots: Staging voor validatie, zero-downtime swaps. Standard, Premium en Isolated V2
    - Security: Ingebouwde auth, geen SDK. Allow Anonymous, Allow authenticated, Logging
    - Custom domain: A record of CNAME, gratis managed TLS certificaat
    - Backup: Max 10 GB, handmatig of schema, geen firewall storage
    - Application Insights: MOnitoring van requests, exceptions, dependencies, performance



---


## Learning Path 4: Deploy and manage Azure compute resources
### Module 5: Configure Azure Container Instances


**Compare containers to virtual machines**

  - Voordelen van containers:
    - Snellere ontwikkeling en code sharing
    - Eenvoudig testen
    - Snellere deployment
    - Hogere workload density en betere resource utilization
   
| | Containers | Virtual Machines |
|---|---|---|
| Isolatie | Lichtgewicht isolatie — geen sterke security boundary | Volledige isolatie van host OS en andere VMs |
| Operating system | Alleen user mode van OS — alleen benodigde services | Volledig OS inclusief kernel — meer resources nodig |
| Deployment | Docker CLI (enkeling) of Kubernetes/AKS (meerdere) | Hyper-V Manager (enkeling) of PowerShell/SCVMM (meerdere) |
| Persistent storage | Azure Disks (single node) of Azure Files/SMB (meerdere nodes) | VHD (single machine) of SMB file share (meerdere servers) |
| Fault tolerance | Orchestrator herstart containers snel op andere node | VM failover naar andere server, OS herstart |



**Review Azure Container Instances**
  - Azure Container Instances (ACI) is de snelste en eenvoudigste manier om container in Azure te draaien. Geen VM beheer nodig
  - Een container image bevat: Code, runtime, system tools, system libraries en settings

  - Kenmerken van een ACI (Azure Container Instance)
    - Fast startup: Containers starten in seconden
    - Public IP en DNS: Direct blootgesteld aan internet via IP en FQDN (Fully Qualified Domain Name)
    - Custom sizes: 0.1-4 vCPU en 0.1-16 GB memory per container, vast voor de levensduur van de container group
    - Persistent storage: Directe mounting van Azure Files file shares
    - Linux en Windows: Beide OS types ondersteund
    - Conscheduled groups: Multi-container groups die host resources delen
    - VNet deployment: Linux container groups kunnen in een Azure VNet worden gedeployed voor private communicatie. Geen public IP


**Implement container groups**
  - Een container group is de top-level resource in ACI. Een collectie containers op dezelfde host machine die lifecycle, resources, netwerk en storage delen
  - Vergelijkbaar met een pod in Kubernetes

  - 3 deployment methoden:
    
| Methode | Beschrijving |
|---|---|
| ARM template | JSON-based IaC — ideaal bij deployment naast andere Azure resources |
| Bicep | Microsoft aanbevolen IaC — compacter dan ARM, volledige IntelliSense support |
| YAML files | Container-focused formaat — ideaal voor deployments met alleen container instances |

  - Netwerk:
    - Container groups delen 1 public IP adres, poorten en DNS label met FQDN (Fully Qualified Domain Name)
    - Port mapping niet ondersteund. Containers in een group delen een port namespace
    - Bij verwijderen van een group worden IP en FQDN vrijgegeven
   
  - Gebruik van multi-container groups:
    - Web app updates: 1 container serveert de app, andere haalt nieuwe content op
    - Log data collectie: App container produceert logs, logging container schrijft naar long-term storage
    - App monitoring: monitoring container controleert periodiek of app correct reageert
    - Front-end en back-end: aparte containers voor web front-end en data back-end


  **Review Azure Container Apps**
  - Azure Container Apps (ACA) is een serverless platform voor containerized applicaties. Geen server configuratie of container orchestratie nodig

  - Gebruik:
    - API endpoint deployen
    - Background processing jobs
    - Event-driven processing
    - Microservices
   
  - Schalen op basis van: HTTP traffic, event-driven processing, CPU/memory load, KEDA scalers (inclusief scale to zer)

  - Kenmerken:
    - Gebouwd op Kubernetes, DAPR, KEDA en envoy
    - Service discovery en traffic splitting
    - Geen directe toegang tot Kubernetes APIs. Volledig managed experience

| | ACI | ACA | AKS |
|---|---|---|---|
| Type | Isolated containers | Serverless microservices | Volledige Kubernetes controle |
| Gebruik | Korte, geïsoleerde taken | Serverless microservices, event-driven | Complexe orchestratie |
| Deployment | Snel, eenvoudig | PaaS, snel | Meer controle, Kubernetes expertise vereist |
| Schalen | Handmatig | HTTP + event-driven autoscaling | Horizontal pod + cluster autoscaling |
| Ideaal voor | Eenmalige taken | Microservices, snelle scaling | Complexe, langlopende applicaties |


- [Lab 17 Implement Container Instances](/03-az104/labs/17-implementicontainer-instances.md)
 

**Summary** 
  - Containers zijn lichter dan VMs. Geen volledig OS, snellere starup, hogere workload density. VMs bieden sterkere isolatie en zijn beter voor stateful workloads
    - ACI: Snelste manier om containers te draaien zonder VM beheer. Custom CPU/memory, Azure Files mounting, Linux en Windows, VNet deployment mogelijk
    - Container groups: Collectie containers op dezelfde host, vergelijkbaar met Kubernetes pod. Deployment via ARM, Bicep of YAML. Delen één public IP en port namespace
    - ACA: Serverless platform voor microservices en event-driven workloads. Gebouwd op Kubernetes/KEDA, scale to zero, geen directe Kubernetes API toegang
    - AKS: Volledige Kubernetes controle voor complexe, langlopende applicaties


