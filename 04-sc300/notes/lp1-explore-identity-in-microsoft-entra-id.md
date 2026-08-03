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

---

**Discuss identity as a control plane**
  - Wat is een control plane?
    - Een control plane is een lang bestaand netwerkconcept. Het is het component verantwoordelijk voor het beaplen hoe traffic door een netwerk stroomt. Dus een control plane is een tool of service die toegang tot resoures stuurt op basis van specifieke criteria. Bij oplossingen in de huidige wereld is user identity de juiste plek om toegang te checken. Identitiy is een duidelijke keuze voor de control plane.
   
  - Met de vele netwerken, devices en applicaties die nodig zijn in het dagelijkse bedrijfsleven, is de enige gemeenschappelijke factor de identity. Elk user, external user, app en device heeft een identity. Daarom zeggen we dat identity de control plane is. Het is essentieel om vast te stellen wie de user is als de kern van vertrouwen voor andere transacties. Als we niet zeker weten wie de user is, doet geen enkele andere system access control of security ertoe. Zodra we zeker zijn van de user, kunnen we elk element van toegang expliciet verifieren; of onze resources nu on-premises, in cloud-hosted servers, of managed SaaS apps zoals Office 365 zijn.

---

**Explore why we have identity**
  - We hebben Zero Trust besproken en identity als de control plane voor toegang tot resources. Maar waarom gebruiken we identity?
    - Identity geeft de mogelijkheid:
      - Authentication: Om te bewijzen wie of wat we zijn
      - Authorization: Om permissions te krijgen om iets te doen
      - Auditing: Om te rapporteren over wat er is gedaan
      - Administration: Om IT te laten managen en self administer van een identity

| Authentication | Authorization | Administration | Auditing |
|---|---|---|---|
| User sign on experience | User sign on experience | Single view management | Track who does what, when, where and how |
| Trusted source(s) | Can a user access the resource | Application of business rules | Focused alerting |
| Federative protocols | What can they do when they access it? | Automated requests, approvals, and access assignment | In-depth collated reporting |
| Level of assurance | | Entitlement management | Governance & compliance |

- Wat is een identity provider (IdP)
  - Een identity provider (IdP) is een systeem dat digitale identiteiten creeert, beheert en opslaat. Microsoft Entra ID is een voorbeeld. De capabilities en features van identity providers kunnen varieren. De meest voorkomende componenten zijn:
    - Een repository van user identities
    - Een authentication systeem
    - Security protocols die beschermen tegen intrusion
    - Iemand die we vertrouwn
   
  - Een identity provider verifieert identiteiten met 1 of meer authentication factors, zoals een wachtwoord of vingerafdrukscan. Een identity provider is vaak een trusted provider voor gebruik met single-sign-on (SSO) om andere resources te benaderen. SSO verbetert usability door password fatique te verminderen. Het biedt ook betere security door het potentiele attack suface te verkleinen. Identity providers kunnen connecties tussen cloud computing resources en users faciliteren. Waardoor de noodzaak voor users om opniuew te authenticeren bij mobile en roaming applicaties afneemt.
 
  - Common Identity Protocols
    - OpenID provider -OpenID Connect (OIDC) is een authentication protocol gebaseerd op het OAuth2 protocol (dat gebruikt wordt voor authorization). OIDC gebruikt de gestandaardiseerde message flows van OAuth2 om identity services te bieden. Specifiek: een system entity (genaamd een OpenID-Provider) geeft JSON geformatteerde identity tokens uit aan OIDC relying parties via een RESTful HTTP API
   
    - SAML Identity provider. Security Assertion Marktup Languague (SAML) is een open standaard voor het uitwisselen van authentication en autorization data tussen een identity provider en een service provider. SAML is een XML-based markup language voor security assertions, wat statements zijn die service providers gebruiken om access-control decisions te maken.

---

**Define identity administration**
  - Wat het is:
    - Beheer van identity objects gedurende hun hele levenscyclus; handmatig of geautomatiseerd
    - Zonder governance: Verlopen/vergeten accounts blijven actief -> security risico

  - Wat het oplevert
    - Configureerbaar rond business processes
    - Schaalbaar naar demand
    - Kostenbesparing door automatisering
    - Flexibiliteit in sync, proliferation, change control
   
  - Kerntaken
    - Provision: Identity aanmaken; Deprovisioning = toegang verwijderen
    - Synchronization: Identity data actueel houden: manual, time-based, of event-drivin
    - Identity Proliferation: Identities verspreid over AD, andere directories, App-specifieke stores
    - Password Management: Service Desk meestal focal point voor forgotten passwords
    - Group Management: Groupen = meest gebruikte manier om access te bepalen, kostbaar te beheren
    - Application Entitlement Management: Coarse-grained (Authorization pillar) vs fine-grained (identity atrributes)
    - User Interface / Change Control: Hoe users updates aanvragen (vaak nog via Service Desk); Change flow manual of geautomatiseerd
   
  - Tools voor automation:
    
 | Tool | Platform | Voorbeeld: user aanmaken |
|---|---|---|
| Azure CLI | Windows/macOS/Linux, Bash-achtig | az ad user create --display-name "New User" ... |
| PowerShell (Microsoft Graph) | Windows/macOS/Linux | New-MgUser -DisplayName "New User" ... |

  - Azure CLI voelt natuurlijker bij linux achtergrond, PowerShell bij Windows
  - Commands: verb-noun shceme, output = objects

  - Microsoft Graph
    - Een REST API endpoint `https://graph.microsoft.com`
    - Toegang tot Entra ID, M365, devices, etc.
    - 3 onderdelen: Graph API, (data ophalen/beheren); Grpah connectors (externe data -> M365 Search); Graph Data connect (data naar Azure stores)
   

---

### Contrast decentralized identity with central identity systems


### Discuss identity management solutions


### Explain Microsoft Entra Business to Business


### Compare Microsoft identity providers


### Define identity licensing


### Explore authentication


### Discuss authorization


### Explain auditing in identity
