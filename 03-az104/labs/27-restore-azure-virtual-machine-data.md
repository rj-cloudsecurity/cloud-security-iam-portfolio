# Exercise 27: Restore Azure Virtual Machine Data

- **Learning Path 6:** Monitor and back up Azure resources
- **Module 2:** Protect your virtual machines by using Azure Backup

---

## Scenario

NW-APP01 had problemen na de backup uit exercise 26. De VM wordt hersteld via de Recovery Services vault door de schijf te vervangen met een eerder restore point.

---

## Gebruikte resources uit Exercise 26

| Resource | Naam |
|---|---|
| Resource group | ex25rg |
| Windows VM | NW-APP01 |
| Recovery Services Vault | azure-backup |

---

## Aangemaakt in deze oefening

| Resource | Naam | Details |
|---|---|---|
| Storage account | restoringstaging20260504 | ex25rg, West Europe — staging locatie voor restore |

---

## Stappen

### 1. Storage account aanmaken

Portal → Storage accounts → Create

| Setting | Value |
|---|---|
| Resource group | ex25rg |
| Storage account name | restoringstaging20260504 |
| Region | West Europe |

### 2. VM stoppen

Portal → Virtual Machines → NW-APP01 → **Stop**

> VM moet gestopt zijn voor restore — anders geeft Azure een foutmelding.

### 3. VM herstellen

Portal → NW-APP01 → Operations → Backup → **Restore VM**

| Setting | Value |
|---|---|
| Restore point | Geselecteerd restore point |
| Restore configuration | Replace existing |
| Staging location | restoringstaging20260504 |

→ **Restore** geklikt. Notificatie: *Triggering restore for NW-APP01*

### 4. Restore monitoren

Portal → Backup pane NW-APP01 → Alerts and Jobs → **View all Jobs** → View details van de Restore job.

Getoonde informatie:
- **Job details** — details over de restore job
- **Job status** — real-time voortgang
- **Sub tasks** — naam en status van deeltaken

---

## Cleanup

```bash
az group delete --name ex25rg --no-wait
```

---

## Key takeaways

- VM moet **gestopt** zijn voordat een restore uitgevoerd kan worden
- **Replace existing** vervangt de huidige schijf met het geselecteerde restore point
- Een staging storage account is vereist voor de restore operatie
- Restore voortgang is te monitoren via de vault → Backup Jobs
- Cross-region restore is mogelijk naar een paired secondary regio
