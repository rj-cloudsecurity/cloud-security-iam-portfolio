Sandbox: Linking a Security Profile to Conditional Access

Type: Eigen verkenning in persoonlijke test-tenant

Bron

Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

Aanleiding

Een security profile geldt pas voor een groep users als je het via Conditional Access toewijst.

Doel

Een Conditional Access policy maken die het security profile "Block website" toepast op de groep DharmaInitiative.

Stappen
Entra admin center -> Entra ID -> Conditional Access -> Policies -> New policy
Naam: Block social media websites
Users: group DharmaInitiative included, mijzelf excluded
Target resources: All internet resources with Global Secure Access
Session: Use Global Secure Access security profile -> Block website
Enable policy: Report-only
Create
Resultaat
Conditional Access policy "Block social media websites" aangemaakt in Report-only
Niet getest: het daadwerkelijk blokkeren, want daarvoor moet de Global Secure Access-client op een apparaat staan
Wat dit aantoont
Het security profile koppel je via de Session-controls van een Conditional Access policy aan een groep users
Bij de vraag over "Marketing tijdens kantooruren" was de volgorde: policy, security profile, Conditional Access. Ik heb de group DharmaInitiative gebruikt in plaats van Marketing.
Een tijdvenster voor kantooruren heb ik niet ingesteld
