# SharePoint tilladelser og adgangsstyring

## Problem

En administrator eller site-ejer skal forstå og administrere tilladelser i SharePoint — hvem der har adgang til hvad, og hvordan man opsætter det korrekt.

## Løsning

### SharePoint tilladelsesniveauer

| Niveau | Rettigheder |
|--------|------------|
| **Fuld kontrol** | Alt — inkl. administration af tilladelser og site-indstillinger |
| **Rediger** | Tilføj, rediger og slet filer og listeelementer |
| **Bidrag** | Tilføj og rediger filer i eksisterende mapper |
| **Læs** | Kun se og downloade filer |
| **Begrænset adgang** | Automatisk tildelt — adgang til specifikke delte filer |

### SharePoint-grupper (standard)

Hvert SharePoint-site oprettes med tre grupper:

| Gruppe | Tilladelse | Typisk brug |
|--------|-----------|-------------|
| **[Site] Ejere** | Fuld kontrol | IT-admins, projektledere |
| **[Site] Medlemmer** | Rediger | Teammedlemmer, medarbejdere |
| **[Site] Besøgende** | Læs | Ledelse, andre afdelinger |

### Tjek tilladelser for et site

1. Gå til SharePoint-sitet
2. Klik tandhjulet → **Webstedsindstillinger** (eller **Siteindstillinger**)
3. Under **Brugere og tilladelser** klik **Webstedstilladelser**
4. Her ses alle grupper og brugere med deres tilladelsesniveau

### Tilføj en bruger til et site

1. Gå til sitet → tandhjulet → **Webstedstilladelser**
2. Klik **Inviter personer** eller **Del websted**
3. Skriv brugerens email
4. Vælg tilladelsesniveau (Ejer, Medlem eller Besøgende)
5. Klik **Tilføj**

### Tilladelser på mappe/fil-niveau

Du kan sætte unikke tilladelser på enkelte mapper eller filer:

1. Gå til dokumentbiblioteket
2. Klik de tre prikker **...** ved mappen/filen → **Administrer adgang**
3. Klik **Avanceret** (eller **Tilladelser for dette element**)
4. Klik **Stop arv af tilladelser** (bryder forbindelsen til overordnet mappe)
5. Tilføj eller fjern brugere som ønsket

**Vigtigt:** Unikke tilladelser gør administration mere kompleks — brug det sparsomt.

### Fjern en brugers adgang

1. Gå til **Webstedstilladelser**
2. Find brugeren eller gruppen
3. Klik de tre prikker → **Fjern bruger fra gruppe**
4. Eller klik **Fjern brugertilladelser** for direkte tildelinger

### Tjek hvad en bestemt bruger kan se

1. Gå til **Webstedstilladelser** → **Kontroller tilladelser**
2. Skriv brugerens email
3. Klik **Kontroller nu**
4. SharePoint viser præcis hvilke tilladelser brugeren har og hvorfra de stammer

### Best practices for tilladelser

1. **Brug grupper, ikke individuelle tilladelser** — lettere at administrere
2. **Arv er din ven** — lad tilladelser arve fra site-niveau nedefter
3. **Minimer unikke tilladelser** — de er svære at overskue og vedligeholde
4. **Gennemgå tilladelser regelmæssigt** — fjern folk der ikke længere har brug for adgang
5. **Dokumenter dine tilladelsesvalg** — specielt for sites med unikke tilladelser
6. **Brug Microsoft 365-grupper** — de synkroniserer automatisk med Teams og Outlook

## Bemærkninger

- Når et team oprettes i Teams, oprettes automatisk et SharePoint-site med matchende tilladelser
- Site Collection Administrators har altid fuld adgang — uanset gruppemedlemskab
- Deling af individuelle filer opretter automatisk "Begrænset adgang"-tilladelser
- Tilladelsesarv kan brydes på ethvert niveau — men det anbefales at holde det simpelt
- PowerShell (PnP.PowerShell) kan bruges til masseadministration af tilladelser
- SharePoint Admin Center giver overblik over alle sites og deres delingsindstillinger
- Sensitivity Labels (følsomhedslabels) kan automatisk styre tilladelser baseret på klassifikation
