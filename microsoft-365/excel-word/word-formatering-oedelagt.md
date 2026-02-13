# Word formatering ødelagt / dokumentet ser forkert ud

## Problem

Et Word-dokument viser forkert formatering: typografier er ændret, sideombrydning er forskudt, marginer er forkerte, tekst hopper rundt, eller dokumentet ser helt anderledes ud på en anden computer.

## Løsning

### 1. Vis formateringsmærker

Start med at gøre usynlig formatering synlig:

1. Klik **Hjem** → **¶** (Vis/skjul formateringsmærker) eller tryk **Ctrl + Shift + 8**
2. Nu kan du se:
   - **¶** = afsnitsskift
   - **→** = tabulatorer
   - **·** = mellemrum
   - Sektionsskift, sideskift, kolonneskift

Ofte skyldes formateringsproblemer usynlige sektionsskift eller ekstra afsnitsmærker.

### 2. Fjern uønsket formatering

**Nulstil formatering på en markering:**

1. Markér den problematiske tekst
2. Tryk **Ctrl + Mellemrum** (fjerner tegnformatering)
3. Tryk **Ctrl + Q** (nulstiller afsnitsformatering)
4. Eller: **Hjem** → **Ryd al formatering** (viskelæderikonet)

**Indsæt som ren tekst:**

Når du kopierer tekst fra andre dokumenter/hjemmesider:

1. Tryk **Ctrl + Shift + V** (indsæt som ren tekst)
2. Eller: **Hjem** → **Indsæt** → **Behold kun tekst**
3. Formatér derefter manuelt med typografier

### 3. Brug typografier korrekt

Typografier er nøglen til konsistent formatering:

1. Gå til **Hjem** → **Typografier**
2. Brug altid typografier som **Normal**, **Overskrift 1**, **Overskrift 2** osv.
3. UNDGÅ at formatere manuelt (fed, kursiv, skriftstørrelse direkte)
4. Ændr en typografi: højreklik den → **Rediger** → ændr skrifttype/størrelse/osv.
5. Alle afsnit med den typografi opdateres automatisk

### 4. Ret sideombrydningsproblemer

**Tekst hopper til næste side:**

1. Markér afsnittet der hopper
2. Højreklik → **Afsnit** → fanen **Tekst- og sideskift**
3. Tjek disse indstillinger:
   - **Hold sammen med næste** — binder afsnittet til det næste
   - **Hold linjer sammen** — forhindrer sideskift midt i afsnittet
   - **Sideskift før** — tvinger afsnittet til en ny side
4. Fjern uønskede flueben

**Mærkelige tomme sider:**

1. Vis formateringsmærker (Ctrl + Shift + 8)
2. Gå til den tomme side
3. Markér og slet eventuelle tomme afsnitsmærker **¶** eller sideskift
4. Tjek om en tabel i bunden af forrige side tvinger et ekstra afsnitsmærke

### 5. Ret marginer og layout

1. Gå til **Layout** → **Marginer** → **Brugerdefinerede marginer**
2. Sæt korrekte marginer (standard: 2,54 cm på alle sider)
3. Tjek **Papirstørrelse**: skal typisk være A4
4. Tjek **Sektionsskift**: hvert afsnit kan have egne marginer

### 6. Dokumentet ser anderledes ud på en anden computer

**Årsag: Manglende skrifttyper**

1. Gå til **Filer** → **Indstillinger** → **Gem**
2. Markér **Integrer skrifttyper i filen**
3. Markér **Integrer kun de tegn, der bruges i dokumentet** (sparer plads)
4. Gem dokumentet — skrifttyperne følger nu med

**Årsag: Forskellige printeropsætninger**

1. Gå til **Filer** → **Indstillinger** → **Avanceret**
2. Under **Udskrivning**: markér **Opdater felter før udskrivning**
3. Word tilpasser layout til standardprinteren — skift printer kan ændre sideombrydning

### 7. Reparer et korrupt dokument

1. Åbn Word (tomt dokument)
2. Gå til **Filer** → **Åbn** → find filen
3. Klik pilen ved **Åbn** → vælg **Åbn og reparer**
4. Word forsøger at reparere korrupt formatering

## Bemærkninger

- Kopiering fra PDF og hjemmesider indsætter ofte skjult formatering — brug altid "Indsæt som ren tekst"
- Normal.dotm er Words standardskabelon — en korrupt Normal.dotm kan ødelægge alle nye dokumenter
- Normal.dotm ligger i `%appdata%\Microsoft\Templates\` — omdøb den og genstart Word for en frisk kopi
- Gem som .docx, IKKE .doc — det gamle format håndterer formatering dårligere
- Kompatibilitetstilstand (vises i titellinjen) begrænser funktioner — konvertér via Filer → Konvertér
