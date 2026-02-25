# AZ-900 Study Notes

## Week 1: 23-2-2026
### - **Learning path:** Introduction to Cloud Infrastructure: Describe cloud concepts
###       - **Module:** Describe cloud computing
###         - **Extra:** FreeCodeCamp AZ‑90

**What is cloud computing**
   - Leveren van computer services over internet, zoals: VM’s, storage, databases en networking

**Shared responsibility model**
   - Microsoft verantwoordlijk voor: alles wat fysiek is en beveiling van de cloud
   - Klant verantwoordelijk voor: data, indentiteiten en apparaten
   - Gedeelde verantwoordelijkeheid: afhankelijk van LaaS/PaaS/Saas

**Cloud Models:**
   - Private cloud: On premises met eigen datacentre, zelf beheer van hardware netwerk en beveiliging
   - Public cloud: Cloud die door meerdere organisaties wordt gebruikt. (Azure, AWS)
   - Hybrid cloud: Combinatie van private en public cloud
   - Multi cloud: meerdere cloud provides tegelijk met Azure Arc

**Consumption-based model**
   - CapEx: Eenmalige inverstering, vooraf betalen voor eigen datacenter en hardware
   - OpEx: Doorlopende kosten, betalen per maand of gebruik
   - Consumption-based model: Alleen betalen voor wat je gebruikt

---
   
### - **Learning path:** Introduction to Cloud Infrastructure: Describe cloud concepts
###    - **Module:** Describe the benefits of using cloud services
###       - **Extra:** FreeCodeCamp AZ‑90
   
**Benefits of high availability and scalability in the cloud**
   - **High availabilty:** diensten blijven draaien doordat Azure meerdere datacenters gebruikt
   - **Scalability:** automatisch meer of midner capaciteit gebruiken wanneer de vraag stijgt of daalt
   - **Vertical scaling:** groter of kleiner maken van één machine
   - **Horizontal scaling:** meer of minder machines toevoegen

**Benefits of reliability and predictability in the cloud**
   - Reliability: cloud blijft werken, zelfs als er iets uitvalt
   - Predictability: vooraf goed te verwachten prestaties
   - Performance: autoscaling en load balancing houden je app snel
   - Cost: cloudkosten goed voorspellen en bijsturen met realtime inzicht en tools

**Benefits of security and governance in the cloud**
   - Governance: policies en audits zorgen dat alles aan de regels voldoet
   - Security: zelf de verantwoordelijkheid kiezen IaaS of PaaS/SaaS

**Benefits of manageability in the cloud**
   - Of the cloud: Automatically scale resources, templates, health alerts
   - In the cloud: webportal, CLI, API, Powershell

---
   
### - **Learning path:** Introduction to Cloud Infrastructure: Describe cloud concepts
###    - **Module:** Describe cloud service types
###       - **Extra:** FreeCodeCamp AZ‑90

IaaS - Infrastructure as a Service
   - Definitie: de infrastructuur (servers, storage, netwerk).
   - Microsoft beheert: hardware, datacenter, netwerk, fysieke beveiliging.
   - Klant beheert: OS, updates, apps, data, configuratie.
   - Voorbeelden: Azure VM, Azure Storage, Azure Virtual Network.
      
PaaS - Platform as a Service
   - Definitie: compleet platform (infrastructuur + OS + runtime)
   - Microsoft beheert: hardware, netwerk, OS, updates, runtime
   - Klant beheert: applicatie en data
   - Voorbeelden: Azure App Service, Azure SQL Database, Azure Functions
      
SaaS - Software as a Service
   - Definitie: kant‑en‑klare app via internet.
   - Microsoft beheert: alles (infrastructuur, OS, app, updates).
   - Klant beheert: instellingen en data.
   - Voorbeelden: Microsoft 365, Outlook, Teams.

---

