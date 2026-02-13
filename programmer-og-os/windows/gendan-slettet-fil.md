# Gendan slettede filer i Windows

## Problem

En fil er blevet slettet ved et uheld, og den skal gendannes. Løsningen afhænger af hvornår og hvordan filen blev slettet.

## Løsning

### 1. Tjek Papirkurven

Det første og nemmeste sted at kigge:

1. Dobbeltklik på **Papirkurven** på skrivebordet
2. Find filen (brug søgefeltet øverst til højre)
3. Højreklik på filen → **Gendan**
4. Filen gendannes til sin oprindelige placering

**Vigtigt:** Filer slettet med **Shift + Delete** springer Papirkurven over og kan ikke gendannes herfra.

### 2. Brug Filhistorik (File History)

Filhistorik skal være aktiveret PÅ FORHÅND for at virke:

1. Højreklik på den mappe hvor filen lå
2. Vælg **Egenskaber** → fanen **Tidligere versioner**
3. Vælg en version fra før filen blev slettet
4. Klik **Gendan** eller **Åbn** for at se indholdet først

#### Aktivér Filhistorik (til fremtiden)

1. Åbn **Indstillinger** → **System** → **Lager** → **Avancerede lagerindstillinger** → **Indstillinger for sikkerhedskopiering**
2. Tilslut en ekstern disk eller vælg en netværksplacering
3. Slå **Sikkerhedskopiér automatisk mine filer** til

### 3. Brug Shadow Copy (Gendannelsespunkter)

Windows opretter automatisk Shadow Copies ved systemgendannelsespunkter:

1. Højreklik på mappen → **Egenskaber** → **Tidligere versioner**
2. Hvis der er gendannelsespunkter tilgængelige, vises de her
3. Vælg en dato og klik **Gendan**

Alternativt via kommandolinjen (admin):

```cmd
vssadmin list shadows
```

### 4. Tjek cloud-synkronisering

Hvis filen lå i en synkroniseret mappe:

- **OneDrive:** Gå til onedrive.com → Papirkurv (gemmer filer i 30 dage)
- **Google Drive:** drive.google.com → Papirkurv
- **Dropbox:** dropbox.com → Slettede filer

Cloud-tjenester har ofte en 30-dages gendannelsesperiode.

### 5. Windows File Recovery (avanceret)

Microsofts gratis værktøj til dybere gendannelse:

1. Installér **Windows File Recovery** fra Microsoft Store
2. Åbn Kommandoprompt
3. Kør f.eks.: `winfr C: D:\Gendannet /regular /n \Users\Brugernavn\Documents\filnavn.docx`

- **Regular mode:** Til nyligt slettede filer på NTFS
- **Extensive mode:** Til ældre slettede filer eller formaterede drev

### 6. Tredjeparts gendannelsesværktøjer

Hvis intet andet virker:

- **Recuva** (gratis) — simpelt og effektivt til de fleste situationer
- **TestDisk/PhotoRec** (gratis, open source) — kraftfuldt men mere teknisk

## Bemærkninger

- Jo hurtigere du handler, jo større chance for gendannelse — nye data kan overskrive slettede filer
- Installér ALDRIG gendannelsesværktøjer på det drev hvor filen blev slettet
- SSD-drev med TRIM gør gendannelse sværere end traditionelle HDD-drev
- Den bedste beskyttelse mod datatab er regelmæssig backup (Filhistorik, OneDrive, ekstern disk)
- Papirkurvens standardstørrelse er 10% af drevet — meget store filer kan springe den over
