# Zoom fejlsøgning (lyd, video, forbindelse)

## Problem

Zoom fungerer ikke korrekt — der er problemer med lyd, video, eller forbindelsen til møder.

## Løsning

### 1. Lydproblemer — andre kan ikke høre mig

1. **Tjek at mikrofonen ikke er muted:** Klik på mikrofon-ikonet nederst til venstre i Zoom
2. **Vælg den rigtige mikrofon:**
   - Klik pilen ved siden af mikrofon-ikonet → vælg den korrekte mikrofon
   - Eller gå til **Indstillinger** → **Lyd** → vælg den rigtige under **Mikrofon**
3. **Test mikrofonen:** Klik **Test Mic** i lydindstillingerne og tal — du bør se udsving på lydmåleren
4. **Tjek Windows-lydindstillinger:**
   - Højreklik på højttalerikonet i proceslinjen → **Lydindstillinger**
   - Under **Input** → tjek at den rigtige mikrofon er valgt
   - Klik **Mikrofon** og tjek at lydstyrken ikke er 0

### 2. Lydproblemer — jeg kan ikke høre andre

1. **Tjek højttalervalg i Zoom:** Klik pilen ved mikrofon-ikonet → kontrollér at den rigtige højttaler/headset er valgt
2. **Test højttaler:** Indstillinger → Lyd → **Test Speaker**
3. **Tjek lydstyrken i Windows:** Klik på højttalerikonet i proceslinjen og skru op
4. **Tjek at Zoom ikke er muted i Windows Volume Mixer:**
   - Højreklik højttalerikonet → **Åbn lydstyrkemixer**
   - Sørg for at Zoom ikke er skruet ned

### 3. Videoproblemer — kameraet virker ikke

1. **Tjek at kameraet ikke er blokeret:** Klik på kameraikonet i Zoom for at aktivere det
2. **Vælg det rigtige kamera:** Klik pilen ved kameraikonet → vælg korrekt kamera
3. **Tjek om andre programmer bruger kameraet:** Luk Teams, Skype, browsere og andre programmer der kan bruge kameraet
4. **Tjek Windows kamera-tilladelser:**
   - Åbn **Indstillinger** → **Privatliv og sikkerhed** → **Kamera**
   - Sørg for at **Kameraadgang** er slået til
   - Sørg for at **Zoom** har tilladelse
5. **Tjek fysisk kamera:** Mange bærbare har en fysisk skyder eller knap til at slå kameraet fra

### 4. Forbindelsesproblemer

**Kan ikke oprette forbindelse til mødet:**

1. Tjek din internetforbindelse (kan du åbne websider?)
2. Tjek at møde-ID og adgangskode er korrekte
3. Prøv at deltage via **browserlinket** i stedet for appen
4. Tjek om din firewall blokerer Zoom:
   - Åbn **Windows Sikkerhed** → **Firewall og netværksbeskyttelse** → **Tillad en app gennem firewallen**
   - Sørg for at **Zoom Video Conference** er tilladt for Private og Offentlige netværk

**Dårlig forbindelse / hakken:**

1. Brug kablet internet i stedet for Wi-Fi hvis muligt
2. Sluk video for at spare båndbredde
3. Luk andre programmer der bruger internet (streaming, downloads)
4. Brug **Zoom** → **Indstillinger** → **Video** → slå **HD** fra
5. Bed andre deltagere gøre det samme hvis de hakker

### 5. Opdatér Zoom

Zoom opdateres ofte og ældre versioner kan have fejl:

1. Åbn Zoom
2. Klik på dit profilbillede øverst til højre
3. Klik **Søg efter opdateringer**
4. Installér hvis tilgængelig og genstart Zoom

### 6. Geninstallér Zoom

Hvis intet andet virker:

1. Åbn **Indstillinger** → **Apps** → **Installerede apps**
2. Find **Zoom** → **Afinstaller**
3. Download den nyeste version fra **zoom.us/download**
4. Installér og log ind igen

### 7. Test før mødet

Brug Zooms testmøde til at teste lyd og video FØR det rigtige møde:

1. Gå til **zoom.us/test**
2. Klik **Join** og test mikrofon, højttaler og kamera

## Bemærkninger

- Zoom kræver minimum 1.5 Mbps upload/download for videoopkald i god kvalitet
- Bluetooth-headsets kan give forsinkelse — kablet headset er mere pålideligt
- Baggrundsstøj kan filtreres: **Indstillinger** → **Lyd** → **Suppress background noise** → **High**
- Virtuelle baggrunde kræver en rimelig ny CPU — deaktivér dem hvis Zoom er langsomt
- I virksomhedsmiljøer kan IT-politikker begrænse visse Zoom-funktioner
