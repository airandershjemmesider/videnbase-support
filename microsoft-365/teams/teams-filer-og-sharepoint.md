# Forstå filer i Teams (SharePoint-integration)

## Problem

Brugere er forvirrede over hvor filer i Teams gemmes, hvordan de hænger sammen med SharePoint, og hvorfor filer nogle gange forsvinder eller er svære at finde.

## Løsning

### Hvor gemmes filer i Teams?

| Sted i Teams | Gemmes i |
|-------------|----------|
| Kanal → Filer-fane | SharePoint (teamets site) |
| Privat chat → Filer | Afsenderens OneDrive |
| Mødechat → Filer | Uploaderens OneDrive |
| Wiki / OneNote | SharePoint (teamets site) |

**Vigtigst:** Filer i kanaler = SharePoint. Filer i chats = OneDrive.

### Find filer i SharePoint fra Teams

1. Gå til kanalen i Teams
2. Klik **Filer**-fanen øverst
3. Klik **Åbn i SharePoint** (øverst i filvisningen)
4. Nu er du i SharePoint-biblioteket for den kanal
5. Her har du fuld adgang til versionshistorik, metadata og avanceret deling

### Mappestruktur i SharePoint

Når du opretter et team med kanaler, oprettes denne struktur i SharePoint:

```
Teamets SharePoint-site
└── Dokumenter (bibliotek)
    ├── General          → filer fra General-kanalen
    ├── Salg             → filer fra Salg-kanalen
    └── Marketing        → filer fra Marketing-kanalen
```

Hver standard-kanal svarer til en mappe i "Dokumenter"-biblioteket.

### Synkroniser Teams-filer til din computer

1. Gå til kanalen → **Filer**-fane
2. Klik **Synkroniser** (OneDrive-ikonet)
3. OneDrive-synkronisering starter og opretter en mappe på din computer
4. Mappen vises i Stifinder under dit firmanavn
5. Filer synkroniseres automatisk begge veje

### Upload filer til en kanal

**Metode 1 — Drag and drop:**
1. Åbn kanalen → **Filer**-fane
2. Træk filer fra Stifinder ind i Teams

**Metode 2 — Upload-knappen:**
1. Klik **Upload** → **Filer** eller **Mappe**
2. Vælg filerne og klik **Åbn**

**Metode 3 — I en besked:**
1. Klik papirklipsen (vedhæft) i beskedfeltet
2. Vælg **Upload fra min computer**
3. Filen uploades til kanalens Filer-fane OG vises i beskeden

### Versionshistorik

1. Gå til **Filer**-fanen i kanalen
2. Klik de tre prikker **...** ved filen → **Versionshistorik**
3. Se alle tidligere versioner med dato og hvem der ændrede
4. Klik på en version for at åbne den
5. Klik **Gendan** for at rulle tilbage til en tidligere version

### Filer "forsvinder" — typiske årsager

1. **Filen blev uploadet i en chat, ikke en kanal** → tjek chat-tråden
2. **Filen ligger i en privat kanal** → du har måske ikke adgang
3. **Filen blev slettet** → tjek SharePoint-papirkurven (gendan inden 93 dage)
4. **Filen ligger i en anden kanal** → brug søgefunktionen øverst i Teams

## Bemærkninger

- Private kanaler har deres EGET SharePoint-site — adskilt fra teamets hoved-site
- Maks filstørrelse til upload i Teams: 250 GB
- Filer i Teams arver tilladelser fra teamet/kanalen — du behøver ikke dele separat
- OneDrive-synkronisering kan pause ved dårlig forbindelse — tjek OneDrive-ikonet i proceslinjen
- Undgå specialtegn i filnavne (#, %, &) — de kan give problemer i SharePoint
- Filer delt i privat chat slettes IKKE hvis du sletter chatten — de ligger stadig i OneDrive
- Filstien i SharePoint har en grænse på 400 tegn — hold fil- og mappenavne korte
