# Sandbox: Creating a Security Group and Users

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Geïnspireerd op de Microsoft Learn oefening **"Exercise - assign licenses to users"**, onderdeel van de SC-300 Learning Path *Implement an identity management solution using Microsoft Entra ID*. Alleen het group-aanmaken deel toegepast, niet letterlijk gevolgd — eigen naamgeving en context gebruikt.

## Aanleiding
Eerste security group aanmaken in de Oceanic Airlines tenant, gekoppeld aan een van de afdelingen uit de sandbox-context.

## Doel
Users en een security group aanmaken met assigned membership, om te oefenen met group-based access management.

## Stappen
1. Nieuwe users aangemaakt: **Frank Lapidus** en **Ana Lucia Cortez**
2. Identity -> Groups -> All groups -> New group
3. Group type: **Security**
4. Group name: **Flight-Operations**
5. Membership type: **Assigned**
6. Owner: eigen administrator account
7. Members: mezelf, Frank Lapidus, Ana Lucia Cortez

## Resultaat
- Users "Frank Lapidus" en "Ana Lucia Cortez" aangemaakt in de Oceanic Airlines tenant
- Security group "Flight-Operations" aangemaakt
- Mezelf, Frank Lapidus, en Ana Lucia Cortez toegevoegd als members

## Wat dit aantoont
- Praktische ervaring met user provisioning en group-based access management in Entra ID
- Begrip van het verschil tussen Assigned en Dynamic membership, en waarom Dynamic (P1-feature) hier niet toepasbaar is in een Free tier tenant
