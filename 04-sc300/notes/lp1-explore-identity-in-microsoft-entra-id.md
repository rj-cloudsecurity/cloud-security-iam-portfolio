# SC-300: Microsoft Identity and Access Administrator
## Learning Path 1: Explore identity in Microsoft Entra ID

  - **SC-300 Started:** 2 August, 2026
  - **SC-300 Exam passed:** 🔄

---

## Explain the identity landscape

**Identity lifecycle (5 onderdelen)**

| # | Onderdeel | Details |
|---|---|---|
| 1 | Zero Trust | Verify Explicitly, Use Least Privilege, Assume Breach |
| 2 | Identity | B2B, B2C, Verifiable Credentials (decentralized providers) |
| 3 | Actions | Authenticate (Prove - AuthN), Authorize (Get - AuthZ), Administer (Configure), Audit (Report) |
| 4 | Usage | Access applications and data, Secure (Cryptography), Dollars (Licenses) |
| 5 | Maintain | Protect, Detect, Respond |

**Toelichting per onderdeel**
  -  1. Altijd ontwerpen met Zero Trust; niet automatisch toegang geven omdat een gebruiker die eerder had, altijd bevestigen
  -  2. ystemen voor geverifieerde accounts: komen van Microsoft Entra ID, business-to-business federation, business-to-customer, decentralized identity providers
  -  3. Users en applicaties authenticaten en authorizen voor toegang; administrators monitoren en onderhouden systemen met governance
  -  4. Toegang tot applicaties en data gebruiken, met andere identity-based services
  -  5. Systemen up-to-date houden

**Classic identity vs Zero Trust identity**
| Classic identity | Zero Trust identity |
|---|---|
| Assets achter een firewall (database, applicatie achter locked gate) | Centraal beleid geeft toegang tot verschillende lokaal beveiligde resources |
| Restrict everything to a secure network | Protect assets anywhere with central policy |

**Context:** vroeger; username/password door de "poort" gaf volledige toegang. Bij grote hoeveelheid cyberaanvallen is alleen het netwerk beveiligen niet genoeg; één gestolen credential geeft bad actors toegang tot alles. Zero Trust beschermt assets overal met policy.

---

## Explore Zero Trust with identity

**Waarom Zero Trust**
Organisaties hebben een nieuw security model nodig dat past bij de complexiteit van hybrid en multicloud omgevingen. Ondersteuning nodig voor cloud, mobile workforce en bescherming van mensen, devices, apps en data; waar ze zich ook bevinden. Zero Trust gaat uit van "assume breach" en verifieert elk verzoek alsof het van een niet-vertrouwd netwerk komt: **"never trust, always verify."**

**Zero Trust principes**

| Principe | Data points / methode |
|---|---|
| Verify Explicitly | User identity en locatie · Device health · Service/workload context · Data classification · Anomalies |
| Use least privilege access | Just-in-time (JIT) · Just-enough-access (JEA) · Risk-based adaptive policies · Data protection against out of band vectors |
| Assume breach | Segmenting access by network, user, devices, app awareness · Encrypting all sessions end to end · Analytics voor threat detection, posture visibility, defenses verbeteren |

**Deploy Zero Trust solutions**

Zero Trust strekt zich uit over het hele digital estate; geïntegreerde security philosophy en end-to-end strategie. Zes fundamentele pilaren:

- Identity
- Endpoints
- Data
- Apps
- Infrastructure
- Network

Elke pilaar is een signal source, een control plane voor enforcement, en een resource om te verdedigen. Focus hier: **Identity pillar.**

Identities (mensen, services, IoT devices) definiëren het Zero Trust control plane. Bij toegang tot een resource: identiteit verifiëren met sterke authenticatie, toegang moet compliant en typisch zijn voor die identiteit, least privilege access principes volgen.

**Zero Trust architecture**

Security policy governs everything. Identity wordt gebruikt om identity en access te verifiëren. Andere blokken: data, apps, networking, infrastructure; radiating outward vanuit het policy center.

Kern van de strategie: een **policy engine** voor dynamische access-beslissingen op kritieke checkpoints (netwerken, apps, data).

- **Identity en access management + endpoint management** -> expliciete verificatie van users en devices via rich signal (device health, sign-in risk)
- **Information protection + cloud security solutions** -> real-time enforcement en bescherming van resources
- **Networking solutions** -> real-time threat protection, detectie en respons op netwerk/infrastructuur
- **SIEM + XDR (geïntegreerd)** -> end-to-end threat prevention, detection, response. Geeft zichtbaarheid over threats across alle resources, koppelt signalen samen, enabled snelle geïntegreerde remediation

Resultaat: alleen de juiste mensen krijgen het juiste toegangsniveau; verhoogt zowel security als productiviteit.

### Discuss identity as a control plane


### Explore why we have identity


### Define identity administration


### Contrast decentralized identity with central identity systems


### Discuss identity management solutions


### Explain Microsoft Entra Business to Business


### Compare Microsoft identity providers


### Define identity licensing


### Explore authentication


### Discuss authorization


### Explain auditing in identity
