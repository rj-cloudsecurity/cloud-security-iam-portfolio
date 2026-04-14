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

































































