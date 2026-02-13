# Fjernskrivebordforbindelse (RDP) opsætning og fejl

## Problem

Du skal oprette en fjernskrivebordforbindelse (Remote Desktop) til en anden computer, eller en eksisterende forbindelse fungerer ikke.

## Løsning

### 1. Aktivér Fjernskrivebord på målcomputeren

Fjernskrivebord skal aktiveres på den computer du vil forbinde TIL:

1. Åbn **Indstillinger** → **System** → **Fjernskrivebord**
2. Slå **Fjernskrivebord** til
3. Bekræft med **Bekræft**
4. Notér **PC-navn** (vises under "Sådan opretter du forbindelse til denne pc")

**NB:** Fjernskrivebord er kun tilgængeligt i Windows Pro, Enterprise og Education — IKKE Windows Home.

### 2. Opret forbindelse fra klientcomputeren

1. Tryk **Win + R**, skriv `mstsc` og tryk Enter (eller søg efter "Forbindelse til fjernskrivebord")
2. Indtast **computernavnet** eller **IP-adressen** på målcomputeren
3. Klik **Opret forbindelse**
4. Indtast brugernavn og adgangskode for en konto på målcomputeren
5. Acceptér certifikatadvarslen (klik **Ja**)

### 3. Justér forbindelsesindstillinger

Før du opretter forbindelse, klik **Vis indstillinger** i RDP-klienten:

- **Fanen Skærm:** Justér opløsning (fuld skærm eller brugerdefineret)
- **Fanen Lokale ressourcer:** Vælg om printer, udklipsholder og drev skal deles
- **Fanen Oplevelse:** Vælg forbindelseshastighed (reducer for langsomme forbindelser)

## Fejlsøgning

### Kan ikke oprette forbindelse

1. **Tjek at målcomputeren er tændt og online**
2. **Ping målcomputeren:**
   ```cmd
   ping [computernavn eller IP]
   ```
3. **Tjek at Fjernskrivebord er aktiveret** på målcomputeren
4. **Tjek firewall:**
   - På målcomputeren: **Windows Sikkerhed** → **Firewall** → **Tillad en app**
   - Sørg for at **Fjernskrivebord** er tilladt for det relevante netværk
5. **Tjek at brugeren har tilladelse:**
   - På målcomputeren: **Indstillinger** → **System** → **Fjernskrivebord** → **Fjernskrivebordsbrugere**
   - Tilføj den bruger der skal have adgang

### Fejl: "Fjerncomputeren kræver godkendelse på netværksniveau"

1. I RDP-klienten: Klik **Vis indstillinger** → **Avanceret** → **Indstillinger** (under Servergodkendelse)
2. Vælg **Opret forbindelse, og advar mig ikke**

Eller på målcomputeren:
1. Åbn **Systemegenskaber** → **Fjernadgang**
2. Fjern flueben ved **Tillad kun forbindelser fra computere, der kører Fjernskrivebord med godkendelse på netværksniveau**

### Fejl: "Interne fejl" eller sort skærm

1. Tryk **Ctrl + Alt + End** (svarer til Ctrl+Alt+Delete i RDP-sessionen)
2. Åbn **Task Manager** og afslut hængende processer
3. Hvis skærmen forbliver sort: Afbryd forbindelsen og opret en ny
4. Opdatér grafikdrivere på målcomputeren

### Langsam eller hakket forbindelse

1. **Reducer farvekvalitet:** I RDP-klienten → **Skærm** → vælg lavere farvedybde (16-bit)
2. **Deaktivér visuelle effekter:** Under **Oplevelse** → vælg **Lav hastighed** eller fjern flueben ved skriftudglatning og baggrundsbilleder
3. **Brug UDP-transport:** Sørg for at port 3389 (TCP og UDP) er åben i firewall
4. **Tjek netværkshastighed:** RDP kræver minimum 1 Mbps for brugbar oplevelse

### RDP fra internet (udenfor netværket)

For at forbinde til en computer der er på et andet netværk:

- **VPN (anbefalet):** Opret VPN-forbindelse til netværket først, derefter brug RDP normalt (se vpn-opsaetning.md)
- **Port forwarding (mindre sikkert):** Videresend port 3389 på routeren til målcomputerens IP — anbefales KUN med stærk adgangskode og NLA aktiveret

### Gem forbindelsesprofil

1. Opsæt forbindelsen med alle indstillinger
2. Klik **Vis indstillinger** → **Gem som** → gem .rdp-filen på skrivebordet
3. Dobbeltklik på filen for hurtigt at forbinde næste gang

## Bemærkninger

- Windows Home understøtter IKKE Fjernskrivebord som vært (server) — kun som klient. Opgrader til Pro eller brug et alternativ som AnyDesk eller TeamViewer
- Kun én bruger kan være logget på ad gangen via RDP (medmindre det er en Windows Server)
- Standardporten for RDP er 3389 — overvej at ændre den af sikkerhedshensyn hvis den er tilgængelig fra internet
- Brug altid stærke adgangskoder til konti med RDP-adgang
- Windows Update kan genstarte maskinen og afbryde RDP-sessioner — konfigurér aktive timer under **Windows Update → Avancerede indstillinger**
