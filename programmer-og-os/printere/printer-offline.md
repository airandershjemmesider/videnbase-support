# Printer vises som offline

## Problem

Printeren vises som "Offline" i Windows, selvom den er tændt og tilsluttet. Udskriftsjobs sendes ikke til printeren.

## Løsning

### 1. Tjek det basale

- Er printeren tændt? (Ikke bare standby — tryk på tænd/sluk-knappen)
- Er kablet tilsluttet ordentligt? (USB eller netværk)
- Har printeren en fejltilstand? (Papirstop, tomt blæk, åben klap — tjek displayet)
- Er printeren forbundet til Wi-Fi? (Se printerens netværksstatus)

### 2. Deaktivér "Brug printer offline"

1. Åbn **Indstillinger** → **Bluetooth og enheder** → **Printere og scannere**
2. Klik på den offline printer
3. Klik **Åbn udskriftskø**
4. Klik **Printer** i menulinjen
5. Fjern fluebenet ved **Brug printer offline**

### 3. Sæt printeren som standardprinter

1. Åbn **Indstillinger** → **Bluetooth og enheder** → **Printere og scannere**
2. Slå **Lad Windows styre min standardprinter** fra
3. Klik på den korrekte printer → **Angiv som standard**

### 4. Genstart Print Spooler

1. Tryk **Win + R**, skriv `services.msc`, tryk Enter
2. Find **Print Spooler**
3. Højreklik → **Genstart**
4. Tjek om printeren nu vises som online

### 5. Fjern og tilføj printeren igen

1. Åbn **Indstillinger** → **Bluetooth og enheder** → **Printere og scannere**
2. Klik på den offline printer → **Fjern enhed**
3. Genstart computeren
4. Tilføj printeren igen (se printer-forbindelse.md eller tilfoej-netvaerksprinter.md)

### 6. Tjek netværksforbindelsen (netværksprinter)

1. Åbn Kommandoprompt
2. Kør: `ping [printerens IP-adresse]`
3. Hvis ping fejler:
   - Tjek at printeren og computeren er på samme netværk
   - Genstart printeren
   - Genstart routeren hvis nødvendigt
4. Hvis ping virker men printeren stadig er offline:
   - Printerens IP kan have ændret sig — tjek den aktuelle IP via printerens display
   - Opdatér porten: **Printeregenskaber** → fanen **Porte** → **Konfigurer port** → ret IP-adressen

### 7. Opdatér eller geninstallér driver

1. Åbn **Enhedshåndtering** (Win + X → Enhedshåndtering)
2. Udvid **Udskriftskøer**
3. Højreklik på printeren → **Opdater driver**
4. Hvis det ikke hjælper: Afinstallér driveren og download den nyeste fra producentens hjemmeside

### 8. Tjek Windows-opdateringer

Nogle gange ødelægger en Windows-opdatering printerdrivere:

1. Tjek om en nylig Windows-opdatering faldt sammen med problemet
2. Åbn **Indstillinger** → **Windows Update** → **Opdateringshistorik**
3. Hvis en opdatering er årsag: Afinstallér den under **Afinstaller opdateringer**

## Bemærkninger

- "Offline"-status kan skyldes strømbesparelse på printeren — mange printere går i dvale og svarer ikke på netværk
- Nogle printere mister Wi-Fi efter strømudfald eller routergenstart — de skal genkobles
- SNMP-status kan give falsk "offline" — under **Printeregenskaber** → **Porte** → **Konfigurer port**, fjern flueben ved "SNMP-status aktiveret"
- Dobbelttjek at ingen anden computer "holder" på printeren med et fastlåst udskriftsjob
