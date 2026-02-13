# Blå skærm (BSOD) — de mest gængse årsager

## Problem

Windows viser en blå skærm med en fejlkode og genstarter automatisk. Dette kaldes BSOD (Blue Screen of Death) og skyldes en kritisk systemfejl.

## Løsning

### 1. Notér fejlkoden

Den blå skærm viser typisk:

- En stoppkode (f.eks. `IRQL_NOT_LESS_OR_EQUAL`)
- Nogle gange en filreference (f.eks. `ntfs.sys`)

Notér begge dele — de peger på årsagen.

### 2. De mest gængse fejlkoder

| Fejlkode | Typisk årsag | Løsning |
|-----------|-------------|---------|
| `IRQL_NOT_LESS_OR_EQUAL` | Driverproblem | Opdatér eller rul drivere tilbage |
| `CRITICAL_PROCESS_DIED` | Korrupt systemfil | Kør SFC og DISM |
| `SYSTEM_SERVICE_EXCEPTION` | Driver eller software | Afinstallér nyligt installeret software |
| `KERNEL_DATA_INPAGE_ERROR` | Diskfejl | Tjek harddisk med chkdsk |
| `PAGE_FAULT_IN_NONPAGED_AREA` | RAM-problem | Test RAM med memtest |
| `WHEA_UNCORRECTABLE_ERROR` | Hardwarefejl | Tjek temperaturer og hardware |
| `DPC_WATCHDOG_VIOLATION` | Driver eller SSD | Opdatér SSD-firmware og drivere |

### 3. Kør systemfilkontrol

Åbn **Kommandoprompt som administrator**:

```cmd
sfc /scannow
```

Hvis det finder fejl det ikke kan reparere, kør derefter:

```cmd
DISM /Online /Cleanup-Image /RestoreHealth
```

Genstart og kør `sfc /scannow` igen.

### 4. Tjek drivere

Drivere er den hyppigste årsag til BSOD:

1. Åbn **Enhedshåndtering** (Win + X → Enhedshåndtering)
2. Kig efter enheder med gult advarselstegn
3. Højreklik → **Opdater driver**
4. Hvis BSOD startede efter en driveropdatering: Højreklik → **Egenskaber** → **Rul driver tilbage**

### 5. Tjek RAM (hukommelse)

1. Tryk **Win + R**, skriv `mdsched.exe` og tryk Enter
2. Vælg **Genstart nu og søg efter problemer**
3. Computeren genstarter og tester hukommelsen
4. Resultatet vises efter Windows starter

For mere grundig test: Download og kør **MemTest86** fra USB.

### 6. Tjek harddisken

Åbn **Kommandoprompt som administrator**:

```cmd
chkdsk C: /f /r
```

Svar **J** for at planlægge tjek ved næste genstart, og genstart computeren.

### 7. Tjek Event Viewer for detaljer

1. Tryk **Win + R**, skriv `eventvwr` og tryk Enter
2. Gå til **Windows-logfiler** → **System**
3. Kig efter røde "Fejl" (Error) tæt på tidspunktet for BSOD
4. Disse giver ofte mere detaljeret information om årsagen

### 8. Brug Fejlsikret tilstand

Hvis Windows ikke kan starte normalt:

1. Tænd computeren og sluk den 3 gange i træk (under Windows-logoen)
2. Windows starter automatisk i **Gendannelsesmiljøet**
3. Vælg **Fejlfinding** → **Avancerede indstillinger** → **Startindstillinger** → **Genstart**
4. Tryk **4** for Fejlsikret tilstand eller **5** for Fejlsikret med netværk

## Bemærkninger

- En enkelt BSOD er sjældent alvorlig — gentagne BSOD kræver fejlsøgning
- Overophedning kan forårsage BSOD — rens støv ud af computeren og tjek at blæsere kører
- Nyligt installeret software eller hardware er ofte skyld i pludselige BSOD-problemer
- Windows gemmer minidump-filer i `C:\Windows\Minidump\` som kan analyseres med WinDbg
- Hvis BSOD kun sker under spil eller tung belastning, peger det typisk på GPU-driver, overophedning eller strømforsyning
