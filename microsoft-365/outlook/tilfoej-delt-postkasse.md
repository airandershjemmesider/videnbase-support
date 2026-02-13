# Tilføj delt postkasse i Outlook

## Problem

En bruger skal have adgang til en delt postkasse (f.eks. info@firma.dk eller salg@firma.dk) i Outlook, men postkassen vises ikke automatisk.

## Løsning

### Metode 1: Automatisk tilføjelse (anbefalet)

Delte postkasser tilføjes normalt automatisk i Outlook, hvis administratoren har givet adgang via Microsoft 365 Admin Center.

1. Luk Outlook helt
2. Vent 15-30 minutter efter administratoren har tildelt adgang
3. Åbn Outlook igen
4. Den delte postkasse bør nu vises i venstre panel under din primære postkasse

### Metode 2: Tilføj manuelt i Outlook

Hvis postkassen ikke vises automatisk:

1. Åbn Outlook
2. Gå til **Filer** → **Kontoindstillinger** → **Kontoindstillinger**
3. Vælg din email-konto og klik **Skift**
4. Klik **Flere indstillinger**
5. Gå til fanen **Avanceret**
6. Klik **Tilføj** under "Åbn disse ekstra postkasser"
7. Skriv navnet på den delte postkasse (f.eks. `info@firma.dk`)
8. Klik **OK** → **Næste** → **Udfør**
9. Genstart Outlook

### Metode 3: Åbn via Outlook på web

1. Gå til [outlook.office.com](https://outlook.office.com)
2. Klik på dit profilbillede øverst til højre
3. Klik **Åbn en anden postkasse**
4. Skriv email-adressen på den delte postkasse
5. Klik **Åbn** — postkassen åbnes i et nyt browservindue

### Send mail fra den delte postkasse

1. Opret en ny mail
2. Klik **Fra** (hvis feltet ikke vises: klik **Indstillinger** → **Vis Fra**)
3. Klik **Fra** → **Anden email-adresse**
4. Skriv den delte postkasses email-adresse
5. Send mailen — den sendes nu som den delte postkasse

### Administratorens rolle (M365 Admin Center)

For at tildele adgang:

1. Log ind på [admin.microsoft.com](https://admin.microsoft.com)
2. Gå til **Teams og grupper** → **Delte postkasser**
3. Vælg postkassen
4. Under **Medlemmer** klik **Rediger**
5. Tilføj brugeren og gem

## Bemærkninger

- Brugeren behøver IKKE en ekstra licens for en delt postkasse (op til 50 GB)
- Over 50 GB kræver postkassen en Exchange Online Plan 2-licens
- Delte postkasser har ikke deres eget password — adgang styres via medlemskab
- Sendte mails fra delt postkasse gemmes i den delte postkasses "Sendt post" (kan konfigureres)
- Automapping (automatisk tilføjelse) kan deaktiveres med PowerShell hvis ønsket
- Nye Outlook-klienten viser delte postkasser automatisk når adgang er tildelt
