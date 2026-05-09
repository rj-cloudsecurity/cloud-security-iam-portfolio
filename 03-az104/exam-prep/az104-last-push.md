# AZ-104 last push

## Backup — Vault Keuze
- Azure Blobs/Disks/PostgreSQL → **Backup Vault**
- VMs/Files/SQL in VM/Site Recovery → **Recovery Services Vault**
- Vault eerst, dan policy, dan koppelen

## Backup — VM Status
- Backup werkt altijd — ook bij stopped/deallocated VM
- Vault en VM moeten in **dezelfde regio** zijn

## Site Recovery — Echte Failover
**Verify → Failover → Reprotect**
- Test failover = alleen drills
- Failback = pas na herstel primary

## Load Balancer
- RDP naar één specifieke VM → **Inbound NAT rule**
- Traffic verdelen over alle VMs → **Load balancing rule**
- VM zonder public IP → mag in backend pool ✓
- VM stopped → mag in backend pool ✓
- Basic IP + Standard LB → **niet compatibel** ✗
- Traffic tussen interne tiers → **Internal Load Balancer**
- SQL injection bescherming → **Application Gateway WAF**

## NSG Default Rules
- Inbound internet → **geblokkeerd** tenzij expliciete Allow
- Inbound VNet → toegestaan
- Geen expliciete Allow voor RDP = niet bereikbaar van internet

## Availability
- Datacenter uitval → **Availability Zone** (99.99%)
- Rack failure / planned maintenance → **Availability Set** (99.95%)
- Één zone = één fysieke locatie — niet meerdere datacenters

## App Service
- ASP.NET = Windows only, PHP/Python = Linux only
- Deployment slots vereist **Standard of hoger**
- Swap staging ↔ production = snelste manier om te reverten

## Identity
- Rol toewijzen ≠ licentie toewijzen
- "Premium P1 features" → **Licenses blade**, niet Directory roles
- Admin group ≠ Application Administrator rol — expliciet toewijzen
- Department aanpassen van gesynchroniseerde user → **on-premises AD**
- UsageLocation → altijd aanpasbaar in Entra ID

## Netwerk Tools
| Vraag | Tool |
|---|---|
| Blokkeert NSG dit pakket? | IP flow verify |
| Wat is de volgende hop? | Next hop |
| Waarom werkt peering niet? | Effective routes |
| Opnemen van packets over tijd | Packet capture |
| RTT latency monitoren | Connection monitor |
| Overzicht alle netwerkresources | Network Insights |

## Sleutelwoorden
| Woord | Antwoord |
|---|---|
| Least privilege | Meest specifieke rol op laagste scope |
| Minimize administrative effort | App Service of ACA |
| Scale to zero | ACA |
| Short-lived isolated task | ACI |
| Centralized console network | Network Insights |
| Fewest NSG rules | ASG |
| Without requiring failover | RA-GRS of RA-GZRS |
| SQL injection | Application Gateway WAF |
| SSL termination | Application Gateway |
| Mount from Azure + on-premises | Azure Files |
