# SC-900: Identity & Access Clusters

  - Dit document bundelt de belangrijkste Microsoft securityproducten en Entra‑functies in duidelijke clusters. Veel diensten hebben overlappende namen en vergelijkbare rollen, waardoor ze lastig te onderscheiden zijn. Door ze te groeperen op functie binnen identity, access, governance en threat protection ontstaat een helder en snel te onthouden overzicht dat helpt bij het herkennen van examenvragen.
  - Deze clusters sluiten goed aan bij een manier van leren die draait om verbanden leggen in plaats van losse definities onthouden, waardoor de structuur van Microsoft‑securitydiensten veel sneller blijft hangen.

## **Identity Protection**
  - Detecteert **risky sign-ins**
  - Detecteerd **risky users**
  - Gebruikt **risk signals** zoals leaked credentials, unfamiliar sign-ins en malware-linked IP's
  - Kan automatisch **risk-based policies** activeren (bv. require MFA, block access)

## **Conditional Access**
  - Voert **policies** uit op basis van signalen
  - Werkt voglens het principe **If this -> then that**
  - Gebruikt signalen zoals user, device, location, app en risk
  - kan **Legacy authentication blokkeren**
  - vormt de **policy-engine** van Microsoft Entra ID

## **Privileged Identity Management (PIM)**
  - Biedt **tijdelijke adminrechten** (Just-in-Time)
  - Ondersteunt **approval workflows**
  - Houdt **audit logs** bij voor privileged access
  - Voorkomt **permanente adminrollen**

## **Access Reviews**
  - Controleert periodiek of toegang nog nodig is
  - Gericht op **guest users**, groepen en applicaties
  - Onderdeel van **Identity Governance**

## **Access Packages**
  - Bundelen toegang voor **onboarding**
  - Combineren apps, groepen en rollen
  - Onderdeel van **Entitlement Management**

## **Defender for Cloud**
  - **Cloud Security Posture Management (CSPM)**
  - Threat protection voor Azure, Hybrid en multi-cloud workloads
  - Aanbevelingen, hardening en secure score voor workloads

## **Defender for Cloud Apps (CASB)
  - Detecteerd **Shadow IT**
  - App discovery
  - **Session control** voor real-time monitoring
  - Policies voor SaaS-applicaties

## **Defender for Identity
  - Beschermt **on-premises Active Directory**
  - Detecteerd laterale beweging, Pass-the-Hash en Pass-the-Ticket
  - Analyseert AD-verkeer op verdachte patronen

## **Defender for Endpoint
  - **Endpoint Detection & Response (EDR)
  - Beschermt Windows, macOS, Linux, iOS en Android
  - Detecteert en reageert op endpoint-dreigingen
    
## **Identity Models
  - Password Hash Sync (PHS): synchroniseert wachtwoordhash naar Entra ID
  - Pass-Through Authentication (PTA): On-prem AD valideert wachtwoorden
  - Federation (ADFS): Externe identity provider verzorgt authenticatie

## **Governance & Compliance
  - Secure Score: meet security posture en geeft aanbevelingen
  - Compliance Manager: assessments, regulatory compliance en verbeteracties
  - Data Minimization: alleen data verzamelen die noodzakelijk is
  - Data Residency / Sovereignty: waar data staat en wie erover mag beslissen
























