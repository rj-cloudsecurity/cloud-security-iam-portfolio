# Exercise: Manage User Roles

**Bron:** SC-300 Learning Path; Implement an identity management solution using Microsoft Entra ID (geïnspireerd op, niet letterlijk gevolgd)
**Uitgevoerd in:** [Oceanic Airlines sandbox](../../00-sandbox/02-adding-first-user.md)

> De Learn-oefening gebruikt een voorbeelduser "Adele Vance". In mijn sandbox pas ik dit toe op mijn eigen Oceanic Airlines-personages in plaats van de Learn-voorbeelddata letterlijk over te nemen.

## Doel
Een gebruiker aanmaken en een Entra ID role toewijzen/verwijderen, om te oefenen met least-privilege role assignment.

## Stappen
1. Nieuwe user aangemaakt: Identity -> Users -> All Users -> + New User
2. Rol toegewezen aan de user: Assigned roles -> + Add assignments -> rol kiezen, bv. Application Administrator
3. Rol weer verwijderd: Assigned roles -> rol selecteren -> Remove

## Resultaat
- User aangemaakt in de Oceanic Airlines tenant
- Role assignment en removal succesvol getest

## Wat dit aantoont
- Praktische ervaring met user provisioning en role assignment/removal in Entra ID
- Begrip van least-privilege toewijzing; een rol geven voor een specifieke taak, weer intrekken als die niet meer nodig is
