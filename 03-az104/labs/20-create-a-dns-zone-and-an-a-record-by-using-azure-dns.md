# Exercise 20: Create a DNS Zone and an A Record by using Azure DNS

- **Learning Path 5:** Configure and manage virtual networks for Azure administrators
- **Module 3:** Host your domain on Azure DNS

---

## Aangemaakt resources

| Property | Value |
|---|---|
| Resource group | ex20rg |
| DNS zone naam | wideworldimportsabcd.com |

---

## DNS Records

### NS records (automatisch aangemaakt)

Gebruikt bij nslookup: `ns1-08.azure-dns.com`

### A record

| Property | Value |
|---|---|
| Name | www |
| Type | A |
| TTL | 1 uur |
| IP address | 10.10.10.10 |

---

## Verificatie

```
nslookup www.wideworldimportsabcd.com ns1-08.azure-dns.com
```

Resultaat: `www.wideworldimportsabcd.com` resolvet naar `10.10.10.10` ✅

---

## Key takeaways

- DNS zone aanmaken in Azure → NS en SOA records worden automatisch aangemaakt
- A record koppelt hostnaam aan IP adres
- nslookup met specifieke Azure name server verifieert de DNS zone configuratie
- In productie: NS records updaten bij domain registrar voor domain delegation
