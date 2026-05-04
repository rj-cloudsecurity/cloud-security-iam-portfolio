
# Exercise 26: Back up an Azure Virtual Machine

- **Learning Path 6:** Monitor and back up Azure resources
- **Module 2:** Protect your virtual machines by using Azure Backup

---

## Scenario

Backup inschakelen voor zowel een Windows als een Linux VM via Azure Backup. Backup wordt ingeschakeld via de Portal (Linux) en via Azure CLI (Windows).

---

## Aangemaakt resources

| Resource | Naam | Details |
|---|---|---|
| Resource group | ex25rg | West Europe |
| VNet | NorthwindInternal | 10.0.0.0/16 |
| Subnet | NorthwindInternal1 | 10.0.0.0/24 |
| Windows VM | NW-APP01 | Win2016Datacenter |
| Linux VM | NW-RHEL01 | RHEL 8 Gen2 |
| Recovery Services Vault | azure-backup | West Europe |

---

## Uitgevoerde CLI commands

### Resource group en VNet aanmaken

```bash
RGROUP=$(az group create --name ex25rg --location westeurope --output tsv --query name)

az network vnet create \
    --resource-group $RGROUP \
    --name NorthwindInternal \
    --address-prefixes 10.0.0.0/16 \
    --subnet-name NorthwindInternal1 \
    --subnet-prefixes 10.0.0.0/24
```

### Windows VM aanmaken

```bash
az vm create \
    --resource-group $RGROUP \
    --name NW-APP01 \
    --size Standard_DS1_v2 \
    --public-ip-sku Standard \
    --vnet-name NorthwindInternal \
    --subnet NorthwindInternal1 \
    --image Win2016Datacenter \
    --admin-username admin123 \
    --no-wait \
    --admin-password <password>
```

### Linux VM aanmaken

```bash
az vm create \
    --resource-group $RGROUP \
    --name NW-RHEL01 \
    --size Standard_DS1_v2 \
    --image RedHat:RHEL:8-gen2:latest \
    --authentication-type ssh \
    --generate-ssh-keys \
    --vnet-name NorthwindInternal \
    --subnet NorthwindInternal1
```

---

## Backup inschakelen via Portal (NW-RHEL01)

1. Portal → Virtual Machines → NW-RHEL01
2. Capabilities tab → Backup
3. SKU: **Standard**
4. Vault: automatisch aangemaakt
5. Policy: DailyPolicy — dagelijks 12:00 UTC, retentie 180 dagen
6. **Enable backup** → daarna **Backup now**

---

## Backup inschakelen via CLI (NW-APP01)

### Recovery Services Vault aanmaken

```bash
az backup vault create \
    --resource-group ex25rg \
    --location westeurope \
    --name azure-backup
```

### Backup inschakelen

```bash
az backup protection enable-for-vm \
    --resource-group ex25rg \
    --vault-name azure-backup \
    --vm NW-APP01 \
    --policy-name EnhancedPolicy
```

### Status monitoren

```bash
az backup job list \
    --resource-group ex25rg \
    --vault-name azure-backup \
    --output table
```

### Initiële backup starten

```bash
az backup protection backup-now \
    --resource-group ex25rg \
    --vault-name azure-backup \
    --container-name NW-APP01 \
    --item-name NW-APP01 \
    --retain-until 18-10-2030 \
    --backup-management-type AzureIaasVM
```

---

## Monitoring

- **Per VM:** Portal → VM → Capabilities → Backup → Last backup status
- **Via vault:** Portal → azure-backup Recovery Services vault → Overview → Backup tab

---

## Cleanup

```bash
az group delete --name ex25rg --no-wait
```

---

## Key takeaways

- Backup inschakelen kan via Portal, CLI én PowerShell
- Recovery Services vault beheert alle backup data en policies
- Linux VM gebruikt SSH keys, Windows VM gebruikt wachtwoord
- EnhancedPolicy ondersteunt hourly backups
- Backup jobs monitoren via `az backup job list` of via de vault in de Portal
