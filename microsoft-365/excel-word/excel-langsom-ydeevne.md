# Excel er langsom (store filer, formler)

## Problem

Excel reagerer langsomt, hænger ved beregninger, tager lang tid om at åbne/gemme, eller fryser helt ved store regneark med mange formler, data eller formatering.

## Løsning

### 1. Reducer filstørrelsen

**Find ud af hvad der fylder:**

1. Tryk **Ctrl + End** i hvert ark for at se det faktisk brugte område
2. Hvis markøren hopper langt ud over dine data, er der usynlige data/formatering
3. Markér de tomme rækker/kolonner og slet dem: **Højreklik** → **Slet**
4. Gem og genåbn filen

**Fjern unødvendig formatering:**

1. Markér det tomme område uden for dine data
2. Gå til **Hjem** → **Ryd** → **Ryd alt**
3. Dette fjerner formatering, data og kommentarer fra de tomme celler

### 2. Optimer formler

**Erstat volatile funktioner:**

Disse formler genberegner ALTID — selv når intet er ændret:
- `NU()` / `NOW()`
- `IDAG()` / `TODAY()`
- `SLUMPTAL()` / `RAND()`
- `INDIREKTE()` / `INDIRECT()`
- `FORSKYDNING()` / `OFFSET()`

Erstat dem med statiske værdier eller brug alternativer som `INDEX()`.

**Skift beregningsmode:**

1. Gå til **Formler** → **Beregningsindstillinger** → **Manuel**
2. Tryk **F9** for at beregne manuelt når du har brug for det
3. Husk at skifte tilbage til **Automatisk** inden du deler filen

**Forenkle LOPSLAG/VLOOKUP:**

- Brug `XLOOKUP` i stedet for `VLOOKUP` (hurtigere og mere fleksibel)
- Brug `INDEX/MATCH` som alternativ
- Sortér data og brug eksakt match (`FALSK`/`FALSE`) for bedre ydeevne

### 3. Reducer betinget formatering

1. Gå til **Hjem** → **Betinget formatering** → **Administrer regler**
2. Skift "Vis formateringsregler for" til **Dette regneark**
3. Gennemgå alle regler — slet duplikater og unødvendige
4. Begræns rækkevidden: brug `A1:A1000` i stedet for `A:A` (hele kolonnen)

### 4. Fjern unødvendige objekter

1. Tryk **Ctrl + G** → **Special** → **Objekter** → **OK**
2. Alle objekter markeres (billeder, figurer, diagrammer, tomme tekstbokse)
3. Tjek om der er usynlige/tomme objekter og slet dem
4. Kopier-paste fra web indsætter ofte usynlige objekter

### 5. Optimer pivottabeller

1. Højreklik pivottabellen → **Pivottabel-indstillinger**
2. Under **Data**: fjern flueben fra **Gem kildedata med filen**
3. Reducer antallet af felter og filtre
4. Brug **Opdater** i stedet for automatisk opdatering

### 6. Gem som .xlsx (ikke .xls)

- `.xlsx`-formatet er komprimeret og langt mere effektivt
- `.xls` er det gamle format (maks 65.536 rækker, langsomt)
- **Filer** → **Gem som** → vælg **Excel-projektmappe (.xlsx)**

### 7. Hardware og indstillinger

- **Deaktiver animationer:** Filer → Indstillinger → Avanceret → Vis → fjern "Deaktiver hardwareacceleration"
- **Deaktiver tilføjelsesprogrammer:** Filer → Indstillinger → Tilføjelsesprogrammer → deaktiver unødvendige
- **Opgradér RAM:** Excel-filer med mange formler bruger meget hukommelse
- **Brug SSD:** gør stor forskel ved åbning og gemning af store filer

## Bemærkninger

- Excel 64-bit kan håndtere større filer end 32-bit — tjek version under Filer → Konto
- Filer over 20 MB bør overvejes konverteret til Power Query / database
- Co-authoring (samtidig redigering) kan gøre store filer langsommere
- Makroer med `ScreenUpdating = False` og `Calculation = xlManual` forbedrer VBA-ydeevne drastisk
- Excel har en grænse på ca. 1 million rækker — overvej Power BI eller Access til større datasæt
