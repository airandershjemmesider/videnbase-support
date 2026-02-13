# Smash Balloon — Opsætning af Social Media Feeds

## Hvad er Smash Balloon

Smash Balloon er en suite af WordPress-plugins der viser sociale medier som feeds direkte på hjemmesiden. Feeds opdateres automatisk når der postes nyt indhold på de tilknyttede konti. Det er den mest udbredte løsning til social media feeds i WordPress.

## De 4 plugins

| Plugin | Formål | Slug |
|--------|--------|------|
| Instagram Feed | Vis Instagram-opslag i grid/carousel | `instagram-feed` |
| Custom Facebook Feed | Vis Facebook Page opslag, events, albums | `custom-facebook-feed` |
| Feeds for YouTube | Vis YouTube-videoer fra kanal eller playliste | `feeds-for-youtube` |
| Custom Twitter Feeds | Vis tweets/X-opslag | `custom-twitter-feeds` |

Der findes også **Social Wall** som kombinerer flere feeds i ét samlet view.

## Gratis vs Pro

| Funktion | Gratis | Pro |
|----------|--------|-----|
| Grundlæggende feed | Ja | Ja |
| Antal feeds | 1 | Ubegrænset |
| Layout-typer | Grid | Grid, Carousel, Masonry, Highlight |
| Hashtag-feeds (Instagram) | Nej | Ja |
| Shoppable feeds | Nej | Ja |
| Album/event feeds (Facebook) | Nej | Ja |
| Lightbox popup | Nej | Ja |
| Filtrering og moderering | Begrænset | Fuld kontrol |
| Prioriteret support | Nej | Ja |

**Anbefaling:** Pro er nødvendig for de fleste kundesites — carousel-layout og lightbox er næsten altid ønsket.

---

## Instagram Feed — Opsætning

### 1. Forbind Instagram-konto

1. Gå til **Instagram Feed → Settings → Sources**
2. Klik **Add New** og vælg **Business** eller **Personal**
3. Log ind med Facebook (Business/Creator) eller direkte Instagram (Personal)
4. Godkend adgang — Smash Balloon gemmer et access token

**Vigtig:** Business/Creator-konto kræves for hashtag-feeds og avanceret data. Personal giver kun egne opslag.

### 2. Opret feed

1. Gå til **Instagram Feed → All Feeds → Add New**
2. Vælg feed-type:
   - **User Timeline** — opslag fra den tilknyttede konto
   - **Public Hashtag** (Pro) — opslag med specifik hashtag
   - **Tagged Posts** (Pro) — opslag hvor kontoen er tagget
3. Vælg kilde (den forbundne konto)

### 3. Layout

| Layout | Beskrivelse | Bedst til |
|--------|-------------|-----------|
| Grid | Ensartet gitter med faste kolonner | Porteføljer, butikker |
| Carousel | Vandret slider med pile | Hero-sektioner, footers |
| Masonry | Pinterest-stil med varierende højder | Blogs, kreative sites |
| Highlight | Fremhæver hvert 3. eller 4. billede | Gallerier med variation |

### 4. Styling

- **Farver:** Arv fra tema eller sæt custom farver (baggrund, tekst, links)
- **Header:** Vis/skjul profil-header med avatar og bio
- **Hover-effekt:** Vis likes/kommentarer eller caption ved hover
- **Load More knap:** Tekst, farve og synlighed kan tilpasses
- **Antal opslag:** Sæt antal synlige opslag (typisk 6-12)
- **Kolonner:** Desktop, tablet og mobil kan sættes separat

### 5. Indsæt på side

- **Shortcode:** Kopiér shortcoden fra feed-oversigten, f.eks. `[instagram-feed feed=1]`
- **Elementor widget:** Smash Balloon har dedikerede widgets — søg "Instagram Feed" i widget-panelet
- **Alternativ i Elementor:** Brug HTML-widget og indsæt shortcoden

---

## Facebook Feed — Opsætning

### 1. Forbind Facebook Page

1. Gå til **Facebook Feed → Settings → Sources**
2. Klik **Add New** og log ind med Facebook
3. Vælg den Page du vil vise feed fra
4. Godkend de nødvendige tilladelser

**Bemærk:** Personlige profiler understøttes ikke — kun Pages.

### 2. Feed-typer

| Type | Beskrivelse | Pro krævet |
|------|-------------|------------|
| Timeline | Sidens opslag i kronologisk rækkefølge | Nej |
| Events | Kommende og tidligere events | Ja |
| Photos | Alle billeder fra siden | Ja |
| Albums | Vis specifikke fotoalbums | Ja |

### 3. Indstillinger

- **Post-typer:** Filtrér på tekst, billeder, video, links eller events
- **Antal opslag:** Typisk 5-10 for timeline
- **Dato-format:** Kan tilpasses til dansk format
- **Tekst-længde:** Sæt maks antal tegn før "læs mere"

---

## Smash Balloon i Elementor

### Placeringsmetoder

1. **Dedikeret widget:** Træk Smash Balloon-widgeten ind — bedste metode
2. **Shortcode-widget:** Brug Elementors Shortcode-widget med feed-koden
3. **HTML-widget:** Alternativ hvis shortcode-widget ikke renderer korrekt

### Responsive indstillinger

- Sæt kolonner separat for desktop/tablet/mobil i Smash Balloon-indstillingerne
- I Elementor: Brug sektionens responsive visibility hvis feedet skal skjules på mobil
- Carousel-layout tilpasser sig automatisk til skærmbredde

### Typiske placeringer

- **Footer:** Social proof — vis seneste opslag i en smal sektion
- **Sidebar:** Kompakt feed med 4-6 billeder i grid
- **Dedikeret sektion:** Fuld bredde med carousel eller masonry
- **Portfolio-side:** Grid med Instagram-billeder som galleri

---

## Performance og GDPR

### Caching

Smash Balloon cacher feeds lokalt i WordPress-databasen. Standard cache-tid er typisk 1-12 timer:
- Ingen API-kald ved hvert sidebesøg
- Hurtigere loadtid efter første indlæsning
- Cache kan tømmes manuelt under plugin-indstillingerne

### GDPR-overvejelser

Feeds indlæser billeder og data fra Facebooks/Instagrams servere:
- Besøgendes IP-adresse sendes til Meta/X
- Tracking-cookies kan sættes af de sociale platforme
- **Kræver cookie-consent** i EU

### Complianz-integration

1. Installer Complianz (eller anden consent-løsning)
2. Kør en cookie-scan efter installation af Smash Balloon
3. Complianz detekterer automatisk social media cookies
4. Feeds blokeres indtil besøgende accepterer marketing/statistik-cookies
5. Complianz viser en placeholder med besked om at acceptere cookies

**Alternativ:** Aktivér Smash Balloons egen GDPR-indstilling under **Advanced → GDPR** — loader kun lokalt cachede billeder, men begrænser funktionaliteten.

---

## Typiske problemer

### "Instagram token expired"

- Tokens udløber efter ca. 60 dage (Personal accounts)
- Business accounts har længere tokenlevetid
- Smash Balloon forsøger automatisk fornyelse, men det fejler nogle gange
- **Løsning:** Gå til Sources → Reconnect den pågældende konto
- **Forebyg:** Sørg for at WP-Cron kører korrekt (token-fornyelse kører via cron)

### Feed viser ikke nye opslag

- Smash Balloon cacher lokalt — nye opslag vises først når cachen udløber
- **Løsning:** Gå til plugin-indstillingerne og klik "Clear Cache"
- Tjek også at kontoen stadig er forbundet under Sources

### API rate limits

- Instagram/Facebook API har grænser for antal kald per time
- Normalt ikke et problem med caching aktiveret
- Hvis feedet viser fejl: Øg cache-tiden til 12-24 timer
- Sites med meget høj trafik: Overvej længere cache-intervaller

### Feed loader ikke (tomt)

- Tjek at JavaScript-konsollen ikke viser fejl
- Sikkerhedsplugins (Wordfence, Sucuri) kan blokere API-kald
- Tjek at PHP-versionen er kompatibel (kræver min. PHP 7.4)
- Ryd Elementor-cache under **Elementor → Tools → Regenerate CSS**

---

## Hurtig tjekliste for opsætning

- [ ] Installér det relevante Smash Balloon plugin
- [ ] Aktivér licens (Pro) under Settings → License
- [ ] Forbind social medie-konto under Sources
- [ ] Opret feed og vælg layout
- [ ] Tilpas styling til kundens brand (farver, kolonner, hover)
- [ ] Sæt responsive kolonner (desktop/tablet/mobil)
- [ ] Indsæt feed på side via widget eller shortcode
- [ ] Test at feedet loader korrekt på frontend
- [ ] Tjek GDPR-compliance med Complianz eller lignende
- [ ] Informér kunden om at token evt. skal fornyes (60 dage)
- [ ] Sæt passende cache-tid (anbefalet: 6-12 timer)
