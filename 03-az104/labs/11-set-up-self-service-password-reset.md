# Exercise 11 Set up self-service password reset
- Learning path 2.: AZ-104: Manage identities and governance in Azure
- Module: 6. Allow users to reset their password with Microsoft Entra self-service password reset

---

## Task 1 Security group aanmaken

Uitgevoerd via **Microsoft Entra admin center > Microsoft Entra ID > Groups > All groups > New group**

| Setting | Value |
|---|---|
| Group type | Security |
| Group name | SSPRTesters |
| Group description | Members are testing the rollout of SSPR |
| Membership type | Assigned |

---

## Task 2 Gebruiker aanmaken

Uitgevoerd via **Microsoft Entra admin center > Microsoft Entra ID > Users > + New user > Create new user**

| Setting | Value |
|---|---|
| User principal name | balas |
| Display name | Bala Sandhu |
| Group | SSPRTesters |

---

## Task 3 SSPR inschakelen — overgeslagen

SSPR inschakelen vereist **Microsoft Entra ID P1 of P2**. Met een gratis Azure account is deze functie niet beschikbaar:

De stappen Enable SSPR, Register for SSPR en Test SSPR zijn daardoor niet uitgevoerd.

---
