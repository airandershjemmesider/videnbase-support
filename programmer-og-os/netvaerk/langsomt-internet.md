# Langsomt internet — fejlsøgning

## Problem

Internetforbindelsen er langsom. Websider tager lang tid om at loade, videoer buffer, og downloads er langsomme.

## Løsning

### 1. Test din hastighed

1. Gå til **speedtest.net** og kør en test
2. Sammenlign resultatet med det din internetudbyder lover
3. Kør testen flere gange og på forskellige tidspunkter

**Tommelfingerregel:**
- Under 10 Mbps: Meget langsomt, problematisk for video
- 10-50 Mbps: OK til normal brug
- 50-100 Mbps: Godt til de fleste
- 100+ Mbps: Hurtigt

### 2. Test med kabel vs. Wi-Fi

Tilslut computeren direkte til routeren med et netværkskabel og test igen:

- **Hastighed OK med kabel, langsom på Wi-Fi:** Problemet er Wi-Fi (se wifi-forbinder-ikke.md)
- **Langsom med begge dele:** Problemet er forbindelsen til udbyderen eller routeren

### 3. Genstart router og modem

1. Sluk modem OG router (tag strømmen fra begge)
2. Vent 30 sekunder
3. Tænd **modem** først — vent til alle lys er stabile (ca. 2 minutter)
4. Tænd **routeren** — vent til den er klar (ca. 2 minutter)
5. Test hastigheden igen

### 4. Tjek hvad der bruger båndbredde

1. Åbn **Task Manager** (Ctrl + Shift + Esc)
2. Gå til fanen **Ydelse** → **Ethernet** eller **Wi-Fi**
3. Klik **Åbn Ressourceovervågning**
4. Gå til fanen **Netværk** for at se hvilke programmer der bruger mest data

Typiske båndbredde-slugere:
- Windows Update i baggrunden
- Cloud-synkronisering (OneDrive, Dropbox, Google Drive)
- Streaming på andre enheder (Netflix, YouTube)
- Spil-opdateringer (Steam, Xbox)

### 5. Skift DNS-server

Langsom DNS kan gøre at websider tager lang tid om at starte med at loade:

Åbn **Kommandoprompt som administrator**:

```cmd
netsh interface ip set dns "Wi-Fi" static 1.1.1.1
netsh interface ip add dns "Wi-Fi" 1.0.0.1 index=2
```

(Erstat "Wi-Fi" med "Ethernet" for kablet forbindelse)

### 6. Ryd DNS-cache

```cmd
ipconfig /flushdns
```

### 7. Tjek for interferens (Wi-Fi)

- Flyt routeren til en central placering
- Placér routeren højt og frit (ikke inde i et skab)
- Hold afstand til mikroovne og andre elektroniske apparater
- Overvej at skifte Wi-Fi-kanal i routerens indstillinger (vælg en med mindre trafik)

### 8. Tjek antal tilsluttede enheder

Log ind på routeren (typisk 192.168.1.1 eller 192.168.0.1) og se hvor mange enheder der er tilsluttet. Mange enheder deler båndbredden.

### 9. Kontakt internetudbyderen

Hvis alt andet er udelukket:

1. Notér dine speedtest-resultater (tidspunkt, hastighed, kabel/Wi-Fi)
2. Ring til udbyderen og rapportér problemet
3. Bed dem tjekke linjen fra deres side
4. Spørg om der er driftsforstyrrelser i dit område

## Bemærkninger

- Internethastighed varierer i løbet af dagen — spidsbelastning er typisk 18-22
- Ældre routere (5+ år) kan være en flaskehals selv med hurtig internetforbindelse
- Ethernet-kabel giver altid den mest stabile og hurtigste forbindelse
- Mesh-Wi-Fi-systemer kan hjælpe i store hjem med dårlig dækning
- VPN reducerer altid hastigheden en smule — prøv at slå VPN fra for at teste
