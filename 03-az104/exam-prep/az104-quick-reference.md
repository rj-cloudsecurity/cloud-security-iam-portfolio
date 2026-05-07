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

## App Service Tiers — Key Features
| Tier | Custom domain | Deployment slots | Autoscale |
|---|---|---|---|
| Free F1 | Nee | Nee | Nee |
| Basic B1 | Ja | Nee | Handmatig (scale up/down only) |
| Standard S1 | Ja | 5 | Ja |
| Premium P1V3 | Ja | 20 | Ja + Elastic + Automatic scaling |

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

## Sidecar Pattern
- Sidecar container = hulpcontainer naast hoofdcontainer voor doorlopende taken
- Init container = eenmalige initialisatie vóór hoofdcontainer start

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
| Azure Private DNS zone
