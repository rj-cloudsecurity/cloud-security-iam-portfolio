# Exercise 13 Provide storage for the public website
- Learning path 3.: AZ-104: Implement and manage storage in Azure
- Module: 2. Configure Azure Blob Storage

---

## Task 1 Storage account aanmaken met high availability

Uitgevoerd via **Azure portal > Storage accounts > + Create**

| Setting | Value |
|---|---|
| Resource group | exercise13 |
| Storage account name | publicwebsiteuaoio |
| Redundancy | Read-access Geo-redundant storage (RA-GRS) |
| Primary location | West Europe |
| Secondary location | North Europe |

---

## Task 2 Anonymous public access inschakelen

Uitgevoerd via **Storage account > Settings > Configuration**

- Allow Blob anonymous access: **Enabled**

## Aantekening

Na het opslaan van de instelling bleef de container access level op Private staan. Na het sluiten en heropenen van de browser werkte de instelling correct.

---

## Task 3 Blob container aanmaken

Uitgevoerd via **Storage account > Data storage > Containers > + Container**

| Setting | Value |
|---|---|
| Name | public |
| Public access level | Blob (anonymous read access for blobs only) |

---

## Task 4 Bestand uploaden en testen

- Bestand geüpload: `cloud.jpg`
- URL: `https://publicwebsiteuaoio.blob.core.windows.net/public/cloud.jpg`
- Bestand toegankelijk via browser zonder authenticatie

---

## Task 5 Soft delete instellen

Uitgevoerd via **Storage account > Overview > Properties > Blob service > Blob soft delete**

- Enable soft delete for blobs: **ingeschakeld**
- Retention: **21 dagen**

Soft delete getest:
- `cloud.jpg` verwijderd — bevestiging: item blijft herstelbaar voor 20 dagen
- Hersteld via **Show deleted blobs > Undelete**
- Bestand weer zichtbaar in container

---

## Task 6 Blob versioning inschakelen

Uitgevoerd via **Storage account > Overview > Properties > Blob service > Versioning**

- Enable versioning for blobs: **ingeschakeld**
- Tweede versie van bestand geüpload — vorige versie zichtbaar via Show deleted blobs

---

## Task 7 Clean up

Resource group `exercise13` en storage account `publicwebsiteuaoio` verwijderd.
