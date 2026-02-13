# Lyd og mikrofon virker ikke i Teams

## Problem

Brugeren kan ikke høre andre eller blive hørt i Teams-opkald og møder. Lyden er forvrænget, mikrofonen opfanges ikke, eller der er ekko.

## Løsning

### 1. Tjek lydindstillinger i Teams

1. Åbn Teams
2. Klik de tre prikker **...** øverst til højre → **Indstillinger**
3. Gå til **Enheder**
4. Tjek at den korrekte **Højttaler**, **Mikrofon** og **Kamera** er valgt
5. Klik **Foretag et testopkald** for at teste lyd og mikrofon
6. Tal ind i mikrofonen — du bør høre din egen stemme afspillet

### 2. Tjek Windows lydindstillinger

1. Højreklik på højttalerikonet i proceslinjen → **Lydindstillinger**
2. Under **Output**: vælg den korrekte lydenhed
3. Under **Input**: vælg den korrekte mikrofon
4. Tal ind i mikrofonen og tjek at VU-meteret bevæger sig
5. Klik **Lydstyrke-mixer** og sørg for at Teams ikke er mutet her

### 3. Giv Teams adgang til mikrofonen

1. Åbn **Windows-indstillinger** → **Beskyttelse af personlige oplysninger** → **Mikrofon**
2. Sørg for at **Tillad apps at få adgang til din mikrofon** er slået til
3. Rul ned og tjek at **Microsoft Teams** har adgang
4. Genstart Teams

### 4. Under et møde — hurtig fejlfinding

1. Klik på de tre prikker **...** i mødebjælken → **Enhedsindstillinger**
2. Skift højttaler og mikrofon direkte i mødet
3. Tjek at du ikke er mutet (mikrofonikonet skal ikke have en streg igennem)
4. Bed modparten tjekke om de er mutet

### 5. Opdater lyddrivere

1. Højreklik **Start** → **Enhedshåndtering**
2. Udvid **Lyd-, video- og spilcontrollere**
3. Højreklik på din lydenhed → **Opdater driver**
4. Vælg **Søg automatisk efter drivere**
5. Genstart computeren

### 6. Ryd Teams-cachen

1. Luk Teams helt (også fra systembakken)
2. Tryk **Win + R**, skriv `%appdata%\Microsoft\Teams` og tryk Enter
3. Slet alt indhold i mappen
4. Start Teams igen og log ind

### 7. Test med en anden enhed

- Tilslut et USB-headset og vælg det i Teams-indstillinger
- Hvis USB-headsettet virker, er det den indbyggede lyd/mikrofon der er problemet
- Bluetooth-enheder kan have forsinkelse — brug kablet forbindelse til vigtige møder

## Bemærkninger

- Bluetooth-headsets med mikrofon: sørg for at vælge "Headset"-profilen (ikke "Stereo") for at mikrofonen virker
- Ekko skyldes ofte at nogen har både højttaler og mikrofon aktiv i samme rum — brug headset
- Teams Web-klienten i browseren kræver separat mikrofontilladelse via browserens adressebar
- VPN kan forårsage lydproblemer — prøv at afbryde VPN midlertidigt
- Netværksproblemer (pakketab, jitter) kan give hakkende lyd — tjek forbindelsen
