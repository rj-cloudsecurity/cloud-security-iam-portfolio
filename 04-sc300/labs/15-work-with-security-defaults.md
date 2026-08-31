# Exercise: Work with Security Defaults

**Bron:** SC-300 Learning Path; Implement an authentication and access management solution

## Doel
Security defaults instellingen verkennen, om het proces te begrijpen.

## Wat ik heb gedaan
1. Microsoft Entra admin center > Identity > Overview > Properties
2. Manage security defaults geopend
3. Gezien dat de tenant al stond op Enabled (recommended), met bevestiging "Your organization is currently using security defaults"
4. Dropdown gewijzigd naar Disabled (not recommended)
5. Waarschuwing verschenen: "With security defaults disabled, your organization is vulnerable to common identity-related attacks"
6. Verplichte reden voor disabling geselecteerd (Other, met tekstveld ingevuld)
7. Save knop werd actief (blauw)
8. Niet daadwerkelijk op Save geklikt, gewijzigd naar Cancel om de instelling niet echt te wijzigen

## Resultaat
Bevestigd volledig uitvoerbaar in de sandbox, zonder P1 of P2 nodig. De UI toont een dropdown in plaats van de Yes/No toggle die de Learn tekst beschrijft, en vraagt bij disabling verplicht een reden op. Instelling zelf niet gewijzigd, om de tenant op de huidige (enabled) staat te houden.

## Wat dit aantoont
- Praktische ervaring met het navigeren naar en verkennen van security defaults instellingen
- Begrip van wanneer je security defaults uitschakelt: zodra je overstapt op Conditional Access policies die ze vervangen
- Kennis van de verplichte reden opgave bij disabling, iets wat niet in de officiele Learn tekst stond
