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
| Logic Apps Contributor | Ja — Logic Apps aanmaken/beheren | Nee |
| Logic App Operator | Nee — alleen lezen/inschakelen/uitschakelen | Nee |

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
- **Entra ID rollen** = directory/tenant beheren (gebruikers, groepen, devices, apps)
- **Azure RBAC rollen** = Azure resources beheren (VMs, storage, netwerken)
- Twee aparte systemen — Global Admin geeft geen toegang tot Azure resources
- Owner = baas van Azure resources maar geen toegang tot Entra ID

## Entra ID Licenties vs Rollen
- Licentie = welke features beschikbaar zijn (SSPR, Conditional Access, PIM)
- Rol toewijzen geeft geen toegang tot premium features
- "Premium P1 features" = Licenses blade, niet Directory roles
- Admin group ≠ Application Administrator rol — expliciet toewijzen
- Licentie verwijderen van user die via groep licentie heeft = user uit groep verwijderen
- Nested groepen erven geen licenties — alleen directe leden
- UsageLocation moet ingesteld zijn voordat licentie toegewezen kan worden

## SSPR — Wie kan configureren
- Global Administrator ✓
- Authentication Policy Administrator ✓
- Password Administrator ✗
- User Administrator ✗
- Security Administrator ✗
- Admins gebruiken altijd two-gate policy — geen security questions
- SSPR vereist minimaal Microsoft Entra ID P1 licentie

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
- targetScope / scope in Bicep = bepaalt waar resources worden gedeployed (welke RG/subscription)
- scope = deployment destination in hiërarchie, location = geografische regio
- ARM template bekijken na deployment = Resource Group → Deployments blade
- -TemplateFile = lokaal bestand
- -TemplateUri = online URL / Blob Storage / GitHub
- -TemplateSpecId = Template Spec opgeslagen in Azure

## PowerShell — Azure RBAC Cmdlets
- **Get-AzRoleDefinition** = haalt de rol definitie op — wat de rol IS, welke permissions hij heeft
- **Get-AzRoleAssignment** = haalt rol toewijzingen op — wie de rol HEEFT op welke scope
- **ConvertTo-Json** = PowerShell object → JSON formaat (exporteren, opslaan, aanpassen)
- **ConvertFrom-Json** = JSON string → PowerShell object (inlezen, gebruiken in script)

Custom rol aanmaken op basis van bestaande rol:
```
Get-AzRoleDefinition -Name "Contributor" | ConvertTo-Json
```
Ezelsbruggetje: **To** = naar JSON toe (exporteren). **From** = van JSON af (inlezen)
- Niemand heeft standaard toegang tot de root management group
- Owner en Contributor werken NIET op root niveau
- Toegang krijgen = **Global Administrator rol + "Access management for Azure resources" aanzetten**
- Na aanzetten krijg je automatisch User Access Administrator op root scope

## Tags
- Tags = metadata op Azure resources voor rapportage en kostenbeheer
- Tags koppelen aan: resources, resource groups, subscriptions
- Tags NIET mogelijk op: Management groups
- "VMs koppelen aan departement voor rapportage" = Tags, niet administrative units
- Administrative units = containers voor Entra ID objecten, niet voor Azure resources

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
1. Action group aanmaken met Stop VM actie (type: Runbook)
2. Budget instellen in Cost Management + Billing

## Availability Set — Maximum Waarden
- Update domains: max 20 (standaard 5)
- Fault domains: max 3 (standaard 2)
- Fault domains = 1 vereist ook update domains = 1
- Update domains = bescherming tegen gepland onderhoud
- Fault domains = bescherming tegen ongepland onderhoud (hardware failure)

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
- Archive = offline = NIET toegankelijk — eerst rehydreren naar Hot, Cool, of Cold

## Storage Redundancy
| Type | Zone spreiding | Secundaire regio | Leestoegang secundair | Sync/Async | Availability |
|---|---|---|---|---|---|
| LRS | Nee | Nee | Nee | Synchroon | 99.9% |
| ZRS | Ja | Nee | Nee | Synchroon | 99.9999% |
| GRS | Nee | Ja | Nee | Primair sync / secundair async | 99.9% |
| RA-GRS | Nee | Ja | Ja | Primair sync / secundair async | 99.99% |
| GZRS | Ja | Ja | Nee | Primair sync / secundair async | 99.9999% |
| RA-GZRS | Ja | Ja | Ja | Primair sync / secundair async | 99.9999% |

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

**GPv2 = meest complete type** — ondersteunt ZRS, Archive, object replication, lifecycle management. Bij twijfel = GPv2.

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
- Asynchronous replication / minimize latency = object replication (niet GRS — regio keuze zelf)

## Storage Account Firewall
1. Public network access → Selected networks instellen
2. Specifiek IP adres toevoegen
- Beide stappen vereist
- **Azure Backup vereist "Allow trusted Microsoft Services to access this storage account" aangevinkt**
- Zonder dit vakje = Azure Backup kan NIET backuppen naar deze storage account

## Azure Data Lake Storage Gen2
- **Geen apart product** — gewoon een GPv2 storage account met hierarchical namespace ingeschakeld
- Hierarchical namespace = echte mappenstructuur (directories/subdirectories) voor big data analytics
- Zonder hierarchical namespace = gewoon Blob storage
- Met hierarchical namespace = Azure Data Lake Storage Gen2
- Sleutelwoord "Data Lake", "big data analytics", "Hadoop", "Spark" → **Enable hierarchical namespace**

## Storage — Identity-Based Access
- **Identity-based access = Azure Files** — ondersteunt AD/Entra ID authenticatie op share én bestandsniveau
- Blob, Queue, Table = alleen access keys, SAS tokens, of RBAC op resource niveau
- Azure Files = enige storage service met Kerberos/AD authenticatie zoals traditionele Windows file server

## Storage — Gebruik per Type
| Sleutelwoord | Storage type |
|---|---|
| Mount / mounten / SMB / NFS | Azure Files |
| Mount from Azure + on-premises | Azure Files |
| Persistent storage voor VM (Docker) | Azure Files (file share) |
| Persistent storage VM disk | Azure Disk |
| Object storage / unstructured data | Azure Blob |
| NoSQL / structured tabular data | Azure Table |
| Identity-based access | Azure Files |

## Azure Files — Authenticatie Methoden
| Methode | Gebruik | Vereiste |
|---|---|---|
| Entra Kerberos | Hybrid identities + internet + geen DC line-of-sight | Entra ID sync |
| OAuth over REST | Programmatische/applicatie toegang | Niet voor eindgebruikers SMB |
| NTLM | Legacy — verouderd | Vereist DC line-of-sight ✗ |
| Entra Domain Services | Linux SMB met managed domain | Complexer — niet voor hybrid |

**Sleutelwoord:** "hybrid identities + geen DC line-of-sight + internet" → **Entra Kerberos**
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
- Authenticatie: Entra ID of SAS token (GEEN shared key via AzCopy)
- make = container aanmaken
- copy = bestanden kopiëren
- sync = synchroniseren inclusief verwijderingen
- Syntax: azcopy copy [source] [destination] [flags]
- --recursive = inclusief subdirectories

## Log Analytics Workspace voor Backup Reports
- Regio maakt niet uit — elke workspace bruikbaar ongeacht locatie

---

## COMPUTE

## VM Size Series
| Letter | Categorie | Geschikt voor |
|---|---|---|
| A | Entry-level/budget | Testen, kleine workloads |
| B | Burstable | Variabele workload — NIET voor constant hoge CPU |
| D | General purpose (Default) | Gebalanceerde CPU/geheugen, web servers |
| E | Extra geheugen | In-memory databases, caches |
| F | Fast CPU | Hoge CPU, batch processing |
| H | HPC | Intensieve rekenkracht, simulaties |
| L | Large storage | Hoge disk throughput, NoSQL, big data |
| M | Massive geheugen | Grootste in-memory databases, SAP HANA, tot 4TB RAM |
| N | Nvidia/GPU | Machine learning, rendering |

**Ezelsbruggetje:** D=Default, E=Extra geheugen, F=Fast CPU, L=Logs/storage, M=Massive, N=Nvidia

## Azure Spot Instances
- Goedkoper maar kunnen worden gestopt door Azure
- Eviction redenen: Azure heeft capaciteit nodig OF prijs overschrijdt jouw maximum
- Geschikt voor: dev/test, workloads zonder SLA vereiste

## Proximity Placement Group (PPG)
- Zorgt dat VMs fysiek zo dicht mogelijk bij elkaar staan (laagste latency)
- PPG en VM/VMSS moeten in **dezelfde regio** staan
- Resource group maakt NIET uit — alleen regio telt
- Sleutelwoord: "low latency", "physically close", "same datacenter"

## App Service Tiers
| Tier | Custom domain | Slots | Autoscale | Storage |
|---|---|---|---|---|
| Free F1 | Nee | Nee | Nee | 1 GB |
| Basic B1 | Ja | Nee | Handmatig | 10 GB |
| Standard S1 | Ja | 5 | Ja | 50 GB |
| Premium P1V3 | Ja | 20 | Ja | 250 GB |
| Isolated I1V2 | Ja | 20 | Ja | 1 TB |

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
- Swap terugdraaien = swap staging ↔ production opnieuw — NOOIT dev ↔ production
- Scale up naar Standard eerst, dan autoscale rules instellen
- Docker container deployen = Publish instelling → Docker container

## App Service — Logging
| Type | Wat |
|---|---|
| Web Server Logging | HTTP requests — method, URI, client IP, port, user agent, response code |
| Application Logging | Applicatie errors, debug info |

## App Service — Diagnostic Logging Severity
- Verbose → Information → Warning → Error → Critical (laag naar hoog)
- "Store all warnings or higher" = severity Warning instellen
- Application Logging (Blob) = langdurig bewaren (meer dan 7 dagen)
- Application Logging (FileSystem) = kortetermijn, max 7 dagen
- Blob logging vereist voor langdurige opslag

## Container Services
| Service | Volledig | Gebruik | Scale to zero | Scaling trigger |
|---|---|---|---|---|
| ACI | Azure Container Instances | Korte geïsoleerde taken | Nee | Handmatig |
| App Service | Azure App Service | Docker web apps | Nee | HTTP / CPU |
| ACA | Azure Container Apps | Serverless microservices | Ja | HTTP / event-driven / CPU |
| AKS | Azure Kubernetes Service | Complexe orchestratie | Nee | Kubernetes HPA |

## AKS — API Server Toegang Beperken
- API server authorized IP ranges = publiek endpoint beperken tot vertrouwde IPs
- Private cluster = API server alleen bereikbaar vanuit VNet
- Kubernetes Metrics Server vereist voor HPA (Horizontal Pod Autoscaler)

## Container Apps — Subnet Vereisten
| Environment type | Minimale subnet grootte |
|---|---|
| Workload profiles | /27 |
| Consumption only | /23 |

## ACR (Azure Container Registry) Tiers
| Tier | Private endpoints | Geo-replication |
|---|---|---|
| Basic | Nee | Nee |
| Standard | Nee | Nee |
| Premium | Ja | Ja |

- Content trust = signed images
- ACR Tasks = automatisch rebuilden bij base image update — werkt op ALLE tiers inclusief Basic

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

## VM Host Caching
| Caching | Gebruik | Dataverlies bij host failure? |
|---|---|---|
| None | Veilig, traagst | Nee |
| Read-only | Reads gecached, writes direct naar storage | Nee |
| Read/Write | Snelst | **Ja — niet voor productie data** |

- "No data loss + performance" = Read-only caching

## VM Redeploy
- Redeploy = VM verplaatsen naar nieuwe Azure host
- Gebruik bij: planned maintenance melding, host problemen
- Tijdelijke disk (D: / /dev/sdb) gaat verloren bij redeploy

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

## Subnet Groottes — Minimale Vereisten
| Resource | Minimale subnet | Adressen totaal | Bruikbare adressen* | Subnetnaam vereist |
|---|---|---|---|---|
| Container Apps Consumption | /23 | 512 | 507 | Vrij te kiezen |
| Application Gateway | /24 aanbevolen | 256 | 251 | Vrij te kiezen |
| Azure Firewall | /26 | 64 | 59 | AzureFirewallSubnet |
| Azure Bastion | /26 | 64 | 59 | AzureBastionSubnet |
| VPN Gateway | /27 | 32 | 27 | GatewaySubnet |
| Container Apps Workload profiles | /27 | 32 | 27 | Vrij te kiezen |
| Azure Route Server | /27 | 32 | 27 | RouteServerSubnet |

*Azure reserveert altijd 5 adressen per subnet: netwerk (.0), gateway (.1), DNS (.2 en .3), broadcast (.255)

## Subnet Mask Overzicht
| Subnet mask | Adressen totaal | Bruikbare adressen | Wat verandert | Voorbeeld range |
|---|---|---|---|---|
| /16 | 65536 | VNet niveau | 3e + 4e octet vrij | 10.10.0.0 – 10.10.255.255 |
| /24 | 256 | 251 | 4e octet vrij | 10.10.1.0 – 10.10.1.255 |
| /25 | 128 | 123 | 4e octet, helft | 10.10.1.0 – 10.10.1.127 |
| /26 | 64 | 59 | 4e octet, kwart | 10.10.1.0 – 10.10.1.63 |
| /27 | 32 | 27 | 4e octet, 1/8 | 10.10.1.0 – 10.10.1.31 |
| /28 | 16 | 11 | 4e octet, 1/16 | 10.10.1.0 – 10.10.1.15 |
| /29 | 8 | 3 | 4e octet, 1/32 | 10.10.1.0 – 10.10.1.7 |
| /30 | 4 | 0 (niet bruikbaar) | 4e octet, 1/64 | 10.10.1.0 – 10.10.1.3 |

**Ezelsbruggetje subnet groottes:**
- /26 = Firewall en Bastion
- /27 = VPN Gateway, Route Server, Container Apps Workload
- /23 = Container Apps Consumption

**Ezelsbruggetje octetten:**
- /8, /16, /24 = nette grenzen — elk octet volledig vrij
- Alles daartussen = deel van 4e octet vrij

## NSG Regels
- Inbound: Subnet NSG eerst → NIC NSG
- Outbound: NIC NSG eerst → Subnet NSG
- Inbound internet = geblokkeerd by default
- Inbound VNet = toegestaan by default
- Beide NSGs moeten toestaan anders geblokkeerd
- NSG koppelen aan: subnet of NIC — niet aan VNet of VM direct
- NSG regio = zelfde regio als subnet/NIC

## NSG Service Tags
- Service tag = vertegenwoordigt alle IP adressen van een Azure service
- Microsoft beheert en update IP adressen achter een service tag automatisch
- Blokkeren van Azure service in NSG = altijd Service tag gebruiken, nooit IP adres
- Voorbeelden: Storage, Sql, AppService, AzureMonitor, AzureBackup

## ASG (Application Security Group)
- Groepeert NICs van meerdere VMs
- Alle NICs moeten in hetzelfde VNet zitten
- "Fewest NSG rules" = altijd ASG
- ASG koppelen aan NIC — niet aan VM direct of subnet

## VNet Peering
- Peering is **niet transitief**
- Peering is **bidirectioneel** — als A gepeerd is met B, kunnen pakketten beide kanten op
- In de portal zie je peerings per VNet — je ziet alleen de eigen kant
- Twee peerings aanmaken nodig (A→B én B→A) — anders werkt het niet
- Gateway transit = VPN/ExpressRoute naar on-premises via hub gateway
- Disconnected = verwijder peer en maak opnieuw aan
- **Nieuw address space toegevoegd aan gepeerd VNet** → klik "Sync" op de peering (portal knop) — dit vernieuwt de routing tabel
- **Topologiewijziging** = structurele netwerkverandering (nieuwe VNet, peering aanpassen, gateway wijzigen) → P2S VPN clients moeten opnieuw geïnstalleerd worden omdat hun lokale routing tabel verouderd is
- Overlappende address spaces = peering niet mogelijk
- **VMs in verschillende VNets = peering vereist voor communicatie — ook voor DNS**

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
- Encrypted connection to on-premises = VPN Gateway (virtual network gateway)

## VPN Gateway Types — Policy-based vs Route-based
| Type | Gebruik | P2S mogelijk? |
|---|---|---|
| Policy-based | Alleen S2S, legacy | ✗ Niet mogelijk |
| Route-based | S2S én P2S | ✓ Vereist voor P2S |

- **P2S VPN vereist altijd route-based gateway**
- Policy-based gateway aanwezig + P2S nodig → verwijder policy-based gateway → deploy route-based
- Gateway subnet hoeft niet opnieuw aangemaakt — bestaat al als er al een gateway was
- Sleutelwoord "point-to-site" of "P2S" → route-based gateway vereist
1. **G**ateway subnet aanmaken (naam: GatewaySubnet, minimaal /27)
2. **V**PN gateway deployen
3. **L**ocal network gateway aanmaken (beschrijft on-premises kant: publiek IP + address range)
4. **C**onnection aanmaken

## Local Network Gateway
- Beschrijft het on-premises netwerk vanuit Azure perspectief
- Bevat: publiek IP van on-premises VPN apparaat + on-premises address range
- On-premises VPN apparaat krijgt nieuw IP → update Local Network Gateway IP adres

## Route Table — Next Hop Types
| Type | Gebruik |
|---|---|
| Virtual appliance | Aangepast IP adres opgeven — NVA, firewall |
| Internet | Publiek internet |
| Virtual network gateway | VPN/ExpressRoute |
| Virtual network | Binnen hetzelfde VNet |
| None | Traffic droppen |

## Route Prioriteit
1. User-defined routes / UDR (hoogste prioriteit — jij bepaalt)
2. BGP routes (dynamisch uitgewisseld via ExpressRoute of VPN — on-premises naar Azure)
3. System routes (Azure standaard — laagste prioriteit)
- Langste prefix wint — /24 wint van /16
- **BGP** = Border Gateway Protocol — routes die automatisch uitgewisseld worden tussen Azure en on-premises netwerk via ExpressRoute of VPN gateway. Niet handmatig configureren — werkt automatisch. AZ-104: onthoud alleen de volgorde.

## DNS Record Types
| Type | Gebruik |
|---|---|
| A | Domeinnaam → IPv4 |
| AAAA | Domeinnaam → IPv6 |
| CNAME | Alias — blijft geldig als IP verandert |
| MX | Email routing |
| TXT | Domeinverificatie |
| NS | Delegatie naar DNS servers |
| SOA | Automatisch aangemaakt |

**CNAME vs A voor web apps:**
- CNAME = domein → ander domein — blijft geldig bij IP wijziging ✓
- A record = domein → IP — moet worden bijgewerkt bij IP wijziging ✗

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
| VNet peering + DNS resolution | Peering alleen = NIET genoeg — zone moet ook gelinkt zijn aan het VNet |
| On-premises resolver krijgt publiek IP | Private DNS zone niet gelinkt aan VNet van on-premises resolver — link aanmaken lost dit op |

## DNS Zone Migratie Tools
- Azure CLI ✓
- Azure Portal ✓
- Azure PowerShell ✗ — geen native zone file import
- CloudShell ✗ — is omgeving, niet een tool op zichzelf

## Custom Domain in Azure DNS — Volgorde
1. Maak Azure public DNS zone aan
2. Kopieer de 4 NS records van Azure
3. Plak die NS records bij je domeinregistrar

## Subdomain Delegatie
- Subdomain delegeren naar andere zone → NS record aanmaken in parent zone

## Private DNS Zone

## VNet Peering vs Virtual Network Link — NIET hetzelfde
| | VNet Peering | Virtual Network Link |
|---|---|---|
| Wat | Netwerkverbinding — VMs kunnen elkaar bereiken | DNS koppeling — VNet mag private DNS zone gebruiken |
| Waar instellen | VNet → Peerings blade | Private DNS Zone → Virtual network links blade |
| Effect | Verkeer kan stromen tussen VNets | VMs in dat VNet kunnen de zone resolven |
| Regio | Maakt niet uit | Maakt niet uit |

**Je kunt peering hebben zonder DNS link** → VMs bereikbaar maar domeinnaam niet resolvable
**Je kunt DNS link hebben zonder peering** → domeinnaam resolvable maar VMs niet bereikbaar via die naam
**Ezelsbruggetje:** Peering = snelweg tussen steden. Virtual Network Link = telefoonboek (weet je het adres)

## Resolvable — wat betekent het
- Resolvable = kan een VM een domeinnaam omzetten naar een IP adres?
- Niet resolvable = VM weet het IP adres niet → kan er niet naartoe verbinden
- Vereiste voor resolvable = VNet moet gelinkt zijn aan de private DNS zone via Virtual Network Link
- Peering alleen = NIET genoeg voor DNS resolution
- Zelfde subscription / zelfde regio = NIET genoeg — alleen Virtual Network Link telt

## Auto-registration
- Auto-registration = VMs in een gelinkt VNet registreren automatisch hun A record in de zone
- Vereist: VNet gelinkt aan zone ÉN auto-registration ingeschakeld op de link
- VNet kan maar **één** registration zone hebben
- Private DNS zone kan meerdere registration VNets hebben
- Auto-registration = alleen private DNS zones — public zones kunnen NIET gelinkt worden

## Overige regels
- DNS Private Resolver = proxy voor on-premises naar Azure DNS — NIET voor auto-registration
- Locatie DNS zone irrelevant — zone in Australia Central kan gelinkt worden aan VNet in West Europe
- Linken aan VNet = alleen private DNS zones — public zones kunnen NIET gelinkt worden

## Samenvatting — wanneer wat nodig
| Doel | Wat nodig |
|---|---|
| VM kan andere VM bereiken | VNet Peering |
| VM kan domeinnaam resolven uit private zone | Virtual Network Link |
| VM registreert automatisch in zone | Virtual Network Link + auto-registration aan |
| Beide bereikbaar én resolvable | Peering + Virtual Network Link |

## Load Balancer — Backend Pool
- VM zonder public IP → mag erin ✓
- VM stopped → mag erin ✓
- Basic IP + Standard LB → niet compatibel ✗
- Standard public IP = altijd Static
- VM verwijderen uit backend pool = public IP verwijderen OF upgraden naar Standard

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
- Verbindt via privé IP — NOOIT via publiek IP
- Werkt binnen hetzelfde VNet of via VNet peering
- Zonder peering = geen verbinding naar andere VNets
- AzureBastionSubnet vereist — minimaal /26

## Network Watcher
- **Automatisch aangemaakt per regio** wanneer VNet wordt aangemaakt
- 2 regio's = 2 Network Watcher instanties — aantal VNets maakt niet uit
- Network Watcher = specifiek voor netwerk gezondheid (VMs, VNets, LB, App Gateway)
- Azure Monitor = logs, metrics, alerts voor alle Azure resources — NIET specifiek netwerk

## Network Watcher Tools — Uitgebreide Uitleg

**IP flow verify**
Test één specifieke flow: wordt dit pakket toegestaan of geblokkeerd door NSG?
Geeft: allow/deny + welke regel.
Keywords in question: "is traffic blocked", "which rule is blocking", "is port X open", "determine if NSG is causing the issue", "allowed or denied to/from a VM"
Verschil met Effective security rules: IP flow verify test één flow, effective security rules toont alle regels.

**Effective security rules**
Toont de complete merged ruleset van subnet NSG + NIC NSG + defaults voor één NIC.
Keywords in question: "merged rules", "all security rules that apply", "which rules apply to NIC", "precedence", "view all inbound and outbound rules"
Verschil met IP flow verify: niet één flow testen maar alle regels overzien.
Valkuil: NSG staat niet in de naam maar toont WEL alle NSG regels.

**Next hop**
Voor één destination IP: via welk next hop gaat het verkeer?
Geeft: next hop type (VirtualNetwork, Internet, VirtualNetworkGateway, VirtualAppliance)
Keywords in question: "what is the next hop for traffic to X", "where is traffic being directed", "next hop for destination"
Verschil met Effective routes: next hop = één destination, effective routes = alle routes.
**VALKUIL: "next hop" als woord in vraag ≠ Next hop tool. "Verify if traffic uses peering" = Effective routes.**

**Effective routes**
Toont alle actieve routes op een NIC — system routes, UDRs, BGP routes samen.
Keywords in question: "all active routes", "why is traffic taking unexpected route", "verify UDR is correct", "verify whether traffic uses virtual network peering as the next hop"
Verschil met Next hop: compleet overzicht, niet één destination.

**Connection troubleshoot**
Eenmalige test: kan VM A endpoint B bereiken? Lost ook DNS op bij FQDN.
Geeft: reachable/unreachable + latency + DNS resolution resultaat
Keywords in question: "can VM reach endpoint", "is there connectivity", "one-time test", "test connectivity to"
Verschil met Connection monitor: eenmalig vs doorlopend.
Verschil met IP flow verify: bereikbaarheid testen vs NSG gedrag testen.

**Connection monitor**
Doorlopende monitoring van bereikbaarheid en latency tussen endpoints. Slaat op in Log Analytics. Alerteerbaar via Azure Monitor.
Keywords in question: "continuously monitor", "ongoing monitoring", "latency over time", "alertable connectivity", "monitor latency between"
Verschil met Connection troubleshoot: continu vs eenmalig.

**Packet capture**
Neemt volledig netwerkverkeer op van een NIC. Max 5 uur. Vereist Network Watcher Agent extension op de VM.
Keywords in question: "capture all traffic", "full packet content", "forensic investigation", "payload", "record all sessions to track traffic for X seconds"
Verschil met NSG flow logs: packet capture = volledige inhoud, NSG flow logs = alleen metadata.

**NSG flow logs**
Logt metadata van alle flows door een NSG — source/destination IP, poort, protocol, allow/deny. Schrijft naar storage account.
Keywords in question: "capture information about IP traffic going to and from a NSG", "log network traffic", "historical traffic", "compliance logging", "which traffic has passed through"
Verschil met packet capture: alleen metadata, geen inhoud.
Verschil met Effective security rules: flow logs = verkeer dat heeft plaatsgevonden, effective security rules = regels die gelden.
Valkuil: NSG staat WEL in de naam maar toont geen regeloverzicht.
**VALKUIL Traffic Analytics:** Traffic Analytics verwerkt NSG flow logs achteraf tot inzichten — het logt zelf NIKS en test NIKS. "Capture" = NSG flow logs, niet Traffic Analytics.

**Traffic Analytics**
Verwerkt NSG flow logs en toont inzichten in Log Analytics — hotspots, verdachte flows, geografische verdeling, trends.
Keywords in question: "insights", "visualize traffic", "hotspots", "suspicious patterns", "geographic distribution", "analyze network traffic"
Vereist: storage account + Log Analytics workspace.
Verschil met NSG flow logs: flow logs = ruwe data, Traffic Analytics = verwerkte inzichten.
Verschil met Network topology: Traffic Analytics = verkeersanalyse, Network topology = visuele kaart van resources.

**VPN troubleshoot**
Diagnosticeert problemen met VPN gateway verbindingen — status, fouten, logs.
Keywords in question: "VPN gateway connection issues", "troubleshoot VPN", "gateway logs", "diagnose VPN"
Verschil met Connection troubleshoot: specifiek voor VPN gateways, niet voor algemene connectivity.

**Network topology**
Visueel overzicht van alle netwerkresources en hun verbindingen binnen een regio — VNets, subnets, VMs, NSGs.
Keywords in question: "visual map of resources", "overview of connected resources", "which resources are connected", "network topology"
Verschil met Traffic Analytics: Network topology = resources en verbindingen, Traffic Analytics = verkeersanalyse.

## Network Watcher — Sleutelwoorden Samenvatting
| Sleutelwoord in vraag | Tool |
|---|---|
| "is traffic blocked" / "which rule is blocking" / "allowed or denied" | IP flow verify |
| "all security rules" / "merged ruleset" / "view all inbound and outbound rules" | Effective security rules |
| "next hop for destination X" / "where is traffic directed" | Next hop |
| "all active routes" / "verify UDR" / "verify whether traffic uses peering as next hop" | Effective routes |
| "can VM reach endpoint" / "test connectivity" / "one-time test" | Connection troubleshoot |
| "continuously monitor" / "ongoing" / "latency over time" / "alertable" | Connection monitor |
| "capture all traffic" / "full packet" / "forensic" / "record sessions for X seconds" | Packet capture |
| "capture IP traffic going to/from NSG" / "log network traffic" / "compliance logging" | NSG flow logs |
| "insights" / "hotspots" / "visualize traffic" / "geographic distribution" | Traffic Analytics |
| "VPN gateway issues" / "troubleshoot VPN" | VPN troubleshoot |
| "visual map of resources" / "network topology" | Network topology |
| "monitor network health" / "centralized console network monitoring" | Azure Network Watcher |
| "diagnostics and telemetry data multiple resources" | Log Analytics workspace |

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

## Multi-User Authorization (MAU) — Resource Guard
- MAU = miauw = kat → Resource Guard beschermt tegen de kat
- Volgorde: **Resource Guard aanmaken → koppelen aan vault → MAU inschakelen**
- Resource Guard = apart Azure resource in andere subscription/tenant voor extra bescherming
- Zonder Resource Guard = MAU niet mogelijk

## Azure Backup
- Werkt altijd — ook bij stopped/deallocated VM
- Vault en VM in dezelfde regio
- Volgorde: Vault → Policy → Koppelen
- Default retention: 30 dagen
- Soft delete retention: 14 dagen
- Blob containers = NIET te backuppen via Azure Backup
- Azure SQL Database = NIET te backuppen via Azure Backup
- Instant Restore = snapshots lokaal opgeslagen — retention verlagen = minder storage

## MARS Agent — Volgorde
1. Recovery Services vault aanmaken
2. MARS agent installeren
3. Vault credentials downloaden en server registreren
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
- Replace existing disk — VM moet nog bestaan, disk blijft in RG na restore — **alleen naar dezelfde VM**
- File Recovery — alleen naar **zelfde of lagere OS versie** — NIET naar hogere versie

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
- Log alert rule = scoped op Log Analytics workspace, niet op VM direct

## Traffic Analytics — Vereisten
- NSG Flow Logs ingeschakeld ✓
- Log Analytics workspace ✓
- **Data Collection Rule (DCR)** ✓ — bepaalt welke data verzameld wordt en waar naartoe
- Storage account ✓
- Vereiste rollen: Owner, Contributor of Network Contributor op subscription scope

## Azure Monitor Network Insights
- Centraal dashboard met metrics, health status en netwerktopologie
- Sleutelwoord: "dashboard", "metrics + topologie overzicht", "meerdere netwerkresources"
- Verschil met Network Watcher: Network Watcher = losse tools, Network Insights = overkoepelend dashboard

## Connection Monitor — Agent Vereisten
| Machine type | Wat installeren | Hoe |
|---|---|---|
| Azure VM | Azure Monitor Agent | Automatisch via portal |
| On-premises server | Azure Monitor Agent extension | Handmatig installeren op server |

- On-premises server monitoren met Connection Monitor = **Azure Monitor Agent extension installeren**
- Recovery Services agent = backup — niet voor network monitoring
- Dependency agent = applicatie dependencies — niet voor network latency

## App Service — HTTP Logging
- HTTP 500 errors zichtbaar maken voor developers = **Web server logging activeren**
- Web server logging legt vast: HTTP method, URI, response code, client IP, user agent, tijdstip
- "Real-time detailed visibility into connection errors" = Web server logging
- Alert rule = notificeert maar geen detail. Workbook = visualisatie bestaande data, geen nieuwe data

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
| Operator | Gebruik | Sleutelwoord in vraag | Voorbeeld |
|---|---|---|---|
| where | Filtert rijen op conditie | "filter", "only show", "errors only" | where Level == "Error" |
| summarize | Groepeert en aggregeert — telt, sommeert, gemiddelde berekent | "aggregate", "group by", "count per", "by column" | summarize count() by Account |
| project | Selecteert alleen specifieke kolommen — verbergt de rest | "select columns", "only show fields" | project TimeGenerated, Account |
| extend | Voegt een nieuwe berekende kolom toe | "add column", "calculate new field" | extend Duration = EndTime - StartTime |
| search in (Table) "value" | Zoekt een waarde in een specifieke tabel | "search in", "find in table" | search in (SecurityEvent) "admin" |
| order by / sort by | Sorteert resultaten | "sort", "order", "ascending", "descending" | order by TimeGenerated desc |
| top | Geeft de eerste N rijen terug | "top X", "first X results" | top 10 by Count |
| distinct | Geeft unieke waarden terug | "unique", "distinct values" | distinct Account |

**Aggregeren** = meerdere rijen samenvatten tot één resultaat — zoals tellen, optellen, gemiddelde. Vergelijkbaar met GROUP BY in SQL.

**Examen sleutelwoord:** "aggregate by column" of "group results by" → altijd **summarize**

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
| WAF | Application Gateway |
| Mount / mounten / SMB / NFS | Azure Files |
| Mount from Azure + on-premises | Azure Files |
| Identity-based access storage | Azure Files |
| Persistent storage VM disk | Azure Disk |
| Persistent storage container | Azure Files (file share) |
| Replicatie andere regio minimale kosten | Standard_GRS |
| Replicatie zelf regio kiezen / minimize latency | Object replication (GPv2 of Premium block blob) |
| Fewest NSG rules | ASG |
| Centralized console network / dashboard metrics topologie | Azure Monitor Network Insights |
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
| Underutilized VMs / unattached disks specifieke RGs | Azure Advisor configuratie aanpassen scope |
| Underutilized VMs / unattached disks algemeen | Azure Advisor Cost |
| Unattached disks identificeren | Azure Cost Management → Advisor recommendations |
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
| Verify of traffic via peering gaat | Effective routes |
| Monitor network health netwerk resources | Azure Network Watcher |
| Diagnostics en telemetry data meerdere resources | Log Analytics workspace |
| Verkeer door firewall sturen | NVA + UDR |
| Scripts eenmalig bij deployment | Custom Script Extension |
| Scripts consistent + compliance | DSC extension |
| Subdomain delegeren | NS record in parent zone |
| Over internet kopiëren naar blob | Azure Storage Explorer |
| Replicatie automatisch paired region | GRS |
| System Center Service Manager alert | ITSMC |
| MAU / Multi-User Authorization vault | Resource Guard aanmaken eerst |
| No data loss + performance disk | Read-only host caching |
| Sensitive data encryptie compliance | Customer-managed keys in Key Vault |
| DNS zone migreren / importeren | Azure CLI of Azure Portal |
| Latency meten / vergelijken on-premises vs Azure | Connection Monitor |
| NSG App Service inbound | Niet mogelijk — App Service is PaaS |
| Groep met assigned license verwijderen | Eerst licentie verwijderen dan groep |
| Low latency VMs fysiek dicht bij elkaar | Proximity Placement Group — zelfde regio |
| Root management group toegang | Global Admin + Access management for Azure resources |
| Blokkeren Azure service in NSG | Service tag gebruiken |
| Deployment destination RG/subscription in Bicep | scope property |
| Azure Backup storage account achter firewall | Allow trusted Microsoft Services aanvinken |
| File recovery naar andere VM | Alleen zelfde of lagere OS versie |
| VM restore replace existing disk | Alleen naar dezelfde VM |
| Encrypted connection to on-premises | VPN Gateway (virtual network gateway) |
| ARM template opgeslagen in Blob Storage | -TemplateUri parameter |
| ARM template lokaal bestand | -TemplateFile parameter |
| ARM template als Template Spec | -TemplateSpecId parameter |
| Network Watcher per regio | Automatisch aangemaakt — 2 regio's = 2 instanties |
| VMs koppelen aan departement rapportage | Tags |
| Associate resources to department billing | Tags |
| Docker container als web app deployen | App Service — Publish → Docker container |
| AKS API server beperken tot VNet | Private cluster |
| AKS API server beperken tot IP ranges | API server authorized IP ranges |
| Hybrid identities Azure Files geen DC line-of-sight | Entra Kerberos authenticatie |
| Data Lake Storage / big data analytics | Enable hierarchical namespace (GPv2) |
| P2S VPN met policy-based gateway | Verwijder policy-based → deploy route-based gateway |
| On-premises server Connection Monitor | Azure Monitor Agent extension installeren |
| HTTP 500 errors zichtbaar voor developers | Web server logging activeren |
| Email ARM Role notificaties | Alleen users ontvangen email — managed identities nooit |
| Custom rol aanmaken op basis van bestaande | Get-AzRoleDefinition -Name "Rol" | ConvertTo-Json |
| Web requests slow + trace cause of delay | Application Insights Profiler |
| Monitor system performance metrics + log events doorlopend | Azure Monitor Agent |
| On-demand troubleshoot VM performance | Azure Performance Diagnostics VM Extension |
| Capture IP traffic going to/from NSG | NSG flow logs |
| Diagnose connectivity issues to/from VM | IP flow verify |
| Visualize/analyze NSG flow log data | Traffic Analytics |
| Conditional access MFA + hybrid joined device | Grant control |
| Conditional access beperkte ervaring in app | Session control |
| Azure Files AD DS volgorde | Sync AD → Enable AD DS → Assign permissions → Mount (S-E-A-M) |
| Container App niet bereikbaar | Check of ingress ingeschakeld is |
| Custom domain toevoegen aan Entra ID volgorde | Provision directory → Add domain → Add DNS to registrar → Verify |
| Redeploy VM naar andere regio | NIET mogelijk via redeploy — gebruik Azure Resource Mover of Site Recovery |
| ExpressRoute + S2S VPN coexistentie minimum SKU | VpnGw1 — Basic SKU ondersteunt geen coexistentie |

---

---

# ⚡ QUICK QUICK REFERENCE — Meest gemaakte fouten

## RBAC & Governance

- **Least privilege in vraag?** → meest specifieke rol. Niet in vraag? → elke werkende rol = Yes
- **Logic App Operator** = alleen lezen/aan/uit — NIET aanmaken. Aanmaken = Logic Apps Contributor of Contributor
- **Does this meet the goal?** → lost PRECIES deze actie het VOLLEDIGE probleem op? Blijft er nog een blokkade? → No
- **Get-AzRoleDefinition** = wat de rol IS (permissions). **Get-AzRoleAssignment** = wie de rol HEEFT
- **ConvertTo-Json** = PowerShell → JSON (exporteren). **ConvertFrom-Json** = JSON → PowerShell (inlezen)
- **Custom rol aanmaken:** `Get-AzRoleDefinition -Name "Contributor" | ConvertTo-Json`
- **Tags** = metadata voor Azure resources (VMs, RGs, subscriptions). Administrative units = Entra ID objecten — NIET voor Azure resources
- **Root management group** = alleen Global Admin + "Access management for Azure resources" aanzetten. Owner/Contributor werken NIET op root niveau
- **Deny erft altijd naar beneden** — Deny op Root = alles eronder geblokkeerd, ongeacht Allow op lagere scope
- **VM aanmaken vereist VNet** — VNet geblokkeerd door policy → VM ook geblokkeerd
- **Managed identities ontvangen GEEN email** van action groups — alleen users (direct of via groep)
- **UsageLocation** moet ingesteld zijn voordat licentie toegewezen kan worden

---

## Storage

- **Identity-based access** = Azure Files — enige storage service met AD/Kerberos authenticatie
- **Mount / SMB / NFS** = Azure Files. **Persistent VM disk** = Azure Disk. **Blob over internet** = Azure Storage Explorer
- **Archive rehydreren** naar Hot, Cool, **of Cold** — niet terug naar Archive
- **Object replication vereisten:** blob versioning source + destination + change feed source. Beide GPv2 of Premium block blob
- **Storage firewall + Azure Backup** = "Allow trusted Microsoft Services" aangevinkt. Zonder = Backup werkt niet

---

## Networking

- **"Next hop" als woord in vraag ≠ Next hop tool**
  - "Verify of traffic via peering gaat" → **Effective routes**
  - "Wordt dit pakket geblokkeerd?" → **IP flow verify**
  - "Alle NSG regels overzien" → **Effective security rules**
  - "Kan VM bereiken?" eenmalig → **Connection troubleshoot**

- **Network Watcher** = netwerk gezondheid (VMs, VNets, LB). **Azure Monitor** = logs/metrics/alerts voor alles
- **Network Watcher per regio automatisch** — 2 regio's = 2 instanties, aantal VNets maakt niet uit
- **VNet Peering ≠ Virtual Network Link**
  - Peering = VMs kunnen elkaar bereiken (verkeer)
  - Virtual Network Link = VMs kunnen domeinnaam resolven (DNS)
  - Peering alleen = DNS werkt NIET. Beide nodig = Peering + Virtual Network Link
- **Proximity Placement Group** = zelfde regio vereist — resource group maakt NIET uit
- **Encrypted connection to on-premises** = VPN Gateway. Private endpoint = Azure services, niet on-premises
- **ARM template in Blob Storage** = `-TemplateUri`. Lokaal = `-TemplateFile`. Template Spec = `-TemplateSpecId`

---

## Compute

- **Redeploy** = VM naar nieuwe Azure host. Tijdelijke disk (D: / /dev/sdb) gaat verloren
- **Availability Set:** Update domains = gepland onderhoud. Fault domains = ongepland. FD=1 vereist UD=1
- **Operator rol** = bestaande resources bedienen — NIET aanmaken. Contributor = aanmaken én beheren

---

## Monitor & Backup

- **Action group EERST, dan alert rule**
- **Azure Backup + stopped VM** = werkt altijd — backup draait ook als VM uit staat
- **File Recovery** = alleen naar zelfde of lagere OS versie
- **Replace existing disk** = alleen naar dezelfde VM
- **MARS volgorde:** Vault → Agent installeren → Vault credentials downloaden → Policy → Backup starten
- **Web requests slow + trace** = Application Insights Profiler
- **Monitor doorlopend VM** = Azure Monitor Agent. **Eenmalig troubleshoot** = Performance Diagnostics

---

## Conditional Access

- **Grant control** = MFA + hybrid joined device afdwingen — dit is wat je nodig hebt voor "require MFA and hybrid device"
- **Session control** = beperkte ervaring binnen apps — NIET voor MFA of device vereisten
- **Alleen MFA configureren in security** = No — dit is geen conditional access policy en dwingt geen hybrid joined device af

---

## Azure Files AD DS — Volgorde S-E-A-M

1. **S**ync on-premises AD met Microsoft Entra Connect
2. **E**nable AD DS authentication op storage account
3. **A**ssign share and directory permissions (RBAC + NTFS)
4. **M**ount file share with AD credentials

**Ezelsbruggetje:** zonder sync weet Azure niet wie de gebruikers zijn. Zonder enable AD DS auth werkt authenticatie niet. Zonder permissions heeft niemand toegang. Dan pas mounten.
