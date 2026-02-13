# Adobe Acrobat Reader problemer og tips

## Problem

Adobe Acrobat Reader fungerer ikke korrekt — PDF-filer åbner ikke, programmet crasher, eller det er langsomt.

## Løsning

### 1. PDF-filer åbner ikke

**Sæt Acrobat Reader som standard PDF-program:**

1. Højreklik på en PDF-fil → **Åbn med** → **Vælg en anden app**
2. Vælg **Adobe Acrobat** eller **Adobe Acrobat Reader**
3. Sæt flueben ved **Brug altid denne app til at åbne .pdf-filer**
4. Klik **OK**

Alternativt via Indstillinger:

1. Åbn **Indstillinger** → **Apps** → **Standardapps**
2. Søg efter `.pdf`
3. Vælg **Adobe Acrobat Reader**

### 2. Acrobat Reader crasher eller fryser

**Reparér installationen:**

1. Åbn Adobe Acrobat Reader
2. Gå til **Hjælp** → **Reparer installation**
3. Følg vejledningen og genstart programmet

**Ryd cache:**

1. Luk Acrobat Reader helt
2. Tryk **Win + R**, skriv `%appdata%\Adobe\Acrobat` og tryk Enter
3. Omdøb mappen **DC** til **DC.old**
4. Åbn Acrobat Reader igen — den opretter en ny, ren mappe

### 3. Acrobat Reader er langsomt

**Deaktivér unødvendige funktioner:**

1. Åbn **Redigér** → **Indstillinger** (Ctrl + K)
2. Under **Generelt:** Fjern flueben ved **Aktivér beskyttet visning ved opstart**
3. Under **Sikkerhed (forbedret):** Fjern flueben ved **Aktivér beskyttet tilstand ved opstart**
4. Under **Sidepaneler:** Slå meddelelsesruden fra hvis den ikke bruges

**Deaktivér opdateringsservice:**

1. Åbn **Redigér** → **Indstillinger** → **Opdatering**
2. Vælg **Kontrollér ikke for opdateringer automatisk** (opdatér manuelt i stedet)

### 4. PDF kan ikke udskrives

1. Prøv **Udskriv som billede:**
   - Gå til **Filer** → **Udskriv**
   - Klik **Avanceret**
   - Sæt flueben ved **Udskriv som billede**
   - Klik **OK** og udskriv
2. Gem PDF'en til skrivebordet først (i stedet for at åbne fra e-mail eller browser)
3. Prøv at udskrive fra en anden PDF-læser (Edge, Chrome)

### 5. PDF vises forkert (skrifter, billeder)

1. Åbn **Redigér** → **Indstillinger** → **Sidevisning**
2. Under **Gengivelse:** Sæt flueben ved **Brug lokale skrifttyper**
3. Under **Sideindhold og information:** Sæt flueben ved **Vis store billeder**

### 6. Afinstallér og geninstallér

Hvis intet andet virker:

1. Åbn **Indstillinger** → **Apps** → **Installerede apps**
2. Find **Adobe Acrobat Reader** → **Afinstaller**
3. Download den nyeste version fra **get.adobe.com/reader**
4. Under installationen: Fjern flueben ved McAfee eller andre tilbud
5. Installér og genstart

## Bemærkninger

- Acrobat Reader DC (gratis) kan læse og kommentere PDF'er. Redigering kræver betalt Acrobat Pro
- Microsoft Edge og Chrome kan også åbne PDF'er — de er hurtigere til simpel læsning
- Meget store PDF'er (100+ MB) kan gøre Acrobat langsomt — overvej at bruge SumatraPDF som et letvægtigt alternativ
- Acrobat Reader opdaterer sig selv i baggrunden — hvis det generer, deaktivér Adobe Acrobat Update Service i services.msc
- Browser-plugin problemer: Gå til **Redigér** → **Indstillinger** → **Internet** og slå browser-integration fra/til
