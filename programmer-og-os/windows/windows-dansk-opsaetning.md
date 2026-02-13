# Dansk opsætning af Windows

## Problem

Windows viser engelske menuer, forkert datoformat, eller bruger forkert decimal-separator. Det kan give problemer i programmer som Excel, hvor komma vs. punktum som decimal-separator er afgørende.

## Løsning

### Sprog og visningssprog

1. Åbn **Indstillinger → Tid og sprog → Sprog og område**
2. Under **Windows-visningssprog** — vælg **Dansk**
3. Hvis dansk ikke er tilgængeligt, klik **Tilføj et sprog** og søg efter **Dansk**
4. Installér sprogpakken (kræver download)
5. Sæt **Dansk** som visningssprog
6. **Log ud og ind igen** for at aktivere sproget

### Tastaturlayout

1. Gå til **Indstillinger → Tid og sprog → Sprog og område**
2. Klik på **Dansk** → **Sprogindstillinger**
3. Under **Tastaturer** — kontrollér at **Dansk** er tilføjet
4. Fjern eventuelt **Engelsk (USA)** hvis det ikke bruges

Skift mellem tastaturer med **Win + Mellemrum** eller klik på sprogbjælken i proceslinjen.

Dansk tastaturlayout har:

- **Æ** til højre for L
- **Ø** til højre for Æ
- **Å** til højre for P

### Dato- og tidsformat

1. Gå til **Indstillinger → Tid og sprog → Sprog og område**
2. Klik på **Regionale formatindstillinger** (eller **Regionalt format**)
3. Sæt format til **Dansk (Danmark)**

Dette giver:

| Indstilling | Værdi | Eksempel |
|-------------|-------|----------|
| Datoformat (kort) | dd-MM-yyyy | 13-02-2026 |
| Datoformat (lang) | d. MMMM yyyy | 13. februar 2026 |
| Tidsformat | HH:mm | 14:30 |
| Ugens første dag | Mandag | |

### Tidszone

1. Gå til **Indstillinger → Tid og sprog → Dato og klokkeslæt**
2. Sæt **Tidszone** til **(UTC+01:00) Bruxelles, København, Madrid, Paris**
3. Slå **Justér automatisk for sommertid** til
4. Slå eventuelt **Indstil tid automatisk** til

### Decimal- og tusindtals-separator (VIGTIGT)

Denne indstilling er kritisk for Excel og andre programmer der arbejder med tal.

1. Gå til **Kontrolpanel → Område** (søg efter "område" i startmenuen)
2. Under fanen **Formater** — klik **Yderligere indstillinger...**
3. Sæt disse værdier:

| Indstilling | Dansk standard |
|-------------|---------------|
| Decimal-separator | **,** (komma) |
| Tusindtals-separator | **.** (punktum) |
| Listeseparator | **;** (semikolon) |

Eksempel: Tallet "en million og en halv" skrives som **1.000.000,50** på dansk.

**Vigtigt for Excel:** Hvis decimal-separatoren er sat til punktum (engelsk standard), vil Excel tolke kommaer forkert i danske regneark. CSV-filer fra danske systemer bruger semikolon som separator netop på grund af komma-decimalen.

### Standard-apps

1. Gå til **Indstillinger → Apps → Standardapps**
2. Sæt ønskede standardprogrammer:

| Type | Anbefaling |
|------|-----------|
| Browser | Kundens foretrukne (Chrome, Edge osv.) |
| PDF-læser | Adobe Acrobat Reader eller Edge |
| Mail | Outlook |
| Kalender | Outlook |

## Bemærkninger

- Sprogpakken kræver download og kan tage et par minutter at installere
- Regionalt format og visningssprog er to forskellige indstillinger — begge skal sættes
- Decimal-separator-indstillingen påvirker ALLE programmer, ikke kun Excel
- Listeseparatoren (semikolon vs. komma) påvirker CSV-import i Excel
- Nogle ældre programmer kræver at man også ændrer **systemlandestandard** (Kontrolpanel → Område → Administration → Skift systemlandestandard → Dansk)
- Genstart computeren efter ændring af systemlandestandard
