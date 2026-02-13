# Makroer blokeres af sikkerhedsindstillinger

## Problem

En bruger forsøger at åbne en Excel- eller Word-fil med makroer, men makroerne kører ikke. Der vises en gul sikkerhedsadvarsel, makroer er deaktiveret, eller filen blokeres helt med beskeden "Microsoft har blokeret makroer".

## Løsning

### 1. Gul bjælke: "Makroer er deaktiveret"

Når filen åbnes fra en pålidelig kilde:

1. Klik **Aktivér indhold** i den gule sikkerhedsbjælke
2. Filen bliver nu en "betroet dokument" og makroerne kører
3. Næste gang filen åbnes, husker Office valget

### 2. Makroer blokeret fra internettet (rød bjælke)

Siden 2022 blokerer Microsoft som standard makroer i filer downloadet fra internettet:

**Løsning — Fjern blokering af filen:**

1. Luk filen i Office
2. Højreklik filen i Stifinder → **Egenskaber**
3. Nederst under **Sikkerhed** markér **Fjern blokering**
4. Klik **Anvend** → **OK**
5. Åbn filen igen — makroerne bør nu kunne aktiveres

**Alternativ — Gem filen i en pålidelig placering:**

1. Åbn Office-appen (Excel/Word)
2. Gå til **Filer** → **Indstillinger** → **Sikkerhedscenter** → **Indstillinger for Sikkerhedscenter**
3. Klik **Placeringer, der er tillid til**
4. Klik **Tilføj ny placering**
5. Vælg en mappe (f.eks. `C:\Betroede makroer\`)
6. Klik **OK**
7. Flyt filen til den betroede mappe og åbn den derfra

### 3. Justér makro-sikkerhedsindstillinger

1. Åbn Excel/Word
2. Gå til **Filer** → **Indstillinger** → **Sikkerhedscenter**
3. Klik **Indstillinger for Sikkerhedscenter**
4. Klik **Makroindstillinger**
5. Vælg et niveau:

| Niveau | Beskrivelse | Anbefaling |
|--------|------------|------------|
| **Deaktiver alle makroer uden besked** | Ingen makroer kører nogensinde | For høj sikkerhed, upraktisk |
| **Deaktiver alle makroer med besked** | Viser advarsel, brugeren vælger | **Anbefalet for de fleste** |
| **Deaktiver alle makroer undtagen digitalt signerede** | Kun signerede makroer tillades | God balance for virksomheder |
| **Aktivér alle makroer** | Alt kører uden advarsel | **Frarådes stærkt** |

6. Vælg **Deaktiver alle makroer med besked** (standard)
7. Klik **OK**

### 4. Makroer kører ikke i .xlsx-filer

Makroer kan KUN gemmes i makro-aktiverede filformater:

| Format | Makroer | Brug |
|--------|---------|------|
| `.xlsx` | Nej | Standard Excel-fil |
| `.xlsm` | Ja | Excel med makroer |
| `.xlsb` | Ja | Binært format (hurtigere) |
| `.docx` | Nej | Standard Word-fil |
| `.docm` | Ja | Word med makroer |

Hvis en fil med makroer gemmes som `.xlsx`, slettes makroerne. Gem altid som `.xlsm` eller `.docm`.

### 5. VBA-editoren åbner ikke

1. Tryk **Alt + F11** for at åbne VBA-editoren
2. Hvis den ikke åbner: gå til **Filer** → **Indstillinger** → **Tilpas båndet**
3. Markér **Udvikler** i højre kolonne
4. Klik **OK**
5. Nu vises fanen **Udvikler** med adgang til makroer og VBA

### 6. Gruppepolitik blokerer makroer (virksomhedsmiljø)

Hvis IT-administratoren har blokeret makroer via gruppepolitik:

- Brugeren kan IKKE selv ændre indstillingerne
- Kontakt IT-afdelingen og forklar behovet
- IT kan oprette undtagelser for specifikke brugere eller placeringer
- Alternativ: konvertér makroer til Office Scripts (Excel) eller Power Automate

## Bemærkninger

- Makroer fra ukendte kilder er en af de mest brugte angrebsvektorer for malware
- Aktivér ALDRIG makroer i filer fra ukendte afsendere
- Microsoft har gradvist strammet makro-sikkerhed siden 2022
- Betroede placeringer omgår alle makro-sikkerhedsindstillinger — brug dem kun til kendte, sikre filer
- Digitalt signerede makroer kræver et code signing-certifikat
- Office Scripts (Excel Online) er Microsofts moderne alternativ til VBA-makroer
- Power Automate kan erstatte mange simple makroer med cloud-baserede flows
