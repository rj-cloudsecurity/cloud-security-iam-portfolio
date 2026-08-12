# SC-300: Microsoft Identity and Access Administrator
## Learning Path 2: Implement an identity management solution using Microsoft Entra ID

  - **SC-300 Started:** 2 August, 2026
  - **SC-300 Exam passed:** 🔄

---

## Learning Path 1: Implement initial configuration of Microsoft Entra ID 
### Module 1: Configure company brand

  - Wat is het:
    - Eigen logo + custom kleurenschema op sign-in pagina's; toegepast bij inloggen op web-based apps (bv. M365 via Entra ID)
    - Vereist licentie: Entra ID P1, P2, of Office 365

  - Hoe instellen:
    - Azure Portal -> Microsoft Entra ID -> Manage -> Company branding
    - Premium licentie vereist om deze menu optie te zien

  - Instellingen
    - Language: automatisch default, niet aan te passen
    - Sign-in page background image: png/.jpg, max 1920x1080px, max 300.000 bytes
    - Banner logo: .png/.jpg, verschijnt na username-invoer + op My Apps portal
    - Username hint: tekst bij "vergeten username", Unicode, geen links/code, max 64 tekens. Niet aanraden bij guest users
    - Sign-in page text and formatting: tekst onderaan sign-in pagina (bv. helpdesk-nummer, legal statement), Unicode, max 1.024 tekens

### Module 2: Configure and manage Microsoft Entra roles
