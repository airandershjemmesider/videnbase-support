# Google Search Console

## Hvad er det

Google Search Console (GSC) er et gratis værktøj fra Google til at overvåge og forbedre en hjemmesides synlighed i Googles søgeresultater. Det viser hvordan Google ser sitet, hvilke søgninger der fører trafik til det, og om der er tekniske problemer med indeksering.

## Opsætning

### Tilføj property

1. Gå til [search.google.com/search-console](https://search.google.com/search-console)
2. Log ind med kundens Google-konto (eller din egen som manager)
3. Klik **Add property**
4. Vælg type:
   - **Domain** (anbefalet) — dækker alle subdomæner og protokoller
   - **URL prefix** — dækker kun den specifikke URL-variant

### Verificering

**DNS TXT record (anbefalet til Domain-type):**
1. Google giver dig en TXT record (fx `google-site-verification=ABC123...`)
2. Tilføj den som TXT record i DNS hos hostingudbyderen
3. Vent 5-10 minutter og klik **Verify**

**Andre metoder (kun URL prefix):**
- HTML-fil upload til roden af sitet
- HTML meta-tag i `<head>`
- Google Analytics (kræver eksisterende GA)
- Google Tag Manager (kræver eksisterende GTM)

### Indsend sitemap

1. Gå til **Sitemaps** i venstre menu
2. Indtast `sitemap_index.xml` (RankMath) eller `sitemap.xml` (Yoast)
3. Klik **Submit**
4. Status skal vise **Success** efter et par minutter

## Daglig brug

### Performance-rapport

- **Klik** — antal gange brugere klikkede på dit site i søgeresultater
- **Visninger** — antal gange dit site blev vist i søgeresultater
- **CTR** — click-through rate (klik / visninger)
- **Gennemsnitlig position** — hvor højt sitet rangerer i gennemsnit

Filtrer på søgeforespørgsler, sider, lande, enheder og dato.

### URL-inspektion

1. Indtast en URL i søgefeltet øverst
2. Se om siden er indekseret af Google
3. Klik **Request Indexing** for at anmode om (gen)indeksering
4. Nyttig når en ny side er oprettet eller en side er opdateret

### Dækning (Pages-rapport)

- **Not indexed** — sider Google kender til men ikke har indekseret
- **Indexed** — sider der er i Googles indeks
- Tjek "Why pages aren't indexed" for specifikke årsager

### Core Web Vitals

- Viser om siderne opfylder Googles hastighedskrav
- Opdelt i Mobile og Desktop
- Klik ind for at se specifikke URL-grupper med problemer

## Fejlsøgning

### "URL is not on Google"

1. **Tjek robots.txt** — besøg `domæne.dk/robots.txt` og se om siden er blokeret
2. **Tjek noindex** — se i sidens HTML eller i RankMath/Yoast om der er sat noindex
3. **Tjek canonical** — se om canonical-tagget peger på en anden URL
4. **Tjek sitemap** — er siden inkluderet i sitemap?
5. **Anmod om indeksering** — brug URL-inspektion og klik Request Indexing

### "Crawled - currently not indexed"

- Google har set siden men valgt ikke at indeksere den
- Typisk årsag: Tyndt indhold, duplikeret indhold, eller lav kvalitet
- Løsning: Forbedre indholdet, tilføj intern linking, fjern duplikater

### "Discovered - currently not indexed"

- Google kender URL'en men har ikke crawlet den endnu
- Kan skyldes crawl-budget eller prioritering
- Løsning: Indsend sitemap igen, tilføj interne links til siden

## Bemærkninger

- Data i GSC har typisk 2-3 dages forsinkelse
- Performance-data kan filtreres op til 16 måneder tilbage
- Tilføj alle relevante brugere (kunden, dig selv) under **Settings → Users and permissions**
- GSC advarsler sendes via e-mail — tjek at notifikationer er slået til
- **Mobile usability** issues påvirker ranking — ret dem hurtigt
- **Manual actions** er alvorlige (Google-straf) — følg vejledningen for at løse dem
- **Security issues** (hacked content, malware) kræver øjeblikkelig handling
