# SC-900: Security, Compliance, and Identity Fundamentals — Study Notes

  - **Started:** 16-3-2026
  - **Exam passed:** -

---

  - **Learning Path 1:** Introduction to Security, Compliance, and Identity
    - **Module 1:** Describe Security and Compliance Concepts
      - **Extra Sources:*FreeCodeCamp SC‑900*
        
**Shared Responsibility Model**

  - On-premises: zelf verantwoordelijk voor alles, van gebouw tot de data.
  - Cloud: gedeelde verantwoordelijkheid

  - Shared responsibility in the cloud
    - IaaS: provider beheert fysieke hardware en netwerk; klant OS, apps en data
    - PaaS: provider beheert OS en Platform; klant app en data
    - Saas: provider beheert bijna alles; klant toegang,identities en data

  - Responsibilities you always keep (cloud)
    - Data: classificatie, bescherming en encryptie
    - Identities & Access: accounts, rechten en authenticatie
    - Endpoints: de apparaten die toegang hebben
    - Configuratie: beveiligingsinstellingen
   
   - AI shared responsibility model
    - AI volgt hetzelfde model maar met extra overwegingen omdat AI beinvloed kan worden door user inputs en outputs an generen
    - een AI-enabled applicatie heeft 3 lagen:
      - AI Platform: onderliggende infrastructuur en AI moedel via APIs
      - AI Application: de app die jij bouwt of deployt bovenop het platform
      - AI Usage: heo mensen in jou organisatie het AI systeem gebruiken

  - What the provider typically handles (AI)
    - Datacenter, fysieke hosts en core platform services beveiligen
    - Model hosting infrastructuur beheren
    - Ingebouwde safety controls bieden zoals filtereing
     
  - What you typically handle (AI)
    - Sensitive data beschermen die je naar het AI systeem stuurt
    - Identity & Access beheren voor AI apps en resources
    - AI oplossingen veilig configureren; allowed users, connectors, logging en retention
    - AI risico's beperken zoals prompt injection en onveilige externe data
    - Acceptable use policies instellen en gebruikers trainen

  - Key takeaway
    - Het Shared Responsibility Model draait om duidelijkheid; hoe hoger het service niveau, hoe meer de provider overneemt. Maar jij blijft altijd verantwoordelijk voor je data, access en hoe de technologie gebruikt wordt.


**Describe defense in depth**

  - Gelaagde aanpak van security, niet afhankelijk van 1 enkele beschermingslijn
  - Elke laag biedt bescherming; als 1 laag doorbroken wordt, stopt de volgende laag de aanvaller

  - Layers of Security
    - Physical security: alleen geautoriseerd personeel toegang tot datacenter
    - Identity & Access: MFA en conditional access om toegang te controleren
    - Perimeter security: DDoS protection om grootschalige aanvallen te filteren
    - Network Security: network segmentation en access controls
    - Compute layer: toegang tot virtual machines beveiligen, poorten sluiten
    - Application layer: application vrij houden van security vulnerabilites
    - Data layer: access controls en encryptie voor business en customer data

  - Confidentiality, Integrity, Availability (CIA)
    - Confidentiality: gevoelige data geheim houden; passwords, klantdata, financiële data; via encryptie
    - Integrity: data correct en ongewijzigd houden; zekerheid dat data niet is aangepast of gemanipuleerd
    - Availability: data beschikbaar maken voor wie het nodig heeft, wanneer ze het nodig hebben

  - Het doel van cybersecurity is CIA beschermen. het doel van cybercriminelen is CIA verstoren.


**Describe the Zero Trust model**

  - Gaat ervan uit dat alles op een open en onbetrouwbaar netwerk zit, ook achter de firewall
  - Principe: Trust no one, verify everything
  - Geen enkel wachtwoord is voldoende; altijd extra verificatie vereist. Geen toegang tot hele netwerken, alleen tot wat gebruiker nodig heeft.

  - Zero Trust guiding principles
    - Verify explicitly: altijd authenticeren en autoriseren op basis van user identity, locatie, device, data classificatie en anomalies
    - Least privileged access: toegang beperken met just-in-time (JIT) en Just-enough-access (JEA) en risk-based adaptive policies
    - Accume breach: ga ervan uit dat er al een breach is; segmenteer toegang, versleutel data en gebruik analytics om bedreigingen te detecteren

  - Six foundational pillars
    - Identities: users, services of devices; altijd verifieren met strong authentication en least privilege
    - Devices: grote attack suface; monitoren op heatlh en compliance
    - Applications: ontdekken welke apps gebruikt worden, inclusief Shadow IT; permissions en access beheren
    - Data: classificeren, labelen en versleutelen; data beschermen ook buiten het netwerk
    - Infrastructure: on-premises of cloud; versie, configuratie en JIT access beoordelen, telemtry gebruiken om aanvallen te detecteren
    - Networks: segmenteren met micro segmentation, real-time threat protection, end-to-end encryption en monitoring












**Describe the Zero Trust model**


































        
