# Windows opdateringer fejler eller sidder fast

## Problem

Windows Update sidder fast under download eller installation, giver fejlkoder, eller vil slet ikke køre. Opdateringer kan hænge på en bestemt procentdel i lang tid.

## Løsning

### 1. Kør Windows Update fejlfinding

1. Åbn **Indstillinger** → **System** → **Fejlfinding** → **Andre fejlfindingsværktøjer**
2. Klik **Kør** ud for **Windows Update**
3. Følg vejledningen og genstart når det er færdigt

### 2. Genstart Windows Update-tjenester manuelt

Åbn **Kommandoprompt som administrator** og kør:

```cmd
net stop wuauserv
net stop cryptSvc
net stop bits
net stop msiserver
ren C:\Windows\SoftwareDistribution SoftwareDistribution.old
ren C:\Windows\System32\catroot2 catroot2.old
net start wuauserv
net start cryptSvc
net start bits
net start msiserver
```

Prøv derefter at køre Windows Update igen.

### 3. Kontrollér diskplads

Opdateringer kræver typisk mindst 10-20 GB ledig plads på C-drevet. Tjek under **Denne pc** og frigør plads hvis nødvendigt (se disk-cleanup.md).

### 4. Installér opdateringen manuelt

1. Notér fejlkoden (f.eks. KB5034441)
2. Gå til [Microsoft Update Catalog](https://www.catalog.update.microsoft.com)
3. Søg efter KB-nummeret
4. Download den rigtige version (x64 for de fleste) og installér manuelt

### 5. Opdatering sidder fast under genstart

Hvis skærmen viser "Arbejder på opdateringer" i over 2 timer:

1. Hold tænd/sluk-knappen nede i 10 sekunder for at slukke
2. Tænd igen — Windows vil forsøge at rulle opdateringen tilbage
3. Hvis det gentager sig, start i **Fejlsikret tilstand** (hold Shift nede mens du klikker Genstart)

## Bemærkninger

- Lad altid computeren være tændt under opdateringer — sluk ikke medmindre den har siddet fast i over 2 timer
- Kumulerede opdateringer kan tage 30-60 minutter på ældre hardware
- Fejlkoder som 0x80070002, 0x80073712, 0x800f0922 løses oftest af trin 2 ovenfor
- Hvis intet virker, kan en **reparationsinstallation** (in-place upgrade) med Windows ISO løse det uden tab af data
