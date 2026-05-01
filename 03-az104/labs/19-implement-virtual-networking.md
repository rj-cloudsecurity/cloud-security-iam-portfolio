# Exercise 19: Implement Virtual Networking

- **Learning Path 5:** Configure and manage virtual networks for Azure administrators
- **Module 2:** Configure network security groups

---

## Aangemaakt resources

### Task 1 — VNet via portal

| Property | Value |
|---|---|
| Resource group | ex19rg |
| VNet naam | CoreServicesVnet |
| Region | West Europe |
| Address space | 10.20.0.0/16 |
| Subnet | SharedServicesSubnet — 10.20.10.0/24 |
| Subnet | DatabaseSubnet — 10.20.20.0/24 |

### Task 2 — VNet via template

Template geëxporteerd van CoreServicesVnet en aangepast:

| Property | Value |
|---|---|
| VNet naam | ManufacturingVnet |
| Address space | 10.30.0.0/16 |
| Subnet | SensorSubnet1 — 10.30.20.0/24 |
| Subnet | SensorSubnet2 — 10.30.21.0/24 |

---

## Task 3 — ASG + NSG

### Application Security Group

| Property | Value |
|---|---|
| Naam | asg-web |
| Resource group | ex19rg |
| Region | West Europe |

### Network Security Group

| Property | Value |
|---|---|
| Naam | myNSGSecure |
| Resource group | ex19rg |
| Gekoppeld aan subnet | SensorSubnet1 (ManufacturingVnet) |

> **Let op:** Lab-script verwijst naar SharedServicesSubnet — dit is een inconsistentie in het Microsoft-materiaal. SensorSubnet1 is het correcte equivalent na de template-aanpassing in Task 2.

### Inbound rule

| Setting | Value |
|---|---|
| Source | Application security group |
| Source ASG | asg-web |
| Destination port ranges | 80, 443 |
| Protocol | TCP |
| Action | Allow |
| Priority | 100 |
| Naam | AllowASG |

### Outbound rule

| Setting | Value |
|---|---|
| Source | Any |
| Destination | Service tag — Internet |
| Destination port ranges | * |
| Protocol | Any |
| Action | Deny |
| Priority | 4096 |
| Naam | DenyInternetOutbound |

---

## Task 4 — DNS

### Public DNS zone

| Property | Value |
|---|---|
| Naam | contosoex19.com |
| Resource group | ex19rg |
| A-record | www → 10.1.1.4 |

**nslookup test:**
```
$ nslookup www.contosoex19.com
Server:         168.63.129.16
Address:        168.63.129.16#53
** server can't find www.contosoex19.com: NXDOMAIN
```

> NXDOMAIN is verwacht — de naam server in het nslookup-commando moet de Azure DNS name server zijn die aan de zone is toegewezen, niet de default resolver.

### Private DNS zone

| Property | Value |
|---|---|
| Naam | private.contosoex19.com |
| Gelinkt aan | ManufacturingVnet |
| Link naam | manufacturing-link |
| A-record | sensorvm → 10.1.1.4 |

---

## Key takeaways

- Een virtual network is een representatie van je eigen netwerk in de cloud.
- Overlappende IP-ranges vermijden — vereenvoudigt troubleshooting.
- Een subnet is een range van IP-adressen binnen een VNet; je kunt een VNet opdelen in meerdere subnets voor organisatie en security.
- Een NSG bevat security rules die network traffic toestaan of weigeren. Er zijn default inbound/outbound rules die je kunt aanpassen.
- Application security groups worden gebruikt om servers met een gemeenschappelijke functie te groeperen, zoals web servers of database servers.
- Azure DNS is een hosting service voor DNS-domeinen. Public DNS zones voor externe naamresolutie; private DNS zones voor naamresolutie binnen VNets.
