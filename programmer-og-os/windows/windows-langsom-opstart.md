# Windows starter langsomt

## Problem

Windows tager lang tid om at starte op, og det kan tage flere minutter fra tænd-knappen trykkes til skrivebordet er klar til brug.

## Løsning

### 1. Deaktivér unødvendige opstartsprogrammer

1. Tryk **Ctrl + Shift + Esc** for at åbne Task Manager
2. Gå til fanen **Startup** (Opstart)
3. Sortér efter **Startup impact** (Opstartspåvirkning)
4. Højreklik på programmer med "Høj" påvirkning du ikke har brug for ved opstart → **Deaktivér**

Typiske programmer der kan deaktiveres: Spotify, Discord, Steam, Adobe Creative Cloud, Teams (hvis du ikke bruger det dagligt).

### 2. Aktivér Hurtig opstart

1. Åbn **Kontrolpanel** → **Strømstyring** → **Vælg hvad tænd/sluk-knapperne gør**
2. Klik **Skift indstillinger, der i øjeblikket er utilgængelige**
3. Sæt flueben ved **Slå hurtig opstart til**
4. Klik **Gem ændringer**

### 3. Tjek harddisken

En langsom harddisk er den mest almindelige årsag til langsom opstart:

- **HDD vs SSD:** Hvis computeren stadig har en mekanisk harddisk (HDD), er opgradering til SSD den mest effektive forbedring. Opstartstiden kan gå fra 2-3 minutter ned til 15-30 sekunder
- **Tjek diskstatus:** Åbn Kommandoprompt som administrator og kør: `wmic diskdrive get status` — resultatet skal vise "OK"

### 4. Kør diskoprydning

Midlertidige filer kan sænke opstart:

1. Tryk **Win + R**, skriv `cleanmgr` og tryk Enter
2. Vælg C-drevet
3. Markér alle kategorier og klik **OK**

Se også disk-cleanup.md for mere detaljeret oprydning.

### 5. Opdatér drivere og Windows

1. Kør **Windows Update** og installér alle ventende opdateringer
2. Åbn **Enhedshåndtering** og tjek om der er gule advarselstrekanter
3. Opdatér især grafikkort- og chipsæt-drivere fra producentens hjemmeside

### 6. Tjek for malware

1. Åbn **Windows Sikkerhed** → **Virus- og trusselsbeskyttelse**
2. Kør en **Fuld scanning**
3. Malware kan sænke opstart markant

## Bemærkninger

- Den vigtigste enkeltforbedring er at skifte fra HDD til SSD
- Hurtig opstart kan give problemer med dual-boot systemer — deaktivér det i så fald
- Hvis opstartstiden pludselig er blevet længere, så tjek nyligt installerede programmer og seneste Windows-opdateringer
- Brug **Hændelsesloggen** (Event Viewer → Windows Logs → System) til at se om der er fejl ved opstart
