# Exercise: Configure and Deploy Self-Service Password Reset

**Bron:** SC-300 Learning Path; Implement an authentication and access management solution

## Doel
SSPR inschakelen voor een test group, een user aanmaken, telefoonnummer registreren, en zelf een wachtwoord reset testen zonder admin hulp.

## Licensing requirements
- Cloud based accounts: Entra ID Premium P1 of P2, of Microsoft 365 Business Standard
- On premises accounts: Entra ID Premium P1 of P2, of Microsoft 365 Business Premium

## Wat wel kan (zonder P1)
- Nieuwe user aanmaken: Identity > Users > New User (bv. Monica Thompson)
- Nieuwe security group aanmaken: Identity > Groups > New Group, group type Security, membership type Assigned, Monica als member
- De Password reset pagina openen: Entra ID > Protection > Password reset

## Wat niet kan (vereist Entra ID P1 of P2, of M365 Business Standard/Premium)
- SSPR daadwerkelijk enablen voor de group (Self-service password reset enabled > Selected > group koppelen > Save)
- Authentication methods, Registration, Notifications en Customization settings voor SSPR configureren
- Registratie van een telefoonnummer voor de user via aka.ms/ssprsetup
- Testen van de daadwerkelijke password reset flow via aka.ms/sspr

## Stappen (theorie, volledige flow)

### Enable self-service password reset
1. Azure portal > Microsoft Entra ID > Password reset
2. Properties > Self-service password reset > Select group
3. Groep selecteren (bv. SSPRTesters) > Select
4. Save

### Add a new user
1. Identity > Users > New User
2. User name: MonicaT, Name: Monica Thompson
3. Password noteren, Create

### Create a group
1. Identity > Groups > New Group
2. Group type: Security, Group name: SSPRTesters, Membership type: Assigned, Member: Monica Thompson
3. Create

### Register for self-service password reset
1. Incognito venster > aka.ms/ssprsetup
2. Inloggen als MonicaT, nieuw wachtwoord instellen
3. Phone optie kiezen, mobiel nummer invullen, code ontvangen en invoeren
4. Registratie afronden

### Test self-service password reset
1. Incognito venster > aka.ms/sspr
2. Email invullen > Forgot my password
3. Verificatie via telefoon (tekst of bellen), code invoeren
4. Nieuw wachtwoord instellen, Finish
5. Inloggen met nieuw wachtwoord ter bevestiging

## Resultaat
Niet volledig uitvoerbaar. User en group aanmaken kan wel (zelfde als eerdere labs), maar het daadwerkelijk enablen en testen van SSPR vereist Entra ID P1 of P2, niet beschikbaar op de Free tier.

## Wat dit aantoont
- Begrip van de SSPR setup flow: licentie vereiste, group gebaseerde rollout, registratie en test stap
- Kennis van de licensing requirements voor SSPR, apart voor cloud based en on premises accounts
- Bewustzijn van de licentie grenzen van een Free tier tenant, en herkenning van hetzelfde premium gated patroon als bij MFA en Conditional Access
