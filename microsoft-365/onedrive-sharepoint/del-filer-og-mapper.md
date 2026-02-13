# Del filer og mapper sikkert i OneDrive og SharePoint

## Problem

En bruger vil dele en fil eller mappe med kolleger eller eksterne personer via OneDrive eller SharePoint, men er usikker på de forskellige delingsmuligheder og sikkerhedsimplikationer.

## Løsning

### Del fra OneDrive (web)

1. Gå til [onedrive.com](https://onedrive.com) og log ind
2. Højreklik på filen eller mappen → **Del**
3. Klik på tandhjulet eller **Linkindstillinger** for at vælge delingstype:
   - **Alle med linket** — alle der har linket kan åbne (mindst sikkert)
   - **Personer i [din organisation]** — kun kolleger med M365-konto
   - **Personer med eksisterende adgang** — kun dem der allerede har adgang
   - **Bestemte personer** — kun de navngivne personer (mest sikkert)
4. Vælg om modtagerne kan **Redigere** eller kun **Vise**
5. Skriv email-adresser eller kopier linket
6. Klik **Send** eller **Kopiér link**

### Del fra Stifinder (Windows)

1. Højreklik på filen i din OneDrive-mappe
2. Vælg **OneDrive** → **Del**
3. Delingsvinduet åbnes — samme muligheder som web
4. Vælg tilladelser og del

### Del fra SharePoint

1. Gå til SharePoint-dokumentbiblioteket
2. Klik de tre prikker **...** ved filen → **Del**
3. Konfigurer delingsindstillinger som ovenfor
4. Klik **Send**

### Oversigt over delingstyper

| Delingstype | Sikkerhed | Brug |
|-------------|-----------|------|
| Bestemte personer | Højest | Fortrolige dokumenter, kontrakter |
| Kun din organisation | Høj | Interne arbejdsdokumenter |
| Alle med linket + kodeord | Mellem | Deling med eksterne, midlertidig adgang |
| Alle med linket | Lavest | Offentlige dokumenter, marketing |

### Avancerede delingsindstillinger

Når du klikker **Linkindstillinger**:

- **Tillad redigering:** fra/til — kontroller om modtageren kan ændre filen
- **Udløbsdato:** sæt en dato hvor linket automatisk deaktiveres
- **Adgangskode:** kræv et password for at åbne linket
- **Bloker download:** tillad kun visning, ikke download (kun visse filtyper)

### Tjek og administrer delinger

1. Gå til OneDrive web
2. Klik **Delt** i venstre menu → **Delt af dig**
3. Her ses alle filer du har delt med andre
4. Klik de tre prikker **...** → **Administrer adgang**
5. Her kan du:
   - Se hvem der har adgang
   - Fjerne personer
   - Ændre tilladelser
   - Slette delingslinks

### Stop deling

1. Højreklik filen → **Del** → **Administrer adgang**
2. Find personen eller linket
3. Klik **X** for at fjerne adgang
4. Eller klik på linket → **Fjern link**

## Bemærkninger

- Administratorer kan begrænse delingsmuligheder — f.eks. blokere "Alle med linket" for eksterne
- Delte filer tæller kun én gang mod lagringskvoten (afsenderens OneDrive)
- Modtagere af delte filer kan se dem under "Delt med mig" i deres eget OneDrive
- Filer delt via SharePoint arver som standard bibliotekets tilladelser
- Udløbsdatoer på links er stærkt anbefalet for ekstern deling
- Administratorer kan opsætte Data Loss Prevention (DLP) politikker der automatisk blokerer deling af følsomt indhold
- Audit logs i M365 Admin Center viser hvem der har delt hvad og med hvem
