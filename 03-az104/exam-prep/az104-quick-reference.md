## Poorten
| Poort | Protocol/Gebruik |
|---|---|
| 80 | HTTP |
| 443 | HTTPS |
| 445 | SMB — Azure Files |
| 3389 | RDP |
| 22 | SSH |
| 5671 | AMQP — Azure Service Bus |
| 587 | SMTP relay — authenticated |
| 25 | SMTP — niet authenticated |

---

## IDENTITIES & GOVERNANCE

## RBAC Rollen
| Rol | Resources beheren | Rollen toewijzen |
|---|---|---|
| Owner | Ja | Ja |
| Contributor | Ja | Nee |
| Reader | Nee | Nee |
| User Access Administrator | Nee | Ja |
| Cost Management Contributor | Nee | Nee — kosten en budgets |
| Billing Reader | Nee | Nee — alleen facturen |
| Storage Account Contributor | Ja | Nee |
| Resource Policy Contributor | Nee | Nee |
| Network Contributor | Ja — netwerken | Nee |
| Virtual Machine Contributor | Ja — VMs | Nee |
| Tag Contributor | Nee — alleen tags | Nee |
| Backup Contributor | Ja — backups | Nee |
| Monitoring Contributor | Ja — monitoring | Nee |
| Log Analytics Contributor | Ja — Log Analytics | Nee |

## Entra ID Rollen
| Rol | Wat |
|---|---|
| Global Administrator | Alles in Entra ID |
| User Administrator | Gebruikers en groepen |
| Application Administrator | App registraties |
| Cloud Application Administrator | Zelfde zonder app proxy |
| Security Administrator | Security instellingen |
| Security Operator | Security events beheren |
| Security Reader | Security data lezen |
| Privileged Role Administrator | Rollen toewijzen in Entra ID |
| Helpdesk Administrator | Wachtwoorden resetten non-admins |
| Password Administrator | Wachtwoorden resetten |
| Guest Inviter | Gastgebruikers uitnodigen |
| License Administrator | Licenties toewijzen |
| Authentication Policy Administrator | SSPR configureren |
| Cloud Device Administrator | Devices beheren — GEEN groepen |

## Entra ID vs Azure RBAC
- **Entra ID rollen** = directory/tenant beheren
- **Azure RBAC rollen** = Azure resources beheren
- Twee aparte systemen — Global Admin geeft geen toegang tot Azure resources

## Entra ID Licenties vs Rollen
- Licentie = welke features beschikbaar zijn (SSPR, Conditional Access, PIM)
- Rol toewijzen geeft geen toegang tot premium features
- "Premium P1 features" = Licenses blade, niet Directory roles
- Admin group ≠ Application Administrator rol — expliciet toewijzen
- Licentie verwijderen van user die via groep licentie heeft = user uit groep verwijderen
- Nested groepen erven geen licenties — alleen directe leden

## SSPR — Wie kan configureren
- Global Administrator ✓
- Authentication Policy Administrator ✓
- Password Administrator ✗
- User Administrator ✗
- Security Administrator ✗
- Admins gebruiken altijd two-gate policy — geen security questions

## Hybrid Entra ID — Attributen Aanpassen
- Gesynchroniseerd vanuit Windows Server AD: Department/Job Title NIET aanpasbaar in Entra ID — moet in on-premises AD
- UsageLocation: altijd aanpasbaar in Entra ID
- Cloud-only users: alle attributen aanpasbaar

## Guest Users
- UPN formaat: user_domain.com#EXT#@tenant.com
- Guest users kunnen geen SSPR gebruiken in resource tenant
- Sleutelwoord "only invite fabrikam.com" = External collaboration settings → Collaboration restrictions

## Traffic Analytics — Vereiste Rollen
- Owner, Contributor of Network Contributor op subscription scope
- Reader, Security Operator = onvoldoende om in te schakelen

## Deny Assignments
- Deny overschrijft altijd allow — ook Owner rol
- Deny op lagere scope wint van allow op hogere scope

## Azure Policy Effects
| Effect | Type | Wat doet het |
|---|---|---|
| Deny | Synchroon | Blokkeert non-compliant resource |
| Audit | Asynchroon | Flaggt alleen |
| Modify | Synchroon | Voegt tags/properties toe automatisch |
| DeployIfNotExists | Asynchroon | Deployt template als resource ontbreekt |
| AuditIfNotExists | Asynchroon | Audit als gerelateerde resource ontbreekt |
| Disabled | — | Policy uitgeschakeld — geen enforcement |

## ARM Template Deployment Scopes
| Scope | Gebruik |
|---|---|
| Resource group | Één resource group |
| Subscription | Meerdere resource groups |
| Management group | Meerdere subscriptions |
| Tenant | Alles |

## ARM Template
- Nooit wachtwoorden plain text — gebruik Azure Key Vault + access policy
- Custom deployment: alleen Subscription, Resource Group, Location aanpasbaar
- copy element = meerdere instances van dezelfde resource deployen
- targetScope in Bicep = bepaalt waar resources worden gedeployed

## Delete Locks
| Resource | Delete lock mogelijk |
|---|---|
| Subscriptions | Ja |
| Resource groups | Ja |
| Individuele resources | Ja |
| Management groups | Nee |
| Storage account data | Nee — gebruik immutability policy |

## Custom Domain Verificatie Entra ID
- TXT record (aanbevolen) of MX record
- A record = niet voor verificatie
- SOA = automatisch aangemaakt

## Budget Alert
1. Action group aanmaken met Stop VM actie
2. Budget instellen in Cost Management + Billing

## Availability Set — Maximum Waarden
- Update domains: max 20 (standaard 5)
- Fault domains: max 3 (standaard 2)
- Fault domains = 1 vereist ook update domains = 1

---

## STORAGE

## Storage Access Tiers
| Tier | Minimum opslag | Retrieval |
|---|---|---|
| Hot | Geen | Snel |
| Cool | 30 dagen | Snel |
| Cold | 90 dagen | Snel |
| Archive | 180 dagen | Uren — offline, niet toegankelijk zonder rehydratie |

## Rehydration uit Archive
- Standard: tot 15 uur
- High: binnen 1 uur (onder 10 GB)
- Archive = offline = NIET toegankelijk — eerst rehydreren naar Hot of Cool

## Storage Redundancy
| Type | Zone spreiding | Secundaire regio | Leestoegang secundair |
|---|---|---|---|
| LRS | Nee | Nee | Nee |
| ZRS | Ja | Nee | Nee |
| GRS | Nee | Ja | Nee |
| RA-GRS | Nee | Ja | Ja |
| GZRS | Ja | Ja | Nee |
| RA-GZRS | Ja | Ja | Ja |

## Storage Redundancy — Copies
| Type | Copies primair | Copies secundair | Totaal |
|---|---|---|---|
| LRS | 3 | 0 | 3 |
| ZRS | 3 | 0 | 3 |
| GRS | 3 | 3 | 6 |
| GZRS | 3 | 3 | 6 |

## Storage Account Types
| Type | Ondersteunde services | Redundancy |
|---|---|---|
| Standard GPv2 | Blob, Queue, Table, Files, Data Lake | LRS, ZRS, GRS, RA-GRS, GZRS, RA-GZRS |
| Premium block blobs | Blob + Data Lake | LRS, ZRS |
| Premium file shares | Azure Files | LRS, ZRS |
| Premium page blobs | Page blobs only | LRS, ZRS |

## Storage Account — Default Waarden
| Property | Default |
|---|---|
| allowBlobPublicAccess | true — open |
| allowSharedKeyAccess | true — aan |
| supportsHttpsTrafficOnly | true — HTTPS only |
| minimumTlsVersion | TLS1_0 |
| accessTier | Hot |
| SKU/replicatie | LRS |
| networkAcls defaultAction | Allow |

**Ezelsbruggetje:** alles staat standaard open en onveilig behalve HTTPS. Als één property ontbreekt of fout is = **No**.

## Storage Replicatie — Sleutelregel
- "Replicatie naar andere regio + minimale kosten" = **Standard_GRS**
- ZRS = alleen zone redundantie, GEEN secundaire regio
- "Compliance / sensitive data" encryptie = customer-managed keys in Key Vault
- "Minimize costs" encryptie = Microsoft-managed keys

## Object Replicatie Vereisten
- Blob versioning op source ✓
- Blob versioning op destination ✓
- Change feed op source ✓
- Beide accounts: General Purpose v2 of Premium block blob

## Azure Import/Export — Volledige Volgorde
1. Dataset CSV aanmaken
2. Driveset CSV aanmaken
3. WAImportExport.exe uitvoeren → journal file
4. Import job aanmaken in Azure Portal
5. Schijven opsturen
6. Import job updaten met tracking nummer

## Azure File Sync — Volgorde
1. Agent installeren op server
2. Server registreren bij Storage Sync Service
3. Sync group aanmaken + cloud endpoint
4. Server endpoint aanmaken

## Azure File Sync — Regels
- Één cloud endpoint per sync group
- Één server endpoint per server per sync group
- Nooit overschrijven bij conflict — conflict naam aanmaken
- Conflictnaam formaat: bestandsnaam-endpointnaam.extensie
- Maximum 100 conflict bestanden per bestand

## AzCopy
- Ondersteunt: blob en file storage
- OS: Windows, Linux, macOS
- Authenticatie: Entra ID of SAS token
- make = container aanmaken
- copy = bestanden kopiëren
- sync = synchroniseren inclusief verwijderingen
- Syntax: azcopy copy [source] [destination] [flags]
- --recursive = inclusief subdirectories

## Storage Account Firewall
1. Public network access → Selected networks instellen
2. Specifiek IP adres toevoegen
- Beide stappen vereist

## Log Analytics Workspace voor Backup Reports
- Regio maakt niet uit — elke workspace bruikbaar ongeacht locatie

---

## COMPUTE

## App Service Tiers
| Tier | Custom domain | Slots | Autoscale |
|---|---|---|---|
| Free F1 | Nee | Nee | Nee |
| Basic B1 | Ja | Nee | Handmatig |
| Standard S1 | Ja | 5 | Ja |
| Premium P1V3 | Ja | 20 | Ja |
| Isolated I1V2 | Ja | 20 | Ja |

## App Service — Runtime Stack vs OS
| Runtime | OS |
|---|---|
| ASP.NET V4.8 | Windows only |
| PHP | Linux only |
| Python | Linux only |
| Ruby | Linux only |
| Node.js | Windows en Linux |
| Java | Windows en Linux |

- Eén plan per OS
- Deployment slots vereist Standard of hoger
- Swap staging ↔ production = snelste manier om te reverten
- Scale up naar Standard eerst, dan autoscale rules instellen

## App Service — Logging
| Type | Wat |
|---|---|
| Web Server Logging | HTTP requests — method, URI, client IP, port, user agent, response code |
| Application Logging | Applicatie errors, debug info |

## Container Services
| Service | Volledig | Gebruik | Scale to zero | Scaling trigger |
|---|---|---|---|---|
| ACI | Azure Container Instances | Korte geïsoleerde taken | Nee | Handmatig |
| App Service | Azure App Service | Docker web apps | Nee | HTTP / CPU |
| ACA | Azure Container Apps | Serverless microservices | Ja | HTTP / event-driven / CPU |
| AKS | Azure Kubernetes Service | Complexe orchestratie | Nee | Kubernetes HPA |

## ACR (Azure Container Registry) Tiers
| Tier | Private endpoints | Geo-replication |
|---|---|---|
| Basic | Nee | Nee |
| Standard | Nee | Nee |
| Premium | Ja | Ja |

- Content trust = signed images
- ACR Tasks = automatisch rebuilden bij base image update

## VM Scale Set Orchestration Modes
- Uniform = large-scale stateless, snelste uitrol
- Flexible = stateful, verschillende VM types
- Orchestration mode kan niet worden gewijzigd na aanmaken

## Availability Opties VMs
| Optie | Beschermt tegen | SLA |
|---|---|---|
| Enkele VM Premium SSD | — | 99.9% |
| Availability set | Rack failures | 99.95% |
| Availability zone | Datacenter failure | 99.99% |

## VM Wijzigingen — Downtime of Niet
| Wijziging | Downtime? |
|---|---|
| VM size wijzigen | Ja |
| NIC loshalen | Ja |
| Nieuwe disk toevoegen | Nee |
| DSC extension toevoegen | Nee |
| Verplaatsen naar andere resource group | Nee |

## VM Tijdelijke Disk
- Windows: drive D — gaat verloren bij redeploy
- Linux: /dev/sdb — gaat verloren bij redeploy

## Site Recovery — Vereiste voor AZ verplaatsing
- VM moet managed disks gebruiken
- Unmanaged disks = niet mogelijk

## Hyper-V Replicatie naar Azure — Vereiste Resources
1. Recovery Services Vault
2. Hyper-V site
3. Replication Policy

## VM Scripts
- Eenmalig bij deployment → Custom Script Extension
- Consistent blijven + compliance → DSC extension

---

## NETWORKING

## NSG Regels
- Inbound: Subnet NSG eerst → NIC NSG
- Outbound: NIC NSG eerst → Subnet NSG
- Inbound internet = geblokkeerd by default
- Inbound VNet = toegestaan by default
- Beide NSGs moeten toestaan anders geblokkeerd
- NSG koppelen aan: subnet of NIC — niet aan VNet of VM direct
- NSG regio = zelfde regio als subnet/NIC

## ASG (Application Security Group)
- Groepeert NICs van meerdere VMs
- Alle NICs moeten in hetzelfde VNet zitten
- "Fewest NSG rules" = altijd ASG
- ASG koppelen aan NIC — niet aan VM direct of subnet

## VNet Peering
- Peering is **niet transitief**
- Peering is **niet automatisch bidirectioneel** — twee peerings nodig (A→B én B→A)
- Gateway transit = VPN/ExpressRoute naar on-premises via hub gateway
- Disconnected = verwijder peer en maak opnieuw aan
- Nieuw address space toegevoegd = Sync the peering
- P2S VPN client herinstalleren na elke topologiewijziging
- Overlappende address spaces = peering niet mogelijk

## Gateway Transit
- Hub heeft VPN Gateway → zet "allow gateway transit" aan op Hub
- Spoke wil gateway gebruiken → zet "use remote gateway" aan op Spoke
- VNet kan maar één VPN Gateway hebben
- Gateway transit werkt ook cross-regio
- GatewaySubnet vereist minimaal /27

## NVA (Network Virtual Appliance)
- VM die werkt als firewall/router
- Vereist UDR om verkeer erdoorheen te sturen
- Voor high availability: meerdere NVAs achter load balancer
- Microsegmentatie = apart subnet voor firewall

## VPN Types
- Site-to-site = heel kantoor → Azure (één VPN apparaat voor iedereen)
- Point-to-site = één laptop → Azure (per persoon)

## Route Table — Next Hop Types
| Type | Gebruik |
|---|---|
| Virtual appliance | Aangepast IP adres opgeven — NVA, firewall |
| Internet | Publiek internet |
| Virtual network gateway | VPN/ExpressRoute |
| Virtual network | Binnen hetzelfde VNet |
| None | Traffic droppen |

## Route Prioriteit
1. User-defined routes (hoogste prioriteit)
2. BGP routes
3. System routes
- Langste prefix wint — /24 wint van /16

## DNS Record Types
| Type | Gebruik |
|---|---|
| A | Domeinnaam → IPv4 |
| AAAA | Domeinnaam → IPv6 |
| CNAME | Alias |
| MX | Email routing |
| TXT | Domeinverificatie |
| NS | Delegatie naar DNS servers |
| SOA | Automatisch aangemaakt |

## DNS Records — Uitgebreide Uitleg

**A record**
Wijst een hostname naar een IP adres.
Gebruik: elke hostname die naar een IP moet wijzen.
Ezelsbruggetje: A = Adres → IP.

**CNAME record**
Wijst een naam naar een andere naam (alias).
Gebruik: subdomeinen zoals www.contoso.com → contoso.azurewebsites.net.
Mag NOOIT op de apex (root) van een domein.
Ezelsbruggetje: CNAME = Canonical Name → andere naam.

**MX record**
Wijst naar de mailserver voor een domein.
Gebruik: email routing voor @contoso.com.
Wijst naar een hostname, niet naar een IP adres.
Ezelsbruggetje: MX = Mail eXchange → alleen voor email.

**TXT record**
Bevat tekst, geen verkeer routeren.
Gebruik: domeinverificatie bij Azure App Service, Microsoft 365, Google etc.
Voor App Service verificatie: naam = asuid.[hostname], waarde = domain verification ID.
Ezelsbruggetje: TXT = bewijzen dat je eigenaar bent.

**NS record**
Delegeert een subdomein naar andere nameservers.
Gebruik: shop.contoso.com delegeren aan een ander team met eigen DNS zone.
Ezelsbruggetje: NS = Name Server → wie beheert dit subdomein.

## DNS Situaties
| Situatie | Oplossing |
|---|---|
| Apex zonder ALIAS/ANAME | A record + TXT |
| Subdomein (www) | CNAME + TXT |
| Custom domain eerste stap | TXT verificatie eerst (asuid) |
| Custom domain volgorde | TXT → CNAME/A → domain toevoegen → TLS → HTTPS Only |
| Email routing | MX record |
| Subdomein delegeren | NS record |
| On-premises → Azure private DNS | DNS Private Resolver + inbound endpoint |
| VM krijgt publiek IP ondanks private endpoint | Zone niet gelinkt aan VNet of geen A record in zone |
| Alles correct maar toch publiek IP | Custom DNS server forwardt niet naar 168.63.129.16 |
| Auto-registration | Maximaal één zone per VNet |
| Eén zone meerdere VNets auto-registration | Toegestaan |
| Public DNS zone linken aan VNet | Niet mogelijk |
| Regio private DNS zone | Maakt niet uit |
| VNet peering + DNS resolution | Peering irrelevant, zone moet gelinkt zijn |
| On-premises resolver krijgt publiek IP | Private DNS zone niet gelinkt aan VNet van resolver |

## Custom Domain in Azure DNS — Volgorde
1. Maak Azure public DNS zone aan
2. Kopieer de 4 NS records van Azure
3. Plak die NS records bij je domeinregistrar

## Subdomain Delegatie
- Subdomain delegeren naar andere zone → NS record aanmaken in parent zone

## Private DNS Zone
- Virtual network link aanmaken met auto-registration = VMs automatisch registreren
- DNS Private Resolver = proxy voor on-premises naar Azure DNS — NIET voor auto-registration
- Locatie DNS zone irrelevant — alleen VNet link telt
- VNet kan maar één registration zone hebben
- Private DNS zone kan meerdere registration VNets hebben

## Load Balancer — Backend Pool
- VM zonder public IP → mag erin ✓
- VM stopped → mag erin ✓
- Basic IP + Standard LB → niet compatibel ✗
- Standard public IP = altijd Static

## Load Balancer — Regels
| Regel | Gebruik |
|---|---|
| Load balancing rule | Verdelen over alle VMs |
| Inbound NAT rule | Doorsturen naar één specifieke VM |

## Load Balancer — Troubleshooting
- Connectivity issues = health probe + NSG rules + VM port response
- Session persistence = Client IP + Protocol

## Load Balancer vs Application Gateway vs Front Door vs Traffic Manager
| | Load Balancer | Application Gateway | Front Door | Traffic Manager |
|---|---|---|---|---|
| Laag | Layer 4 | Layer 7 | Layer 7 | DNS |
| Scope | Regionaal | Regionaal | Globaal | Globaal |
| SSL termination | Nee | Ja | Ja | Nee |
| WAF | Nee | Ja | Ja | Nee |
| Path-based routing | Nee | Ja | Ja | Nee |
| Caching | Nee | Nee | Ja | Nee |

## Application Gateway Extra
- Path-based routing = URL pad → verschillende backend pools
- Multi-site routing = meerdere domeinen op één gateway via CNAME
- Connection draining = graceful removal van backend server
- Health probe = HTTP 200-399 = gezond

## On-premises via VPN load balancen
- Internal Load Balancer of Application Gateway (intern geconfigureerd)
- Public Load Balancer = alleen internet traffic

## Azure Bastion
- Verbindt via privé IP
- Werkt binnen hetzelfde VNet of via VNet peering
- Zonder peering = geen verbinding naar andere VNets
- AzureBastionSubnet vereist — minimaal /26

## Network Watcher Tools — Uitgebreide Uitleg

**IP flow verify**
Test één specifieke flow: wordt dit pakket toegestaan of geblokkeerd door NSG?
Geeft: allow/deny + welke regel.
Sleutelwoord in vraag: "wordt verkeer geblokkeerd", "welke regel blokkeert", "is poort X open"
Verschil met Effective security rules: IP flow verify test één flow, effective security rules toont alle regels.

**Effective security rules**
Toont de complete merged ruleset van subnet NSG + NIC NSG + defaults voor één NIC.
Sleutelwoord in vraag: "merged rules", "alle geldende regels", "welke regels gelden voor NIC", "precedence"
Verschil met IP flow verify: niet één flow testen maar alle regels overzien.
Valkuil: NSG staat niet in de naam maar toont WEL alle NSG regels.

**Next hop**
Voor één destination IP: via welk next hop gaat het verkeer?
Geeft: next hop type (VirtualNetwork, Internet, VirtualNetworkGateway, VirtualAppliance)
Sleutelwoord in vraag: "via welke route gaat verkeer naar X", "next hop voor destination"
Verschil met Effective routes: next hop = één destination, effective routes = alle routes.

**Effective routes**
Toont alle actieve routes op een NIC — system routes, UDRs, BGP routes samen.
Sleutelwoord in vraag: "alle actieve routes", "waarom neemt verkeer onverwachte route", "UDR correct"
Verschil met Next hop: compleet overzicht, niet één destination.

**Connection troubleshoot**
Eenmalige test: kan VM A endpoint B bereiken? Lost ook DNS op bij FQDN.
Geeft: reachable/unreachable + latency + DNS resolution resultaat
Sleutelwoord in vraag: "kan VM bereiken", "is er connectiviteit", "test eenmalig"
Verschil met Connection monitor: eenmalig vs doorlopend.
Verschil met IP flow verify: bereikbaarheid testen vs NSG gedrag testen.

**Connection monitor**
Doorlopende monitoring van bereikbaarheid en latency tussen endpoints. Slaat op in Log Analytics. Alerteerbaar via Azure Monitor.
Sleutelwoord in vraag: "doorlopend", "continu monitoren", "latency over tijd", "alerteerbaar"
Verschil met Connection troubleshoot: continu vs eenmalig.

**Packet capture**
Neemt volledig netwerkverkeer op van een NIC. Max 5 uur. Vereist Network Watcher Agent extension op de VM.
Sleutelwoord in vraag: "volledige pakketinhoud", "forensisch onderzoek", "payload", "deep inspection"
Verschil met NSG flow logs: packet capture = volledige inhoud, NSG flow logs = alleen metadata.

**NSG flow logs**
Logt metadata van alle flows door een NSG — source/destination IP, poort, protocol, allow/deny. Schrijft naar storage account.
Sleutelwoord in vraag: "historisch verkeer", "welk verkeer is er geweest", "logging voor compliance"
Verschil met packet capture: alleen metadata, geen inhoud.
Verschil met Effective security rules: flow logs = verkeer dat heeft plaatsgevonden, effective security rules = regels die gelden.
Valkuil: NSG staat WEL in de naam maar toont geen regeloverzicht.

**Traffic Analytics**
Verwerkt NSG flow logs en toont inzichten in Log Analytics — hotspots, verdachte flows, geografische verdeling, trends.
Sleutelwoord in vraag: "inzichten", "dashboard", "hotspots", "verdachte patronen", "geografische verdeling"
Vereist: storage account + Log Analytics workspace.
Verschil met NSG flow logs: flow logs = ruwe data, Traffic Analytics = verwerkte inzichten.
Verschil met Network topology: Traffic Analytics = verkeersanalyse, Network topology = visuele kaart van resources.

**VPN troubleshoot**
Diagnosticeert problemen met VPN gateway verbindingen — status, fouten, logs.
Sleutelwoord in vraag: "VPN gateway verbinding", "VPN problemen", "gateway logs"
Verschil met Connection troubleshoot: specifiek voor VPN gateways, niet voor algemene connectivity.

**Network topology**
Visueel overzicht van alle netwerkresources en hun verbindingen binnen een regio — VNets, subnets, VMs, NSGs.
Sleutelwoord in vraag: "visuele kaart", "overzicht van resources", "welke resources zijn verbonden"
Verschil met Traffic Analytics: Network topology = resources en verbindingen, Traffic Analytics = verkeersanalyse.

## Network Watcher — Sleutelwoorden Samenvatting
| Sleutelwoord in vraag | Tool |
|---|---|
| "wordt pakket geblokkeerd" / "welke regel" | IP flow verify |
| "alle NSG regels" / "merged ruleset" | Effective security rules |
| "next hop voor destination X" | Next hop |
| "alle actieve routes" / "UDR correct" | Effective routes |
| "kan VM bereiken" / "eenmalig testen" + DNS | Connection troubleshoot |
| "doorlopend" / "continu" / "latency over tijd" | Connection monitor |
| "volledige pakketinhoud" / "forensisch" | Packet capture |
| "historisch verkeer" / "logging compliance" | NSG flow logs |
| "inzichten" / "hotspots" / "geografisch" | Traffic Analytics |
| "VPN gateway problemen" | VPN troubleshoot |
| "visuele kaart resources" | Network topology |

## Network Watcher — Wanneer Niet
- Niet voor PaaS services
- Niet voor web analytics
- Gebruik Azure Service Health voor platform problemen

## Service Endpoint
- Directe verbinding van VNet naar Azure service via Azure backbone
- Sleutelwoord "traverse through Azure backbone" = Service endpoint

---

## MONITOR & BACKUP

## Backup Vault vs Recovery Services Vault
| | Backup Vault | Recovery Services Vault |
|---|---|---|
| Azure Blobs/Disks/PostgreSQL | ✓ | ✗ |
| Azure VMs/Files/SQL in VM | ✗ | ✓ |
| Site Recovery/On-premises | ✗ | ✓ |
| Container Instances/App Service | ✗ | ✗ |

## Azure Backup
- Werkt altijd — ook bij stopped/deallocated VM
- Vault en VM in dezelfde regio
- Volgorde: Vault → Policy → Koppelen
- Default retention: 30 dagen
- Soft delete retention: 14 dagen
- Blob containers = NIET te backuppen via Azure Backup
- Azure SQL Database = NIET te backuppen via Azure Backup

## MARS Agent — Volgorde
1. Recovery Services vault aanmaken
2. MARS agent installeren
3. **Vault credentials downloaden en server registreren** ← eerst dit
4. Backup policy configureren
5. Backup starten

## Recovery Services Vault Verwijderen
1. Stop backup van alle protected items
2. Disable soft delete
3. Permanently remove all items in soft delete state
4. Dan pas vault verwijderen
- VM verwijderen = NIET vereist

## Azure Backup — Pre-Check Statussen
| Status | Oorzaak |
|---|---|
| Warning | VM Agent niet up to date |
| Critical | NSG blokkeert Azure Backup communicatie |

## Azure Backup — Restore Opties
- Create new VM
- Restore Disk
- Replace existing disk — VM moet nog bestaan, disk blijft in RG na restore
- File Recovery — alleen naar zelfde of compatibele OS versie

## Site Recovery — Volledige Lifecycle
**Setup:** Initiate replication
**Drill:** Test failover → Clean up
**Echte failover:** Verify → Failover → Reprotect
**Herstel:** Failback → Reprotect again

## Site Recovery — RSV Locatie
- RSV moet in de **secundaire** regio staan
- Recovery plan = hoe failover verloopt
- Replication policy = hoe data gekopieerd wordt

## Azure Monitor
- Alert rules: één per signal
- Action groups: één per unieke set ontvangers
- Alert state = altijd handmatig — nooit automatisch
- Shared dashboard: max 30 dagen data
- **Action group EERST aanmaken, dan alert rule**

## Azure Monitor Agent vs Performance Diagnostics
| Agent | Wat | Doorlopend? |
|---|---|---|
| Azure Monitor Agent | Logs en metrics verzamelen | Ja |
| Network Watcher Agent | Packet capture | Ja |
| Performance Diagnostics | VM performance diagnose | Nee — eenmalig |

## Application Insights Features
| Feature | Gebruik |
|---|---|
| Funnels | Doorloopt gebruiker het hele proces? |
| Retention | Komen gebruikers terug? |
| User Flows | Welk pad nemen gebruikers? |
| Impact | Hoe beïnvloeden laadtijden conversie? |
| Profiler | Trace web requests — welke code is traag? |

## KQL Operators
| Operator | Gebruik |
|---|---|
| where | Filtert rijen |
| summarize | Aggregeert |
| project | Selecteert kolommen |
| extend | Voegt kolommen toe |
| search in (Table) "value" | Zoekt in specifieke tabel |

---

## SLEUTELWOORDEN
| Sleutelwoord | Antwoord |
|---|---|
| Least privilege | Meest specifieke rol op laagste scope |
| Minimize administrative effort | App Service of ACA |
| Scale to zero | ACA |
| Short-lived isolated task | ACI |
| Without requiring failover | RA-GRS of RA-GZRS |
| SQL injection | Application Gateway WAF |
| SSL termination | Application Gateway |
| Mount from Azure + on-premises | Azure Files |
| Replicatie andere regio minimale kosten | Standard_GRS |
| Fewest NSG rules | ASG |
| Centralized console network | Network Insights |
| RDP to specific VM via load balancer | Inbound NAT rule |
| Connect without exposing RDP/SSH | Azure Bastion |
| Aggregate query results by column | KQL summarize |
| Datacenter failure / 99.99% SLA | Availability zone |
| Rack failure / 99.95% SLA | Availability set |
| Large-scale stateless VM scale set | Uniform orchestration mode |
| Premium P1 features toewijzen | Licenses blade |
| Modify Department synced user | On-premises AD |
| RDP alleen vanaf on-premises | NSG — Allow on-premises, Deny internet |
| Temporary external access storage | SAS token |
| Store password in ARM template | Azure Key Vault |
| Back up files single server | MARS agent |
| Central backup multiple machines | MABS |
| Prevent accidental deletion | Delete lock |
| Name resolution across multiple VNets | Azure Private DNS zone |
| Underutilized VMs / unattached disks | Azure Advisor Cost |
| Service Bus queue scaling | Event-driven trigger in ACA |
| Verify custom domain in Entra ID | TXT of MX record |
| Auto-delete group after X days | Microsoft 365 group expiration policy |
| Specify next hop IP address | Virtual appliance |
| Traverse through Azure backbone | Service endpoint |
| Signed container images | Content trust in ACR |
| Private endpoints ACR | Premium tier vereist |
| Geo-replication ACR | Premium tier vereist |
| On-premises via VPN load balancen | Internal LB of Application Gateway |
| Packet capture vereist | AzureNetworkWatcherExtension installeren |
| Trace web requests performance | Application Insights Profiler |
| ITSM integratie Service Manager | IT Service Management Connector (ITSMC) |
| Privé verbinding Azure Monitor | AMPLS |
| Retain logs specific period | Log Analytics workspace settings |
| Auto-register VMs in private DNS | Virtual network link met auto-registration |
| Web server logs HTTP requests | Web Server Logging |
| App errors debug logs | Application Logging |
| Path-based routing URL | Application Gateway |
| Meerdere domeinen één gateway | Application Gateway multi-site |
| Eenmalig VM performance diagnose | Performance Diagnostics |
| Continu latency monitoren | Connection monitor |
| VPN problemen diagnosticeren | VPN troubleshoot |
| NSG blokkeert welke regel | IP flow verify |
| Verkeer door firewall sturen | NVA + UDR |
| Scripts eenmalig bij deployment | Custom Script Extension |
| Scripts consistent + compliance | DSC extension |
| Subdomain delegeren | NS record in parent zone |
| Over internet kopiëren naar blob | Azure Storage Explorer |
| Replicatie zelf regio kiezen | Object replication |
| Replicatie automatisch paired region | GRS |
| System Center Service Manager alert | ITSMC |
