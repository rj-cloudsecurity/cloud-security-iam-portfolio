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
| 587 | SMTP relay — outbound email via authenticated SMTP |
| 25 | SMTP — mail traffic (niet authenticated) |

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

## Application Security Groups (ASG)
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

## RBAC Roll
