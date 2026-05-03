
# Exercise 24: Create an NVA and Virtual Machines

- **Learning Path 5:** Configure and manage virtual networks for Azure administrators
- **Module 5:** Configure Azure Virtual Network routing

---

## Scenario

NVA deployen in het dmzsubnet en IP forwarding inschakelen zodat verkeer van publicsubnet via de NVA naar privatesubnet wordt gerouteerd.

---

## Aangemaakt resources

| Resource | Naam | Details |
|---|---|---|
| Resource group | ex23rg | West Europe (hergebruikt van exercise 23) |
| NVA VM | nva | Ubuntu 22.04, dmzsubnet |

---

## Uitgevoerde CLI commands

### NVA deployen

```bash
az vm create \
    --resource-group ex23rg \
    --name nva \
    --vnet-name vnet \
    --subnet dmzsubnet \
    --image Ubuntu2204 \
    --admin-username azureuser \
    --admin-password <password>
```

### IP forwarding inschakelen op Azure NIC

```bash
# NIC ID ophalen
NICID=$(az vm nic list \
    --resource-group ex23rg \
    --vm-name nva \
    --query "[].{id:id}" --output tsv)

# NIC naam ophalen
NICNAME=$(az vm nic show \
    --resource-group ex23rg \
    --vm-name nva \
    --nic $NICID \
    --query "{name:name}" --output tsv)

# IP forwarding inschakelen op NIC
az network nic update --name $NICNAME \
    --resource-group ex23rg \
    --ip-forwarding true
```

### IP forwarding inschakelen in de VM zelf

```bash
# Public IP ophalen
NVAIP="$(az vm list-ip-addresses \
    --resource-group ex23rg \
    --name nva \
    --query "[].virtualMachine.network.publicIpAddresses[*].ipAddress" \
    --output tsv)"

# IP forwarding inschakelen via SSH
ssh -t -o StrictHostKeyChecking=no azureuser@$NVAIP 'sudo sysctl -w net.ipv4.ip_forward=1; exit;'
```

---

## Key takeaways

- Een NVA deployen als Ubuntu VM in het dmzsubnet
- IP forwarding moet op **twee niveaus** ingeschakeld worden: op de Azure NIC én binnen het OS van de VM
- Zonder IP forwarding op de Azure NIC wordt doorgestuurd verkeer geblokkeerd door Azure
- Zonder IP forwarding in het OS wordt verkeer niet doorgestuurd door de VM zelf
- De NVA op 10.0.2.4 fungeert als next hop voor de custom route uit exercise 23
