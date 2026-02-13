# GTmetrix — ydeevne og hastighedstest

## Hvad er det

GTmetrix er et online værktøj der tester hjemmesiders hastighed og performance. Det måler Core Web Vitals, giver en samlet performance-score og viser et detaljeret vandfalds-diagram over alle requests. Gratis versionen er tilstrækkelig til de fleste behov.

## Brug

### Kør en test

1. Gå til [gtmetrix.com](https://gtmetrix.com)
2. Indtast kundens URL
3. Vælg testlokation: **London, UK** (tættest på Danmark i gratis versionen)
4. Klik **Test your site**
5. Vent 30-60 sekunder på resultatet

### Testindstillinger (med gratis konto)

- **Lokation:** London, UK (standard)
- **Browser:** Chrome Desktop (standard)
- **Throttling:** Unthrottled (standard — kører med serverforbindelsens fulde hastighed)

## Forstå scores

### Performance Score

- Samlet score fra 0-100% baseret på Lighthouse
- **Grøn (90-100):** Godt
- **Orange (50-89):** Behøver forbedring
- **Rød (0-49):** Dårligt

### Core Web Vitals

| Metric | Hvad det måler | Godt | Dårligt |
|--------|---------------|------|---------|
| **LCP** (Largest Contentful Paint) | Hvor hurtigt hovedindholdet er synligt | Under 2,5s | Over 4,0s |
| **TBT** (Total Blocking Time) | Hvor lang tid browseren er blokeret af JS | Under 200ms | Over 600ms |
| **CLS** (Cumulative Layout Shift) | Hvor meget layoutet "hopper" under indlæsning | Under 0,1 | Over 0,25 |

### Andre metrics

- **FCP** (First Contentful Paint) — hvornår det første indhold vises
- **SI** (Speed Index) — hvor hurtigt indholdet visuelt fyldes ind
- **TTI** (Time to Interactive) — hvornår siden er fuldt interaktiv

## Typiske problemer og løsninger

### Langsom LCP (Largest Contentful Paint)

| Problem | Løsning |
|---------|---------|
| Store billeder | Komprimér med ShortPixel/Imagify, brug WebP-format |
| Langsom server-responstid | Opgrader hosting, aktivér server-caching, brug CDN |
| Hero image loader sent | Tilføj `preload` til hero-billedet |
| Render-blocking CSS/JS | Defer non-critical CSS og JS |
| Ingen browser-caching | Konfigurér cache-headers eller brug WP Rocket |

### Høj TBT (Total Blocking Time)

| Problem | Løsning |
|---------|---------|
| Tung JavaScript | Defer og async på non-critical scripts |
| For mange 3rd party scripts | Fjern unødvendige plugins og tracking-koder |
| jQuery-tungt tema | Overvej tema-skift eller optimering |
| Ubrugt JavaScript | Identificér og fjern med Coverage-tab i DevTools |

### Høj CLS (Cumulative Layout Shift)

| Problem | Løsning |
|---------|---------|
| Billeder uden dimensioner | Sæt width og height attributter på alle `<img>` tags |
| Web fonts loader sent | Brug `font-display: swap` og preload fonts |
| Dynamisk indhold (annoncer, embeds) | Reservér plads med faste dimensioner |
| Elementer der springer ind | Undgå at indsætte indhold over eksisterende indhold |

## Waterfall-diagram

### Hvad det viser

Vandfalds-diagrammet viser hver enkelt request browseren laver, i kronologisk rækkefølge. For hvert request kan du se:

- **Filnavn og type** (HTML, CSS, JS, billede, font)
- **Størrelse** (komprimeret og ukomprimeret)
- **Timing** (DNS, connect, TLS, wait, download)
- **Status** (200 OK, 301/302 redirect, 404 not found)

### Sådan læser du det

1. **Lange blå/grønne bjælker** = store downloads → komprimér eller optimer
2. **Lange lilla bjælker (wait/TTFB)** = langsom server → hosting-problem eller tung backend
3. **Mange redirects (301/302)** = unødvendige omdirigeringer → fjern eller minimer
4. **Mange requests** = for mange filer → kombiner, fjern unødvendige, lazy load
5. **Render-blocking resources** = CSS/JS der blokerer visning → defer eller async

## Fejlsøgning

### Score svinger mellem tests

- GTmetrix deler testservere — belastning varierer
- Kør 3-5 tests og brug gennemsnittet
- Test på samme tidspunkt for sammenlignelighed

### Score er god men sitet føles langsomt

- GTmetrix tester fra serverlokation — ikke brugerens lokation
- Tjek med rigtige brugerdata i Google Search Console (Core Web Vitals)
- Tjek med PageSpeed Insights for Chrome UX Report data

## Bemærkninger

- **Gratis version:** 1 test ad gangen, kun London, kun Desktop Chrome
- **Pro version:** Flere lokationer (inkl. Nordeuropa), mobile tests, monitoring, API, historik
- Brug GTmetrix som supplement til PageSpeed Insights — de måler lidt forskelligt
- GTmetrix-scores er lab-data (simulerede forhold) — ikke rigtige brugeroplevelser
- Gem screenshots af resultater til kunden som dokumentation for forbedringer
- Test ALTID både forside og en underside (de kan have meget forskellig performance)
