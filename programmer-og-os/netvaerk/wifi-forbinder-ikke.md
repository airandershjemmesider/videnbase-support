# WiFi forbinder ikke eller mister forbindelse

## Problem

Computeren kan ikke oprette forbindelse til Wi-Fi, eller forbindelsen falder ud med jævne mellemrum.

## Løsning

### 1. Tjek det basale

- Er Wi-Fi slået til? Tjek Wi-Fi-ikonet i proceslinjen og sørg for at **Flytilstand** er slået fra
- Er routeren tændt og fungerer? Tjek om andre enheder kan forbinde
- Er du inden for rækkevidde? Flyt tættere på routeren og prøv igen

### 2. Glem netværket og opret forbindelse igen

1. Klik på Wi-Fi-ikonet i proceslinjen
2. Højreklik på det problematiske netværk → **Glem**
3. Klik på netværket igen → **Opret forbindelse**
4. Indtast adgangskoden på ny

### 3. Genstart netværksadapter

1. Åbn **Indstillinger** → **Netværk og internet** → **Avancerede netværksindstillinger**
2. Find din Wi-Fi-adapter
3. Klik **Deaktivér** — vent 10 sekunder — klik **Aktivér**

Alternativt via Kommandoprompt (admin):

```cmd
netsh interface set interface "Wi-Fi" disable
timeout /t 10
netsh interface set interface "Wi-Fi" enable
```

### 4. Nulstil netværksindstillinger

1. Åbn **Indstillinger** → **Netværk og internet** → **Avancerede netværksindstillinger**
2. Klik **Netværksnulstilling**
3. Klik **Nulstil nu**
4. Computeren genstarter og alle netværksindstillinger nulstilles

**OBS:** Du skal indtaste alle Wi-Fi-adgangskoder igen efter nulstilling.

### 5. Opdatér Wi-Fi-driver

1. Åbn **Enhedshåndtering** (Win + X → Enhedshåndtering)
2. Udvid **Netværkskort**
3. Højreklik på Wi-Fi-adapteren → **Opdater driver**
4. Vælg **Søg automatisk efter drivere**

Hvis det ikke hjælper:
- Gå til computerproducentens hjemmeside (HP, Lenovo, Dell)
- Download den nyeste Wi-Fi-driver til din model

### 6. Deaktivér strømbesparelse for Wi-Fi

1. Åbn **Enhedshåndtering**
2. Højreklik på Wi-Fi-adapteren → **Egenskaber**
3. Gå til fanen **Strømstyring**
4. Fjern flueben ved **Tillad, at computeren slukker denne enhed for at spare strøm**
5. Klik **OK**

### 7. Skift DNS-server

1. Åbn **Indstillinger** → **Netværk og internet** → **Wi-Fi** → **Hardwareegenskaber**
2. Klik **Rediger** ud for DNS-servertildeling
3. Vælg **Manuel** og slå **IPv4** til
4. Foretrukken DNS: `8.8.8.8` (Google) eller `1.1.1.1` (Cloudflare)
5. Alternativ DNS: `8.8.4.4` eller `1.0.0.1`

### 8. Genstart routeren

1. Sluk routeren (tag strømmen)
2. Vent mindst 30 sekunder
3. Tænd routeren og vent 2-3 minutter til den er klar
4. Prøv at forbinde igen

## Bemærkninger

- Wi-Fi 5 GHz er hurtigere men har kortere rækkevidde end 2.4 GHz — prøv at skifte bånd
- Mikroovne, babyalarmer og Bluetooth-enheder kan forstyrre 2.4 GHz Wi-Fi
- Hvis mange enheder er på netværket, kan routeren blive overbelastet
- Et ustabilt Wi-Fi-signal kan skyldes forældet router-firmware — tjek for opdateringer i routerens admin-panel
- Hvis kun én computer har problemer, peger det på en driver- eller softwarefejl snarere end routeren
