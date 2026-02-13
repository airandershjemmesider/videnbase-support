# Problemer med samtidig redigering (co-authoring)

## Problem

Flere brugere forsøger at redigere det samme Word-, Excel- eller PowerPoint-dokument samtidig, men oplever problemer: ændringer synkroniseres ikke, dokumentet låses, brugere kan ikke se hinandens markør, eller der opstår konflikter.

## Løsning

### Forudsætninger for co-authoring

Co-authoring kræver at ALLE disse betingelser er opfyldt:

1. Filen er gemt i **OneDrive**, **SharePoint** eller **Teams** (IKKE lokalt)
2. Alle brugere har en **Microsoft 365-licens**
3. Alle brugere bruger en **understøttet version** af Office (365, 2019+)
4. **AutoGem** er aktiveret (slået til i øverste venstre hjørne)
5. Filen er i **moderne format** (.docx, .xlsx, .pptx — IKKE .doc, .xls, .ppt)

### 1. AutoGem er deaktiveret

1. Åbn filen fra OneDrive/SharePoint/Teams
2. Tjek øverste venstre hjørne — **AutoGem** skal stå til **Til**
3. Hvis den er slået fra: slå den til
4. Hvis knappen er gråtonet: filen er sandsynligvis gemt lokalt — flyt den til OneDrive

### 2. "Filen er låst til redigering"

**Typiske årsager:**
- En bruger har filen åben i en ældre Office-version
- Filen er i .doc/.xls-format (gammel format understøtter ikke co-authoring)
- AutoGem er slået fra hos den anden bruger

**Løsning:**
1. Bed den anden bruger lukke filen
2. Hvis personen ikke kan findes: vent 10 minutter (låsen udløber automatisk)
3. Konvertér filen til .docx/.xlsx: **Filer** → **Gem som** → vælg nyt format
4. Sørg for at alle bruger Microsoft 365 (ikke Office 2016 eller ældre)

### 3. Ændringer synkroniseres ikke

1. Tjek internetforbindelsen — co-authoring kræver online adgang
2. Tryk **Ctrl + S** for at tvinge en synkronisering
3. Tjek om der er synkroniseringsfejl i OneDrive (klik OneDrive-ikonet i proceslinjen)
4. Luk og genåbn filen
5. Prøv at åbne filen i Office Online (browseren) — fungerer co-authoring her?

### 4. Konflikter ved redigering

Når to brugere redigerer det samme afsnit/celle:

**Word:**
- Word viser en besked om at der er ændringer af andre
- Klik **Gem** for at flette ændringerne
- Ved konflikt: Word markerer begge versioner, og du vælger hvilken der beholdes

**Excel:**
- Excel viser en grøn ramme omkring celler andre redigerer
- Hvis to redigerer samme celle: den der gemmer sidst "vinder"
- Konfliktende ændringer vises i en dialogboks

**PowerPoint:**
- Andre brugeres markør vises med farve og navn
- Konflikter er sjældne da man typisk redigerer forskellige slides

### 5. Kan ikke se andre brugeres tilstedeværelse

1. Tjek at filen er åben fra sky-lokationen (ikke en lokal kopi)
2. Andre brugeres ikoner bør vises øverst til højre i dokumentet
3. Klik på et ikon for at springe til deres markørposition
4. Hvis ingen ikoner vises: AutoGem er muligvis slået fra, eller filen er åbnet lokalt

### 6. Office Online som alternativ

Hvis desktop-co-authoring fejler:

1. Åbn filen i browseren via OneDrive eller SharePoint
2. Klik **Rediger i browser**
3. Co-authoring i browseren er mere pålidelig (men med færre funktioner)
4. Skift til desktop-appen når samtidig redigering ikke er nødvendig

## Bemærkninger

- Co-authoring i Excel har begrænsninger: pivottabeller, diagrammer og VBA-makroer kan ikke redigeres samtidigt
- Filer med adgangskode understøtter ikke co-authoring
- Password-beskyttede sektioner i Word blokerer co-authoring
- Maks antal samtidige brugere: ca. 100 (Word/PowerPoint), ca. 40 (Excel)
- Co-authoring virker bedst med fast internetforbindelse — ustabil forbindelse giver synkroniseringsproblemer
- Versionshistorikken gemmer automatisk alle ændringer — du kan altid rulle tilbage
- Offline-redigering: ændringer synkroniseres når brugeren kommer online igen, men konflikter kan opstå
