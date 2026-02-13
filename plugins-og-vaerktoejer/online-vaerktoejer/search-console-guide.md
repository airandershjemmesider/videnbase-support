# Google Search Console — Komplet Guide

## Hvad er Search Console

Google Search Console (GSC) er Googles gratis værktøj til at overvåge hvordan et site præsterer i søgeresultater. Det er det eneste sted du kan se:

- Præcis hvilke søgeord der bringer trafik til sitet
- Hvordan Google indekserer siderne
- Tekniske problemer der påvirker synlighed
- Core Web Vitals og mobilvenlighed

GSC er uundværligt for alle sites. Opsæt det altid som det første ved nye projekter.

## Verificering

### Metode 1: DNS TXT Record (anbefalet)

Bedst til **Domain property** (dækker alle subdomæner og protokoller):

1. Gå til [search.google.com/search-console](https://search.google.com/search-console)
2. Klik **Add property** → Vælg **Domain**
3. Indtast domænet (fx `eksempel.dk` — uden https://)
4. Google giver en TXT record (fx `google-site-verification=AbCdEf123456`)
5. Tilføj TXT recorden i DNS hos hostingudbyderen
6. Vent 5-10 minutter → Klik **Verify**

### Andre Verifikationsmetoder

Disse virker kun med **URL prefix** property:

| Metode | Hvordan |
|--------|---------|
| HTML fil | Upload en `.html` fil til sitets rod |
| HTML tag | Tilføj `<meta>` tag i sidens `<head>` |
| Google Analytics | Automatisk hvis GA4 allerede er installeret |
| GTM | Automatisk hvis GTM-containeren er installeret |

**Anbefaling:** Brug altid Domain property med DNS-verificering. Det giver det mest komplette billede.

## Tilføj Sitemap

1. Gå til **Sitemaps** i venstre menu
2. Indtast sitemap-URL:
   - RankMath: `sitemap_index.xml`
   - Yoast: `sitemap_index.xml`
3. Klik **Submit**
4. Vent — status skal vise **Success**

RankMath genererer automatisk et sitemap med alle offentlige sider, indlæg og custom post types. Tjek at kun relevante indholdstyper er inkluderet under RankMath → Sitemap Settings.

## Performance Rapport

Den vigtigste rapport i GSC. Viser fire metrics:

| Metric | Betydning | Godt tegn |
|--------|-----------|-----------|
| **Clicks** | Antal klik fra søgeresultater til dit site | Stigende trend |
| **Impressions** | Antal gange dit site blev vist i søgeresultater | Stigende trend |
| **CTR** | Klik divideret med visninger (i procent) | Over 3-5% gennemsnitligt |
| **Average Position** | Gennemsnitlig placering i søgeresultater | Under 10 (side 1) |

### Filtrér og Analysér

- **Queries** — se hvilke søgeord der driver trafik
- **Pages** — se hvilke sider der præsterer bedst
- **Countries** — geografisk fordeling
- **Devices** — mobil vs. desktop vs. tablet
- **Search Appearance** — rich results, FAQ, osv.
- **Dates** — sammenlign perioder for at se trends

## URL Inspection

Tjek en specifik sides indexeringsstatus:

1. Indtast URL i søgefeltet øverst
2. Se om siden er i Googles indeks
3. Tjek **Coverage**, **Mobile Usability** og **Rich Results**
4. Klik **Request Indexing** for at bede Google om at (gen)crawle siden
5. Begrænsning: Ca. 10-12 requests per dag

**Brug ved:** Nye sider, opdateret indhold, rettet fejl.

## Indexering (Pages Rapport)

Viser status for alle kendte URL'er:

### Indexed

- Sider der er i Googles indeks og kan vises i søgeresultater
- Tjek at vigtige sider er her

### Not Indexed — Årsager

| Status | Betydning | Handling |
|--------|-----------|---------|
| Crawled, not indexed | Google har set siden men valgt ikke at indeksere | Forbedre indhold, tilføj interne links |
| Discovered, not indexed | Google kender URL men har ikke crawlet den | Indsend sitemap, tilføj interne links |
| Excluded by noindex | Siden har `noindex` tag | Fjern noindex hvis siden skal indekseres |
| Blocked by robots.txt | robots.txt blokerer crawling | Ret robots.txt |
| Duplicate without canonical | Google ser siden som duplikat | Sæt korrekt canonical tag |
| Soft 404 | Siden returnerer 200 men ligner en 404 | Tilføj indhold eller redirect |

## Core Web Vitals

Viser om siderne opfylder Googles hastighedskrav:

- **LCP (Largest Contentful Paint)** — skal være under 2,5 sek
- **INP (Interaction to Next Paint)** — skal være under 200 ms
- **CLS (Cumulative Layout Shift)** — skal være under 0,1

Rapporten er opdelt i **Mobile** og **Desktop**. Klik ind for at se hvilke URL-grupper der har problemer. Brug PageSpeed Insights til detaljeret analyse af specifikke sider.

## Mobile Usability

Viser problemer med mobilvisning:

- Tekst for lille til at læse
- Klikbare elementer for tæt på hinanden
- Indhold bredere end skærmen
- Viewport ikke konfigureret

Ret disse problemer — de påvirker både brugeroplevelse og ranking.

## Links Rapport

### External Links

- Hvilke sider andre sites linker til (backlinks)
- Hvilke domæner der linker til dig
- Hvilken ankertekst der bruges

### Internal Links

- Hvilke sider har flest interne links
- Brug til at finde sider med for få interne links (orphan pages)

## Removals

Fjern sider midlertidigt fra søgeresultater:

1. Gå til **Removals** → **New Request**
2. Indtast URL
3. Vælg: Fjern midlertidigt (6 måneder) eller ryd cached version
4. **Bemærk:** Dette er midlertidigt — for permanent fjernelse brug `noindex` eller slet siden

## IndexNow vs Manuelt

| Metode | Hastighed | Brug |
|--------|-----------|------|
| **IndexNow** | Minutter til timer | Plugin-baseret, automatisk ved publicering |
| **Request Indexing (GSC)** | Timer til dage | Manuel, god til enkelt-sider |
| **Sitemap submission** | Dage til uger | Automatisk crawling baseret på sitemap |

RankMath understøtter IndexNow — aktivér det under **RankMath → Instant Indexing**. Det sender automatisk nye og opdaterede URL'er til Bing og Yandex (Google har ikke officielt tilsluttet sig IndexNow endnu, men tester det).

## Forbind med Andre Tjenester

### GA4

1. Gå til GA4 → **Admin** → **Product Links** → **Search Console**
2. Klik **Link** og vælg GSC property
3. Nu kan du se søgedata direkte i GA4 under **Acquisition** → **Search Console**

### RankMath

1. Gå til **RankMath** → **General Settings** → **Analytics**
2. Forbind med Google-kontoen
3. Vælg Search Console property
4. RankMath viser nu GSC-data direkte i WordPress-dashboardet

## Hurtig Tjekliste for Ny Site

- [ ] Search Console property oprettet (Domain type)
- [ ] DNS TXT verificering gennemført
- [ ] Sitemap indsendt (`sitemap_index.xml`)
- [ ] URL Inspection kørt på forsiden og vigtigste sider
- [ ] Core Web Vitals tjekket (efter sitet har trafik)
- [ ] Mobile Usability tjekket
- [ ] Kundens Google-konto tilføjet som ejer/bruger
- [ ] GA4 forbundet med Search Console
- [ ] RankMath forbundet med Search Console
- [ ] IndexNow aktiveret i RankMath
- [ ] Robots.txt verificeret (`domæne.dk/robots.txt`)
- [ ] Notifikationer slået til for e-mail advarsler
