# Exercise 3. Assign licenses to users

- Learning path 2.: AZ-104: Manage identities and governance in Azure
- Module: 2. Create, configure, and manage identities

In deze oefening maak ik een gebruiker en een security group aan in Microsoft Entra ID, wijs ik een licentie toe aan de groep, en verwijder ik de gebruiker daarna.

---

## Task 1 Gebruiker aanmaken

Uitgevoerd via **Microsoft Entra admin center > Identity > Users > All Users > + New user > Create new user**

| Setting | Value |
|---|---|
| User principal name | ChrisG |
| Name | Chris Green |
| First name | Chris |
| Last name | Green |
| Password | [eigen wachtwoord] |

Gecontroleerd: account Chris Green zichtbaar in All users lijst.

---

## Task 2 Security group aanmaken

De oefening verwijst naar **Identity > Groups**, maar in de Microsoft Entra admin center staat dit onder **Microsoft Entra ID > Groups**.

Uitgevoerd via **Microsoft Entra admin center > Microsoft Entra ID > Groups > All groups > New group**

| Setting | Value |
|---|---|
| Group type | Security |
| Group name | Marketing |
| Membership type | Assigned |
| Owners | eigen admin account |
| Members | Chris Green |

Gecontroleerd: groep Marketing zichtbaar in All groups lijst.

---

## Task 3 Licentie toewijzen aan groep — overgeslagen

Deze stap vereist toegang tot de **Microsoft 365 admin center > Billing > Licenses**. Dit vereist een zakelijke Microsoft 365 subscription. Met een persoonlijk Azure account is deze pagina niet toegankelijk:

> *"Your account doesn't have permission to view or manage this page. Login is not supported for consumer users without business presence."*

---

## Task 4 Gebruiker verwijderen

Gebruiker ChrisG en groep Marketing verwijderd via de Microsoft Entra admin center.

> Verwijderde gebruikers blijven 30 dagen herstelbaar via **Users > Deleted users**. Na 30 dagen wordt het account permanent verwijderd. Herstel is niet mogelijk na permanente verwijdering. Vereiste rol: Global administrator, User administrator, of Partner Tier Support.

---
