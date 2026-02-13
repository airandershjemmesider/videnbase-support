# Gendan slettede eller overskrevne filer

## Problem

En bruger har ved et uheld slettet en fil, overskrevet indhold, eller har brug for at gå tilbage til en tidligere version af et dokument i OneDrive eller SharePoint.

## Løsning

### Gendan slettede filer fra OneDrive

#### Papirkurven (op til 93 dage)

1. Gå til [onedrive.com](https://onedrive.com)
2. Klik **Papirkurv** i venstre menu
3. Find filen (brug søgning eller sortér efter dato)
4. Markér filen med flueben
5. Klik **Gendan** i topmenuen
6. Filen gendannes til sin oprindelige placering

#### Second-stage papirkurv (admin)

Hvis filen er slettet fra papirkurven:

1. I papirkurven klik **Second-stage papirkurv** nederst
2. Find filen her (den gemmes i yderligere 93 dage)
3. Markér og klik **Gendan**

### Gendan slettede filer fra SharePoint

1. Gå til SharePoint-sitet
2. Klik **Papirkurv** i venstre menu (eller **Webstedsindhold** → **Papirkurv**)
3. Find og markér filen
4. Klik **Gendan**
5. Filen gendannes til sit oprindelige bibliotek og mappe

### Gendan en overskrevet fil (versionshistorik)

For OneDrive og SharePoint:

1. Gå til dokumentbiblioteket
2. Klik de tre prikker **...** ved filen → **Versionshistorik**
3. Se alle tidligere versioner med dato, tidspunkt og hvem der ændrede
4. Hold musen over en version:
   - Klik versionen for at **åbne og se den**
   - Klik pilen → **Gendan** for at gøre den til den aktive version
5. Den gendannede version bliver den nye aktuelle — den overskrevne version gemmes stadig i historikken

### Gendan en hel OneDrive til et tidligere tidspunkt

Hvis mange filer er påvirket (f.eks. ransomware eller massesletning):

1. Gå til [onedrive.com](https://onedrive.com)
2. Klik tandhjulet → **Indstillinger** → **Gendan din OneDrive**
3. Eller klik **Indstillinger** → **OneDrive-indstillinger** → **Gendan din OneDrive**
4. Vælg en dato og tid på tidslinjen (op til 30 dage tilbage)
5. Gennemgå de ændringer der vil blive fortrudt
6. Klik **Gendan**

### Gendan filer fra Stifinder (Windows)

Hvis filen lå i en synkroniseret OneDrive-mappe:

1. Åbn Stifinder og naviger til OneDrive-mappen
2. Højreklik på mappen → **Egenskaber** → **Tidligere versioner**
3. Vælg en version og klik **Gendan** eller **Åbn**

### Gendan Word/Excel/PowerPoint (autogemt)

For Office-filer med AutoGem aktiveret:

1. Åbn filen i Word/Excel/PowerPoint
2. Klik filnavnet i titellinjen
3. Klik **Versionshistorik**
4. Vælg en tidligere version fra listen
5. Klik **Gendan** for at erstatte den aktuelle version

### Tidsfrister for gendannelse

| Kilde | Tidsgrænse |
|-------|-----------|
| OneDrive papirkurv | 93 dage |
| SharePoint papirkurv (first stage) | 93 dage |
| SharePoint papirkurv (second stage) | 93 dage samlet |
| Versionshistorik | Ubegrænset (standard) |
| OneDrive "Gendan din OneDrive" | 30 dage |
| Windows tidligere versioner | Afhænger af systemkonfiguration |

## Bemærkninger

- Versionshistorik er aktiveret som standard i OneDrive og SharePoint — det koster ingen ekstra plads (versioner tæller ikke mod kvoten i OneDrive)
- I SharePoint tæller versioner mod sitets lagerkvote
- Administratorer kan konfigurere antal versioner der gemmes (standard: 500 i SharePoint)
- "Gendan din OneDrive" er særligt nyttig ved ransomware-angreb
- Filer slettet af en administrator kan gendannes via SharePoint Admin Center eller PowerShell
- Hvis 93-dages fristen er overskredet, kontakt Microsoft Support — de kan i sjældne tilfælde hjælpe
- Backup-løsninger som Veeam eller AvePoint kan give længere opbevaringstider
