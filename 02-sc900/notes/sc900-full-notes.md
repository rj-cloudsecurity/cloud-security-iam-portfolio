# SC-900: Security, Compliance, and Identity Fundamentals — Study Notes

  - **Started:** 16-3-2026
  - **Exam passed:** -

---

  - **Learning Path 1:** Introduction to Security, Compliance, and Identity
    - **Module 1:** Describe Security and Compliance Concepts
      - Extra Sources:*FreeCodeCamp SC‑900 & John Savill's Technical Training*

        
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

      
---


  - **Learning Path 1:** Introduction to Security, Compliance, and Identity
    - **Module 2:** Describe identity concepts 
      - Extra Sources:*FreeCodeCamp SC‑900 & John Savill's Technical Training*

        
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


---


  - **Learning Path 2:** Introduction to Microsoft Entra
    - **Module 1:** Describe the function and identity types of Microsoft Entra ID 
      - Extra Sources:*FreeCodeCamp SC‑900 & John Savill's Technical Training*

        
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


---


  - **Learning Path 2:** Introduction to Microsoft Entra
    - **Module 2:** Describe the authentication capabilities of Microsoft Entra ID
      - Extra Sources:*FreeCodeCamp SC‑900 & John Savill's Technical Training*


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
   

---


  - **Learning Path 2:** Introduction to Microsoft Entra
    - **Module 2:** Describe the authentication capabilities of Microsoft Entra ID
      - Extra Sources:*FreeCodeCamp SC‑900 & John Savill's Technical Training*

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





























