# SC-900: Security, Compliance, and Identity Fundamentals — Study Notes

  - **Started:** 16-3-2026
  - **Exam passed:** -

---

  - **Learning Path 1:** Introduction to Security, Compliance, and Identity
    - **Module 1:** Describe Security and Compliance Concepts
      - Extra Sources: FreeCodeCamp SC‑900 & John Savill's Technical Training

        
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
      - AI Platform: onderliggende infrastructuur en AI model via APIs
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


**Describe encryption and hashing**
  - Encryptie maakt data onleesbaar voor onbevoegeden. Om versleutelde data te lezen moet je het decrypten met secret key.

  - Two types of encryption
    - Symmetric encryption: zelfde key voo rencryptie en decryptie
    - Asymmetric encryption: public key en private key pair; wat met de public key versleuteld is kan alleen met de private key gedecrypt worden. Wordt gebruikt voor HTTPS en electronic data signing

  - Encryption for data at rest
    - Data die opgeslagen is op een fysiek apparaat zoals een server of database
    - Zonder de juiste keys is de data onleesbaas; ook als een aanvaller de harde schijf heeft

  - Encryption for data in transit
    - Data die beweegt van 1 locatie naar een andere, zoals over het internet
    - HTTPS is een voorbeeld van encryption is transit
    - Beschermt data tegen buitenstaanders tijdens het transport

  - Encryption for data in use
    - Data in niet-permanente opslag zoals RAM of CPU cache
    - Wordt beveiligd via een enclave; een soort beveiligde lockbox die data versleuteld houdt terwijl de CPU het verwerkt

  - Hashing
    - Converteert tekst aar een unieke fixed-length waarde; een hash
    - Dezelfde tekst geef altijd dezelfde hash met hetzelfde algoritme
    - Geen keys nodig en niet te decrypten; anders dan encryptie
    - Vaak gebruikt voor het opslaan van passwords; het systeem vergelijkt hashes, niet plain text passwords
    - Risico; hackers kunnen brute-force dictionary attacks uitvoeren omdat hash functions deterministisch zijn
    - Oplossing: Salting; een random waarde toevoegen aan de input zodat dezelfde passwords toch verschillende hashes krijgen
   

**Describe governance, risk, and compliance (GRC) concepts**
  - Organisaties hebben een gestructureerde aanpak nodig voor GRC vanwege toenemende complexiteit in regelgeving. Een GRC framework bestaat uit policies, operational processes en technologieen om risico's te verminderen en compliance te verbeteren

  - Governance
    - Systeem van regels, processen en praktijken waarmee een organisatie haar activiteiten stuurt en controleert
    - Bepaalt wie, wat, waar en wanneer gebruikers en applicaties toegang hebben tot bedrijfsresources
    - Bepaalt wie administrative privileges heeft en voor hoe lang

  - Risk
    - Proces van identificeren, beoordelen en reageren op bedreigingen die impact hebben op bedrijfs- of klantdoelen
    - External risks: politieke en economische factoren, natuurrampen, pandemieen, security breaches
    - Internal risks: datalekken, intellectual property thieft, fraude, insider trading
    
  - Compliance
    - Voldoen aan lokale, nationale of internationale wet- en regelgeving
    - Bepaalt welke data beschermd moet worden, welke processen vereist zijn en wat de gevolgens zijn bij niet-naling
    - Compliance is niet hetzelfde als security; security is breder, compliance is alleen het wettelijk minimum

  - Compliance-related concepts
    - Data residency: regelgeving over waar data fysiek opgeslagen mag worden en hoe het internationaal overdragen ma gworden
    - Data sovereignty: data valt onder de wetten van het land waar het verzameld, opgeslagen of verwerkt wordt; 1 dataset kan onder meerdere jurisdicties vallen
    - Data privacy: transparantie over het verzamelen, verwerken en delen van personal data; organistaties moeten voldoen aan privacy wet- en regelgeving


**Summary**
  - Shared Responsibility Model: On-premises: alles zelf. Cloud: gedeeld — hoe hoger het service niveau (IaaS → PaaS → SaaS) hoe meer de provider overneemt. Altijd jouw verantwoordelijkheid: data, identities, endpoints en configuratie
  - Defense in depth: gelaagde beveiliging via physical, identity, perimeter, network, compute, application en data layers; doel is CIA beschermen, Confidentiality, Integrity en Availability
  - Zero Trust: trust no one, verify everything;
    - 3 principes: Verify explicitly, Least privilegded access, Assume breach
    - 6 pillars: Identities, Devices, Applications, Data, Infrastructure en Networks
  - Ecnryption: Symmetric (zelfde key), Assymetric (public/private key pair)
      - Data at rest, in transit en in use
      - Hashing is eenrichtingsverkeer zonder keys, gebruikt voor passwords, beveiligd met salting tegen brute-force attacks
  - GRC: Governance stuurt en controleert activiteiten; Risk identificeert interne en externe bedreigingen; Compliance voldoet aan wet- en regelgeving; compliance is niet hetzelfde als security; data residency, sovereignty en privacy zijn compliance-gerelateerde concepten
    
  
---


  - **Learning Path 1:** Introduction to Security, Compliance, and Identity
    - **Module 2:** Describe identity concepts 
      - Extra Sources: FreeCodeCamp SC‑900 & John Savill's Technical Training
        
**Define authentication and authorization**
  - Authentication (AuthN)
    - Bewijzen dat je bent wie je zegt dat je bent
    - Voorbeeld: gebruikersnaam vertelt wie je bent, wachtwoord bewijst het
    - Gebruikersnaam + wachtwoord samen zijn een vorm van authentication

  - Authorization (AuthZ)
    - Bepaalt waar een geauthenticeerde gebruiker naartoe mag en wat hij mag zien en doen
    - Voorbeeld hotel: receptie verifieert wie je bent (authentication), keycard geeft toegang tot alleen jouw kamer en relevante liften (authorization)
    - Bepaalt het niveau van toegang en permissions tot data en resources

  - Multifactor authentication (MFA)
    - Versterkt authentication door meer dan 1 bewijs te vereisen:
      - Something you know: wachtwoord of PIN
      - Something you have: telefoon of security key
      - Something you are: biometrics

  - Passwordless authentication
    - Vermindert afhankelijkheid van wachtwoorden door sterkere alternatieven zoals passkeys of Windows Hello for business
    - Veel passwordless methoden zijn phishing-resistant; beschermt gebruikers ook als ze op een neppe inlogpagina terechtkomen


**Define identity as the primary security perimeter**
  - De traditionele 0n-premises netwerkperimeter is neit meer voldoende. Door remote werken, BYOD, partners en IoT devices is de security perimeter veel groter geworden. Identity is de nieuwe security perimeter.

  - Een identity is alles wat iemand of iets definieert; username, wachtwoord, authorization level. Een identity kan gekoppeld zijn aan een user, applicatie, device of iets anders

  - The Security perimeter extends to
    - SaaS applications buiten het corporate netwerk
    - Persoonlijke devices van medewerkers (BOYD)
    - Unmanged devices van partners of klaten
    - IoT devices in het netwerk en bij klanten

  - Four pillars of an identity infrastructure
    - Administration: aanmaken en beheren van identities voor users, devices en services; wie mag identities aanmaken, updaten en verwijderen
    - Authentication: vaststellen dat iemand echt is wie hij zegt te zijn; het uitdagen van een partij voor legitieme credentials
    - Authorization: bepalen welk toegangsniveau een geauthenticeerde user of service heeft binnen een applicatie of service
    - Auditing: bijhouden wie wat doet, wanneer, waar en hoe; reporting, alert en governance van identities


**Describe the role of the identity provider**
  - Modern authentication is een overkoepelende term voor authenticatie en autorisatie tussen een client (laptop of telefoon) en een server (website of applicatie). Centraal hierin staat de identity provider
  - Een identity provider maakt, beheert en onderhoud identity informatie en biedt authentication, authorization en auditing services aan vanuit 1 centraal punt

  - Hoe werkt het:
    - Client stuurt een identity naar de identity provider
    - Identity provider verifieert de identity
    - Identity provider geeft een security token uit
    - Client stuurt het token naar de server
    - Server valideert het token via zijn trust relationship met de identity provider
    - Gebruiker of applicatie krijg toegang tot de gevraagde resources
   
  - Tokens
    - Tokens zijn time-limited en bevatten claims over de identity en wat mag die doen
    - ID token: bewijs dat de gebruiker ingelogd is (authentication)
    - Access token: wat een client gebruikt om toegang te krijgen tot een protected resource zoals een API (authorization)
   
  - Voorbeelden van identity providers
    - Microsoft Entra ID (cloud based)
    - Google, Amazon, Linkedin, Github

  - Single sing-on (SS0)
    - Geburiker logt 1 keer in en die credential geeft toegang to meerdere applicaties
    - SSO binnen 1 identity provider: 1 inlog, meerdere apps
    - Federation: 2 verschillende identity providers vertrouwen elkaar om gebruikers over grenzen heen te authenticeren


**Describe the concept of directory services and Active Directory**
  - Een directory is een hierarchische structuur die informatie opslaat over objecten op een netwerk. Een directory service maakt die data beschikbaar voor users, administrators, services en applicaties

  - Active Directory (AD)
    - Set van directory services ontwikkeld door Microsoft voor on-premises domain-based networks
    - Bekendste service: Active Directory Domain Services (AD DS)
    - AD DS slaat informatie op over domain members zoals devices en users, verifieert credentials en definieert access rights
    - Een server die AD DS draait is een domain controller (DC)
    - Centraal component in organisaties met een on-premises IT infrastructure
    - Beheert meedere on-premises componenten met 1 identity per user
   
  - Beperkingen van AD DS
    - Ondersteunt geen mobile devices
    - Ondersteunt geen SaaS applicaties
    - Ondersteunt geen monderne authentication methoden

  - Evolutie naar de cloud
    - Door groei van cloud services, SaaS applicaties en personal devices ontstond de behoefte aan modern authentication
    - Microsoft Entra ID (voorheen Azure AD) is het antwoord hierop
    - Onderdeel van de Microsoft Entra family
    - Biedt Identity as a Service IDaaS voor alle apps; zowel cloud als on-premises


**Describe the concept of federation**
  - Federartion maakt toegang mogelijk tot services over organisatie- domein grenzen heen door trust relationshops te configureren tussen identity providers. Geen aparte username en wachtwoord nodig per domein.

  - Hoe het werkt
    - Website in domain A gebruikt Identity Provides A (IdP-A)
    - User in domain B authenticeert met Identity Provider B (IdP-B)
    - IdP-A heeft een trust relationship geconfigureerd met IdP-B
    - Website accepteert de authenticatie van de user via trust relationship tussen IdP-A en IdP-B

  - Belangrijk:
    - Trust is niet altijd bidirectioneel; Als IdP-A IdP-B vertrouwt betekent dat niet automatisch dat IdP-B IdP-A vertrouwt
    - Moet apart geconfigureerd worden

  - Voorbeelden
    - B2B collaboration: inloggen met een account van een andere organisatie
    - Social identity provider: inloggen met Google account op een exterene applicatie

**Summary**
  - Authentication (AuthN) bewijst wie je bent
  - Authorization (AuthZ) bepaalt wat je mag
  - Idenitity is de nieuwe security perimeter; traditioneel netwerk niet meer voldoende door remote werken, BYOD, IoT en externe partners; 4 pillars: Administration, Authentication, Authorization en Auditing
  - Identity provider beheert identities centraal en geeft time-limited tokens uit; ID token voor authentication, access token voor authorization; SSO via 1 inlog voor meerdere apps;  federation tussen 2 identity providers via trust relationship
  - Active Directory (AD DS) is de on-premises directory service met domain controllers
    - Beperking: geen support voor mobile devices, SaaS of modern authentication; Microsoft Entra ID is de cloud-based opvolger van IDaaS
    - Federation geeft toegang over organisatiegrenzen via trust relationships tussen identity providers; trust is niet altijd bidirectional


---


  - **Learning Path 2:** Introduction to Microsoft Entra
    - **Module 1:** Describe the function and identity types of Microsoft Entra ID 
      - Extra Sources: FreeCodeCamp SC‑900 & John Savill's Technical Training
        
**Describe Microsoft Entra ID**
  - Microsoft Entra ID (voorheen Azure Active Directory) is Microsoft's cloud-based identity and access management service. Organistaies gebruiken het zodat medewerkers, gasten en anderen kunnen inloggen en toegang krijgen tot resources.
    - Interal resources: apps op het corporate netwerk, intranet en cloud apps van de organisatie zelf
    - External services: Microsoft 365, Azure portal en SaaS applicaties

  - Microsoft Entra ID kan gesynchroniseerd wowrden met on-premises Active Directory, andere directory services, of als standalone service gebruikt worden.

  - Identity Secure Score
    - Percentage dat aangeeft hoe goed je alighned bent met Microsoft's best practice aanbevelingen voor security
    - Helpt om je identity security posture te meten, verbeteringen te plannen en het succes van verbeteringen te reviewen

  - Basic terminology
    - Tenatn: een instance van Microsoft Entra ID voor 1 oragnistaie; bevat users, groups, devices, application, access en compliance policies; heeft een unieke teant ID en domeinnaam; fungeert als security en administrative boundary
    - directory: logische container binnen een tenat die alle identity en access management resources bevat; users,groups, applicaties, devices; vergelijkbaar met een database van identities. Een tenant heeft altijd maar 1 directory
    - Multi-tenant: organisatie met meer dan 1 instance van Microsoft Entra ID; bijvoorbeeld bij meerdere subsidiaries, fusies of geografische grenzen met verschillende regelgeving

  - Who uses Microsoft Entra ID
    - IT admins: toegang tot corporate apps en resources beheren, MFA instellen, identities en credentials beschermen
    - Developers: SSO toevoegen aan applicaties via standaarden, APIs gebruiken voor gepersonaliseerde app ervaringen
    - Subscribers: Azure, Microsoft 365 en Dynamics 365 gebruikers hebben automatisch toegang tot Microsoft Entra ID
      

**Describe types of identities**
  - Drie Categorieen:
    - Users: mensen
    - Fysieke devices
    - Software-based objects: workload identities

  - User identities: Vertegenwoordigen mensen zoals medewerkers en externe gebruikers. Gekarakteriseerd oor hoe ze authenticeren en hun user type property
    - Internal member: medewerker van organistatie; authenticeert intern via eigen microsoft Entra ID; UserType=member
    - External guest: consultants, vendors en partners; authenticeert via extern account of externe identity provider - UserType=Guest beperkte rechten
    - External member: gebruiker van een andere tenant die member-level toegang nodig heeft; authenticeert extern maar UserType=Member
    - Internal guest: intern account aangemaakt voor externe partij maar ingesteld als Guest; legacy scenario, B2B collaboration is nu gebruikelijker
   
  - Workload Identities: Identity toegewezen aan een software workload zodat die kan authenticeren en toegang krijgen tot andere services en resources. Moeilijker te beveiligen dan user identities omdat credentials veilig opgeslagen moeten wroden en het lastig is bij te houden wanneer een workload identity aangemaakt of ingetrokken meot worden
    - Applications en service principles: een service principal is een identity voor een applicatie; wordt aangemaakt wanneer een applicatie geregistreerd wordt in Microsoft Entra ID
    - Managed identities: type service principal dat automatisch beheerd wordt door Microsoft Entra ID; geen credentials nodig voor developers; gratis
      -  System-assigned: gekoppeld aan de lifecycle van 1 Azure resource; wordt automatisch verwijderd als de resource verwijderd wordt
      -  User-assigned: standalone identity die aan meerdere resources toegewezen kan worden; moet expliciet verwijderd worden

  - Device identities
    - Microsoft Entra registered: persoonlijke device (BYOD); geen organisatieaccount nodig om in te loggen op het device
    - Microsoft Entra joined: device gekoppeld aan zowel on-premises Active Directory als Microsoft Entra ID

  - Devices geregistreerd of joined aan Microsoft Entra ID krijgen SSO tot cloud-based resources. Microsoft Intune beheert devices via mobile device management (MDM) en mobile application management (MAM)

  - Groups: geeft toegangsrechten aan meerdere identities tegelijk in plaats van individueel; core principe van Zero Trust
    - Security groups: beheert user en device toegang tot gedeelde resources; leden kunnen users, devices, andere groepen en service principals zijn; vereist administrator rol
    - Microsoft 365 group: voor samenwerking; gedeelde mailbox, calender, SharePoint; alleen users als leden, geen administrator nodig
   
  - Groepen kunnen handmatig beheerd worden of via dynamic membership met automatische regels


**Describe hybrid identity**

  - Veel organisaties gebruiken zowel on-premises als cloud applicaties. Users verwachten overal makkelijk toegang. Hybrid identity zorgt voor 1 enkele identity voor authenticatie en autorisatie, ongeacht waar de applicatie staat.
  
  - Hybrid identity is accomplished through
    - Inter-directory provisioning: een identity aanmaken tussen twee verschillende directory servies; meest voorkomend scenario: user uit Active Directory provisioneren naar Microsoft Entra ID
    - Synchronization: zorgt ervoor dat identity informatie van on-premises users en groups overeenkomt met de cloud
   
  - Microsoft Entra Cloud Sync
    - Tool voor inter-directory provisioning en synchronization van users, group en contacts naar Microsoft Entra ID
    - Werkt via de Microsoft Entra cloud provisioning agent; een lichtgewicht brug tussen Microsoft Entra ID en Active Directory
    - Agent word on-premises of IaaS omgeving geinstalleerd
    - Provisioning configuratie wordt opgeslagen in Microsoft Entra ID
    - Gebruikt de SCIM specifatie; standaard voor het automatisch uitwisselen van user en group identity informatie tussen identity domains; wordt de de facto standaard voor provisioning


**Describe external identities**
  - Samenwerking met mensen buiten je organisatie vereist soms toegang to je apps en data voor externe gebruiekrs. Microsoft Entra External ID biedt oplossingen voor het werken met externe identities; van corporate accounts tot social identity providers zoals Google of Facebook

  - 2 Scenarios
    - Colloborate with business guests: samenwerken met externe partners en gasten
    - Secure your apps for consumers and business customers: authenticatie en identity management voor consumer apps
   
  - 2 tenant configurations
    - Workforce tenant: voor medewerkers, interne apps en organisatie resources; externe gasten en partners kunnen uitgenodigd worden
    - External tenant: exclusief voor External ID scenarios; voor het publiceren van apps naar conusmenten of zakelijke klanten
   
  - Collaborate with business guests - B2B collaboration
    - Deel company app en services met externe gasten terwijl je controle houdt over corporate data
    - Gasten loggen in met hun eigen credentials van hun eigen organisatie of identity provider
    - Geen aparte credentials nodig in jouw organisatie
    - Geschikt voor: Office 365 apps, SaaS apps en line-of-business applicaties

  - Secure your apps for consumers and business customers - CIAM
    - Customer Identity and Acces Management (CIAM) oplossing voor consumer apps
    - Functies: self-service registration, personalized sign-in experiences, SSO met social en enterprise identities, customer account management
    - Ingebouwd in Microsoft Entra ID; profiteert van platform features zoals security, compliance en scalability

**Summary**
  - Microsoft Entra ID is Microsoft's cloud-based IAM service; 1 tenant, 1 directory; synchroniseerbaar met on-premises Active Directory
  - Identities voor users (internal/external, member/guest), devices (registered, joined, hybrid joined) en workloads (service principals, managed identities)
  - Managed identities elimineren credential beheer voor developers; system=assigned aan 1 resource, user-assigned herbruikbaar
  - Groups voor toegangsbeheer (security) of samenwerking (Microsoft 365); handmatig of dynamic membership
  - Hybrid identity via Microsoft Entra Cloud Sync met SCIM; synchroniseert on-premises Active Directory naar cloud
  - External identities via B2B collaboration voor business gasten of CIAM voor consumer apps

---


  - **Learning Path 2:** Introduction to Microsoft Entra
    - **Module 2:** Describe the authentication capabilities of Microsoft Entra ID
      - Extra Sources: FreeCodeCamp SC‑900 & John Savill's Technical Training


**Describe authentication methods**
  - Passwords zijn de meest voorkomende vorm van authenticatie maar ook de meest kwetsbare. Microsoft Entra ID biedt meerdere authenticatiemethoden als aanvulling of vervanging

  - Passwords
    - Meest gebruikte vorm maar grootste risico bij single-factor authentication
    - Makkelijk te onthouden = makkelijk te hacken
    - Sterke passwords zijn moeilijk te onthouden; impact op productiviteit
   
  - Phone
    - SMS based authentication: gebruiker ontvangt verificatiecode via sms- kan als primary of secondary authenticatie gebruikt worden
    - Voice call verification: geautomatiseerde telefonische oproep waarbij gebruiker een nummer indrukt ter bevestiging; alleen als secondary authenticatie

  - OATH (open Authentication)
    - Open standaard voor time-based one-time password (TOTP) codes
    - Software OATH tokens: app genereert OTP op basis van een secret key vanuit Microsoft Entra ID
    - Hardware OATH tokens: fysiek apparaat zoals een key fob dat elke 30 of 60 seconden een code genereert
    - Alleen als secondary authenticatie voor SSPR of MFA
   
  - Passwordless authentication Vervangt passwords met sterkere methoden die moeilijker te copieren zijn door aanvallers.
    - Windows Hello for Business: combineert iets wat je hebt (device + certificate/key) met iets wat je weet (pin) of bent (biometrics); primary en secondary authenticatie
    - PIDO2: open standaard voor passwordless authenticatie via een externe security key (USB, Bluetooth of NFC) unphishable, primary en secondary authenticatie
    - Microsoft Authenticator app: app of iOS of Android; gebruiker bevestigt inlog via biometrics of PIN op telefoon; kan ook OATH verificatiecodes genereren; primary en secondary authenticatie
    - Certificate-based authentication (CBA): authenticatie via X.509 certificates direct tegen Microsoft Entra ID; alleen als primary passworldless authenticatie

  - Primary en secondary authentication
    - Primary: hoofdmethode bij inloggen
    - Secondary: aanvullende verificatie bij MFA of SSPR; niet alle methoden kunnen als primary gebruikt worden
   

  **Describe multifactor authentication**
  - MFA vereist meer dan 1 vorm van identificatie bij het inloggen. Verbetert de security van een identity aanzienlijk terwijl het eenvoudig blijft voor gebruikers
  - Three factors
    - Something you know: password of PIN
    - Something you have: telefoon of hardware key
    - Something you are: biometrics zoals vingerafdruk of face scan
   
  - Microsoft Entra ID verwerkt MFA automatisch zonder aanpassingen aan applicaties of services. Gebruikers kunnen kiezen uit de verificatiemethoden die ze geregistreerd hebben. Administrators kunnen bepaalde methoden verplichten
  - Supported verification methods
    - Microsoft Authenticator app
    - Windows Hello for Business
    - FIDO2 security key
    - OATH hardware token
    - OATH software token
    - SMS
    - Voice Call

  - Security defaults and multifactor authentication
    - Set van basis identity security mechanismen aanbevolen door microsoft
    - Gratis en automatisch toegepast wanneer ingeschakeld
    - Enforced: MFA registratie voor alle users, MFA verplicth voor administrators, MFA vereist voor alle users wanneer nodig
    - Geschikt voor organisaties die security willen verbeteren zonder complexe configuratie of voor organisaties opde gratis tier van Microsoft Entra ID
    - Minder geschikt voor organisaties met Microsoft Entra ID P1 of P2 licenties of complexere security requirements
   
      
**Describe self-service password reset**
  - Self-service password reset (SSPR) laat users hun wachtwoord zelf wijzigen of resetten zonder hup van een administrator of helpdesk
  - Key benefits
    - Verlaagt IT support kosten
    - Users kunnen sneller weer aan het werk
    - Administrators kunnen security instellingen aanpassen zonder inlog te verstoren
    - Bevat audit logs beschikbaar via een API; te importeren in een SIEM system
      
  - Requirements voor SSPR
    - Microsoft Entra ID licentie toegewezen
    - SSPR ingeschakeld door een administrator
    - Geregistreerd met authenticatiemethode; minimaal 2 aanbevolen
   
  - Available authentication methods
    - Mobile app notification
    - Mobile app code
    - Email
    - Mobile phone
    - Office phone
    - Security questions; alleen beschikbaar bij SSPR, niet bij normaal inloggen. Administrators kunnen geen security questions gebruiken
   
  - Belangrijke details
    - Administrator accounts zijn standaard ingeschakeld voor SSPR en vereisen 2 authenticatiemethoden
    - Administrators kunnen geen security questions gebruiken
    - Password write-back: wachtwoorden wordt ook teruggezet naar on-premises Active Directory zodat users direct kunnen inloggen op on-premises devices en applicaties
    - Email notificaties kunnen ingesteld worden bij SSPR events; bij admins accounts worden alle global admins genotificeerd
   

**Describe password protection and management capabilities**
  - Microsoft Entra password protection vermindert het risico dat users zwakke wachtwoorden instellen door bekende zwakke wachtwoorden en varienten te detecteren en blokkeren

  - Global banned password list
    - Automatisch bijgehouden en toegepast op alle users in een Microsoft Entra tenant
    - Beheerd door het Microsoft Entra ID Protection team op basis van real-world security telemtry data
    - Blokkeert bekende zwakke wachtwoorden en varianten via smart fuzzy-matching technieken
    - Kan niet worden uitgeschakeld
   
  - Custom banned password list
    - Admins kunnen eigen lijst aanmaken voor organisatiespecifieke termen
    - Voorbeelden: brand names, product names, locaties, interne termen en afkortingen
    - Gecombineerd met de global banned password list
    - Vereist Microsoft Entra ID P1 of P2 licentie

  - Protecting against password spray
    - Password spray attacks proberen een klein aantal zwakke wachtwoorden tegen alle accounts in een organisatie
    - Microsoft Entra password protection blokkeert alle bekende zwakke wachtwoorden die gebruikt worden bij password spray attacks
    - Gebaseerd op real-world security telemetry data van Microsoft Entra ID
   
  - Hybrid security
    - Microsoft Entra password protection kan geintegreerd worden in een on-premises Active Directory omgeving
    - On-premises component ontvangt de global banned password list en custom policies van Microsoft Entra ID
    - Domain controllers verwerken password change events met de lijsten
    - Zorgt ervoor dat password protection overal toegepast wordt waar een user zijn wachtwoord wijzigt


**Summary**
  - Passwords zijn de zwakste authenticatiemethode; vervangen of aanvullen met Phone, OATH tokens, Passwordless methodesn zoals Windows Hello for Business, FIDO2, Microsoft Authenticatior of Certificate-based authentications (CBA)
  - MFA vereist something you know, something you have en something you are; Microsoft Entra verwerkt dit automatisch, Security defaults zijn gratis en enforced basis MFA voor alle users
  - SSPR laat users zelf wachtwoord resetten zonder helpdesk; vereist licentie, admin activatie en minimaal 2 authenticatiemethoden; Password write-back synchroniseert naar on-premises Active Directory
  - Password protection blokkeert zwakke wachtwoorden via global banned password list en custom banned password list; beschermt tegen password spray attacks, werkt ook on-premises via hybrid security


---


  - **Learning Path 2:** Introduction to Microsoft Entra
    - **Module 3:** Describe access management capabilities of Microsoft Entra
      - Extra Sources: FreeCodeCamp SC‑900 & John Savill's Technical Training

**Describe Conditional Access**
  - Conditional Access is een feature van Microsoft Entra ID die een extra beveilingslaag toevoegt voordat geauthenticeerde users toegang krijgen tot data of resources. Werkt via policies die signalen analyseren zoals user, locatie, device, applicatie en risico om automatisch toegangbeslissingen te nemen
  - Conditional Acces Policies zijn if-then statements; bijvoorbeeld: als een user tot een bepaalde groep behoort, dan is MFA vereist.
  - Belangrijk: Conditional Access wordt toegepast na first-factor authentication; het is geen eerste verdedigingslinie tegen DoS aanvallen
  - Conditional access policy components: een policy bestaat uit twee componenten: assignments en access controls
  - Assignments bepaalt de who, what, where van de policy. Alle assignments zijn logisch AND; alle assignments moeten voldaan zijn om policy te activeren
      - Users: wie de policy includeert of excludeert; alle users, specifieke users en groups, directory roles, external guests en workload identities
      - Target resources:
        - Cloud apps: Microsoft applicaties, Office 365, Azure services en Microsoft Entra geregistreerde applicaties
        - User actions: policy gebaseerd op acties zoals het registreren van security informatie of het joinen van devices
        - Global Secure Access: beveiligen van traffic via Global Secure Acces service
        - Authentication context: extra beveiliging voor specifieke data of acties binnen applicaties

      - Network: toegang controleren op basis van netwerk of fysieke lokatie; trusted networks, IP ranges of named locations
      - Conditions:
        - Sign in risk: kans dat een sign in niet geautoriseerd is door de identity owner
        - User risk: kans dat een identity of account gecompromitteerd is
        - Insider risk: risicosignalen vanuit Microsoft Purview
        - Device platform: operating system van het device
        - Client apps: browser, mobiele app of desktop client
        - Filters for devices: policies targeten op specifieke device eigenschappen

      - Access controls
        - Bepaald hoe de polici gehandhaafd wordt na assignments
          - Block access: toegang volledig blokkeren
          - Grant access: toegang verlenen zonder of met extra controls zoals MFA, specifieke authenticatiemethoden, device compliance, of password change
          - Session: beperkte ervaring binnen specifieke cloud applicaties; bijvoorbeeld downloaden, kopieren of printen blokkeren voor gevoelige documenten, sign-in frequency isntellen of application enforced restrictions


**Describe Global Secure Access in Microsoft Entra**
  - Global Secure Access is microsoft's Security Edge (SSE) oplossing, gebouwd op Zero Trust principes. Het combineert Microsoft Entra Internet Access, Microsoft Entra Internet Acces for Microsoft Services en Microsoft Entra Private Access; samen met Microsoft Defender for Cloud apps; om netwerk, identity en endpoint access controls samen te brengen

  - SSE helpt organisaties met:
    - Verminderen van risico van lateral movement via gecompromitteerde VPN tunnel
    - Beveiligingsperimeter rondom internet-bassed assets
    - Betere service op remote locaties zoals branch offices

  - Microsoft Entra Internet Access
    - Identity-centric Secure Web Gateway (SWG) oplossing voor SaaS applicaties en internet traffic. Beschermt users, devices en data tegen internet-based bedreigingen.
      - Web content filtering: toegang tot websites reguleren op basis van content categorieen en domeinnamen
      - Universial Conditional Access: Conditional Access policies toepassen op alle internet bestemmingen, ook die niet gefedereerd zijn met Microsoft Entra ID
      - Universal Continuous Acccess Evaluation (CAE): apps en Microsoft Entra communiceren continu om user access up-to-date te houden; wijzigingen zoals locatie of security risico worden in near real time verwerkt

    - Vereist Microsoft Entra Suite of standalone microsoft Entra Internet Access licentie.

  - Microsoft Entra Internet Access for Microsoft Services
    - Directe connectiviteit naar Microsoft services zoals Echange Online, SharePoint Online en Microsoft Teams
    - Compliant network check: vereist dat users via Global Secure Access verbinen voordat ze toegang krijgen to mMicrosoft Entra ID applicaties; beschermt tegen token theft
    - Universal tenant restrictions; voorkomt data exfiltration naar ongeautoriseerde tenants of persoonlijke accounts
    - Source IP restoration: hersteld het originele IP adres van user in sign-in logs zodat locatie-based Conditional Access policies accuraat blijven
    - Enriched Microsoft 365 logs: gedetailleerde network traffic logs voor Microsoft traffic

  - Microsoft Entra Internet Access for Microsoft Services is included with a Microsoft Entra ID P1 or P2 license, making it available to a broad range of organizations
    
  - Microsoft Entra Private Access
    - Vervangt legacy VPNs met Zero Trust Network Access (ZTNA) aanpak; geeft per app toegang in plaats van brede netwerktoegang
      - Quick Access: admins definieren private resources via FQDN, IP adres of IP range en poorten; gegroepeerd in 1 applicatie met Conditional Access policies
      - Per app Access: meer granulaire aanpak waarbij elke enterprise applicatie eigen resource definities, users assignments en Conditional Access policies heeft

  - Global Secure Access dashboard
      - Dashboard in Microsoft Entra admin center met visualisaties van network traffic. Admins kunnen users, devices, cross-tenant access, web category filtering en device status monitoren
       
  - Securing AI Workloads
    - Global Secure Access zorgt ervoor dat traffic van AI services door dezelfde identity-aware security controls gaat als andere enterprise traffic; Conditional Access policies met compliant network checks, user risk, device state en locatie; Zero Trust principles uitgebreid naar AI workloads


**Describe Microsoft Entra roles and role-based access control (RBAC)**
  - Microsoft Entra roles beheren permissions voor Microsoft Entra resources. Role-based access control (RBAC) is het beheren van toegang via rollen

  - Built-in roles: Rollen met een vaste set van permissions die niet aangepast kunnen worden
    - Global administrator: toegang tot alle administratieve features in Microsoft Entra; wordt automatisch toegewezen aan de degene die de tenant aanmaakt
    - User administrator: aanmaken en beheren van users en groups, support tickets en service health monitoren
    - Billing administrator: aankopen doen, subscriptions en support tickets beheren, service health monitoren
   
  - Custom roles: Flexibele rollen die je zelf samenstelt uit een lijst van beschikbare permissions; dezelfde permissions als de built-in roles maar jij kiest welke je includeert
    - 2 stappen:
      - Stap 1: custom role definition aanmaken; permissions kiezen uit preset lijst
      - Stap 2: role assignment aanmaken; role toewijzen aan users of groups op een bepaalde scope

    - Scope bepaalt tot welke resources de role member toegang heeft:
      - Organization-wide scope: permissions over alle resources
      - Object scope: permissions over 1 specifieke resource zoals 1 applicatie
    - Vereist Microsoft Entra ID P1 of P2 licentie.
   
    - Least privilege: best practice: geef users alleen de toegang die ze nodig hebben. Beperk de schade bij een gecompromitteerd account; vooral belangrijk bij AI services die grote hoeveelheden data kunnen benaderen
   
    - Categories of Microsoft Entra roles
      - Microsoft Entra specific roles: beheren resources binnen Microsoft Entra ID; bijvoorbeeld User Admin, Application, Admin, Groups admin
      - Service-specific roles: beheren features binnen een specifieke Microsoft 365 service; bijvoorbeeld Exchange admin, Intune admin, SharePoint admin, Teams admin
      - Cross-over roles: spans meerdere services; bijvoorbeeld Security admin en Compliance admin
     
  - Difference between Microsoft Entra RBAC en Azure RBAC
    - Microsoft Entra RBAC: beheert toegang tot Microsoft Entra resources zoals users, groups en applicaties
    - Azure RBAC: beheert toegang tot Azure resources zoals virtual machines en storage via Azure Resource Management


**summary**
  - Passwords zijn de zwakste authenticatiemethode; aanvullen of vervangen met sterkere methoden zoals, MFA, passwordless of certificate-based authentication
  - MFA vereist something you know, something you have en something you are. Drastisch betere security
  - SSPR laat users zelf hun wachtwoord resetten zonder helpdesk. Vereist licentie, admin activatie en minimaal 2 authenticatiemethoden
  - Password protection blokkeert zwakke wachtwoorden via global en custom banned password lists, werkt ook on-premises via hybrid security
  - Conditional Access analyseert signalen zoals user, locatie, device en risico om automatisch toegang te verlenen, blokkeren of beperken via if-then policies
  - Global Secure Access is Microsoft's SSE oplossing gebouwd op Zero Trust; combineert Internet Access, Internet Access for Microsoft Services en Private Access voor netwerk, identity en endpoint beveiliging
  - Microsoft Entra RBAC beheert toegang via built-in en custom roles; altijd least privilege toepassen; verschil met Azure RBAC: Entra beheert identity resources, Azure beheert cloud infrastructure resources


---


  - **Learning Path 2:** Introduction to Microsoft Entra
    - **Module 4:** Describe the identity protection and governance capabilities of Microsoft Entra
      - Extra Sources: FreeCodeCamp SC‑900 & John Savill's Technical Training

**Describe Microsoft Entra ID Governance**
  - Identity governance oplossing die organisaties helpt de juiste mensen de juiste toegang te geven to de juiste resources; via AI-drivin insight, process automation en increased visibility
  - 4 kernvragen
    - Welke identities hebben toegang tot welke resources?
    - Wat doen die identities met die toegang?
    - Zijn er organizational controls voor toegangsbeheer?
    - Kunnen auditors verifieren dat de controls werken?

  - Identity lifecyle: Join, move en leave proces; digitale identity aanmaken, aanpassen en verwijderen op basis van HR signalen
    - Inbound provisioning: automatisch user identities aanmaken vanuit HR systemen zoals Workday of SuccesFactors
    - Lifecycle workflows: automatische taken bij key events zoals starten, van rol wisselen of vertrekken
    - Automatic assignment policies: automatisch group membership, app roles en SharePoint roles aanpassen op basis van user attributen
    - User provisioning: accounts aanmaken, updaten en verwijderen in andere applicaties
   
  - Access lifecyle: Beheren van toegang gedurende de gehele loopbaan van een user
    - Dynamic groups: Attribute-based rules bepalen automatisch group membership
    - Entitlement management: users kunnen toegang aanvragen via acces packages; separation of duties checks; recurring access reviews met AI-powered suggestions

  - Privileged access lifecycle: Monitoring en beheer van administrative rights
    - Microsoft Entra Privileged Identity Management (PIM): minimaliseert het aantal mensen met toegang tot resources in Microsoft Entra, Azure en andere Microsoft services; comprehensive governance controls
   
  - Identity governance for AI agents
    - Agent identities: accounts in Microsoft Entra ID voor AI agents; zelfde governance als human identities; verantwoorlijke persoon houdt toezicht; toegang vervalt wanneer niet meer nodig


**Describe access reviews**
  - Microsoft Entra Access reviews helpen organisaties group membership, toegang tot enterprise applicaties en role assignments efficient te beheren. Regelmatige access reviews zorgen ervoor dat alleen de juiste mensen toegang hebben
  - Use cases:
    - Te veel users in privileged roles: controleren wie administrative access heeft en gasten of partners verwijderen die dat niet meer nodig hebben
    - Business critical data access: users moeten peeriodiek bevestigen waarom ze toegang nodig hebben
    - Policy exception list: uitzonderingen op policies beheren en aan auditors bewijzen dat deze regelmatig gereviewed worden
    - Guest access in groups: group owners bevestigen of gasten nog legitieme toegang nodig hebben
    - Recurring reviews: access reviews instellen op wekerlijkse, maandelijkse, kwartaallijkse of jaarlijkse basis

  - Manage user and guest acces
    - Users of decision makers kunnen gevraagd worden om toegang te bevestigen of te ontkennen
    - Reviewers kijgen suggesties van Microsoft Entra ID
    - Admins kunnen voortang bijhouden; geen toegangswijzigingen totdat review voltooid is
    - Na afloop: handmatig of automatisch toegang verwijderen van users die het niet meer nodig hebben
   
  - Multi-stage access reviews
    - Ondersteunt tot drie review stages met meerdere typen reviewers
    - Zorgt voor compelexe workflows voor recertification en audit requirements
    - Vermindert het aantal beslissingen per reviewer

  - AI-Powered recommendations
    - Analyseert signalen zoals sign-in activity, user-to-group affiliation en andere contextdate
    - Suggereert of toegang goedgekeurd of geweigerd moet worden
    - AI-identified peer outliers: users met afwijkende toegangspatronen krijgen extra aandacht


**Describe entitlement management**
  - Identity governance feature die organisaties helpt de identity en access lifecycle op schaal te beheren via automatisering van access request workflows, access assignments, reviews en expiration

  - Uitdagingen die entitlement management oplost
    - Users weten niet welke toegang ze nodig hebben of wie het moet goedkeuren
    - Users houden toegang langer dan nodig
    - Toegang voor externe users is moeilijk consistent te beheren
   
  - Capabilities
    - Access packages delegeren aan non-administrators: packages bevatten resources die users kunnen aanvragen; managers definieren policies zoals wie kan aanvragen, wie goedkeurt en wanneer toegang verloopt
    - External users beheren: automatisch uitgenodigd bij goedkeuren; B2B account automatisch verwijderd als toegang verloopt en geen andere packages meer actief zijn
    - AI agent identities: entitlement management ondersteunt ook toegangsbeheer voor AI agents; sponsers zorgen dat toegang alleen actief is zolang nodig
   
  - Access packages: Bundle van alle resources die een user nodig heeft voor een project of taak:
    - Security groups
    - Microsoft 365 Groups
    - Enterprise applications
    - SharePoint Online sites

  - Microsoft Entra terms of use: Informatie presenteren aan users voordat ze toegang krijgen tot data of een applicatie; voor legal of compliance requirements
    - Use cases: voor toegang tot gevoelige data, op terugkerende basis, op basis van user attributen of voor alle users
    - Gepresenteerd als PDF; ook op mobile devices
    - Conditional Access policies vereisen acceptatie van terms of use voordat toegang verleend wordt
    - Admins kunnen zien wie akkoord is gegaan en wie heeft geweigerd


**Describe the capabilities of Privileged Identity Management**
  - PIM is een service in Microsoft Entra ID voor het beheren, controleren en monitoren van toegang tot belangrijke resources in Microsoft Entra ID, Azure en andere Microsoft online services zoals Microsoft 365 en Intune.
  - PIM kernmerken
    - Just in time: privileged acces alleen wanneer nodig
    - Time-bound: start- en einddatum voor toegang
    - Approval-based: specifieke goedkeuring vereist voor activatie
    - Visible: notificaties bij activatie van privileged roles
    - Auditable: volleidge access history te downloaden

  - Waarom PIM gebruiken
    - Minimaliseert het aantal mensen met toegang tot gevoelige resources
    - Beperkt risico van misbruik door time-limiting
    - Vereist justification en MFA bij activatie van een role
    - Biedt oversight over wat users doen met admin privileges

  - Wat kun je beheren met PIM
    - Microsoft Entra roles: built-in en custom roles voor Microsoft Entra ID en Microsoft 365
    - Azure roles: RBAC roles voor management groups, subscriptions, resource groups en resources
    - PIM for groups: just-in-time membership en ownership van groups; voor Microsoft Entra Roles, Azure roles, Azure SQL, Key Vault, Intune en non-Microsoft applicaties
   
  - General workflow
    - Assign: Roles toewijzen aan users, groups, service principals of managed identities; eligible assignments vereisen activatie, active assignments niet; met scope en duration
    - Activate: eligible users activeren de role voor een bepaalde duration met een reden
    - Approve or Deny: delegated approvers ontvangen notificaties en keuren request goed of af
    - Extend and renew: verlopen of bijne verlopen assignments kunnen verlengd of hernieuwd worden

  - Audit
    - Pim audit history toont alle role assignments en activaties van afgelopen 30 dagen voor alle privileged roles


**Describe Microsoft Entra ID Protection**
  - Helpt organisaties identity-based risks te detecteren, onderzoeken en remedieren; voor zwel user identities als workload identities. Risico;s kunnen doorgegeven worden aan Conditional Access voor toegangsbeslissingen of aan een SIEM tool voor verder onderzoek

  - Detect risks: Microsoft analyseert dagelijks signalen van Microsoft Entra ID, Microsoft accounts en Xbox om risico gedrag te detecteren
    - Sign-in risk: kans dat een authenticatieverzoek niet geautoriseerd is door de identity owner; voorbeelden: anonymous IP address, atypical travel, unfamiliar sign-in properties
    - User risk: kans dat een identity of account gecompromitteerd is; voorbeelden: leaked credentials, suspicious sending patterns, user reported suspicious activity
    - Belangrijk: ID Protection detecteert alleen risico's bij gebruik van correcte credentials; incorrecte credentials worden niet gemarkeerd
   
  - Investigate risks: 3 key reports voor administrators:
    - Risk detections: elk gedetecteerd risico wordt gerapporteerd
    - Risky sign-ins: sign-in waarbij 1 of meer risk detections zijn gerapporteerd
    - Risky users: user met 1 of meer risky sign-ins of risk detections
   
  - Remediate
    - Automatisch: risk-based Conditional Access policies dwingen controls af zoals strong authentication, MFA of secure password reset; bij succesvolle completion wordt het risico automatisch geremediated
    - Handmatig: administrator reviewt risico's en kan dismiss, confirm safe of confrim compromise uitvoeren

    - Export Data kan geexporteerd worden via Microsoft GRaph APIs naaR:
      - SIEM tools
      - Log Analytics workspace
      - Storage account
      - Event HUbs


**Describe Microsoft Entra Verified ID**
  - Managed verifiable credentials service gebaseerd op open standaarden. Automatiseert verificatie van identity credentials en maakt privacy-beschermde interactie mogelijk tussen oragnisaties en users

  - Why do we need it?
    - Moeilijk om digitale credentials cryptografisch beveiligd, privacy compiant en machine readable aan te bieden
    - Gebrek aan controle over hoe identity data gebruikt en gedeeld wordt na het verstrekken
   
    - How it works
      - Issuer: organisatie die claims bevestigt en digitaal gesigneerde credentials verstrekt; bijvoorbeeld een werkgever, universiteit of overheidsinstantie
      - User: ontvangt en beheert credentials in een digital wallet; presenteert credentials aan de verifier; claims zijn cryptografisch gesigneerd met de private key van de user
      - Verifier: vraagt bewijs op en verifieert of de claims voldoen aan de vereisten; bijvoorbeeld een werkgever of bank

  - Verifiable data registry: Onderliggend netwerk dat fungeert als trust systeem; bevat metadata en public keys; verifier leest metadata om credentials te verifieren
  - Microsoft Entra Verified ID: Gebruikt het did:web trust syteem waarbij de issuer's decentralized identifier (DID) gekoppeld is aan een web domein van de organisatie

  - Account recorvery met Verified ID
    - Helpt users toegang te herwinnen als alle authenticatiemethoden verloren zijn; anders dan SSPR vereist dit geen geregistreerde authenticatiemethode
    - Process: identity verificatie via trusted third-party provider; government-issued ID valideren; verifiable credential in MIcrosoft Authenticator; Face Check via Azure AI matcht selfie met ID foto; Temporary Access Pass (TAP) om in te loggen en authenticatiemethoden opnieuw te registreren

  - AI en verifiable credentials
    - Bescherming tegen AI-generated deepfakes en identity fraud
    - Verified ID bevestigt dat interacties echte, geverifieerde personen betreffen


**Describe Microsoft Entra integration with Microsoft Security Copilot**
  - Microsoft Security Copilot is een generative AI-powered security oplossing die AI en menselijke expertise combineert om administrators en security teams sneller en effectiever te laten reageren op aanvallen. Microsoft Entra is 1 van die plugins die Security Copilot van accurate informatie voorziet
  - Wat security Copilot doet met Microsoft Entra
    - Identity risks onderzoeken en oplossen
    - Identities en toegang beoordelen met AI-driven inteliignce
    - Sign-ins en risky users verkennen via natural language
    - Gaps in access policies vinden
    - Identity workflows generen
    - Security best practices aanbevelen

  - Standalone en embedded experiences
    - Standalone: via securitycopilot.microsoft.com; natural language promts gebruiken voor identity-related onderzoeken; gebruikersinformatie opvragen, siky sign-ins bekijken, audit logs analyseren
    - Embedded: ingebouwd in Microsoft Entra admin center workflows; bijvoorbeeld riksy users report in Identity Protection toont auotmiasch een Copilot samenvatting van het risiconiveau en aanbevelingen


**Summary**
  - ID Governance zorgt dat de juiste mensen de juiste toegang hebben via identity lifecycle (join,move,leave), access lifecycle (dynamic groups, entitlement management) en privileged acces lifecyle (PIM)
  - Access reviews controleren periodiek wie nog toegang nodig heeft; ondersteunt multi-stage reviews en AI-powered aanbelevlingen
  - Entitlement management automatiseert acces request workflows via access packages; beheert ook external users en AI agent identities; terms of use via Conditional Acces afdwingen
  - PIM geeft just-in-time, time-bound en approval-based toegang tot privileged roles; auditable en vereist justification en MFA; werkt voor Microsoft Entra roles, Azure roles en groups
  - ID Protection detecteert sign-in risk en user risk via dagelijkse signaalanalyse; drie reports: risk detections, risky sign-ins en risky users; automatische of handmatige remediation via Conditional Access; exporteerbaar naar SIEM
  - Verified ID is een verifiable credentials service met issuer, user en verifier; gebruikt did:web trust syteem; ondersteunt account recovery via Face Check en Temporary Acces Pass
  - Security Copilot integreert met Microsoft Entra voor AI-driven identity onderzoeken via standalone en embedded experiences; gespecialisserde agents voor access reviews, Conditional Access optimalisatie en identity risk management


---


  - **Learning Path 3:** Introduction to Microsoft security solutions
    - **Module 1:** Describe Microsoft Security Copilot
      - Extra Sources: FreeCodeCamp SC‑900 & John Savill's Technical Training
        
**Get acquainted with Microsoft Security Copilot**
  - Microsoft Security Copilot is een AI-powered, cloud-based security analyse tool die analysts helpt om bedreigingen snel te onderzoeken, signalen op machine speeds te verwerken en risico's sneller te beoordelen

  - Top security uitdagingen
    - Toenemend aantal complexiteit van aanvallen
    - Tekort aan security talent; behoefte aan automatisering en consolidatie van tools
    - Zichtbaar in security, privacy, compliance en governance

  - Use cases
    - Investigate and remediate security threats: complexe security alerts omzetten naar bruikbare samenvattingen met stap-voor-sap response guidance
    - Build KQL queries or analyze suspicious scripts: technische taken uitvoeren via natural language zonder handmatig scripts te schrijven
    - Understand risks and manage security posture: breed inzicht van de omgeving met geprioriteerde risico's
    - Troubleshoot IT issues faster: relevante informatie snel samenvatten en actionable insights geven
    - Define and manage security policies: policies definieren, conflicten controleren en samenvatten
    - Configure secure lifecycle workflows; groups aanmaken en access parameters instellen met stap-voor-stap guidance
    - Develop reports for stakeholders: duidelijke rapporten genereren afgestemd op het publiek
   
  - Standalone en embedded experience
    - Standalone: via de dedicated site; gebruikers communiceren via natural language in de promt bar; output als tekst, afbeeldingen of documenten
    - Embedded: Copilot capabilities ingebouwd in Microsoft security producten zoals Microsoft Defender XDR; incident samenvatten, scripts analyseren, KQL queries genereren
   
  - Natural Language Processing (NLP)
    - Gebouwd op Azure OpenAI Service met Large Language Models (LLMs)
    - Kan menselijke taal lezen, begrijpen en verwerken
    - LLMs geven brede algemene kennis maar zijn ook getraind op security specifieke bronnen

  - Integration with security-specific sources
    - Combineert LLMs met Microsofts global threat intelligence; meer dan 65 biljoen dagelijkse signalen
    - Integreert via plug-ins met Microsoft security producten; non-Microsoft producten en open-source intelligence feeds
    - Verbinding met organisatie knowledge bases voor meer context en relevante responses
    - Jouw data wordt niet gebruikt om de AI modellen te trainen


**Describe Microsoft Security Copilot terminology**
  - Terminology
    - Session: en gesprek binnen Copilot; Copilot onthoudt de conext binnen een sessie
    - Promt: een specifieke vraag of opdracht die je invoert in de promt bar
    - Capability: een functie die Copilot gebruikt om een deel van een probleem op te lossen; ook wel skill genoemd
    - Plugin: een verzameling van capabilities voor een specifieke resourc
    - Workspace: een aparte Copilot werkomgeving binnen de tenant
    - Agents: AI-powered tools die autonoom security en IT taken beheren
    - Orchestrator: het systeem dat capabilities combineert om een promt te beantwoorden

  - Promt bar en sessions
    - Prompt bar is het centrale punt van Security Copilot; je geeft hier opdrachten in natural language
    - Wees specifiek in je promts voor betere resultaten
    - Copilot promtbooks met voorgeselecteerde prompts voor minder ervaren gebruikers
    - De hele dialoog van vraag en antwoord heet een session; context wordt bijgehouden binnen een sessie
   
  - Plugins and capabilities
    - Plugins integreren Copilot met externe bronnen zoals Microsoft Sentinel, Microsoft Defender XDR en Microsoft Intune
    - Elke plugin biedt een verzameling van capabilities specifiek voor die databron
    - Voorbeelden van Defender XDR capabilites: incident samenvatten, scripts analyseren, KQL queries genereren, incident reports maken
    - Ondersteunt Microsoft plugins, non-microsoft plugins zoals ServiceNow en Splunk, en custom plugins
    - Soomige plugins vereisen configuratie of authenticatie

  - Workspaces
    - Aparte werkomgevingen binnen een tenant; vergelijkbaar met kamers in een huis
    - Tenant = het huis, workspace = een kamer
    - Gebruikers kunnen toegang hebben tot bepaalde workspaces op basis van hun rol
    - Voordelen: kosten monitoren per team, sessiedata opslaan volgens geo-specifieke regelgeving en lokale data protection wetgeving

  - Agents
    - Geavanceerde AI-powered assistants die verder gaan dan alleen vragen beantwoorden
    - Kunnen autonoom high-volume security en IT taken beheren
    - Geintegreerd met Microsoft security tools en partner oplossingen
    - Leren van feedback en passen zich aan aan de workflows van de organisatie
    - Werken binnen Microsoft Zero Trust framework
   
  - Orchestrator
    - Het systeem dat capabilities combineert om een promt te beantwoorden
    - Composeert meerdere capabilities samen tot 1 coherent antwoord


**Describe how Microsoft Security Copilot processes prompt requests**
  - Process flow
    - Submit a promt: Het proces begint wanneer een gebruiker een promt invoert in de promt bar
    - Orchestrator: De promt gaat naar de copilot-backend, de orchestrator. Deze bepaalt de initiele context en stelt een plan op door beschikbare capabilities (skills) te combineren om de vraag te beantwoorden
    - Build context: Zodra het plan staat, voert Copilot dit uit om alle benodigde data en context op te halen
    - Plugins: Tijdens het uitvoeren van het plan analyseert Copilot alle beschikbare data, patronen en plugin-bronnen om relevante inzichten te genereren.
    - Responding: Copilot combineert alle verzamelde informatie en gebruikt het LLM om een reactie te formuleren die logisch en begrijpelijk is voor een mens
    - Response: De reacie wordt geformatteerd en gecontroleerd volgens Microsoft's Responsible AI-richtlijnen voordat deze wordt teruggestuurd
    - Recieves response: De gebruiker ontvangt de uiteindelijke reactie van Copilot

  - Process log
    - Tijdens het verwerken van prompt genereert Copilot een zichtbaar process log
    - Dit log toont welke capability is gebruikt, zodat de gebruiker kan beoordelen of de informatie uit een betrouwbare bron komt
    - Het log laat ook zien dat de output safety checks heeft doorlopen, onderdeel van Microsoft's Responsible AI-commitment
 

**Describe the elements of an effective prompt**
  - Een effectieve prompt geeft Microsoft Security Copilot voldoende richting, context en beperkingen om een waardevolle, bruikbare reactie te genereren. De kwaliteit van de output hangt sterk af van hoe duidelijk, specifiek en volledig de promt is

  - Wat een effectieve prompt bevat: bestaat uit 4 kernonderdelen die samen bepalen hoe Copilot redeneert en welke data het gebruikt
    - Goal: Het concrete security-doel of de specifieke informatie die je nodig hebt. Dit kan een vraag, opdracht of instructie zijn
    - Context: Waarom je deze informatie nodig hebt of hoe je de output gaat gebruiken. Denk aan tijdsperiode, relevant incident, of dat het bedoeld is voor een rapport.
    - Expections: De gewenste vorm van de output, zoals een tabel, lijst met acties, samenvatting, diagram of doelgroepgerichte tekst
    - Source: Bekende informatie, relevantie data sources of specifieke plugins die Copilot moet gebruiken. Sommige plugins hebben extra context nodig om goed te functioneren
   
  - Voorbeelden van hoe deze elementen werken
    - Goal: Informatie over een threat actor
    - Contect: Je gebruikt het voor een incidentrapport
    - Expectations: Een lijst met IoCs en TTPs
    - Source: Microsoft Defender XDR data of specifieke plugins
  - Deze vier elementen vormen samen de basis voor een prompt die Copilot effectief kan verwerken

  - Additional prompting tips: Naast de 4 basiselementen zijn er aanvullende richtlijnen die helpen om betere resultaten te krijgen
    - Schrijf duidelijk, specifiek en beknopt
      - Basic prompt: Pearl Sleet actor
      - Better prompt: Give me information about Pearl Sleet activity, including know IoCs and TTPs
    - Itereer op je prompts
      - LLM-systemen kunnen verieren in hun antwoorden. door vervolgprompts te geven kun je verfijnen, verduidelijken of alternatieve invalshoeken proberen
    - Geef voldoende context
      - Basic prompt: Summarize incident 15134
      - Better prompt: Summarize incident 15314 in Microsoft Defender XDR into a paragraph for my manager and list all involed intities
    - Gebruik positieve instructies
      - Basic prompt: Give me list of unmanaged devices
      - Better prompt: Give me a list of high-risk unmanaged devices, Exlude devices named "test"
    - Spreek Copilot direct aan
      - Gebruik you should of you must, omdat dit duidelijker is dan het model indirect aanspreken

  - Flexibiliteit in promtopbouw
    - Hoewel deze richtlijnen helpen om sterke prompts te schrijven, ben je niet beperkt tot een vaste structuur. Copilot is ontworlpen om natuurlijke taal te begrijpen, dus je kunt prompts formuleren op een manier die voor jou logisch voeld. De 4 elementen en tips zijn hulpmiddelen, geen verplicht format


**Describe how to enable Microsoft Security Copilot**
  - Provision Capacity
    - Security Copilot werkt met provisioned capactiy (per uur betaald) en overage capacity (op gebruik betaald)
    - De rekeneenheid heet Security Compute Unit (SCU); dit wordt gebruikt in zowel de standalone als ambedded ervaring
    - Je kunt overage SCUs instellen (unlimited of een maximum) voor onverwachte pieken in gebruik
    - Vereisten om capacity te provisionen:
      - Een actief Azure subscription
      - Minimaal de rol Azure Owner of Azure Contributor op resource group niveau
      - Let op: een Global Microsoft Entra Administrator heeft deze Azure rollen niet automatisch
    - Er zijn 2 manieren om capacity in te stellen:
      - Via Security Copilot zelf (aanbevolen); een wizard begeleidt je door het proces
      - Via de Azure Portal; handmatig de gegevens invoeren
    - Minimum: 1 SCU; Maximum 100 SCUs
    - Na het inrichten komt er een usage monitoring dashboard beschikbaar met tot 90 dagen aan data, inclusief welke plugins gebruikt zijn en door wie
   
  - Set Up the Default Enviroment
    - Vereiste rol: minimaal Security Administrator
    - Tijdens de setup configureer je de volgende instellingen:
      - SCU capacity; koppel de eerder ingerichte capacity aan de workspace (elke workspace heeft zijn eigen capacity)
      - Data storage; kies in welke regio klantdata opgeslagen wordt (bv EU, UK, US, Aus, Japan, Canada, Z-A)
      - Prompt evaluation; beperk dit tot jouw geo of sta wereldwijde evaluatie toe
      - Microsoft Purview audit logging; optioneel inschakelen voor het opslaan van admin- en gebruikersacties en Copilot-responses
      - Data sharing opties (per workspace)
          - Toestaan dat Microsoft data gebruikt om productprestaties te valideren via human review
          - Toestaan dat Microsoft data gebruikt om het security AI model te verbeteren; dit geeft Microsoft geen toestemming om foundational models te trainen met jouw data
      - Plugin settings; beheer wie plugins mag toevoegen, welke plugins beschikbaar zijn voor de organisatie, en of Copilot toegang krijgt tot Microsoft 365 services
     
  - Role Permissions
    - Permissies worden per workspace ingesteld
    - Gebruik altijd het principe van least privilege
    - Er zijn 2 soorten rollen die toegang geven:
      - Microsoft Entra ID roles (bredere scope, niet alleen Copilot)
        - Global Admin
        - Security Admin
        - Security Operator
        - Security Reader
      - Microsoft Security Copilot roles (aleen voor Copilot platform:
        - Copilot Owner; volledige beheertoegang
        - Copilot Contributor; gebruikerstoegang
        - Security Admin en Global Admin erven automatisch de Copilot Owner rol
        - Alleen owners/admins kunnen rol-toewijzingen doen in Copilot
        - Er is een speciale groep: Recommended Microsoft Security roles; Voeg je deze toe als Contributor, dan krijgen alle gebruikers met relevante Entra ID rollen automatisch toegang tot Copilot

  - Copilot Plugins en Role Requirements
    - Copilot gaat nooit verder dan de toegang die jij hebt; je eigen rechten bepalen wat Copilot kan doen
    - Individuele plugins hebben soms eigen rolvereisten, naast je Copilot-rol. Voorbeeld:
      - Microsoft Sentinel plugin; vereist minimaal de rol Sentinel Reader
      - Microsoft Intune plugin; vereist iets als de Intune Endpoint Security Manager rol
    - De meeste Microsoft plugins gebruiken het OBO-model (On Behalf Of); Copilot logt automatisch in op gekoppelde producten als de plugin is ingeschakeld
    - Plugin-instellingen worden per workspace beheerd

**Summary**
  - Microsoft Security Copilot is een AI-powered, cloud-based security tool gebouwd op Azure OpenAI Service en getraind op meer dan 65 biljoen dagelijkse threat intelligence signalen.
  - Het helpt security analysts om bedreigingen sneller te onderzoeken, risico's te beoordelen en technische taken uit te voeren via natural language.
      - Beschikbaar als Standalone (eigen portal) en Embedded in producten zoals Microsoft Defender XDR
      - Werkt via plugins (integraties met Microsoft- en non-Microsoft producten zoals Microsoft Defender XDR
      - Verwerkt prompts via orchestrator die capabilities combineert en output toetst aan Responsible AI-richtlijnen
      - Een effectieve prompt bevat: Goal, Context, Expectations en Source
      - Capacity wordt gemeten in SCUs en vereist minimaal een Azure Owner/Contributer rol om in te richten
      - Role Permissions worden per workspace ingesteld; Copilot gaat nooit verder dan de toegangsrechten van de gebruiker zelf



  - **Learning Path 3:** Introduction to Microsoft security solutions
    - **Module 2:** Describe core infrastructure security services in Azure 
      - Extra Sources: FreeCodeCamp SC‑900 & John Savill's Technical Training

**Describe Azure DDoS protection**
  - Distributed Denial of Service Attacks: een aanval probeert de resources van je applicaties en server te overbelasten zodat echte gebruikers er niet meer bij kunnen. de 3 meest voorkomende typen:
    - Volumetric attacks: Overspoelen het netwerk met schijnbaar legitiem verkeer zodat echte traffic er niet doorheen komt
    - Protocol attacks: Misbruiken zwakheden in layer 3 (network) en layer 4 (transport) protocollen om serverresources uit te putten
    - Resource (application) layer attacks: richten zich op web application packets om datacommunicatie tussen hosts te verstoren

  - What is Azure DDoS Protection?
      - Azure DDoS Protection analyseert binnenkomend netwerkverkeer en filtert alles eruit dat op een aanval lijkt. Het beschermt op layer 3 en layer 4.
      - Belangrijkste functies:
        - Always-on traffic monitoring: 24/7 monitoring; bij detectie wordt aanvalsverkeer automatisch omgeleid en gefilterd, en word je binnen enkele minuten gewaarschuwd via Azure Monitor
        - Adaptive real time tuning; leert jouw applicatieverkeer over tijd en pas het profiel automatisch aan
        - Telemetry, monitoring en alerting; rijke telemetrie via Azure Monitor; integratie mogelijk met Azure Event Hubs, Azure Monitor logs en Azure Storage

  - Tiers
      - DDoS Network Protection: Uitgebreidere bescherming, automatisch afgestemd op Azure resources binnen een virtual network; inclusief extra services zoals DDoS rapid response support, cost protection en kortingen op WAF
      - DDoS IP Protection: Pay-per-protected IP model; bevat dezelfde kern-engineeringfuncties maar zonder de extra value-addes services

  - Waarom niet vertrouwen op standaard Azure infrastructurebescherming
    - De standaard infrastructurebescerming heeft een hogere drempel dan de meeste applicaties aankunnen
    - Biedt geen telemetry of alerting
    - Azure DDoS Protection geeft dedicated monitoring met applicatiesspecifieke drempelwaarden en een profiel afgestemd op jouw verwachte traffic

    - Voor bescherming op layer 7 (application layer) heb je aanvullend een Web Application Firewall (WAF) nodig
   
  
        


































