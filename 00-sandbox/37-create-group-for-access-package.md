# Sandbox: Creating a Group as a Resource for an Access Package

**Type:** Eigen verkenning in persoonlijke test-tenant

## Bron
Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

## Aanleiding
Een access package geeft toegang tot een resource. De oefenvraag gebruikt een SharePoint-site, maar mijn tenant heeft alleen een Microsoft Entra Suite-trial en dus geen SharePoint.

## Doel
Een security group maken die als resource in een access package kan dienen.

## Stappen
1. Entra admin center -> Entra ID -> Groups -> New group
2. Group type: **Security**, naam **Island Resources**
3. De group beschikbaar gemaakt als resource in de catalog **General** van Entitlement management

## Resultaat
- Security group "Island Resources" aangemaakt
- In de access package wizard verschijnt hij als type *Group and Team*, subtype *Security*

## Wat dit aantoont
- Een access package kan een group als resource gebruiken, als alternatief voor een SharePoint-site
- Een resource moet in een catalog staan voordat je hem aan een access package kunt toevoegen
