# AZ-104: Azure Administrator Associate

  - **Started:** 11-4-2026
  - **Exam passed:** -

  ---

## Inhoudsopgave

### Learning Path 1: Prerequisites for Azure administrators

- [Module 1: Introduction to Azure Cloud Shell](#module-1-Introduction-to-Azure-Cloud-Shell)

- [Module 2: Deploy Azure infrastructure by using JSON ARM templates](#module-2-Deploy-Azure-infrastructure-by-using-JSON-ARM-templates)

---

## Learning Path 1: Prerequisites for Azure administrators
### Module 1: Introduction to Azure Cloud Shell

**What is Azure Cloud Shell?**
  - Azure Cloud Shell is een command-line omgeving die je via de browser kunt openen om Azure resources te beheren zoals VMs, storage en networking; vergelijkbaar met Azure CLI of Azure PowerShell
  - Microsoft beheerd Cloud Shell, waardoor je altijd toegang hebt tot de meest recente versies van de Azure CLI en PowerShell modules, zonder dat je zelf updates hoeft bij te houden
  - Cloud Shell is gekoppeld aan je eigen account en bijbehorende permissions, en draait op een infrastructuur met double encryption at rest standaard ingeschakeld
  - Cloud Shell biedt cloud storage om bestanden te bewaren tussen sessies door, zoals SSH keys en scripts; ook toegankelijk vanaf verschillende machines
  - Via de ingebouwde Cloud Shell editor kun je bestanden die in die cloud storage staan direct bewerken vanuit de Cloud Shell interface

**How does Azure Cloud Shell work?**
  - Cloud Shell is toegankelijk via 3 manieren: direct via https://shell.azure.com, vanuit de Azure portal, of via code snippets in Microsoft Learn
  - Bij het openen van een Cloud Shell sessie wordt een tijdelijke host aangemaakt, vooraf geconfigureerd met de laatste versies van PowerShell en Bash; je kiest zelf welke command-line omgeving je wilt gebruiken
  - Sessies worden automatisch beeindigd na 20 minuten inactiviteit. Bestanden op de CloudDrive blijven bewaard, maar je moet een nieuwe sessie starten om weer toegang te krijgen.
  - Bestanden kun je opslaan via de Azure CloudDrive, zodat je ze vanuit een andere sessie of een ander apparaat kunt benaderen
  - Je kunt ook een Azure Storage File Share koppelen aan Cloud Shell, die gekoppeld is aan een specifieke regio. Zo heb je toegang tot de inhoud van die share vanuit Cloud Shell
  - Bestanden op de CloudDrive of File Share kun je bewerken via de Cloud Shell editor; te openen via het {} icoon, of via het commando code <bestandsnaam. Let op: het code commande werkt alleen in de classic mode.
  - Cloud Shell sessies komen standaard met een uitgebreide set vooraf geconfigureerde tools, verdeeld in categorieen:
    - Linux tools; bash, zsh, sh. tmux, dig
    - Azure tools: Azure CLI, AzCopy, Azure Functions CLI, Service Fabric CLI
    - Text editors; code, vim, nano, emacs
    - Source control: git
    - Build tools; make, maven, npm, pip
    - Containers; Docker Machine, Kuberctl, Helm
    - Databases; MySQL client, PostgreSQL client, sqlcmd
    - Other; Terraform, Ansible, Puppet Bolt, HashiCorp Packer, Office 365 CLI

**When should you use Azure Cloud Shell?**
  - Gebruik Cloud Shell wel als je:
    - Een beveiligde command-line sessie wilt openen vanuit elke browser, zonder installatie van plug-ins of add-ons op je apparaat.
    - Bestanden wilt bewaren tussen sessies door
    - Wilt werken in Bash of PowerShell, naar eigen voorkeur
    - Scripts of bestanden wilt bewerken via Cloud Shell editor

  - Gebruik Cloud Shell niet als je:
    - Een sessie langer dan 20 minuten open wilt laten voor langlopende scripts; de sessie wordt zonder waarschuwing verbroken en de huidige staat gaat verloren
    - Admin permissions nodig hebt zoals sudo access binnen Azure CLI of PowerShell
    - Tools wilt installeren die niet ondersteund worden in de beperkte Cloud Shell omgeving en een custom VM of container vereisen
    - Storage uit meerdere regio's nodig hebt; Cloud Shell ondersteunt slechts 1 regio per storage-allocatie, wat back-up en synchronisatie vereist
    - Meerdere sessies tegelijk nodig hebt; Cloud Shell staat slechts 1 instance tegelijk toe en is niet geschikt voor gelijktijdig werk over meerdere subscriptions of tenants

**Summary**
  - Azure Cloud Shell is een browser toegankelijk command-line omgeving voor het beheren van Azure resources; geen lokale installatie van Azure CLI of PowerShell vereist
  - Je kiest zelf o je werkt in Bash of PowerShell, direcht vanuit de browser
  - Cloud Shell biedt mechanismen om bestanden tussen sessies te bewaren, en geeft toegang tot minimalistische versie van Visual Studio Code editor voor complexere bewerkingen


---


## Learning Path 1: Prerequisites for Azure administrators
### Module 2: Deploy Azure infrastructure by using JSON ARM templates

**Explore Azure Resource Manager template structure**
  - Wat is infrastructure as code?
    - Infrastructure as a code (IaC) betekent dat je je infrastructuur beschrijft via code, net zoals applicatiecode; opgeslagen en geversioneerd in dezelfde source repository.
    - Voordelen: consistent configurations, improved scalability, faster deployments, better traceability
   
  - Wat is ARM template
    - Arm templates zijn JSON-bestanden die de infrastructuur en configuratie voor een deployment definieren.
    - Ze gebruiken declarative syntax; je beschrijft wat je wilt deployen, nie hoe. Dit staat tegenover imperative syntax. waarbij je elke stap handmatig specificeert
   
  - Benefits of using ARM templates
    - ARM templates zijn idempotent: je kunt dezelfde template meerdere keren resources waar mogelijk parallel aan; sneller dan scripted deployments
    - Ingebouwde validatie: de template wordt gecontroleerd voor de deployment start.
    - Templates zijn op te splitsen in kleinere, herbruikbare componenten die je kunt linken of nesten
    - Integreerbaar met CI/CD tools zoals Azure Pipelines en GitHub Actions
   
  - ARM template file structure
| Element | Verplicht | Beschrijving |
|---|---|---|
| schema | Ja | Locatie van het JSON schema bestand |
| contentVersion | Ja | Versienummer van de template (bijv. 1.0.0.0) |
| apiProfile | Nee | Verzameling van API versions per resource type |
| parameters | Nee | Waarden die je opgeeft tijdens deployment |
| variables | Nee | Waarden om template expressions te vereenvoudigen |
| functions | Nee | User-defined functions voor hergebruik binnen de template |
| resources | Ja | De resources die je wilt deployen of updaten |
| output | Nee | Waarden die worden teruggegeven na deployment |

  - Deploy an ARM template to Azure
    - 3 manieren:
      - Deploy a local template
      - Deploy a linked template
      - Via een CI/CD pipeline
    - Voor een lokale deployment heb je Azure CLI of Azure PowerShell nodig
    - Stappen:
      - Resource group aanmaken
      - Deployment starten met:
        - (CLI) az deployment group create
        - PowerShell: New-AzResourceGroupDeployment

  - Add resources to the template
    - Resources voeg je toe via syntax {resource-provider}/{resource-type}
      - bv Microsoft.Storage/storageAccounts
    - Per resource type defineer je verplichte properties zoals
      - type
      - apiVersion
      - Name
      - Location
      - sku
      - kind
        
**Exercise - Create and deploy an Azure Resource Manager template**
- [Exercise 1 Create and deploy an Azure Resource Manager template](/03-az104/exercises/1-create-and-deploy-an-azure-resource-manager.md)

**Add flexibility to your Azure Resource Manager template by using parameters and outputs**
  - ARM-template parameter
    - Parameters maken een ARM template herbruikbaar door waarden zoals SKU, naam of capaciteit per deployment te kunnen varieren; zonder de template zelf aan te passen
    - Je kunt parameters meegeven via de command line of via parameter file
    - Maximum aantal parameters per template is 256
    - Beschikbare properties per parameter: type, defaultValue, allowedValues, minValue, maxValue, minLength, maxLength, en metadata (description
    - Toegastane parameter types: string, secureString, integer, boolean, object, secureObject, array

  - Aanbevelingen voor parameter
    - Gebruik parameters voor omgevingsafhankelijke instellingen zoals SKU, grootte of capaciteit, en voor resource namen
    - Geef altijd een description mee en gebruik default values waar mogelijk
    - Hardcode nooit gebruikersnamen of wachtwoorden; gebruik altijd parameter met type secureString of secureObject. Deze waarden zijn na deployment niet meer uit te lezen
   
  - Parameter gebruiken in een ARM template
    - Parameter definitie staat in de parameters sectie van de template
    - Referentie in de resource definitie via de syntax [parameters('parameternaam')]
    - Bij deployment meegegeven via CLI: --parameters storageAccountType=Standard_LRS

  - ARM template outputs
    - In de outputs sectie geef je aan welke waarden worden teruggegeven na een succesvolle deployment
    - Beschikbare properties: condition (optioneel, boolean), type, value (optioneel, expression), copy (optioneel, voor meerdere output waarden)
    - De reference () functie haalt de runtime state van een resource op, bijvoorbeeld voor het teruggeven van storage endpoints

  - Deploy an ARM template again
    - ARM templates zijn idempotent: opnieuw deployen naar dezelfde omgeving zonder wijzigingen heeft geen effect
    - Alleen gewijzigde waarden worden opnieuw deployed. Resources worden aangemaakt als ze nog niet bestaan, of bijgewerkt als er een wijziging is

**Exercise - Add parameters and outputs to your Azure Resource Manager template**
- [Exercise 2 Add parameters and outputs to your Azure Resource Manager template](/03-az104/exercises/2-add-parameters-and-outputs-to-your-azure-resource-manager-template.md)


**Summary**
  - ARM Templates zijn JSON-bestanden voor het deployen van Azure infrastructuur via declarative syntac (IaC). Templates zijn idempotent, hebben ingebouwde validatie, en bestaan uit verplichte elementen (schema, contentVersion, resources) en optionele elementen (parameters, variables, functions, outputs)
    - Parameters maken templates herbruikbaar met ondersteuning voor allowedValues, defaultValue en beveiligde types zoals secureString
    - Outputs geven waarden terug na deployment via de reference () functie
    - Deployments via CLI:az deployment group create
    - Deployments via PowerShell: New-AzResourceGroupDeployment



---



## Learning Path 2: Manage identities and governance in Azure
### Module 1: Understand Microsoft Entra ID 


**Examine Microsoft Entra ID**
  - Microsoft Entra ID is een PaaS directory service beheerd door Microsoft in de cloud; geen eigen infrastructure nodig, maar ook minder controle over de implementatie
  - Verschil met AD DS: AD DS draait als service op Windows Server (domain controller) en is gericht op on-premises apps. Entra ID is gericht op web-based appes en cloud resources
  - Mogelijkheiden: SSO, MFA, identity protection, SSPR, Conditional Access, Application Proxy, federation tussen organisaties
  - Gratis tier is automatisch inbegrepen bij elke Azure subscription. Premium features vereisen betaalde tiers (Basic/Premium), deels automatisch inbegrepen bij Microsoft 365

  - Tenants
    - Entra ID is multi-tenatn by design; elke tenant is een geisoleerde directory instantie
    - Een tenatn vertegenwoordigt een organisatie die zich heeft aangemeld voor een Microsoft cloud service (Azure, Microsoft 365, Intune)
    - Een Azure subscription is altijd gekoppeld aan precies 1 entra tenant, maar dezelfde tenant kan aan meerdere subscriptions gekoppeld zijn
    - Elke tenant krijgt een standaard DNS naam met het suffix onmicrosoft.com. Een custom domain toevoegen is mogelijk en gebruikelijk
   
  - Schema
    - Het Entra ID schema bevat minder object types dan AD DS; geen computer class (wel device), geen Organizational Units (OUs)
    - Geen OUs betekent geen Group Policy Objects (GPOs); beheer via group membership in plaats van OU-hierarchie
    - Applications wordne weergegeven door 2 classes:
      - Application (definitie)
      - servicePrincipal (instantie per tenant)


     
**Compare Microsoft Entra ID and Active Directory Domain Services**
  
| Kenmerk | AD DS | Microsoft Entra ID |
|---|---|---|
| Structuur | Hiërarchisch (X.500) | Flat (geen OUs) |
| Locating resources | DNS | REST API via HTTP/HTTPS |
| Query protocol | LDAP | REST API |
| Authenticatie | Kerberos | SAML, WS-Federation, OpenID Connect |
| Autorisatie | - | OAuth |
| Beheer | OUs en GPOs | Group membership |
| Computer objects | Ja | Nee (wel device objects) |
| Multi-tenant | Nee | Ja |
| Primaire focus | On-premises apps | Web-based / internet apps |
| Communicatie | - | HTTP (port 80) / HTTPS (port 443) |

  - AD DS maakt deel uit van de bredere Windows Active Directory suite: AD CS, AD LDS, AD FS en AD RMS. AD DS op een Azure VM deployen is mogelijk maar maakt geen gebruik van Microsoft Entra ID.



**Examine Microsoft Entra ID as a directory service for cloud apps**
  - Elke cloud service die authenticatie nodig heeft zou standaard een eigen Entra tenant aanmaken; het is efficienter om 1 gedeelde directory te gebruiken voor alle microsoft cloud services
  - Entra ID biedt 1 identity service voor Microsoft 365, Azure, Dynamics 365 en intune, inclusief SSO voor externe services zoals Facebook, Google en Yahoo
  - Ontwikkelaars kunnen Entra ID gebruiken als centralized authentication en authorization provider voor applicaties in Azure, ook in combinatie met on-premises AD DS
  - Voor Azure App Service kun je Entra authenticatie direct inschakelen via de Authentication/Authorization blade in de Azure portal; per deployment slot instelbaar


    
**Compare Microsoft Entra ID P1 and P2 plans**
  - P1 en P2 zijn betaalde tiers bovenop de Free en Office 365 edities, beschikbaar als losse licentie of via Microsoft Enterprise Mobility + Security (inclusief Intune en Auzre Information Protection)

  - P1 Features
    - Self-service group management: Gebruikers kunnen groepen aanmaken en beheren
    - Advanced security reports en alerts: Machine learning-based anomaly detection
    - Multi-factor authentication (MFA): Werkt op on-premises apps (VPN, RADIUS, Azure, Microsoft 365, Dynamics 365 en 3rd party gallery apps
    - Microsoft Identity Manager (MIM): Bridge tussen on-premises authenticaton stores (AD DS, LDAP, Oracle) en Entra ID
    - SLA van 99,9 beschikbaarheid
    - Password reset with writeback: SSPR volgt het on-premises AD password policy
    - Cloud App Discovery: ontdekt meest gebruikte cloud apps
    - Conditional Access op basis van device, group of location
    - Microsoft Entra Connect Health; Monitoring en operationeel inzicht in Entra ID
   
  - P2 Features
    - Microsoft Entra ID Protection: User risk policies en sign-in policies, gedragsanalyse en risk flagging
    - Microsoft Entra Privilged Identity Management (PIM): extra beveiliging voor privileged users, permanent en tijdelijke admins, policy workflow voor gebruik en admin privileges


**Examine Microsoft Entra Domain Services**
  - Microsoft Entra Domain Services (AAD DS) biedt managed domain services in de cloud: Group Policy management, domain joining en Kerberos authenticatie; volleidg compatibel met on-premises AD DS, zonder zelf domain controllers te heoven deployen
    - Vereist Entra ID P1 of P2. Kosten zijn per uur op basis van de grootte van de directory
    - Alternatieven zonder AAD DS: site-to-side VPN naar on-premises AD DS, of replica domain controllers als VMs in Azure; beide duurder en meer beheer

  - Voordelen:
    - Geen beheer van domain controllers, updates of replicatie
    - Geen Domain Admis of Enterprise Admins groepen nodig
    - Bruikbaar als cloud-only service zonder on-premises AD DS
    - Migratie van apps die LDAP, NTLM of Kerberos gebruiken naar de cloud zonder VPN
   
  - Berperkingen:
    - Alleen het basis computer Active Directory object wordt ondersteund
    - Schema uitbreiden is niet mogelijk
    - OU-structuur is flat; geen nested OUs
    - Ingebouwde GPOs zijn beschikbaar maar niet te targeten op OUs, geen WMI filter of security-group filtering



---



## Learning Path 2: Manage identities and governance in Azure
### Module 2: Create, configure, and manage identities 

**Create, configure, and manage users**
  - Elk account dat toegang nodig heeft tot resources vereist een user account in Entra ID. Na authenticatie bouwt Entra ID een access token om te bepalen welke resources de gebruiker kan benaderen
  - Beheer via de Microsoft Entra admin center; je werkt altijd met 1 directory tegelijk, wisselen van Directory + Subscribtion panel of de Switch directory knop

  - 3 typen gebruikers:
    - Cloud identities: bestaan alleen in Entra ID (admins, zelf beheerde gebruiker)
      - Source: Microsoft Entra ID.
    - Directory-synchronized identities; bestaan in on-premises AD DS en worden gesynchroniseerd naar Entra ID. Aanbevolen tool: Microsoft Entra Cloud Sync (lichtgewicht, ondersteunt meerdere forests) Voor complexe scenario's (device sync, groupen > 50.000 leden): Microsoft Entra Connect Sync.
       - Source Windows Server AD
    - Guest users: bestaan buiten de organisateie (externe vendors, contractors, andere cloud providers)
       - Source: invited User. Account verwijderen trekt direct alle toegang in


**Exercise - Restore or remove deleted users**
- [Exercise 3 Assign licenses to users](/03-az104/exercises/3-assign-licenses-to-users.md)


**Exercise - Restore or remove deleted users**
- [Exercise 4 Restore or remove deleted users](/03-az104/exercises/4-restore-or-remove-deleted-users.md)


**Create, configure, and manage groups**
  - 2 typen groepen:
    - Security groups: Beheren toegang tot gedeelde resources. Members: users, devices, service principals. Vereist een Entra administrator.
    - Microsoft 365 groups: Bieden samenwerking via gedeelde mailbox, calender, bestanden en SharePoint. Toegankelijk voor users en admins, ook voor externe gebruikers.

  - 3 membership types:
    - Assigned: Members worden handmatig toegevoegd en beheerd
    - Dynamic User: Users worden automatisch toegevoegd/verwijderd op basis van device attributen. Alleen voor security groups; Microsoft 365 groups ondersteunen geen dynamic devices

  - Dynamic membership vereist Entra ID P1 licentie (of Intune for Education voor device based rules)


**Exercise - Add groups in Microsoft Entra ID**
- [Exercise 5 Add groups in Microsoft Entra ID](/03-az104/exercises/5-add-groups-in-microsoft-entra-id.md)



**Configure and manage device registration**
  - 3 manieren om devices te registreren in Microsoft Entra ID:

| | Entra Registered | Entra Joined | Hybrid Entra Joined |
|---|---|---|---|
| Definitie | Persoonlijk device, geen org-account vereist voor inloggen | Alleen Entra ID, org-account vereist | On-premises AD + Entra ID |
| Doelgroep | BYOD / mobiele devices | Cloud-only of hybrid orgs | Orgs met bestaande on-premises AD |
| Device eigenaar | Gebruiker of org | Organisatie | Organisatie |
| OS | Windows 10+, macOS, iOS, Android, Linux | Windows 10/11 (geen Home), Server 2019+, macOS 13+ | Windows 10/11, Server 2016/2019/2022 |
| Beheer | MDM (Intune) | MDM (Intune) | Group Policy, Configuration Manager, Intune |
| SSO | Cloud resources | Cloud + on-premises | Cloud + on-premises |

  - Device writeback is niet meer ondersteund. Vervangen door Cloud Kerberos Trust voor on-premises SSO en Windows Hello for Business in hybrid omgevingen
  - Dynamic membershpi in groepen en Conditional Access vereisen device identity via Entra ID
  - MDM tools zoals Intune kunnen policies afdwingen: encryptie, wachtwoordcomplexiteit, software-updates



**Manage licenses**
  - 





























