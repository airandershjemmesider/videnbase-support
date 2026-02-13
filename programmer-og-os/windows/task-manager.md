# Brug Task Manager til fejlsøgning

## Problem

Computeren er langsom, et program hænger, eller du har brug for at finde ud af hvad der bruger systemressourcerne.

## Løsning

### 1. Åbn Task Manager

Tre måder at åbne den:

- **Ctrl + Shift + Esc** (hurtigste)
- **Ctrl + Alt + Delete** → vælg Task Manager
- Højreklik på proceslinjen → **Task Manager**

Klik **Flere detaljer** hvis den åbner i kompakt visning.

### 2. Fanen Processer — find ressource-slugere

Klik på kolonneoverskrifterne for at sortere:

- **CPU:** Klik for at se hvad der bruger mest processorkraft. Normalt bør intet bruge mere end 5-10% når du ikke arbejder aktivt
- **Hukommelse:** Klik for at se hvad der bruger mest RAM. Chrome er ofte en storforbruger
- **Disk:** Klik for at se hvad der læser/skriver mest til disken. 100% diskforbrug peger ofte på en langsom HDD
- **Netværk:** Klik for at se hvad der bruger båndbredde

### 3. Afslut et program der hænger

1. Find programmet under **Processer**
2. Klik på det for at markere det
3. Klik **Afslut opgave** nederst til højre
4. Hvis det ikke virker: Højreklik → **Gå til detaljer** → Højreklik → **Afslut procestræ**

### 4. Fanen Ydelse — systemovervågning

Giver overblik over systemets helbred:

- **CPU:** Viser belastning over tid. Konstant 100% betyder at noget kræver for meget
- **Hukommelse:** Viser brugt vs. tilgængelig RAM. Hvis den er næsten fuld, har du brug for mere RAM eller færre programmer
- **Disk:** 100% aktiv tid på en HDD er normalt for langsom disk — SSD løser det
- **Netværk:** Viser aktuel netværkshastighed

Klik **Åbn Ressourceovervågning** nederst for endnu mere detaljeret information.

### 5. Fanen Startup (Opstart) — kontrollér opstart

1. Viser alle programmer der starter med Windows
2. **Startup impact** kolonnen viser påvirkningen: Høj, Medium, Lav
3. Højreklik → **Deaktivér** for programmer du ikke har brug for ved opstart
4. Genstarten er nødvendig for at ændringen træder i kraft

Programmer der typisk kan deaktiveres:
- Spotify, Discord, Steam, Skype
- Producentens bloatware (HP, Lenovo, Dell værktøjer)
- Adobe-programmer (medmindre du bruger dem dagligt)

Programmer der IKKE bør deaktiveres:
- Windows Security / Defender
- Lydkort-software (Realtek)
- Cloud-synkronisering du aktivt bruger (OneDrive, Dropbox)

### 6. Fanen Detaljer — avanceret visning

- Viser ALLE kørende processer med PID (proces-ID)
- Højreklik på en proces → **Angiv prioritet** for at give den mere eller mindre CPU-tid
- Højreklik → **Angiv tilhørsforhold** for at begrænse processen til bestemte CPU-kerner
- Nyttigt til at identificere ukendte processer — søg på procesnavnet online

### 7. Fanen Tjenester — baggrundstjenester

- Viser Windows-tjenester og deres status (Kører / Stoppet)
- Højreklik for at starte eller stoppe en tjeneste
- Klik **Åbn Tjenester** nederst for fuld tjenestestyring

## Bemærkninger

- Task Manager opdaterer hvert 1. sekund som standard. Højreklik → **Opdateringshastighed** for at ændre
- Hvis Task Manager ikke kan åbnes, kan det skyldes malware eller gruppepolitik — prøv `taskmgr` fra Kør-dialogen
- Brug **Ressourceovervågning** (resmon) for dybere analyse af disk, netværk og hukommelse
- `Antimalware Service Executable` (Windows Defender) bruger ofte meget CPU/disk under scanning — dette er normalt
- Proces med navnet "System" der bruger meget disk skyldes typisk Windows Search indeksering eller Superfetch
