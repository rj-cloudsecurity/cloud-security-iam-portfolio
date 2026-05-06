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

## NSG Associatie
- Subnets ✓
- Network interfaces (NICs) ✓
- VNets ✗
- VMs ✗ (via NIC, niet direct)

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

## ARM Template Deployment Scopes
| Scope | Gebruik |
|---|---|
| Resource group | Één resource group |
| Subscription | Meerdere resource groups, nieuwe RGs aanmaken |
| Management group | Meerdere subscriptions |
| Tenant | Alles |

## App Service Tiers — Key Features
| Tier | Custom domain | Deployment slots | Autoscale |
|---|---|---|---|
| Free F1 | Nee | Nee | Nee |
| Basic B1 | Ja | Nee | Handmatig |
| Standard S1 | Ja | 5 | Ja |
| Premium P1V3 | Ja | 20 | Ja + Elastic |

## Container Services Vergelijking
| Service | Gebruik | Scale to zero | Kubernetes API |
|---|---|---|---|
| ACI | Korte geïsoleerde taken | Nee | Nee |
| App Service | Docker web apps, autoscaling op HTTP | Nee | Nee |
| ACA | Serverless microservices, event-driven | Ja | Nee |
| AKS | Complexe orchestratie, volledige controle | Nee | Ja |

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

## Azure Monitor — Limieten
- Shared dashboard: maximaal 30 dagen data

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

## Private DNS Zone
- Virtual network link aanmaken met auto-registration enabled
- Auto-registration werkt met zowel statische als dynamische IP adressen

## Network Watcher
- Één instantie per regio (niet per VNet)
- Voor netwerk health monitoring: Network Watcher (niet Azure Monitor)
- Packet capture vereist: AzureNetworkWatcherExtension installeren op VM

## SAS Token vs Access Key
| | SAS Token | Access Key |
|---|---|---|
| Scope | Specifieke resource of container | Heel storage account |
| Expiry | Instelbaar | Geen expiry |
| Gebruik | Tijdelijke externe toegang | Volledige interne toegang |

## SSPR
- Guests: niet ondersteund in resource tenant
- Synced users: ondersteund met password writeback via Entra Connect
- Cloud-only users: altijd ondersteund
- Minimum licentie: Entra ID P1

## Lifecycle Management
- Werkt alleen op block blobs (niet page blobs, niet append blobs)
- Access tracking inschakelen vereist voor regels op basis van laatste toegang
- Tiers: Hot → Cool → Cold → Archive (alleen in deze richting automatisch)

## ARM Deployment Scope
Onthoud de hiërarchie — deploy altijd één niveau boven wat je wilt aanmaken of aanspreken:
Tenant → Management Group → Subscription → Resource Group → Resource

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
| Even traffic distribution | Five-tuple hash |
| Same server every request | Session persistence |
| POSIX ACLs / Data Lake | Hierarchical namespace |
| Network health monitoring | Network Watcher |
| Underutilized VMs | Azure Advisor Cost |
| Temporary external access to storage | SAS token |
| Datacenter failure protection | Availability zone |
| Rack failure protection | Availability set |

