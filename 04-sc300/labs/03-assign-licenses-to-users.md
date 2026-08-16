# Exercise: Assign Licenses to Users

**Bron:** SC-300 Learning Path; Implement an identity management solution using Microsoft Entra ID

## Doel
Een user en security group aanmaken, en een licentie toewijzen aan de group via het Microsoft 365 admin center.

## Stappen

### 1. Nieuwe user aanmaken
- Identity -> Users -> All Users -> + New user -> Create new user
- User principal name: ChrisG
- Name: Chris Green

### 2. Security group aanmaken
- Identity -> Groups -> All groups -> New group
- Group type: Security
- Group name: Marketing
- Membership type: Assigned
- Owner: eigen administrator account
- Member: Chris Green

### 3. Licentie toewijzen aan de group
- Microsoft 365 admin center (admin.microsoft.com) -> Billing -> Licenses
- Licentie selecteren -> Groups -> + Assign license
- Marketing group zoeken en selecteren -> Assign

## Resultaat
- Stap 1 en 2 zijn conceptueel doorlopen
- Stap 3 (license assignment) **niet uitgevoerd**; vereist een betaalde Microsoft 365 licentie in de tenant

## Wat dit aantoont
- Begrip van waar licentiebeheer plaatsvindt: **Microsoft 365 admin center**, niet Entra ID zelf
- Begrip van group-based licensing: licenties worden aan een group toegewezen, niet per individuele user, wat schaalbaarder is bij group-membership wijzigingen
- Bewustzijn van de licentie-vereisten en beperkingen van een gratis tenant

## Restore/remove deleted users
- Verwijderde users blijven 30 dagen in suspended state, binnen die periode volledig te herstellen
- Na 30 dagen: automatische permanente verwijdering, niet meer terug te draaien
- Vereiste rollen om te restoren/permanent verwijderen: Global Administrator, Partner Tier-1 Support, Partner Tier-2 Support, of User Administrator
