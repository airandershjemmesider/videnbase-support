# Ahrefs — SEO-værktøj

## Hvad er det

Ahrefs er en af de mest udbredte SEO-platforme. Det bruges til site audits, keyword research, backlink-analyse og konkurrentanalyse. Ahrefs crawler det meste af internettet og har en af de største backlink-databaser. Det er et betalt værktøj med forskellige prisplaner.

## Hovedfunktioner

### Site Audit

Kører en fuld crawl af kundens hjemmeside og finder tekniske SEO-fejl.

1. Gå til **Site Audit** → tilføj projekt med kundens domæne
2. Konfigurér crawl-indstillinger (antal sider, crawl-hastighed)
3. Kør audit og vent på resultater
4. Gennemgå fejl opdelt i kategorier:
   - **Errors** (kritisk) — broken links, 5xx server fejl, manglende title tags
   - **Warnings** (vigtige) — lange title tags, manglende meta descriptions, langsom side
   - **Notices** (info) — muligheder for forbedring

**Typiske fund og løsninger:**
- Broken internal links → ret eller fjern links
- Missing H1 tags → tilføj H1 på hver side
- Duplicate content → sæt canonical tags
- Slow pages → optimer hastighed (se GTmetrix guide)
- Orphan pages → tilføj intern linking

### Keywords Explorer

Research af søgeord og søgevolumen.

1. Gå til **Keywords Explorer**
2. Indtast et seed keyword (fx "tandlæge randers")
3. Vælg land: **Denmark**
4. Se resultater:
   - **Search volume** — månedlige søgninger
   - **Keyword Difficulty (KD)** — hvor svært det er at ranke (0-100)
   - **CPC** — pris per klik i Google Ads
   - **SERP overview** — hvem ranker allerede og deres metrics

**Nyttige rapporter:**
- **Matching terms** — variationer af dit søgeord
- **Related terms** — relaterede emner
- **Questions** — spørgsmål folk stiller
- **Also rank for** — hvad top-resultater også ranker for

### Site Explorer

Analyse af backlinks og organisk trafik for ethvert domæne.

1. Gå til **Site Explorer**
2. Indtast domæne (kundens eller konkurrentens)
3. Oversigt viser:
   - **Domain Rating (DR)** — domænets overordnede autoritet (0-100)
   - **Backlinks** — antal links der peger til domænet
   - **Referring domains** — antal unikke domæner der linker
   - **Organic keywords** — antal søgeord domænet ranker for
   - **Organic traffic** — estimeret månedlig trafik fra Google

**Nyttige rapporter:**
- **Organic keywords** — se alle søgeord og positioner
- **Top pages** — hvilke sider får mest trafik
- **Backlinks** — alle indgående links med detaljer
- **Competing domains** — hvem konkurrerer om de samme søgeord

### Content Explorer

Find populært indhold i en niche.

1. Gå til **Content Explorer**
2. Indtast et emne (fx "wordpress sikkerhed")
3. Se artikler sorteret efter organic traffic, social shares eller referring domains
4. Brug til at finde idéer til indhold og linkbuilding-muligheder

### Rank Tracker

Overvåg keyword-placeringer over tid.

1. Tilføj et projekt med kundens domæne
2. Tilføj de søgeord du vil overvåge
3. Vælg land og lokation (fx Denmark)
4. Ahrefs tjekker positioner automatisk og viser tendenser
5. Se positionsændringer, SERP features og konkurrenter

## Daglig brug for kundesupport

### Tjek om ny side er indekseret

1. Site Explorer → indtast den specifikke URL
2. Se om Ahrefs har fundet siden og om den ranker for søgeord
3. Bemærk: Ahrefs opdaterer ikke i realtid — der kan være forsinkelse

### Find broken links

1. Site Audit → kør crawl
2. Filtrér på "Broken links" under Issues
3. Eksportér listen og ret de ødelagte links

### Overvåg placeringer

1. Rank Tracker → åbn kundens projekt
2. Se aktuelle positioner og ændringer
3. Identificér keywords der er faldet — undersøg årsagen

### Konkurrentanalyse

1. Site Explorer → indtast konkurrentens domæne
2. Se deres top keywords og top pages
3. Find "Content Gap" — søgeord konkurrenten ranker for som kunden ikke gør
4. Brug det til at planlægge nyt indhold

## Fejlsøgning

### Data matcher ikke Google Search Console

- Ahrefs estimerer data baseret på egen crawler og klikrate-modeller
- GSC viser faktiske data fra Google
- Brug GSC som sandhed for egne data, Ahrefs til research og konkurrentanalyse

### Site Audit finder for mange/få sider

- Tjek crawl-indstillinger: Er robots.txt respekteret korrekt?
- Er der redirect-loops eller uendelige URL-parametre?
- Justér crawl-scope under projektindstillinger

## Bemærkninger

- Ahrefs er betalt — prisplaner starter fra ca. $99/måned
- Der findes en begrænset gratis version: **Ahrefs Webmaster Tools** (kun Site Audit og Site Explorer for egne sites)
- Ahrefs opdaterer sin database løbende men ikke i realtid — data kan være 1-4 uger gamle
- DR (Domain Rating) er Ahrefs' egen metric — Google bruger den IKKE direkte til ranking
- Kombinér altid Ahrefs-data med Google Search Console for det fulde billede
- Eksportér rapporter som CSV/PDF til kunder der ønsker dokumentation
