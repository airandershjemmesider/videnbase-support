# Tilføj en netværksprinter i Windows

## Problem

Du skal tilføje en printer der er tilsluttet netværket via kabel eller Wi-Fi, så du kan udskrive fra din computer.

## Løsning

### 1. Find printerens IP-adresse

Du har brug for printerens IP-adresse. Find den på én af disse måder:

- **På printerens display:** Gå til Netværk/Network → TCP/IP eller Print Network Configuration
- **Udskriv konfigurationsside:** De fleste printere har en knap eller menuindstilling til dette
- **Tjek routerens admin-side:** Log ind på routeren (typisk 192.168.1.1) og se listen over tilsluttede enheder

### 2. Automatisk søgning (nemmeste metode)

1. Åbn **Indstillinger** → **Bluetooth og enheder** → **Printere og scannere**
2. Klik **Tilføj enhed**
3. Vent mens Windows søger efter printere på netværket
4. Hvis printeren vises: klik på den og følg vejledningen

### 3. Manuel tilføjelse (hvis automatisk søgning ikke finder den)

1. Åbn **Indstillinger** → **Bluetooth og enheder** → **Printere og scannere**
2. Klik **Tilføj enhed**
3. Klik **Tilføj manuelt** (eller "Den printer, jeg søger efter, er ikke angivet")
4. Vælg **Tilføj en printer ved hjælp af en TCP/IP-adresse eller et værtsnavn**
5. Klik **Næste**
6. Vælg **TCP/IP-enhed** under Enhedstype
7. Indtast printerens IP-adresse i feltet **Værtsnavn eller IP-adresse**
8. Lad Portnavn stå som det er
9. Klik **Næste** — Windows kontakter printeren og finder driveren

### 4. Installér driver

Hvis Windows ikke finder driveren automatisk:

1. Vælg producent og model fra listen
2. Eller klik **Windows Update** for at hente flere drivere
3. Eller klik **Har diskette** og peg på den downloadede driver fra producentens hjemmeside

### 5. Delt printer fra en anden computer

Hvis printeren er tilsluttet en anden Windows-computer og delt:

1. Vælg **Vælg en delt printer efter navn** under manuel tilføjelse
2. Indtast: `\\computernavn\printernavn`
3. Eller klik **Gennemse** for at finde den på netværket

### 6. Test udskrift

1. Gå til **Indstillinger** → **Printere og scannere** → klik på den nye printer
2. Klik **Udskriv en testside**
3. Tjek at siden udskrives korrekt

### 7. Sæt som standardprinter

1. Klik på den nye printer under Printere og scannere
2. Klik **Angiv som standard**

Eller slå fra at Windows styrer standardprinteren: **Indstillinger** → **Printere og scannere** → slå **Lad Windows styre min standardprinter** fra.

## Bemærkninger

- Sørg for at computeren og printeren er på **samme netværk** (samme subnet)
- Statisk IP på printeren anbefales i erhvervsmiljøer, så adressen ikke ændrer sig
- Hvis printerens IP ændrer sig (DHCP), skal forbindelsen muligvis oprettes igen — overvej at reservere IP i routeren
- Firewall kan blokere printerforbindelsen — tilføj en undtagelse for port 9100 (RAW), 631 (IPP) eller 515 (LPR)
- HP-printere fungerer ofte bedst med HP Smart-appen, Epson med Epson Smart Panel
