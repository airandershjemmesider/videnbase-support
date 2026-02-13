# OneDrive synkroniseringsproblemer

## Problem

OneDrive synkroniserer ikke filer korrekt. Filer sidder fast med synkroniseringsstatus "venter", OneDrive-ikonet viser fejl (rødt kryds eller gul trekant), eller ændringer lokalt afspejles ikke i skyen.

## Løsning

### 1. Tjek OneDrive-status

1. Klik på OneDrive-ikonet (skyen) i proceslinjen nederst til højre
2. Tjek status:
   - **Hvid sky:** alt er synkroniseret
   - **Blå sky:** synkronisering er i gang
   - **Sky med gul trekant:** der er advarsler
   - **Sky med rødt kryds:** synkronisering er stoppet/fejler
3. Klik på ikonet for at se detaljer om fejl

### 2. Genstart OneDrive-synkronisering

1. Højreklik på OneDrive-ikonet i proceslinjen
2. Klik tandhjulet → **Afslut OneDrive**
3. Tryk **Win + R**, skriv `%localappdata%\Microsoft\OneDrive\OneDrive.exe` og tryk Enter
4. OneDrive starter og begynder at synkronisere igen

### 3. Nulstil OneDrive

Hvis genstart ikke hjælper:

1. Tryk **Win + R**
2. Skriv: `%localappdata%\Microsoft\OneDrive\onedrive.exe /reset`
3. Tryk Enter
4. Vent 1-2 minutter — OneDrive bør starte automatisk
5. Hvis ikke: start OneDrive manuelt fra Startmenuen

### 4. Løs specifikke synkroniseringsfejl

**"Filen er i brug":**
- Luk filen i alle programmer
- Tjek om filen er åben i en anden app (Excel, Word)
- Genstart computeren hvis nødvendigt

**"Filnavnet er ikke tilladt":**
- Fjern specialtegn: `# % & * : < > ? / \ | "`
- Forkort filnavnet (maks 400 tegn inkl. sti)
- Fjern punktum i slutningen af filnavnet

**"Ikke nok plads":**
- Tjek ledig plads lokalt og i skyen
- OneDrive giver 1 TB per bruger med M365-licens
- Brug "Filer efter behov" for at frigøre lokal plads

### 5. Aktiver "Filer efter behov"

Denne funktion sparer lokal diskplads:

1. Højreklik OneDrive-ikonet → tandhjulet → **Indstillinger**
2. Gå til **Synkronisering og backup**
3. Under **Filer efter behov**: slå det til
4. Filer vises i Stifinder men downloades kun når du åbner dem
5. Ikoner i Stifinder viser status:
   - **Sky (blå):** kun i skyen, downloades ved åbning
   - **Grønt flueben:** synkroniseret og tilgængelig offline
   - **Grønt flueben i cirkel:** altid tilgængelig offline

### 6. Tjek netværk og proxy

1. Sørg for stabil internetforbindelse
2. Firewalls/proxy: OneDrive kræver adgang til `*.sharepoint.com` og `*.onedrive.com`
3. VPN kan forsinke synkronisering — test uden VPN

### 7. Frakobl og tilknyt OneDrive igen (sidste udvej)

1. Højreklik OneDrive-ikonet → tandhjulet → **Indstillinger**
2. Gå til **Konto** → **Fjern tilknytning til denne pc**
3. Log ind igen med din M365-konto
4. Vælg placering for OneDrive-mappen (brug standarden)
5. Synkroniseringen starter forfra

## Bemærkninger

- OneDrive kan synkronisere op til 300.000 filer (anbefalet under 100.000 for bedste ydeevne)
- Filer over 250 GB kan ikke synkroniseres
- Midlertidige filer (~$fil.docx) synkroniseres ikke — det er normalt
- "Filer efter behov" kræver Windows 10 1709 eller nyere
- Upload-hastigheden begrænses automatisk for at undgå at fylde båndbredden — dette kan justeres i OneDrive-indstillinger
- Konfliktfiler (når to personer redigerer samtidig offline) får suffikset "-Brugerens computer" i filnavnet
