# Lab: Configure Authentication Session Controls

**Bron:** SC-300 Learning Path — Implement an authentication and access management solution

## Doel
Het doel van deze oefening is het configureren van een Conditional Access policy met een sign‑in frequency van 30 dagen, in report‑only mode.  
In dit lab wordt duidelijk dat deze configuratie **niet uitvoerbaar** is binnen de huidige tenant vanwege ontbrekende licenties.

---

## Lab Log — Uitvoering

### Stap 1 — Conditional Access openen
- Microsoft Entra admin center geopend  
- Navigatie: Identity > Protection > Conditional Access  
- **Resultaat:** direct een melding dat Conditional Access niet beschikbaar is:

> **Create your own policies and target specific conditions like cloud apps, sign-in risk, and device platforms with Microsoft Entra ID Premium.**  
> **Your organization does not have sufficient licensing to access this product.**

### Conclusie op dit punt
- Conditional Access kan **niet worden geopend**  
- Hierdoor kunnen de configuratiestappen niet praktisch worden uitgevoerd  
- De oefening wordt daarom verder **theoretisch** beschreven

---

## Theoretische stappen (zoals beschreven in de SC‑300 learning path)

### Stap 2 — Nieuwe policy starten (theorie)
- New policy  
- Naam: *Sign in frequency*

### Stap 3 — Gebruikers toewijzen (theorie)
- Assignments > Users and groups > Include > eigen administrator account

### Stap 4 — Cloud apps selecteren (theorie)
- Cloud apps or actions > Cloud apps > Select apps > Office 365

### Stap 5 — Session controls instellen (theorie)
- Access controls > Session > Sign-in frequency  
- Waarde: 30  
- Units: Days

### Stap 6 — Policy activeren (theorie)
- Enable policy: Report-only  
- Create

---

## Resultaat
De oefening kan **niet worden uitgevoerd** omdat Conditional Access functionaliteit alleen beschikbaar is met **Microsoft Entra ID Premium P1/P2**.  
De tenant beschikt niet over deze licenties, waardoor de configuratie niet toegankelijk is.

---

## Wat dit aantoont
- Je hebt de juiste navigatie gevolgd en correct vastgesteld dat Conditional Access niet beschikbaar is  
- Je herkent licentie‑afhankelijke functionaliteit binnen Entra ID  
- Je documenteert een lab correct, inclusief beperkingen  
- Je toont begrip van de theoretische configuratiestappen ondanks dat de tenant dit niet ondersteunt
