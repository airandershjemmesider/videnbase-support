# Skærmdeling fejler eller er langsom i Teams

## Problem

Brugeren kan ikke dele sin skærm i et Teams-møde, deltagerne ser en sort skærm, delingen er langsom/hakkende, eller knappen til skærmdeling er gråtonet.

## Løsning

### 1. Tjek at skærmdeling er tilladt

1. I mødet: klik **Del indhold** (ikonet med pil op i en firkant) i mødebjælken
2. Hvis knappen er gråtonet: mødearrangøren har muligvis deaktiveret deling for deltagere
3. Bed arrangøren gå til **Mødeindstillinger** → **Hvem kan præsentere** → sæt til **Alle**

### 2. Vælg den rigtige delingstype

| Type | Hvornår |
|------|---------|
| **Skærm** | Del alt på en bestemt skærm (inkl. notifikationer!) |
| **Vindue** | Del kun ét program — mere sikkert og bruger færre ressourcer |
| **PowerPoint Live** | Bedste oplevelse til præsentationer — deltagere kan selv browse slides |
| **Whiteboard** | Til brainstorm og tegning |

Vinduesdeling er næsten altid bedre end fuld skærmdeling.

### 3. Sort skærm ved deling

**Problem:** Deltagerne ser en sort/tom skærm.

Løsninger:
1. Stop delingen og del igen
2. Prøv at dele et **vindue** i stedet for hele skærmen
3. Deaktiver hardware-acceleration i Teams:
   - Klik **...** → **Indstillinger** → **Generelt**
   - Slå **GPU-hardwareacceleration** fra
   - Genstart Teams
4. Opdater grafikkort-driveren

### 4. Langsom eller hakkende deling

1. **Luk unødvendige programmer** — de bruger CPU og hukommelse
2. **Brug kablet netværk** i stedet for WiFi
3. **Sænk skærmopløsningen** midlertidigt til 1080p
4. **Sluk kameraet** mens du deler — frigiver båndbredde
5. **Deaktiver baggrundseffekter** på kamera — de bruger meget CPU

### 5. Giv Teams tilladelse til skærmoptagelse (Windows)

1. Åbn **Windows-indstillinger** → **Beskyttelse af personlige oplysninger** → **Skærmoptagelse** (eller **Grafik**)
2. Sørg for at Teams har tilladelse
3. På Windows 11: tjek under **Indstillinger** → **System** → **Skærm** → **Grafik** at Teams ikke er sat til strømbesparelse

### 6. Problemer med flere skærme

- Hvis du har flere skærme: vælg den specifikke skærm du vil dele (ikke "Desktop")
- Teams viser en forhåndsvisning af hver skærm — vælg den rigtige
- DPI-skalering på forskellige skærme kan give mærkelige størrelsesforhold

### 7. Skærmdeling i browseren

Teams i browseren (Edge/Chrome) kræver ekstra tilladelse:

1. Når du klikker "Del": browseren viser en popup
2. Vælg **Hele skærmen**, **Vindue** eller **Fane**
3. Klik **Del**
4. Hvis popup ikke vises: tjek at popups ikke er blokeret

## Bemærkninger

- Teams desktop-appen har bedre deling end browserversionen — brug altid desktop-appen til vigtige møder
- "Inkluder computerlyd" skal slås til separat hvis du vil dele lyd fra en video/præsentation
- Skærmdeling bruger 1-2 Mbps upload — sørg for stabil internetforbindelse
- Gæstebrugere har muligvis begrænsede delingsrettigheder afhængigt af organisationens politik
- Admin kan blokere skærmdeling via Teams-politikker i Teams Admin Center
