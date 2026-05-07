# AZ-104 Quick Reference — Key Facts

## Poorten
| Poort | Protocol/Gebruik |
|---|---|
| 80 | HTTP |
| 443 | HTTPS |
| 445 | SMB — Azure Files |
| 3389 | RDP — Remote Desktop |
| 22 | SSH |
| 5671 | AMQP — Azure Service Bus / health data |

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
| LRS | 3 kopieën in 1 datacenter | Nee | Nee | Nee |
| ZRS | 3 kopieën over 3 zones | Ja | Nee | Nee |
| GRS | LRS + secundaire regio | Nee | Ja | Nee |
| RA-GRS | GRS + leestoegang | Nee | Ja | Ja |
| GZRS | ZRS + secundaire regio | Ja | Ja | Nee |
| RA-GZRS | GZRS + leestoegang | Ja | Ja | Ja |

## Storage Account Types — Data Lake Gen2
| Type | Ondersteunt Data Lake Gen2 |
|---|---|
| Standard general-purpose v2 | Ja — enable hierarchical namespace |
| Premium block blobs | Ja — enable hierarchical namespace |
| Premium file shares | Nee — alleen Azure Files |
| Premium page blobs | Nee — alleen page blobs voor VM disks |

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
| Intrekken | Key regenereren | Role assignment verwijderen | Token laten verlopen of stored access policy intrekken | Policy wijzigen |
| Gebruik | Legacy apps zonder Entra ID | Gebruikers en moderne apps via Entra ID | Tijdelijke externe toegang | Toegangscontrole op basis van signalen |
| Least privilege | Nee | Ja | Ja | Niet van toepassing op storage data |

## NSG Associatie
- Subnets ✓
- Network interfaces (NICs) ✓
- VNets ✗
- VMs ✗ (via NIC, niet direct)
- NSG moet in dezelfde regio zijn als het subnet waaraan het wordt gekoppeld

## Network Interface (NIC)
- Virtuele netwerkkaart van een VM
- Elke VM heeft minimaal één NIC
- NIC heeft een privé IP adres en een koppeling aan een subnet
- NSG koppel je aan subnet of NIC — niet aan VNet
- VM met twee subnets = twee NICs aanmaken en koppelen

## NSG Traffic evaluatie
- Inbound: Subnet NSG eerst → NIC NSG
- Outbound: NIC NSG eerst → Subnet NSG
- Beide moeten toestaan anders geblokkeerd

## RBAC Rollen
| Rol | Resources beheren | Rollen toewijzen |
|---|---|---|
| Owner | Ja | Ja |
| Contributor | Ja | Nee |
| Reader | Nee (alleen lezen) | Nee |
| User Access Administrator | Nee | Ja |
| Cost Management Contributor | Nee | Nee — alleen kosten bekijken en budgets beheren |
| Storage Account Contributor | Ja — storage accounts + access keys | Nee |

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

## ARM Template Deployment Scopes
| Scope | Gebruik |
|---|---|
| Resource group | Één resource group |
| Subscription | Meerdere resource groups, nieuwe RGs aanmaken |
| Management group | Meerdere subscriptions |
| Tenant | Alles |

## ARM Deployment Scope — Ezelsbruggetje
Onthoud de hiërarchie — deploy altijd één niveau boven wat je wilt aanmaken of aanspreken:
Tenant → Management Group → Subscription → Resource Group → Resource

## ARM Template — Inline Parameters
- Inline = direct in het deployment commando via `--parameters`
- Voor een array: `--parameters arrayParam='["value1","value2"]'`
- Parameters file = apart JSON bestand, niet inline
- Template aanpassen = nooit doen voor variabele waarden

## App Service Tiers — Volledig Overzicht
| Tier | Max instances | Storage | Custom domain | Slots | Autoscale |
|---|---|---|---|---|---|
| Free F1 | 1 | 1 GB | Nee | Nee | Nee |
| Basic B1 | 3 | 10 GB | Ja | Nee | Handmatig |
| Standard S1 | 10 | 50 GB | Ja | 5 | Ja |
| Premium P1V3 | 30 | 250 GB | Ja | 20 | Ja + Elastic |
| Isolated I1V2 | 100 | 1 TB | Ja | 20 | Ja |

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
| ACI | Korte geïsoleerde taken | Nee | Nee | Handmatig |
| App Service | Docker web apps, autoscaling op HTTP | Nee | Nee | HTTP / CPU / schema |
| ACA | Serverless microservices, event-driven | Ja | Nee | HTTP / event-driven / CPU |
| AKS | Complexe orchestratie, volledige controle | Nee | Ja | Kubernetes HPA |

## ACA Scaling Triggers
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

## Availability Opties VMs
| Optie | Beschermt tegen |
|---|---|
| Availability set | Rack failures binnen datacenter |
| Availability zone | Volledige datacenter failure |
| VM Scale Set | Schalen op vraag |
| Site Recovery | Regio-brede disaster |

## VM Scale Set — Configuratie
- Instellen via: Availability options (niet Management) bij aanmaken VM
- Orchestration modes: Uniform (zelfde image) of Flexible (aanbevolen, verschillende images)

## Availability Set Defaults
- Update domains: 5 (niet wijzigbaar na aanmaken)
- Fault domains: 2 (niet wijzigbaar na aanmaken)

## Disk Types — OS Disk Ondersteuning
| Type | OS disk mogelijk |
|---|---|
| Ultra disk | Nee |
| Premium SSD v2 | Nee |
| Premium SSD | Ja |
| Standard SSD | Ja |
| Standard HDD | Ja |

## Azure Backup
- Default VM backup retention: 30 dagen
- Soft delete retention: 14 dagen
- Instant Restore snapshots: instelbaar (standaard 5 dagen)

## Azure Backup — MARS Agent Registratie Volgorde
1. Recovery Services vault aanmaken
2. MARS agent installeren op on-premises server
3. **Vault credentials downloaden en server registreren** ← eerst dit
4. Backup policy configureren
5. Backup starten

## Azure Site Recovery — Failover Statussen
| Stap | Status |
|---|---|
| 1 | Starting failover |
| 2 | Committing failover |
| 3 | **Failover committed** ← vereist vóór reprotection |
| 4 | Reprotect — replicatie omdraaien naar primaire regio |

## Azure Monitor — Limieten
- Shared dashboard: maximaal 30 dagen data

## Azure Monitor — Alert States
- New, Acknowledged, Closed
- Altijd handmatig ingesteld — nooit automatisch gewijzigd door het systeem
- Action groups kunnen acties uitvoeren maar wijzigen de alert state niet

## Azure Monitor — Action Group vs Alert Processing Rule
- **Action group** = definitie van wie/wat wordt genotificeerd (email, SMS, runbook)
- **Alert processing rule** = optionele modifier op bestaande alerts
- Voor backup failure notificatie: eerst action group aanmaken, dan koppelen aan alert

## KQL Operators
| Operator | Wat het doet | Voorbeeld |
|---|---|---|
| `where` | Filtert rijen op conditie | `where Computer == "VM1"` |
| `summarize` | Groepeert en aggregeert — gebruik voor "aggregate by column" | `summarize count() by Account` |
| `project` | Selecteert en hernoemt kolommen | `project Account, TimeGenerated` |
| `extend` | Voegt berekende kolommen toe | `extend Duration = EndTime - StartTime` |
| `order by` | Sorteert resultaten | `order by TimeGenerated desc` |
| `take` | Neemt N rijen | `take 10` |
| `distinct` | Unieke waarden | `distinct Account` |

## VM Extensies
| Extensie | Doel |
|---|---|
| Azure Monitor agent | Verzamelt logs en metrics, stuurt naar Log Analytics workspace |
| Custom Script Extension | Voert scripts uit na deployment — software installeren, configuratie |
| DSC extension | Desired State Configuration — afdwingen van configuratiestatus |
| VMAccess extension | Toegangsherstel — wachtwoord resetten, SSH key vervangen |
| BGInfo extension | Toont systeeminformatie op het bureaublad van Windows VMs |

## Azure Advisor Categorieën
| Categorie | Gebruik |
|---|---|
| Cost | Underutilized VMs, kostenbesparing |
| Performance | Applicaties sneller maken |
| Reliability | High availability verbeteren |
| Security | Beveiligingsproblemen |
| Operational Excellence | Processen en workflows |

## Delete Locks — Wel/Niet
| Resource | Delete lock mogelijk |
|---|---|
| Subscriptions | Ja |
| Resource groups | Ja |
| Individuele resources (VMs, storage accounts) | Ja |
| Management groups | Nee |
| Storage account data (blobs, files) | Nee — gebruik immutability policy |

## SSL Certificaat bij Resource Group Verplaatsing
- SSL certificaat kan niet direct worden verplaatst
- Verwijder uit bron RG → verplaats alle andere resources → upload opnieuw in doel RG

## P2S VPN na VNet Peering
- P2S VPN client moet worden herinstalleerd na het configureren van VNet peering
- Routes worden bij installatie gecached — herinstallatie downloadt nieuwe routes

## DNS — Overzicht
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
| SOA | Start of Authority — zone informatie | Automatisch aangemaakt |
| SRV | Service locatie — poort en protocol | VoIP, SIP |
| NS | Name server records | Delegatie naar DNS servers |

## Private DNS Zone
- Virtual network link aanmaken met auto-registration enabled voor automatische registratie
- Auto-registration werkt met zowel statische als dynamische IP adressen
- DNS Private Resolver ≠ virtual network link — zijn twee verschillende dingen

## Network Watcher — Diagnostische Tools
| Tool | Gebruik |
|---|---|
| Packet capture | Legt alle netwerk packets vast — inhoudelijk inspecteren |
| Next hop | Identificeert de volgende routing hop voor één specifiek pakket |
| Effective routes | Toont alle actieve routes op een NIC — gebruik voor peering verificatie |
| Connection troubleshoot | Valideert bereikbaarheid — toont geen routing beslissingen |
| IP flow verify | Controleert of een pakket wordt toegestaan of geblokkeerd door NSG |

## Network Watcher — Algemeen
- Één instantie per regio (niet per VNet)
- Voor netwerk health monitoring: Network Watcher (niet Azure Monitor)
- Packet capture vereist: AzureNetworkWatcherExtension installeren op VM
- Network In/Out metrics tonen volume maar niet inhoud van verkeer

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

## Lifecycle Management
- Werkt alleen op block blobs (niet page blobs, niet append blobs)
- Access tracking inschakelen vereist voor regels op basis van laatste toegang
- Tiers: Hot → Cool → Cold → Archive (alleen in deze richting automatisch)

## AzCopy
- `azcopy copy` — eenmalige kopie van bron naar doel
- `azcopy sync` — synchroniseert inclusief verwijderingen — gevaarlijk voor migratie
- Ondersteunt resumable transfers
- Ondersteunt blob en file storage

## Sleutelwoorden in examenvragen
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
| Underutilized VMs | Azure Advisor Cost |
| Temporary external access to storage | SAS token |
| Datacenter failure protection | Availability zone |
| Rack failure protection | Availability set |
| Service Bus queue scaling | Event-driven trigger in ACA |
| Scale automatically on CPU/metric | Scale up naar Standard/Premium eerst, dan autoscale instellen |
| Deploy Docker container in App Service | Publish → Docker Container |
| Identity-based access for file share | Configure identity-based access in File share settings |
| Name resolution across multiple VNets | Azure Private DNS zone |
| Performance root cause analysis | Azure Monitor metrics |
| Aggregate query results by column | KQL summarize operator |
| Verify peering routing path | Effective routes op network interface |
| Intermittent connectivity load balancer | Health probe + NSG rules + VM port response |
| Register on-premises server with vault | Download vault credentials and register server first |
| Refresh cache in container app | Sidecar container |
| Pass array inline in ARM deployment | --parameters switch in deployment command |
