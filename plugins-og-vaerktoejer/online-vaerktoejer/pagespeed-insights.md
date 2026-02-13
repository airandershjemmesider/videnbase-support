# Google PageSpeed Insights

## Hvad er det

Google PageSpeed Insights (PSI) er Googles eget gratis værktøj til at måle hjemmesiders hastighed og brugeroplevelse. Det kombinerer to datakilder: lab-data (Lighthouse-simulering) og field-data (Chrome UX Report fra rigtige brugere). Da Google selv bruger Core Web Vitals som rankingfaktor, er PSI den mest autoritative kilde til at vurdere performance.

## Forskel fra GTmetrix

| Aspekt | PageSpeed Insights | GTmetrix |
|--------|-------------------|----------|
| **Datakilde** | Lab-data + rigtige brugerdata (CrUX) | Kun lab-data |
| **Brugerdata** | Ja — Chrome UX Report (28 dages rullende data) | Nej |
| **Testlokation** | Variabel (Googles servere) | Valgfri (London gratis) |
| **Primær metric** | INP (Interaction to Next Paint) | TBT (Total Blocking Time) |
| **Relevans for SEO** | Direkte — Google bruger CrUX data til ranking | Indirekte — kun lab-data |

**Konklusion:** Brug PSI til SEO-vurdering (rigtige brugerdata), GTmetrix til detaljeret fejlsøgning (bedre waterfall).

## Brug

### Kør en test

1. Gå til [pagespeed.web.dev](https://pagespeed.web.dev)
2. Indtast kundens URL
3. Klik **Analyze**
4. Vent 10-30 sekunder
5. Resultatet viser to sektioner:
   - **Field data** (øverst) — rigtige brugerdata fra Chrome UX Report
   - **Lab data** (nederst) — Lighthouse-simulering

### Desktop vs Mobile

- Klik fanen **Mobile** eller **Desktop** øverst
- **Test BEGGE** — Google ranker baseret på mobile-first indexing
- Mobile scores er næsten altid lavere end desktop (langsommere simuleret forbindelse)

## Core Web Vitals

### De tre primære metrics

| Metric | Hvad det måler | Godt (grøn) | Behøver arbejde (orange) | Dårligt (rød) |
|--------|---------------|-------------|--------------------------|----------------|
| **LCP** | Hvornår hovedindholdet er synligt | Under 2,5s | 2,5s - 4,0s | Over 4,0s |
| **INP** | Responstid ved brugerinteraktion | Under 200ms | 200ms - 500ms | Over 500ms |
| **CLS** | Visuelt layout-spring under indlæsning | Under 0,1 | 0,1 - 0,25 | Over 0,25 |

### Field data vs Lab data

- **Field data (grøn/orange/rød badges):** Baseret på rigtige brugere over 28 dage. Dette er hvad Google bruger til ranking
- **Lab data (performance score):** Simuleret test med fast forbindelse. Nyttigt til debugging men ikke direkte brugt til ranking
- Hvis der ikke er nok trafik, vises "Not enough data" for field data

## Typiske anbefalinger og løsninger

### "Serve images in next-gen formats"

- **Problem:** Billeder er i PNG eller JPEG — tungere end nødvendigt
- **Løsning:** Konvertér til WebP-format
- **WordPress:** Brug ShortPixel, Imagify eller EWWW Image Optimizer — de konverterer automatisk
- **Elementor:** Sørg for at image optimization plugin også håndterer Elementor-billeder

### "Reduce unused JavaScript"

- **Problem:** JavaScript-filer loades men bruges ikke (eller kun delvist)
- **Løsning:**
  1. Defer/async non-critical JavaScript
  2. Fjern ubrugte WordPress-plugins
  3. Brug WP Rocket eller Autoptimize til at optimere JS
  4. Tjek hvilke scripts der er unødvendige med Coverage-tab i Chrome DevTools

### "Eliminate render-blocking resources"

- **Problem:** CSS og JS filer i `<head>` blokerer visning af siden
- **Løsning:**
  1. Generer Critical CSS (inline det vigtigste CSS i `<head>`)
  2. Defer resten af CSS med `media="print"` trick eller plugin
  3. Tilføj `defer` eller `async` attribut til JS-filer
  4. WP Rocket håndterer dette automatisk med "Optimize CSS Delivery" og "Load JavaScript Deferred"

### "Reduce initial server response time"

- **Problem:** Serveren er langsom til at svare (høj TTFB)
- **Løsning:**
  1. Aktivér server-side caching (WP Rocket, LiteSpeed Cache)
  2. Opgrader hosting hvis det er en billig delt hosting
  3. Brug CDN (Cloudflare, BunnyCDN)
  4. Optimer database (WP-Optimize plugin)

### "Properly size images"

- **Problem:** Billeder er større end de vises
- **Løsning:**
  1. Resize billeder til den faktiske visningstørrelse
  2. Brug responsive images (srcset — WordPress gør dette automatisk)
  3. ShortPixel/Imagify komprimerer og resizer automatisk

### "Avoid large layout shifts"

- **Problem:** Elementer flytter sig mens siden loader
- **Løsning:**
  1. Sæt width og height på alle billeder og iframes
  2. Reservér plads til annoncer og embeds
  3. Brug `font-display: swap` til web fonts
  4. Preload fonts med `<link rel="preload">`

## Fejlsøgning

### Score er grøn i lab men orange/rød i field

- Lab-data simulerer én specifik bruger — field-data repræsenterer alle brugere
- Mange brugere kan have langsomt internet eller gamle telefoner
- Fokusér på field-data da det er hvad Google bruger

### Field data siger "Not enough data"

- Sitet har for få Chrome-brugere til at generere data
- Fokusér på lab-data indtil der er nok trafik
- Tjek også om der er data på origin-niveau (hele domænet samlet)

### Stor forskel mellem mobile og desktop

- Normalt — mobile simulerer en langsommere forbindelse
- Fokusér på mobile-scores da Google bruger mobile-first indexing
- Typiske mobile-forbedringer: Mindre billeder, færre scripts, critical CSS

## Bemærkninger

- PSI er gratis og kræver ingen konto
- Field-data opdateres dagligt (28-dages rullende vindue)
- INP erstattede FID (First Input Delay) som Core Web Vital i marts 2024
- Kør PSI EFTER ændringer og vent mindst 28 dage for at se effekt i field-data
- Lab-data ændrer sig med det samme — nyttigt til at verificere optimeringer
- Gem screenshots til kunden som før/efter dokumentation
- Google Search Console → Core Web Vitals rapporten bruger de samme CrUX data som PSI
