# Chrome fejlsøgning (langsom, crasher, extensions)

## Problem

Google Chrome er langsom, crasher, bruger for meget hukommelse, eller extensions skaber problemer.

## Løsning

### 1. Chrome er langsom

**Ryd browserdata:**

1. Tryk **Ctrl + Shift + Delete**
2. Vælg tidsinterval: **Altid**
3. Markér:
   - Cachelagrede billeder og filer
   - Cookies og andre webstedsdata (NB: du logges ud af alle sider)
4. Klik **Ryd data**

**Luk unødvendige faner:**

- Hver fane bruger RAM. 20+ åbne faner kan bruge flere GB hukommelse
- Brug **Ctrl + Shift + D** til at gemme alle faner som bogmærker hvis du vil gemme dem

**Deaktivér hardwareacceleration (hvis Chrome er langsom eller glitcher):**

1. Åbn **Indstillinger** (chrome://settings)
2. Klik **System** i venstremenuen
3. Slå **Brug hardwareacceleration, når den er tilgængelig** fra
4. Genstart Chrome

### 2. Chrome crasher

**Opdatér Chrome:**

1. Klik **⋮** (tre prikker) → **Hjælp** → **Om Google Chrome**
2. Chrome tjekker automatisk for opdateringer og installerer dem
3. Klik **Genstart** hvis der er en opdatering

**Nulstil Chrome til standardindstillinger:**

1. Åbn **Indstillinger** → **Nulstil indstillinger**
2. Klik **Gendan indstillingerne til de oprindelige standardindstillinger**
3. Klik **Nulstil indstillinger**

Dette beholder bogmærker og adgangskoder men nulstiller startside, faner, søgemaskine og extensions.

**Opret en ny profil (hvis nulstilling ikke hjælper):**

1. Klik på profilikonet øverst til højre
2. Klik **Tilføj** for at oprette en ny profil
3. Test om Chrome fungerer i den nye profil
4. Hvis ja: Den gamle profil er korrupt — overfør bogmærker manuelt

### 3. Chrome bruger for meget hukommelse

**Brug Chromes egen Task Manager:**

1. Tryk **Shift + Esc** (inde i Chrome)
2. Se hvilke faner og extensions der bruger mest hukommelse
3. Markér ressource-krævende processer → **Afslut proces**

**Aktivér Memory Saver:**

1. Åbn **Indstillinger** → **Ydelse**
2. Slå **Hukommelsesbesparelse** til
3. Inaktive faner frigør automatisk hukommelse

### 4. Extensions skaber problemer

**Test i inkognito-tilstand:**

1. Tryk **Ctrl + Shift + N** for at åbne inkognito-vindue
2. Extensions er som standard deaktiverede i inkognito
3. Hvis Chrome fungerer fint i inkognito: En extension er årsagen

**Find den problematiske extension:**

1. Åbn **chrome://extensions**
2. Deaktivér alle extensions
3. Aktivér dem én ad gangen og test efter hver
4. Når problemet vender tilbage, har du fundet synderen

**Fjern uønskede extensions:**

1. Åbn **chrome://extensions**
2. Klik **Fjern** på extensions du ikke genkender eller ikke bruger

### 5. Chrome starter ikke

1. Tjek om Chrome allerede kører: **Task Manager** (Ctrl + Shift + Esc) → find "Google Chrome" → **Afslut opgave**
2. Prøv at starte igen
3. Hvis det stadig ikke virker: Omdøb Chrome-profilen:
   - Tryk **Win + R**, skriv `%LOCALAPPDATA%\Google\Chrome\User Data`
   - Omdøb mappen **Default** til **Default.old**
   - Start Chrome — den opretter en ny profil

### 6. Webside vises forkert

1. Prøv **Ctrl + F5** (hard refresh — omgår cache)
2. Prøv i inkognito-tilstand
3. Ryd cache for den specifikke side: **F12** → **Netværk** → markér **Deaktiver cache** → genindlæs

## Bemærkninger

- Chrome opdaterer sig selv automatisk — sørg for at genstarte browseren regelmæssigt
- Adgangskoder og bogmærker synkroniseres via Google-kontoen — de forsvinder ikke ved nulstilling
- Chrome med 50+ extensions bliver altid langsom — hold antallet nede
- Alternativ: **Edge** er baseret på samme teknologi som Chrome og bruger generelt mindre hukommelse
- Virksomhedspolitikker (Group Policy) kan forhindre ændringer af visse Chrome-indstillinger
