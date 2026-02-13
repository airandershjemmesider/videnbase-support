# Opret og administrer regler i Outlook

## Problem

En bruger vil automatisk sortere, flytte, markere eller videresende mails baseret på afsender, emne eller andre kriterier.

## Løsning

### Opret en regel i Outlook desktop

1. Åbn Outlook
2. Gå til **Filer** → **Administrer regler og påmindelser**
3. Klik **Ny regel**
4. Vælg en skabelon eller start fra en tom regel:
   - **Flyt meddelelser fra en bestemt person til en mappe** (mest brugt)
   - **Flyt meddelelser med bestemte ord i emnet til en mappe**
   - **Start fra en tom regel** for fuld kontrol
5. Klik **Næste** og vælg betingelser (afsender, emneord, osv.)
6. Klik **Næste** og vælg handling (flyt til mappe, markér, videresend osv.)
7. Klik **Næste** og vælg eventuelle undtagelser
8. Giv reglen et navn og vælg om den skal køres på eksisterende mails
9. Klik **Udfør**

### Hurtig regel fra en eksisterende mail

1. Højreklik på en mail
2. Vælg **Regler** → **Opret regel**
3. Sæt betingelsen (f.eks. fra denne afsender)
4. Vælg handling (f.eks. flyt til mappe)
5. Klik **OK**

### Opret en regel i Outlook på web

1. Gå til [outlook.office.com](https://outlook.office.com)
2. Klik tandhjulet → **Vis alle Outlook-indstillinger**
3. Gå til **Mail** → **Regler**
4. Klik **Tilføj ny regel**
5. Konfigurer betingelser og handlinger
6. Klik **Gem**

### Mest brugte regeltyper

| Formål | Betingelse | Handling |
|--------|-----------|---------|
| Sortér nyhedsbreve | Fra indeholder "newsletter" | Flyt til "Nyhedsbreve"-mappe |
| Fremhæv chefen | Fra er [chefens email] | Markér som vigtig, afspil lyd |
| Arkivér automatisk | Ældre end 30 dage | Flyt til Arkiv |
| Videresend til kollega | Emne indeholder "hastende" | Videresend til [kollega] |
| Ryd op i CC-mails | Du er på CC (ikke TO) | Markér som læst, flyt til "CC"-mappe |

### Administrer eksisterende regler

1. Gå til **Filer** → **Administrer regler og påmindelser**
2. Her kan du:
   - **Aktivere/deaktivere** regler med fluebenet
   - **Redigere** en regel ved at vælge den og klikke **Skift regel**
   - **Slette** en regel ved at vælge den og klikke **Slet**
   - **Ændre rækkefølgen** med pil op/ned (regler kører i rækkefølge)
3. Klik **Anvend** → **OK**

### Kør regler på eksisterende mails

1. Gå til **Filer** → **Administrer regler og påmindelser**
2. Klik **Kør regler nu**
3. Vælg hvilke regler der skal køres
4. Vælg hvilken mappe de skal køres på
5. Klik **Kør nu**

## Bemærkninger

- Server-side regler (oprettet i Outlook på web) kører altid — også når Outlook er lukket
- Klient-side regler (kun i desktop) kører kun når Outlook er åben
- Regler der videresender til eksterne adresser kan blokeres af administratoren
- Maks antal regler er 256 KB samlet størrelse (ca. 30-50 regler afhængigt af kompleksitet)
- "Stop behandling af flere regler" er nyttig hvis flere regler overlapper
- Regler kan gå i stykker ved omdøbning af mapper — tjek reglerne efter mappeændringer
