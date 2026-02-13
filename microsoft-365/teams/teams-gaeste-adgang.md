# Invitér eksterne gæster til Teams

## Problem

En bruger vil invitere en ekstern person (udenfor organisationen) til at deltage i et team, en kanal eller et møde i Microsoft Teams.

## Løsning

### Invitér gæst til et team

1. Åbn Teams og gå til det team du vil invitere til
2. Klik de tre prikker **...** ved teamnavnet → **Tilføj medlem**
3. Skriv gæstens email-adresse (f.eks. `partner@andetfirma.dk`)
4. Teams genkender at det er en ekstern bruger og tilføjer "(Gæst)" efter navnet
5. Klik **Tilføj**
6. Gæsten modtager en invitation via email med et link til at deltage

### Hvad gæsten skal gøre

1. Gæsten åbner invitationsmailen og klikker **Åbn Microsoft Teams**
2. Hvis gæsten har en Microsoft-konto: de logger ind med den
3. Hvis gæsten IKKE har en Microsoft-konto: de opretter en gratis konto eller bruger engangskode
4. Gæsten får adgang til teamet med begrænset funktionalitet

### Invitér ekstern til et møde

1. Opret et nyt møde i Teams-kalenderen
2. I feltet **Tilføj deltagere**: skriv den eksterne persons email
3. Send invitationen
4. Den eksterne deltager kan deltage via linket i invitationen — uden Teams-konto

### Gæsterettigheder (standard)

| Gæsten kan | Gæsten kan IKKE |
|------------|-----------------|
| Sende beskeder i kanaler | Se andre teams i organisationen |
| Dele filer | Oprette nye teams eller kanaler |
| Deltage i møder | Se organisationens adressebog |
| Redigere delte filer | Administrere team-indstillinger |
| Bruge chat | Tilføje apps/bots/connectors |

### Administratoropsætning (kræves for gæsteadgang)

Gæsteadgang skal være aktiveret af IT-administratoren:

1. Log ind på [admin.teams.microsoft.com](https://admin.teams.microsoft.com)
2. Gå til **Brugere** → **Gæsteadgang**
3. Slå **Tillad gæsteadgang i Teams** til
4. Konfigurer hvilke funktioner gæster må bruge (opkald, møder, beskeder)
5. Gem ændringerne — det kan tage op til 24 timer før de træder i kraft

### Azure AD ekstern samarbejde (avanceret)

For mere kontrol over gæstepolitikker:

1. Log ind på [entra.microsoft.com](https://entra.microsoft.com)
2. Gå til **Eksternt samarbejde** → **Indstillinger for eksternt samarbejde**
3. Her kan du:
   - Tillade/blokere specifikke domæner
   - Kræve MFA for gæster
   - Begrænse gæsteinvitationer til administratorer

### Fjern en gæst

1. Gå til teamet → klik **...** → **Administrer team**
2. Find gæsten under **Medlemmer og gæster**
3. Klik **X** ud for gæstens navn
4. Bekræft fjernelsen

## Bemærkninger

- Gæstebrugere tæller IKKE med i din M365-licens — de er gratis
- Gæster identificeres med "(Gæst)" efter deres navn i Teams
- Gæsteadgang er noget andet end "Anonym deltager" i møder (anonym kræver ingen konto)
- Filer delt med gæster gemmes i SharePoint — tjek delingstilladelser
- Gæster kan tilgå Teams via desktop-app, browser eller mobil-app
- Organisationens compliance-politikker (retention, DLP) gælder også for gæsters indhold
- Uaktive gæstekonti bør gennemgås regelmæssigt af IT — fjern gæster der ikke længere har behov
