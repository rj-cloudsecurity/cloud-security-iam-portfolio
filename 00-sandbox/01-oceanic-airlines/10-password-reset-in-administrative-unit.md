# Sandbox: Resetting a Password as Global Administrator

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 Learning Path *Implement an identity management solution using Microsoft Entra ID*.

## Aanleiding
Uitzoeken wat ik als Global Administrator kan doen met users die in de administrative unit **The Looking Glass** zitten.

## Doel
Testen of een Global Administrator wachtwoorden kan resetten van users in een administrative unit.

## Stappen
1. Ingelogd als Global Administrator
2. Wachtwoord gereset van een user uit de administrative unit **The Looking Glass** (Bonnie of Greta)

## Resultaat
- Als Global Administrator kan ik de wachtwoorden resetten van users in de administrative unit The Looking Glass

## Wat dit aantoont
- Een Global Administrator heeft rechten over de hele tenant en wordt niet beperkt door de scope van een administrative unit
- Een AU beperkt alleen beheerders die een rol **met de AU als scope** hebben gekregen, niet de rechten van een tenant-brede rol
