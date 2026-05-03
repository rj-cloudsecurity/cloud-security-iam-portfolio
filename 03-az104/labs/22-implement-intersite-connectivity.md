# Exercise 22: Implement Intersite Connectivity

- **Learning Path 5:** Configure and manage virtual networks for Azure administrators
- **Module 4:** Configure Azure Virtual Network peering

---

## Lab scenario

De organisatie segmenteert core IT-services van de manufacturing afdeling. In dit lab wordt connectiviteit geconfigureerd tussen de twee gesegmenteerde gebieden via VNet peering en een custom route.

---

## Aangemaakt resources

| Resource | Naam | Details |
|---|---|---|
| Resource group | ex22rg | West Europe |
| VM 1 | CoreServicesVM | VNet: CoreServicesVnet |
| VM 2 | ManufacturingVM | VNet: ManufacturingVnet |

### CoreServicesVnet

| Property | Value |
|---|---|
| Address range | 10.0.0.0/16 |
| Subnet naam | Core |
| Subnet range | 10.0.0.0/24 |
| Private IP CoreServicesVM | 10.0.0.4 |

### ManufacturingVnet

| Property | Value |
|---|---|
| Address range | 172.16.0.0/16 |
| Subnet naam | Manufacturing |
| Subnet range | 172.16.0.0/24 |
| Private IP ManufacturingVM | 172.16.0.4 |

---

## Task 3: Network Watcher — voor peering

Connectiviteitstest van CoreServicesVM naar ManufacturingVM vóór peering:

| Test | Resultaat |
|---|---|
| Connectivity | ❌ Unreachable (316/316 probes failed) |
| Outbound NSG | ❌ Deny — `DefaultRule_DenyAllOutBound` op CoreServicesVM-nsg |
| Inbound NSG | ✅ Allow — `UserRule_RDP` op ManufacturingVM-nsg |
| Next hop | Next hop type: None |

> Verwacht resultaat — de VNets zijn nog niet gepeerd, dus verkeer wordt geblokkeerd door de default DenyAllOutBound regel.

---

## Task 4: VNet Peering configureren

Peering aangemaakt vanuit CoreServicesVnet:

| Setting | Value |
|---|---|
| Peering link naam (local) | CoreServicesVnet-to-ManufacturingVnet |
| Peering link naam (remote) | ManufacturingVnet-to-CoreServicesVnet |
| Remote VNet | ManufacturingVnet |
| Forwarded traffic | Ingeschakeld op beide kanten |

**Status na aanmaken:** `Connected` — Fully Synchronized ✅

---

## Task 5: PowerShell test — na peering

Private IP CoreServicesVM: `10.0.0.4`

```powershell
Test-NetConnection 10.0.0.4 -port 3389
```

Output:

```
ComputerName     : 10.0.0.4
RemoteAddress    : 10.0.0.4
RemotePort       : 3389
InterfaceAlias   : Ethernet
SourceAddress    : 172.16.0.4
TcpTestSucceeded : True
```

✅ Verbinding succesvol na peering.

---

## Task 6: Custom Route

Nieuw subnet toegevoegd aan CoreServicesVnet:

| Property | Value |
|---|---|
| Subnet naam | perimeter |
| Address range | 10.0.1.0/24 |

Route table aangemaakt:

| Property | Value |
|---|---|
| Naam | rt-CoreServices |
| Propagate gateway routes | No |

Route toegevoegd:

| Property | Value |
|---|---|
| Route naam | PerimetertoCore |
| Destination type | IP Addresses |
| Destination | 10.0.0.0/16 |
| Next hop type | Virtual appliance |
| Next hop address | 10.0.1.7 (toekomstige NVA) |

Route table gekoppeld aan subnet `perimeter` van `CoreServicesVnet`.

---

## Cleanup

```bash
az group delete --name ex22rg --no-wait
```

---

## Key takeaways

- Standaard kunnen resources in verschillende VNets niet met elkaar communiceren.
- VNet peering verbindt twee of meer VNets naadloos in Azure.
- Gepeerde VNets functioneren als één netwerk voor connectiviteit — verkeer loopt via de Microsoft backbone.
- System-defined routes worden automatisch aangemaakt per subnet. User-defined routes overschrijven of vullen deze aan.
- Azure Network Watcher biedt tools om connectiviteit te testen, diagnostics uit te voeren en verkeer te analyseren.
