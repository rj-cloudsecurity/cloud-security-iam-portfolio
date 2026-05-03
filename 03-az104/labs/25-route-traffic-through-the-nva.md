# Exercise 25: Route Traffic Through the NVA

- **Learning Path 5:** Configure and manage virtual networks for Azure administrators
- **Module 5:** Configure Azure Virtual Network routing

---

## Scenario

Twee VMs deployen (public en private subnet) en via traceroute verifiëren dat verkeer van public naar private via de NVA loopt, en verkeer van private naar public direct gaat.

---

## Aangemaakt resources

| Resource | Naam | Subnet | IP |
|---|---|---|---|
| Resource group | ex23rg | — | West Europe |
| VM | public | publicsubnet | 10.0.0.4 |
| VM | private | privatesubnet | 10.0.1.4 |
| NVA | nva | dmzsubnet | 10.0.2.4 |

---

## Uitgevoerde CLI commands

### cloud-init.txt aanmaken

```bash
code cloud-init.txt
```

Inhoud:

```
#cloud-config
package_upgrade: true
packages:
   - inetutils-traceroute
```

### VMs deployen

```bash
az vm create \
    --resource-group ex23rg \
    --name public \
    --vnet-name vnet \
    --subnet publicsubnet \
    --image Ubuntu2204 \
    --admin-username azureuser \
    --no-wait \
    --custom-data cloud-init.txt \
    --admin-password <password>

az vm create \
    --resource-group ex23rg \
    --name private \
    --vnet-name vnet \
    --subnet privatesubnet \
    --image Ubuntu2204 \
    --admin-username azureuser \
    --no-wait \
    --custom-data cloud-init.txt \
    --admin-password <password>
```

### VM status monitoren

```bash
watch -d -n 5 "az vm list \
    --resource-group ex23rg \
    --show-details \
    --query '[*].{Name:name, ProvisioningState:provisioningState, PowerState:powerState}' \
    --output table"
```

### Public IP adressen ophalen

```bash
PUBLICIP="$(az vm list-ip-addresses \
    --resource-group ex23rg \
    --name public \
    --query "[].virtualMachine.network.publicIpAddresses[*].ipAddress" \
    --output tsv)"

PRIVATEIP="$(az vm list-ip-addresses \
    --resource-group ex23rg \
    --name private \
    --query "[].virtualMachine.network.publicIpAddresses[*].ipAddress" \
    --output tsv)"
```

---

## Traceroute verificatie

### Public → Private (via NVA)

```bash
ssh -t -o StrictHostKeyChecking=no azureuser@$PUBLICIP 'traceroute private --type=icmp; exit'
```

Output:

```
traceroute to private.kzffavtrkpeulburui2lgywxwg.gx.internal.cloudapp.net (10.0.1.4), 64 hops max
1   10.0.2.4  0.710ms  0.410ms  0.536ms
2   10.0.1.4  0.966ms  0.981ms  1.268ms
```

✅ Hop 1 = NVA (10.0.2.4) → verkeer loopt via de NVA zoals bedoeld.

### Private → Public (direct)

```bash
ssh -t -o StrictHostKeyChecking=no azureuser@$PRIVATEIP 'traceroute public --type=icmp; exit'
```

Output:

```
traceroute to public.kzffavtrkpeulburui2lgywxwg.gx.internal.cloudapp.net (10.0.0.4), 64 hops max
1   10.0.0.4  1.095ms  1.610ms  0.812ms
```

✅ Directe verbinding — geen NVA in het pad, want de custom route geldt alleen voor publicsubnet.

---

## Cleanup

```bash
az group delete --name ex23rg --no-wait
```

---

## Key takeaways

- Custom route op publicsubnet dwingt verkeer via de NVA (10.0.2.4) naar privatesubnet
- Verkeer van privatesubnet naar publicsubnet gebruikt default system routes — geen NVA
- IP forwarding op NIC én in het OS zijn beide vereist voor correcte doorstuur-werking
- traceroute toont de exacte route die pakketten afleggen — handig voor verificatie en troubleshooting
