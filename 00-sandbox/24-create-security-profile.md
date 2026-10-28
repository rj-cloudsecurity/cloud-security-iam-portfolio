Sandbox: Creating a Global Secure Access Security Profile

Type: Eigen verkenning in persoonlijke test-tenant

Bron

Eigen verkenning, onderdeel van de SC-300 voorbereiding. Opgezet aan de hand van oefenexamenvragen die ik omzet in praktische sandbox-oefeningen.

Aanleiding

Een web content filtering policy werkt pas als hij in een security profile zit.

Doel

Een security profile maken en de policy "Block social media" eraan koppelen.

Stappen
Entra admin center -> Global Secure Access -> Secure -> Security profiles -> Create profile
Naam: Block website
Policy Block social media gekoppeld aan het profile
Resultaat
Security profile "Block website" met de policy "Block social media"
Wat dit aantoont
Een security profile bundelt policies en vormt de schakel tussen de filterpolicy en Conditional Access
De volgorde: web content filtering policy, dan security profile, dan Conditional Access
