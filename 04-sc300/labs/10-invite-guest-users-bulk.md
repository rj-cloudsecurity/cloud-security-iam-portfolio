# Exercise: Invite Guest Users in Bulk

**Bron:** SC-300 Learning Path; Implement an identity management solution using Microsoft Entra ID

## Doel
Meerdere guest users tegelijk uitnodigen via een CSV-bestand.

## Niet volledig uitgevoerd
Deze oefening is niet praktisch doorlopen — geen CSV-template gedownload, ingevuld of geüpload. Vastgelegd als theorie/proces-kennis.

## Stappen (theorie)
1. Microsoft Entra admin center -> Identity -> Users -> All Users
2. Bulk operations -> Bulk invite
3. Sample CSV template downloaden
4. Template invullen — belangrijkste kolommen:
   - **Email address to invite** — het adres dat de uitnodiging ontvangt
   - **Redirection url** — waar de user naartoe gaat na het accepteren van de invite
5. CSV opslaan en uploaden onder "Upload your csv file"
6. Validatie wordt automatisch uitgevoerd — bij fouten: eerst oplossen voordat je kunt submitten
7. Na succesvolle validatie: Submit
8. Job status bekijken via "Bulk operation results" — toont # Success, # Failure, en reden bij eventuele failures

## Resultaat
Niet uitgevoerd in de sandbox — individuele invite is al wel gedocumenteerd (Desmond Hume-lab).

## Wat dit aantoont
- Begrip van bulk invite als schaalbare uitbreiding op de individuele invite-flow
- Kennis van de CSV-vereisten (email address, redirection url) en het validatie/foutafhandelingsproces
