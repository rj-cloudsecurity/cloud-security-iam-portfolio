
# Exercise 23: Create Custom Routes

- **Learning Path 5:** Configure and manage virtual networks for Azure administrators
- **Module 5:** Configure Azure Virtual Network routing

---

## Scenario

Verkeer van de public subnet naar de private subnet moet altijd via een NVA (perimeter/DMZ subnet) lopen. Hiervoor wordt een custom route aangemaakt die verkeer naar de virtual appliance stuurt.

---

## Aangemaakt resources

| Resource | Naam | Details |
|---|---|---|
| Resource group | ex23rg | West Europe |
| VNet | vnet | 10.0.0.0/16 |
| Subnet | publicsubnet | 10.0.0.0/24 |
| Subnet | privatesubnet | 10.0.1.0/24 |
| Subnet | dmzsubnet | 10.0.2.0/24 |
| Route table | publictable | BGP propagation: false |
| Custom route | productionsubnet | Naar NVA op 10.0.2.4 |

---

## Uitgevoerde CLI commands

### Resource group aanmaken

```bash
az group create --name ex23rg --location westeurope
```

### Route table aanmaken

```bash
az network route-table create \
    --name publictable \
    --resource-group ex23rg \
    --disable-bgp-route-propagation false
```

### Custom route aanmaken

```bash
az network route-table route create \
    --route-table-name publictable \
    --resource-group ex23rg \
    --name productionsubnet \
    --address-prefix 10.0.1.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 10.0.2.4
```

### VNet en subnets aanmaken

```bash
az network vnet create \
    --name vnet \
    --resource-group ex23rg \
    --address-prefixes 10.0.0.0/16 \
    --subnet-name publicsubnet \
    --subnet-prefixes 10.0.0.0/24

az network vnet subnet create \
    --name privatesubnet \
    --vnet-name vnet \
    --resource-group ex23rg \
    --address-prefixes 10.0.1.0/24

az network vnet subnet create \
    --name dmzsubnet \
    --vnet-name vnet \
    --resource-group ex23rg \
    --address-prefixes 10.0.2.0/24
```

### Subnet verificatie

```
AddressPrefix    Name           ProvisioningState    ResourceGroup
---------------  -------------  -------------------  ---------------
10.0.0.0/24      publicsubnet   Succeeded            ex23rg
10.0.1.0/24      privatesubnet  Succeeded            ex23rg
10.0.2.0/24      dmzsubnet      Succeeded            ex23rg
```

### Route table koppelen aan publicsubnet

```bash
az network vnet subnet update \
    --name publicsubnet \
    --vnet-name vnet \
    --resource-group ex23rg \
    --route-table publictable
```

✅ Route table `publictable` gekoppeld aan `publicsubnet`.

---

## Key takeaways

- Custom routes (UDRs) overschrijven de default system routes van Azure
- Next hop type `VirtualAppliance` stuurt verkeer via een NVA
- Route table koppelen aan subnet zorgt dat de routes actief worden voor dat subnet
- Een subnet kan aan slechts één route table gekoppeld worden
- BGP route propagation uitschakelen voorkomt dat on-premises routes automatisch worden doorgepropageerd
