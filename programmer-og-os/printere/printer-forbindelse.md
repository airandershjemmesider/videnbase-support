# Printer forbinder ikke (USB, netværk, Wi-Fi)

## Problem

Printeren kan ikke oprette forbindelse til computeren, uanset om den er tilsluttet via USB, netværkskabel eller Wi-Fi.

## Løsning

### USB-printer

1. **Tjek det basale:**
   - Er USB-kablet sat ordentligt i i begge ender?
   - Prøv en anden USB-port (undgå USB-hubs — brug en port direkte på computeren)
   - Prøv et andet USB-kabel hvis muligt

2. **Geninstallér printeren:**
   - Åbn **Indstillinger** → **Bluetooth og enheder** → **Printere og scannere**
   - Hvis printeren vises: klik på den → **Fjern enhed**
   - Tag USB-kablet ud, vent 30 sekunder, sæt det i igen
   - Windows bør finde printeren automatisk

3. **Installér driver manuelt:**
   - Gå til printerproducentens hjemmeside (HP, Epson, Canon, Brother)
   - Download den nyeste driver til din printermodel og Windows-version
   - Installér og følg vejledningen

### Netværksprinter (kabel)

1. **Tjek at printeren er på netværket:**
   - Udskriv en konfigurationsside fra printerens display (typisk under Netværk/Network)
   - Notér printerens IP-adresse
   - Åbn Kommandoprompt og kør: `ping [IP-adresse]`
   - Hvis ping fejler, er printeren ikke korrekt tilsluttet netværket

2. **Tjek kablet:** Sørg for at netværkskablet er sat i og at der er lys ved netværksporten

3. Se `tilfoej-netvaerksprinter.md` for tilføjelse af netværksprinter

### Wi-Fi-printer

1. **Tjek Wi-Fi-forbindelse:**
   - Sørg for at printeren er forbundet til det **samme** Wi-Fi-netværk som computeren
   - Mange printere har en Wi-Fi-statusknap eller menu i displayet
   - Hvis printeren har 5 GHz og 2.4 GHz, prøv 2.4 GHz (bedre rækkevidde og kompatibilitet)

2. **Genopret Wi-Fi-forbindelse:**
   - Gå til printerens netværksindstillinger i displayet
   - Vælg **Wi-Fi Setup Wizard** eller lignende
   - Vælg dit netværk og indtast adgangskoden

3. **WPS-forbindelse (hvis routeren understøtter det):**
   - Tryk WPS-knappen på routeren
   - Inden for 2 minutter: Tryk WPS-knappen på printeren eller vælg WPS i printermenuen

### Generelt for alle forbindelsestyper

1. **Kør printerfejlfinding:**
   - Åbn **Indstillinger** → **System** → **Fejlfinding** → **Andre fejlfindingsværktøjer**
   - Klik **Kør** ud for **Printer**

2. **Genstart Print Spooler-tjenesten:**
   - Tryk **Win + R**, skriv `services.msc`, tryk Enter
   - Find **Print Spooler**
   - Højreklik → **Genstart**

3. **Genstart printeren:** Sluk printeren helt, vent 30 sekunder, tænd igen

## Bemærkninger

- Mange moderne printere kræver en app fra producenten (HP Smart, Epson Smart Panel) — disse gør opsætningen nemmere
- Firewall kan blokere netværksprintere — tilføj en undtagelse hvis nødvendigt
- Hvis printeren pludselig stoppede med at virke, tjek om en nylig Windows-opdatering kan have ødelagt driveren
- Ældre printere (10+ år) har måske ikke drivere til Windows 11
