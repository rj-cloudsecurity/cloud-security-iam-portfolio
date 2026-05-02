# Exercise 21: Create Alias Records for Azure DNS

- **Learning Path 5:** Configure and manage virtual networks for Azure administrators
- **Module 3:** Host your domain on Azure DNS

---

## Setup via script

Script gecloned van GitHub en uitgevoerd in Azure Cloud Shell:

```bash
git clone https://github.com/MicrosoftDocs/mslearn-host-domain-azure-dns.git
cd mslearn-host-domain-azure-dns
chmod +x setup.sh
./setup.sh
```

### Aangemaakt door setup script

| Resource | Naam | Details |
|---|---|---|
| VNet | bePortalVnet | 10.0.0.0/16 |
| Subnet | bePortalSubnet | 10.0.0.0/24 |
| NSG | bePortalNSG | Inbound port 80 allow (priority 101) |
| NIC 1 | webNic1 | 10.0.0.4 |
| NIC 2 | webNic2 | 10.0.0.5 |
| VM 1 | webVM1 | Gekoppeld aan webNic1 |
| VM 2 | webVM2 | Gekoppeld aan webNic2 |
| Public IP | myPublicIP | Gekoppeld aan load balancer |
| Load balancer | myLoadBalancer | Distribueert traffic over webVM1 en webVM2 |

---

## Alias record configuratie

DNS zone gebruikt uit exercise 20: `wideworldimportsabcd.com`

| Setting | Value |
|---|---|
| Name | *(leeg — zone apex)* |
| Type | A |
| Alias record set | Yes |
| Alias type | Azure resource |
| Azure resource | myPublicIP |

> Name leeg laten = record geldt voor de zone apex (`wideworldimportsabcd.com` zelf, ook wel `@`).

---

## Verificatie

Public IP van load balancer geopend in browser → webpagina toont naam van de VM waarnaar de load balancer de request heeft gestuurd (webVM1 of webVM2).

---

## Key takeaways

- CNAME records worden niet ondersteund op zone apex niveau — alias records wel
- Alias record koppelt zone apex aan Azure resource (Public IP, Traffic Manager, CDN, Front Door)
- Bij IP-wijziging van de onderliggende resource wordt het alias record automatisch bijgewerkt — geen dangling DNS records
- Load balancing op zone apex niveau is alleen mogelijk via alias records
