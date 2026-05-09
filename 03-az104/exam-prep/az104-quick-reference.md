# AZ-104 Quick Reference — Key Facts

## Poorten
| Poort | Protocol/Gebruik |
|---|---|
| 80 | HTTP (Hypertext Transfer Protocol) |
| 443 | HTTPS (Hypertext Transfer Protocol Secure) |
| 445 | SMB (Server Message Block) — Azure Files |
| 3389 | RDP (Remote Desktop Protocol) |
| 22 | SSH (Secure Shell) |
| 5671 | AMQP (Advanced Message Queuing Protocol) — Azure Service Bus / health data |
| 587 | SMTP relay (Simple Mail Transfer Protocol) — outbound email via authenticated SMTP |
| 25 | SMTP (Simple Mail Transfer Protocol) — mail traffic (niet authenticated) |

---

## IDENTITIES & GOVERNANCE

## RBAC (Role-Based Access Control) Rollen
| Rol | Resources beheren | Rollen toewijzen |
|---|---|---|
| Owner | Ja | Ja |
| Contributor | Ja | Nee |
| Reader | Nee (alleen lezen) | Nee |
| User Access Administrator | Nee | Ja |
| Cost Management Contributor | Nee | Nee — alleen kosten bekijken en budgets beheren |
| Storage Account Contributor | Ja — storage accounts + access keys | Nee |
| Resource Policy Contributor | Nee | Nee — alleen policy definitions en assignments beheren |

## Entra ID Licenties vs Rollen
- Rol = wat je mag doen (lezen, schrijven, beheren resources)
- Licentie = welke features beschikbaar zijn (SSPR, Conditional Access, PIM)
- P1 licentie toewijzen = via Licenses blade in Entra ID
- Rol toewijzen geeft geen toegang tot premium features
- Sleutelwoord "Premium P1 features" = licentie toewijzen, niet rol

## Hybrid Entra ID — Attributen Aanpassen
- Users gesynchroniseerd vanuit Windows Server AD: Job Info attributen (Department, Job Title) NIET aanpasbaar in Entra ID — moet in on-premises AD
- UsageLocation: altijd aanpasbaar in Entra ID voor alle users ongeacht source
- Cloud-only users: alle attributen aanpasbaar in Entra ID

## Microsoft 365 Groepen vs Security Groepen — Expiration Policy
- Expiration policy (automatisch verwijderen na X dagen) = alleen Microsoft 365 groepen
- Security groepen ondersteunen geen expiration policy
- Zowel assigned als dynamic Microsoft 365 groepen ondersteunen expiration

## Traffic Analytics — Vereiste Rollen
- Vereist Azure RBAC rol op subscription scope
- Owner, Contributor of Network Contributor
- Reader, Security Operator = onvoldoende om in te schakelen
- Reader kan wel visualisaties bekijken als Traffic Analytics al is ingeschakeld
- Entra ID rollen ≠ Azure RBAC rollen — zijn twee verschillende systemen

## Deny Assignments
- Deny overschrijft altijd allow — ook Owner rol
- Deny op lagere scope wint van allow op hogere scope

## Azure Policy Effects
| Effect | Type | Wat doet het |
|---|---|---|
| Deny | Synchroon | Blokkeert non-compliant resource aanmaken |
| Audit | Asynchroon | Flaggt alleen, blokkeert niet |
| Modify | Synchroon | Voegt tags/properties toe automatisch |
| DeployIfNotExists | Asynchroon | Deployt template als resource niet bestaat |
| AuditIfNotExists | Asynchroon | Audit als gerelateerde resource ontbreekt |

## Azure Policy Definitie Secties
| Sectie | Inhoud |
|---|---|
| policyRule | If/then logica — conditie en effect |
| parameters | Variabelen voor herbruikbaarheid |
| mode | Welke resources worden geëvalueerd (All of Indexed) |
| metadata | Beschrijvende informatie + RemediationDescription veld |

## ARM (Azure Resource Manager) Template Deployment Scopes
| Scope | Gebruik |
|---|---|
| Resource group | Één resource group |
| Subscription | Meerdere resource groups, nieuwe RGs aanmaken |
| Management group | Meerdere subscriptions |
| Tenant | Alles |

## ARM Deployment Scope — Ezelsbruggetje
Onthoud de hiërarchie — deploy altijd één niveau boven wat je wilt aanmaken of aanspreken:
Tenant → Management Group → Subscription → Resource Group (RG) → Resource

## ARM Template — Inline Parameters
- Inline = direct in het deployment commando via `--parameters`
- Voor een array: `--parameters arrayParam='["value1","value2"]'`
- Parameters file = apart JSON (JavaScript Object Notation) bestand, niet inline
- Template aanpassen = nooit doen voor variabele waarden

## ARM Template — Wachtwoorden
- Sla wachtwoorden nooit op in plain text in een template
- Gebruik Azure Key Vault + access policy om wachtwoorden op te slaan
- ARM template verwijst naar Key Vault secret tijdens deployment

## Delete Locks — Wel/Niet
| Resource | Delete lock mogelijk |
|---|---|
| Subscriptions | Ja |
| Resource groups (RGs) | Ja |
| Individuele resources (VMs, storage accounts) | Ja |
| Management groups | Nee |
| Storage account data (blobs, files) | Nee — gebruik immutability policy |

## Custom Domain Verificatie in Microsoft Entra ID
- Verificatie vereist een DNS record bij je domeinprovider
- Twee opties: TXT record (aanbevolen) of MX record
- Azure geeft je een verificatiecode die je als TXT of MX record toevoegt
- A record = IP adres koppeling — niet voor verificatie
- SOA = zone informatie — automatisch aangemaakt, niet aanpasbaar
- RRSIG = DNSSEC handtekening — niet relevant voor Entra verificatie

## Budget Alert — Vereiste Stappen
1. Action group aanmaken van type Runbook met Stop VM actie
2. Budget settings wijzigen in Cost Management + Billing — drempel instellen en action group koppelen
- Beide stappen zijn vereist — budget is de trigger, action group is de actie

---

## STORAGE

## Storage Access Tiers
| Tier | Minimum opslag | Retrieval | Gebruik |
|---|---|---|---|
| Hot | Geen | Snel | Frequent accessed |
| Cool | 30 dagen | Snel | Infrequent, goedkoper dan Hot |
| Cold | 90 dagen | Snel | Infrequent, goedkoper dan Cool |
| Archive | 180 dagen | Uren (rehydration) | Zelden accessed |

## Rehydration uit Archive
| Prioriteit | Tijd |
|---|---|
| Standard | Tot 15 uur |
| High | Binnen 1 uur (objecten onder 10 GB) |

## Storage Redundancy
| Type | Beschrijving | Zone spreiding | Secundaire regio | Direct leestoegang secundair |
|---|---|---|---|---|
| LRS (Locally Redundant Storage) | 3 kopieën in 1 datacenter | Nee | Nee | Nee |
| ZRS (Zone Redundant Storage) | 3 kopieën over 3 zones | Ja | Nee | Nee |
| GRS (Geo Redundant Storage) | LRS + secundaire regio | Nee | Ja | Nee |
| RA-GRS (Read-Access Geo Redundant Storage) | GRS + leestoegang | Nee | Ja | Ja |
| GZRS (Geo Zone Redundant Storage) | ZRS + secundaire regio | Ja | Ja | Nee |
| RA-GZRS (Read-Access Geo Zone Redundant Storage) | GZRS + leestoegang | Ja | Ja | Ja |

## Storage Account Types — Volledig Overzicht
| Type | Ondersteunde services | Redundancy opties |
|---|---|---|
| Standard general-purpose v2 | Blob, Queue, Table, Azure Files, Data Lake Storage | LRS, ZRS, GRS, RA-GRS, GZRS, RA-GZRS |
| Premium block blobs | Blob Storage (inclusief Data Lake Storage) | LRS, ZRS |
| Premium file shares | Azure Files | LRS, ZRS |
| Premium page blobs | Page blobs only | LRS, ZRS |

## Storage Account Types — ZRS Live Migration
- Live migration naar ZRS mogelijk vanuit: LRS of GRS
- Live migration naar ZRS NIET mogelijk vanuit: RA-GRS (eerst omzetten naar LRS of GRS)
- General-purpose V1 en BlobStorage ondersteunen ZRS niet — alleen GPv2, FileStorage en BlockBlobStorage

## Object Replicatie Vereisten
- Blob versioning op source ✓
- Blob versioning op destination ✓
- Change feed op source ✓ (niet destination)

## Identity-based Access — Azure Files
- Alleen file shares ondersteunen identity-based access via Microsoft Entra Kerberos
- Blob, Queue en Table gebruiken REST API — geen Kerberos ondersteuning
- Vereist: identity-based access inschakelen op de file share instellingen
- SAS tokens bieden geen domeinintegratie — gebruik identity-based access voor AD DS/Entra authenticatie

## Storage Toegang — Vergelijking
| | Access key | Azure role | SAS token | Conditional Access |
|---|---|---|---|---|
| Scope | Heel storage account | Specifieke rol op gekozen scope | Specifieke resource of container | Aanmelding — niet storage specifiek |
| Expiry | Geen | Geen | Instelbaar | Niet van toepassing |
| Intrekken | Key regenereren | Role assignment verwijderen | Token laten verlopen | Policy wijzigen |
| Gebruik | Legacy apps zonder Entra ID | Gebruikers en moderne apps via Entra ID | Tijdelijke externe toegang | Toegangscontrole op basis van signalen |
| Least privilege | Nee | Ja | Ja | Niet van toepassing op storage data |

## Lifecycle Management
- Werkt alleen op block blobs (niet page blobs, niet append blobs)
- Access tracking inschakelen vereist voor regels op basis van laatste toegang
- Tiers: Hot → Cool → Cold → Archive (alleen in deze richting automatisch)

## AzCopy
- `azcopy copy` — eenmalige kopie van bron naar doel
- `azcopy sync` — synchroniseert inclusief verwijderingen — gevaarlijk voor migratie
- Ondersteunt blob en file storage
- Ondersteunde OS: Windows, Linux en macOS
- Authenticatie: Microsoft Entra ID of SAS token — geen Kerberos, API key of Microsoft Authenticator

## DNS Zone Migratie
- DNS zone file importeren: Azure CLI of Azure Portal
- Azure PowerShell = niet ondersteund voor zone file import
- Cloud Shell = uitvoeringsomgeving voor CLI, geen zelfstandige tool

---

## COMPUTE

## App Service Tiers — Volledig Overzicht
| Tier | Max instances | Storage | Custom domain | Slots | Autoscale |
|---|---|---|---|---|---|
| Free F1 | 1 | 1 GB | Nee | Nee | Nee |
| Basic B1 | 3 | 10 GB | Ja | Nee | Handmatig |
| Standard S1 | 10 | 50 GB | Ja | 5 | Ja |
| Premium P1V3 | 30 | 250 GB | Ja | 20 | Ja + Elastic |
| Isolated I1V2 | 100 | 1 TB | Ja | 20 | Ja |

## App Service — Runtime Stack vs OS
| Runtime | OS |
|---|---|
| ASP.NET V4.8 | Windows only |
| PHP | Linux only |
| Python | Linux only |
| Ruby | Linux only |
| Node.js | Windows en Linux |
| Java | Windows en Linux |
- Eén App Service plan per OS — ASP.NET + PHP vereist twee plannen
- Meerdere web apps kunnen één App Service plan delen in dezelfde regio

## App Service — Scale up vs Scale out
| | Scale up | Scale out |
|---|---|---|
| Wat | Grotere tier — meer CPU/geheugen/features | Meer instances van dezelfde tier |
| Wanneer | App heeft meer resources nodig per instance | App heeft meer capaciteit nodig door meer verkeer |
| Autoscale vereist | Eerst scale up naar Standard of hoger | Dan autoscale regels instellen |

## App Service — Publish instelling
- **Code** → kies Runtime stack (.NET, Node.js, Python etc.)
- **Docker Container** → Runtime stack niet beschikbaar — runtime zit in de container
- Voor een Docker image: altijd Publish → Docker Container instellen

## App Service — Deployment Slots
- Swap slots om snel terug te keren naar vorige versie
- Staging → Production swap = snelste manier om te reverten
- Restore backup = langzamer en vereist vooraf geconfigureerde backup

## App Service — Diagnostic Logging Severity
| Level | Wat het logt |
|---|---|
| Verbose | Alles — elke detailstap |
| Information | Normale operatie |
| Warning | Onverwacht maar niet kritiek |
| Error | Fouten die actie vereisen |
| Critical | Ernstige fouten — applicatie kan niet doorgaan |

- "Warnings or higher" = Warning + Error + Critical
- Application Logging Blob = bewaring langer dan 7 dagen
- Application Logging FileSystem = maximaal 7 dagen

## Container Services Vergelijking
| Service | Gebruik | Scale to zero | Kubernetes API | Scaling trigger |
|---|---|---|---|---|
| ACI (Azure Container Instances) | Korte geïsoleerde taken | Nee | Nee | Handmatig |
| App Service | Docker web apps, autoscaling op HTTP | Nee | Nee | HTTP / CPU / schema |
| ACA (Azure Container Apps) | Serverless microservices, event-driven | Ja | Nee | HTTP / event-driven / CPU |
| AKS (Azure Kubernetes Service) | Complexe orchestratie, volledige controle | Nee | Ja | Kubernetes HPA |

## ACA (Azure Container Apps) Scaling Triggers
- **HTTP** — schaalt op inkomend HTTP verkeer
- **Event-driven** — schaalt op basis van externe events zoals Azure Service Bus queue length
- **CPU/Memory** — schaalt op resource gebruik
- Voor Service Bus: altijd event-driven, niet HTTP

## Sidecar Pattern
- Sidecar container = hulpcontainer naast hoofdcontainer voor doorlopende taken
- Deelt hetzelfde netwerk en volumes als de hoofdcontainer
- Voorbeelden: cache verversen, logs doorsturen, config updates, monitoring
- Init container = eenmalige initialisatie vóór hoofdcontainer start, stopt daarna
- Voor "automatisch cache refreshen" = sidecar

## Persistent Storage in Containers
- ACI persistent storage = Azure File share (niet blob)
- Container op meerdere nodes = Azure Files/SMB

## VM Scale Set Orchestration Modes
| Mode | Gebruik |
|---|---|
| Uniform | Large-scale stateless workloads, alle VMs identiek, snelste uitrol |
| Flexible | Meer controle over individuele VMs, verschillende configuraties mogelijk |
- Sleutelwoord "large-scale stateless" + "as quickly as possible" = Uniform
- Orchestration mode kan niet worden gewijzigd na aanmaken

## Availability Opties VMs (Virtual Machines)
| Optie | Beschermt tegen | SLA |
|---|---|---|
| Enkele VM Premium SSD | — | 99.9% |
| Availability set | Rack failures binnen datacenter | 99.95% |
| Availability zone | Volledige datacenter failure | 99.99% |
| VM Scale Set | Schalen op vraag | — |
| Site Recovery | Regio-brede disaster | — |

## Availability Set — Update vs Fault Domains
- Update domains: beschermen tegen planned maintenance — één update domain tegelijk herstart
- Fault domains: beschermen tegen unplanned hardware failure — rack niveau
- Planned maintenance vereist meerdere update domains
- Datacenter failure vereist availability zones, niet availability sets
- Fault domains = 1 vereist ook update domains = 1 — anders foutmelding van Azure

## Availability Set Defaults
- Update domains: 5 (niet wijzigbaar na aanmaken)
- Fault domains: 2 (niet wijzigbaar na aanmaken)

## VM Scale Set — Configuratie
- Instellen via: Availability options (niet Management) bij aanmaken VM

## VM Tijdelijke Disk
- Windows VMs: tijdelijke disk = drive D
- Linux VMs: tijdelijke disk = /dev/sdb
- Data op tijdelijke disk gaat verloren bij redeploy of host failure
- Data op drive C (Windows) of OS disk blijft behouden na redeploy

## Disk Types — OS Disk Ondersteuning
| Type | OS disk mogelijk |
|---|---|
| Ultra disk | Nee |
| Premium SSD v2 | Nee |
| Premium SSD | Ja |
| Standard SSD | Ja |
| Standard HDD | Ja |

## VM Extensies
| Extensie | Doel |
|---|---|
| Azure Monitor agent | Verzamelt logs en metrics, stuurt naar Log Analytics workspace |
| Custom Script Extension | Voert scripts uit na deployment — software installeren, configuratie |
| DSC extension | Afdwingen van configuratiestatus |
| VMAccess extension | Toegangsherstel — wachtwoord resetten, SSH key vervangen |
| BGInfo extension | Toont systeeminformatie op het bureaublad van Windows VMs |

---

## NETWORKING

## NSG (Network Security Group) Associatie
- Subnets ✓
- Network interfaces (NICs) ✓
- VNets ✗
- VMs ✗ (via NIC, niet direct)
- NSG moet in dezelfde regio zijn als het subnet waaraan het wordt gekoppeld

## NSG Traffic evaluatie
- Inbound: Subnet NSG eerst → NIC NSG
- Outbound: NIC NSG eerst → Subnet NSG
- Beide moeten toestaan anders geblokkeerd

## NSG Default Rules
- Inbound: VNet verkeer toegestaan, internet geblokkeerd tenzij expliciete Allow regel
- Outbound: al het verkeer toegestaan
- Default rules kunnen niet worden verwijderd maar kunnen worden overschreven met hogere prioriteit

## Network Interface (NIC)
- Virtuele netwerkkaart van een VM
- Elke VM heeft minimaal één NIC
- NIC heeft een privé IP adres en een koppeling aan een subnet
- NSG koppel je aan subnet of NIC — niet aan VNet
- VM met twee subnets = twee NICs aanmaken en koppelen
- NIC moet in dezelfde regio en subscription zijn als de VM

## ASG (Application Security Group)
- Groepeert network interfaces van meerdere VMs
- Gebruik als bron of doel in NSG regel
- Alle NICs in de ASG moeten in hetzelfde VNet zitten
- Minimale NSG regels — één regel voor de groep i.p.v. één per VM
- Voor "fewest number of NSG rules" = altijd ASG

## Publiek IP Adres Types
| Type | Gedrag bij VM stop/deallocate |
|---|---|
| Dynamisch publiek IP | Wordt vrijgegeven — nieuw IP bij opnieuw starten |
| Statisch publiek IP | Blijft altijd hetzelfde — ook na stop/deallocate |

## P2S (Point-to-Site) VPN na VNet Peering
- P2S VPN client moet worden herinstalleerd na het configureren van VNet peering
- Routes worden bij installatie gecached — herinstallatie downloadt nieuwe routes
- Elke topologiewijziging vereist herinstallatie van VPN client

## VNet Peering — Disconnected Status
- Disconnected = één van de peering links is verwijderd
- Oplossing: verwijder de disconnected peer en maak opnieuw aan
- Adres space wijzigen of subnet verwijderen lost disconnected status niet op

## DNS (Domain Name System) — Overzicht
| Optie | Gebruik |
|---|---|
| Azure-provided name resolution | Alleen binnen één VNet, geen custom domeinnamen |
| Azure Private DNS zone | Meerdere VNets, custom domeinnamen, minimale beheerinspanning |
| Azure Public DNS zone | Publiek toegankelijke domeinen |
| DNS server op VM | Werkt maar veel beheer — nooit de juiste keuze als Private DNS zone beschikbaar is |
| Azure DNS Private Resolver | Proxy voor queries tussen on-premises en Azure DNS |

## DNS Record Types
| Type | Wat het doet | Gebruik |
|---|---|---|
| A | Domeinnaam → IPv4 adres | Directe IP koppeling |
| AAAA | Domeinnaam → IPv6 adres | IPv6 |
| CNAME | Domeinnaam → andere domeinnaam | Aliassen — blijft geldig als IP wijzigt |
| MX | Mail exchange | Email routing |
| TXT | Tekst informatie | Domeinverificatie, SPF records |
| SOA | Zone informatie | Automatisch aangemaakt |
| SRV | Service locatie — poort en protocol | VoIP, SIP |
| NS | Name server records | Delegatie naar DNS servers |

## Private DNS Zone
- Virtual network link aanmaken met auto-registration enabled voor automatische registratie
- Auto-registration werkt met zowel statische als dynamische IP adressen
- DNS Private Resolver ≠ virtual network link — zijn twee verschillende dingen

## Load Balancer — NAT rule vs Load balancing rule
| | Load balancing rule | Inbound NAT rule |
|---|---|---|
| Doel | Verdelen over alle VMs in pool | Doorsturen naar één specifieke VM |
| Gebruik | HTTP/HTTPS traffic verdeling | RDP/SSH naar specifieke VM |
| Sleutelwoord | "distribute traffic" | "forward to VM1 only" |

## Load Balancer — Backend Pool Vereisten
- VM zonder public IP kan worden toegevoegd aan backend pool
- VM in stopped state kan worden toegevoegd aan backend pool
- Public IP SKU van VM moet overeenkomen met SKU van load balancer
- Basic IP op VM + Standard load balancer = niet compatibel — verwijder IP of upgrade naar Standard
- Geen IP = altijd goed, verkeerd SKU = altijd fout

## Internal vs Public Load Balancer
- Internal (private) load balancer: verdeelt traffic binnen VNet
- Public load balancer: verdeelt internet traffic naar VMs
- Internal load balancer Standard SKU: kan VMs in verschillende subnets van hetzelfde VNet load balancen
- Load balancer kan geen VMs in verschillende VNets load balancen

## Internal Load Balancer — Backend Pool Regels
- VMs moeten in hetzelfde VNet zitten als de load balancer
- Verschillende subnets binnen hetzelfde VNet = toegestaan (Standard SKU)
- Verschillende availability sets = toegestaan (Standard SKU)
- Verschillende VNets = niet toegestaan
- Subnet in load balancer config = frontend subnet, geen beperking op backend VMs

## Application Gateway vs Load Balancer
| | Load Balancer | Application Gateway |
|---|---|---|
| Laag | Layer 4 (TCP/UDP) | Layer 7 (HTTP/HTTPS) |
| SSL termination | Nee | Ja |
| WAF | Nee | Ja (WAF tier) |
| SQL injection bescherming | Nee | Ja (WAF tier) |
| Routing op URL pad | Nee | Ja |

## Internal vs Public Load Balancer — Gebruik
| | Internal Load Balancer | Public Load Balancer |
|---|---|---|
| Traffic | Binnen VNet tussen tiers | Van internet naar VMs |
| Toegankelijk van internet | Nee | Ja |
| Sleutelwoord | "between tiers", "not accessible from internet" | "internet traffic", "public endpoint" |

## Load Balancer — Troubleshooting
| Probleem | Oplossing |
|---|---|
| VMs niet bereikbaar | Check health probe configuratie |
| VMs reageren niet op probe | Zorg dat VMs reageren op de geconfigureerde poort |
| Traffic bereikt VMs niet | Verify NSG rules staan inbound traffic toe |
| SKU mismatch | Load balancer en public IP moeten zelfde SKU hebben |
| Ongelijke traffic verdeling | Change distribution mode naar five-tuple hash |
| Users verliezen sessiedata | Stel session persistence in op Client IP + Protocol |

## Load Balancer — Session Persistence vs Connectivity
- Session persistence oplossing: alleen als users naar verschillende servers worden gerouteerd
- Connectivity issues oplossing: health probe, NSG rules, VM poort response
- Session persistence verandert routing maar lost geen bereikbaarheidsproblemen op

## Network Watcher — Diagnostische Tools
| Tool | Gebruik |
|---|---|
| Packet capture | Legt alle netwerk packets vast — inhoudelijk inspecteren, max 5 uur |
| Next hop | Identificeert de volgende routing hop voor één specifiek pakket |
| Effective routes | Toont alle actieve routes op een NIC — gebruik voor peering verificatie |
| Connection troubleshoot | Valideert bereikbaarheid — toont geen routing beslissingen |
| Connection monitor | Monitort bereikbaarheid en latency (RTT) continu over tijd |
| IP flow verify | Controleert of een pakket wordt toegestaan of geblokkeerd door NSG |

## Network Watcher — Algemeen
- Één instantie per regio (niet per VNet)
- Voor netwerk health monitoring: Network Watcher (niet Azure Monitor)
- Packet capture vereist: AzureNetworkWatcherExtension installeren op VM

## Network Watcher — IP Flow Verify vs Flow Logs
| Tool | Gebruik | Administratieve inspanning |
|---|---|---|
| IP flow verify | Directe NSG check — geeft direct antwoord welke NSG blokkeert | Minimaal |
| NSG/VNet flow logs | Logt al het IP verkeer — vereist handmatige analyse achteraf | Hoog |

## Azure Monitor Network Insights vs Network Watcher
| | Network Insights | Network Watcher |
|---|---|---|
| Gebruik | Gecentraliseerd overzicht alle netwerkresources | Diagnostiek van individuele resources |
| Configuratie | Geen | Extensie soms vereist |
| Schaal | Subscription-breed | Per resource |
| Sleutelwoord | "centralized console", "hundreds of resources" | "troubleshoot", "diagnose", "packet capture" |

## Netwerk Diagnostiek Commands
| Command | Gebruik |
|---|---|
| `netstat -an` | Toont alle luisterende poorten en actieve verbindingen |
| `Test-NetConnection` | PowerShell — test TCP verbinding of ping naar host |
| `ping` | ICMP test — controleert bereikbaarheid |
| `tracert` / `traceroute` | Toont routing pad naar doel |
| `nslookup` | DNS lookup — naam naar IP resolutie |
| `nbtstat -c` | NetBIOS name cache — legacy Windows naming |
| `ipconfig` | IP configuratie van network interfaces |

## Azure Bastion
- Verbindt via privé IP — geen publiek IP vereist op de VM
- Werkt binnen hetzelfde VNet of via VNet peering
- Zonder peering = geen verbinding naar andere VNets
- Jij → internet → Portal → Bastion → privé IP → VM
- Sleutelwoord "connect without exposing RDP/SSH" = Azure Bastion

## SSL (Secure Sockets Layer) Certificaat bij Resource Group Verplaatsing
- SSL certificaat kan niet direct worden verplaatst
- Verwijder uit bron RG → verplaats alle andere resources → upload opnieuw in doel RG

---

## MONITOR & BACKUP

## Azure Backup Vault vs Recovery Services Vault
| | Azure Backup Vault | Recovery Services Vault |
|---|---|---|
| Nieuwer/ouder | Nieuwer | Ouder |
| Azure Blobs | ✓ | ✗ |
| Azure Disks | ✓ | ✗ |
| PostgreSQL | ✓ | ✗ |
| Azure VMs | ✗ | ✓ |
| Azure Files | ✗ | ✓ |
| SQL in Azure VM | ✗ | ✓ |
| Site Recovery | ✗ | ✓ |
| On-premises (MARS/MABS) | ✗ | ✓ |
| Container Instances | ✗ | ✗ |
| App Service | ✗ | ✗ — eigen ingebouwde backup |

## Recovery Services Vault — Regio Vereiste
- Vault en VM moeten in dezelfde regio zijn
- Resource group locatie is irrelevant — alleen resource locatie telt
- Verschillende resource groups of OS types zijn toegestaan als regio overeenkomt

## Azure Backup — Eerste Inrichting Volgorde
1. Recovery Services vault aanmaken
2. Backup policy aanmaken
3. Resources koppelen aan policy en beschermen
- Vault moet eerst bestaan voordat policy kan worden aangemaakt

## Azure Backup
- Default VM backup retention: 30 dagen
- Soft delete retention: 14 dagen
- Instant Restore snapshots: instelbaar (standaard 5 dagen)
- Backup werkt ook als VM gestopt/deallocated is — snapshots van disks
- Auto-shutdown heeft geen invloed op backup schedule

## Azure Backup — MARS Agent Registratie Volgorde
1. Recovery Services vault aanmaken
2. MARS agent installeren op on-premises server
3. **Vault credentials downloaden en server registreren** ← eerst dit
4. Backup policy configureren
5. Backup starten

## Azure Backup Agents — Vergelijking
| Agent/Tool | Gebruik |
|---|---|
| MARS agent | Files, folders en system state op individuele Windows server |
| MABS | Centrale backup van workloads — SQL, SharePoint, Hyper-V, meerdere machines |
| Site Recovery Provider | Disaster recovery / replicatie via Azure Site Recovery |
| Azure Connected Machine agent | Azure Arc — on-premises servers via Azure beheren |

## Recovery Services Vault Verwijderen — Vereiste Stappen
1. Stop backup van alle protected items
2. Disable soft delete feature
3. Permanently remove all items in soft delete state
4. Dan pas vault verwijderen
- VM verwijderen is niet vereist
- Read lock op vault blokkeert verwijdering — niet instellen

## Azure Site Recovery — Failover Statussen
| Stap | Status |
|---|---|
| 1 | Starting failover |
| 2 | Committing failover |
| 3 | **Failover committed** ← vereist vóór reprotection |
| 4 | Reprotect — replicatie omdraaien naar primaire regio |

## Azure Site Recovery — Volledige Lifecycle
**Setup fase (eenmalig):**
1. Initiate replication — replicatie instellen van primary naar secondary

**Disaster Recovery drill (periodiek):**
2. Run test failover — testen of failover werkt zonder productie te beïnvloeden
3. Clean up test failover — testomgeving opruimen

**Echte failover (bij uitval):**
4. Verify VM health — controleer of VMs healthy en protected zijn
5. Run failover — VMs aanmaken in secondary region
6. Reprotect — replicatierichting omdraaien (secondary → primary)

**Herstel primary region:**
7. Run failback — terugschakelen naar primary region
8. Reprotect again — replicatierichting weer omdraaien (primary → secondary)

## Azure Monitor — Alert States
- New, Acknowledged, Closed
- Altijd handmatig ingesteld — nooit automatisch gewijzigd door het systeem
- Action groups kunnen acties uitvoeren maar wijzigen de alert state niet

## Azure Monitor — Alert Rules vs Action Groups
| | Alert rule | Alert processing rule | Action group |
|---|---|---|---|
| Doel | Detecteert event en triggert | Verwerkt/suppressed bestaande alerts | Definieert wie/wat wordt genotificeerd |
| Notificatie | Via gekoppelde action group | Nee | Ja — email, SMS, runbook |
| Aantal | Één per signal | Optioneel | Één per unieke set ontvangers |

## Azure Monitor — Alert Rules en Action Groups Tellen
- Alert rules: één per signal/conditie
- Action groups: één per unieke set ontvangers
- Meerdere alert rules kunnen dezelfde action group delen

## Azure Monitor — Limieten
- Shared dashboard: maximaal 30 dagen data

## KQL (Kusto Query Language) Operators
| Operator | Wat het doet | Voorbeeld |
|---|---|---|
| `where` | Filtert rijen op conditie | `where Computer == "VM1"` |
| `summarize` | Groepeert en aggregeert — gebruik voor "aggregate by column" | `summarize count() by Account` |
| `project` | Selecteert en hernoemt kolommen | `project Account, TimeGenerated` |
| `extend` | Voegt berekende kolommen toe | `extend Duration = EndTime - StartTime` |
| `order by` | Sorteert resultaten | `order by TimeGenerated desc` |
| `take` | Neemt N rijen | `take 10` |
| `distinct` | Unieke waarden | `distinct Account` |
| `search in (TableName) "value"` | Zoekt specifieke waarde in specifieke tabel | `search in (EventLogs) "error"` |

## Azure Advisor Categorieën
| Categorie | Gebruik |
|---|---|
| Cost | Underutilized VMs, kostenbesparing, unattached disks |
| Performance | Applicaties sneller maken |
| Reliability | High availability verbeteren |
| Security | Beveiligingsproblemen |
| Operational Excellence | Processen en workflows |

## Azure Advisor — Unattached Disks
- Azure Advisor Cost = identificeert unattached disks en geeft aanbevelingen
- Voor het examen: Advisor voor unattached disks, niet Azure Monitor of Billing Administrator

---

## SLEUTELWOORDEN IN EXAMENVRAGEN
| Sleutelwoord in de vraag | Antwoord |
|---|---|
| Minimizes administrative effort | App Service, ACA — nooit AKS of VMs |
| Minimizes cost | Goedkoopste tier die voldoet — niet overdimensioneren |
| Least privilege | Meest specifieke rol op laagste scope — nooit Owner of Global Admin |
| Without requiring a failover | RA-GRS of RA-GZRS |
| Automatically | Dynamic groups, lifecycle management, Modify policy, autoscale |
| Prevent accidental deletion | Delete lock |
| Encrypted connection to on-premises | VPN gateway |
| Scale to zero | ACA |
| Short-lived isolated task | ACI |
| Custom domain + autoscale + Docker | App Service |
| Even traffic distribution / connection timeouts | Five-tuple hash |
| Same server every request / session data loss | Session persistence Client IP + Protocol |
| POSIX ACLs / Data Lake | Hierarchical namespace |
| Network health monitoring | Network Watcher |
| Underutilized VMs / unattached disks | Azure Advisor Cost |
| Temporary external access to storage | SAS token |
| Datacenter failure protection / 99.99% SLA | Availability zone |
| Rack failure protection / 99.95% SLA | Availability set |
| Service Bus queue scaling | Event-driven trigger in ACA |
| Scale automatically on CPU/metric | Scale up naar Standard/Premium eerst, dan autoscale instellen |
| Deploy Docker container in App Service | Publish → Docker Container |
| Identity-based access for file share | Configure identity-based access in File share settings |
| Name resolution across multiple VNets | Azure Private DNS zone |
| Performance root cause analysis | Azure Monitor metrics |
| Aggregate query results by column | KQL summarize operator |
| Search specific value in specific table | KQL search in (TableName) "value" |
| Verify peering routing path | Effective routes op network interface |
| Monitor RTT latency between VMs | Connection monitor in Network Watcher |
| Centralized console network monitoring | Azure Monitor Network Insights |
| Intermittent connectivity load balancer | Health probe + SKU matching |
| RDP to specific VM via load balancer | Inbound NAT rule |
| Register on-premises server with vault | Download vault credentials and register server first |
| Refresh cache in container app | Sidecar container |
| Pass array inline in ARM deployment | --parameters switch in deployment command |
| Check listening ports on server | netstat -an |
| Fewest NSG rules for subset of VMs | ASG |
| Back up files/folders on single server | MARS agent |
| Central backup of workloads/multiple machines | MABS |
| Store password securely in ARM template | Azure Key Vault + access policy |
| Large-scale stateless workloads VM scale set | Uniform orchestration mode |
| Enable Traffic Analytics | Owner, Contributor of Network Contributor rol |
| Verify custom domain in Entra ID | TXT of MX record bij domeinprovider toevoegen |
| SQL injection bescherming voor web app | Application Gateway WAF tier |
| SSL termination at load balancer | Application Gateway |
| Mount file share from Azure and on-premises | Azure Files |
| Auto-delete group after X days | Microsoft 365 group met expiration policy |
| Modify Department attribute synced user | Moet in on-premises AD — niet in Entra ID |
| Traffic between internal tiers verdelen | Internal Load Balancer |
| Premium P1 features toewijzen | Licenses blade in Entra ID — niet rol toewijzen |
| Connect to VM without exposing RDP/SSH | Azure Bastion |
| Backup VM regardless of running state | Azure Backup — werkt altijd, ook bij stopped VM |
