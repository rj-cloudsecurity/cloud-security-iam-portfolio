## Exercise - change group license assignments

**Kan niet volledig uitgevoerd worden** — vereist beschikbare M365-licenties, niet aanwezig in Free tier sandbox

### Wat de oefening zou doen
- Entra ID -> Groups -> group -> Manage -> Licenses — bekijkt huidige toewijzingen (aanpassen gebeurt in M365 admin center)
- M365 admin center -> Billing -> Licenses -> licentie kiezen -> Groups -> + Assign licenses -> group selecteren -> Assign
- Wijziging zichtbaar in zowel Entra admin center als M365 admin center

---

### Group-based licensing errors (examen-kernstof — theorie, geen hands-on nodig)

Bij directe user-licensing zie je fouten direct (bv. via PowerShell Set-MgUserLicense). Bij group-based licensing gebeurt toewijzing op de achtergrond — fouten worden pas achteraf gerapporteerd op het user-object, niet meteen.

**Not enough licenses**
- Te weinig licenties beschikbaar voor een product in de group
- Check via: Entra ID -> Billing -> Licenses -> All products
- PowerShell error: CountViolation

**Service plans that conflict**
- Twee service plans die niet samen toegewezen kunnen worden (bv. E1 direct + E3 via group -> SharePoint/Exchange Plan 1 vs Plan 2 conflicteren)
- Oplossing: 1 van de 2 plannen uitschakelen — admin beslist, Entra ID lost dit niet automatisch op
- PowerShell error: MutuallyExclusiveViolation

**Other products depend on this license**
- Een service plan is vereist voor een andere service plan om te werken — fout ontstaat bij verwijderen (bv. user uit group halen)
- Oplossing: zorg dat de vereiste plan via andere weg blijft toegewezen, of schakel dependent services uit
- PowerShell error: DependencyViolation

**Usage location isn't allowed**
- Sommige services niet beschikbaar in bepaalde landen (wet-/regelgeving)
- Usage location moet ingesteld zijn voor license-toewijzing (User -> Profile -> Edit)
- Zonder ingestelde locatie: user erft de locatie van de directory
- PowerShell error: ProhibitedInUsageLocationViolation
- Aanbevolen: usage location altijd correct instellen voordat je group-based licensing gebruikt

**Duplicate proxy addresses**
- Exchange Online: users met dezelfde proxy address -> license assignment faalt ("Proxy address is already being used")
- Na oplossen: Reprocess de group om licenties opnieuw toe te passen

**Mail/ProxyAddresses attribute change**
- License-wijziging triggert automatisch een proxy address recalculation -> kan user-attributes veranderen

**LicenseAssignmentAttributeConcurrencyException**
- Ontstaat als user in meerdere groups zit met dezelfde licentie -> concurrency-conflict
- Entra ID lost dit automatisch op via retry — geen actie nodig

**Meerdere product-licenties op 1 group**
- Mogelijk (bv. E3 + Enterprise Mobility + Security samen)
- Als 1 product niet toegewezen kan worden (business logic probleem) -> geen enkele van de licenties in de group wordt toegewezen

**Group verwijderen met licenties erop**
- Eerst alle licenties verwijderen voordat je de group kunt verwijderen
- Dependent licenses (bv. Audio Conferencing afhankelijk van Skype for Business) worden bij group-verwijdering omgezet van inherited naar direct assignment

**Producten met prerequisites (add-ons)**
- Add-on (bv. Microsoft Workplace Analytics) vereist een prerequisite service plan in dezelfde group (bv. Exchange Online Plan 1 of 2)
- Zonder prerequisite in de group: foutmelding, add-on wordt niet toegewezen
- Tip: je kunt losse groups maken per prerequisite (bv. apart voor E1-users en E3-users) om licenties efficiënt te verdelen

**Force reprocessing**
- Group: Group -> Licenses -> Reprocess-knop
- User: User -> Licenses -> Reprocess-knop
- Nodig na het oplossen van een error, om de toewijzing opnieuw te laten proberen

**Migratie: individuele licenties naar group-based licensing**
- Vermijd dat users tijdelijk hun licentie verliezen tijdens migratie
- Aanbevolen proces:
  1. Bestaande automation (PowerShell) laten draaien
  2. Nieuwe licensing group aanmaken, juiste users toevoegen
  3. Licenties toewijzen aan de group (zelfde staat als huidige automation)
  4. Verifiëren dat alle users licenties hebben (direct + inherited — kost geen extra licentie, want 1 license = 1 consumption ook al sta je op 2 manieren geregistreerd)
  5. Checken op errors per group
  6. Pas dan geleidelijk directe assignments verwijderen, gemonitord op een subset eerst

**Wijzigen van license plan (bv. E1 naar E3) — aandachtspunten vooraf**
- Check dat: licentie via group komt (niet direct toegewezen), genoeg licenties beschikbaar zijn, geen conflicterende services aanwezig zijn
- Bij on-prem sync (Entra Connect) of Dynamic groups: wijzigingen duren langer om door te syncen naar license-toewijzing
- Removal + nieuwe assignment gebeuren simultaan — geen tijdelijk verlies van toegang
