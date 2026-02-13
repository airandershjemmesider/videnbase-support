# Frigør diskplads i Windows

## Problem

C-drevet er ved at være fuldt, og Windows advarer om lav diskplads. Computeren kan blive langsom eller opdateringer kan fejle når der mangler plads.

## Løsning

### 1. Diskoprydning (Disk Cleanup)

1. Tryk **Win + R**, skriv `cleanmgr` og tryk Enter
2. Vælg **C:** drevet
3. Klik **Opryd systemfiler** for at få adgang til flere kategorier
4. Markér følgende:
   - **Windows Update-oprydning** (kan frigøre flere GB)
   - **Midlertidige filer**
   - **Midlertidige internetfiler**
   - **Papirkurv**
   - **Leveringsoptimering**
   - **Tidligere Windows-installationer** (hvis tilgængelig — frigør ofte 10+ GB)
5. Klik **OK** → **Slet filer**

### 2. Aktivér Storage Sense (Lagerassistent)

Storage Sense rydder automatisk op med jævne mellemrum:

1. Åbn **Indstillinger** → **System** → **Lager**
2. Slå **Lagerassistent** til
3. Klik **Konfigurer Lagerassistent**:
   - Kør Lagerassistent: **Hver måned**
   - Slet midlertidige filer: **Til**
   - Slet filer i Papirkurven efter: **30 dage**
   - Slet filer i Downloads efter: **Aldrig** (medmindre du er sikker)

### 3. Find store filer og mapper

Under **Indstillinger** → **System** → **Lager**:

1. Klik på **Vis flere kategorier**
2. Gennemgå de største kategorier:
   - **Apps og funktioner** — afinstallér programmer du ikke bruger
   - **Midlertidige filer** — slet alt der kan slettes
   - **Andre** — viser store mapper Windows ikke kan kategorisere

### 4. Slet midlertidige filer manuelt

Tryk **Win + R** og åbn disse mapper én ad gangen:

- `%temp%` — markér alt (Ctrl+A) og slet. Spring filer over der er i brug
- `temp` — samme procedure
- `prefetch` — samme procedure

### 5. Flyt store filer

Overvej at flytte følgende til et andet drev eller ekstern disk:

- **Videoer og film** (ofte flere GB)
- **Billeder og fotos** (kan fylde meget over tid)
- **Spil** (Steam/Epic kan bruge 50-100 GB per spil)
- **Downloads-mappen** — gennemgå og slet gamle filer

### 6. Reducer WinSxS-mappen

Åbn **Kommandoprompt som administrator**:

```cmd
Dism.exe /online /Cleanup-Image /StartComponentCleanup
```

Dette fjerner gamle komponentversioner og kan frigøre adskillige GB.

## Bemærkninger

- Slet ALDRIG filer direkte i `C:\Windows\` — brug kun de officielle værktøjer
- `hiberfil.sys` kan frigøres med `powercfg /h off` i admin-kommandoprompt (deaktiverer dvale)
- `pagefile.sys` bør normalt ikke ændres medmindre du ved hvad du gør
- Kør Diskoprydning mindst én gang i kvartalet for at holde systemet sundt
- Hvis C-drevet konstant er fuldt, overvej at opgradere til en større SSD
