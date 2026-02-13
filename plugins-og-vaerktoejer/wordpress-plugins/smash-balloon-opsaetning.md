# Smash Balloon Social Feeds — Opsætning

## Hvad er det

Smash Balloon er en samling plugins der viser social media feeds direkte på hjemmesiden. Du kan vise Instagram-billeder, Facebook-opslag, YouTube-videoer og tweets i et pænt layout der matcher hjemmesidens design.

Smash Balloon fås som separate plugins:
- **Instagram Feed** (gratis + Pro)
- **Custom Facebook Feed** (gratis + Pro)
- **Feeds for YouTube** (gratis + Pro)
- **Custom Twitter Feeds** (Pro)
- **Social Wall** (Pro — kombinerer flere feeds)

## Opsætning: Instagram Feed

### Trin 1: Installation
1. Gå til **Plugins → Tilføj nyt**
2. Søg efter "Smash Balloon Instagram"
3. Installér og aktivér **Smash Balloon Social Photo Feed**

### Trin 2: Forbind Instagram-konto
1. Gå til **Instagram Feed → Settings**
2. Klik **Add Source**
3. Vælg kontotype:
   - **Personal** — viser kun egne billeder (enklere opsætning)
   - **Business** — kræver Facebook Business-side, giver flere muligheder
4. Følg autorisationsflowet og godkend forbindelsen
5. Kontoen vises nu under "Sources"

### Trin 3: Opret feed
1. Gå til **Instagram Feed → All Feeds**
2. Klik **Add New**
3. Vælg feedtype:
   - **User Timeline** — billeder fra en specifik konto
   - **Hashtag** (Pro) — billeder med et bestemt hashtag
   - **Tagged** (Pro) — billeder hvor kontoen er tagget
4. Vælg den forbundne konto som kilde
5. Vælg layout og antal billeder

### Trin 4: Tilpas design
- **Layout:** Grid, Carousel, Masonry, Highlight
- **Antal kolonner:** Tilpas til desktop, tablet og mobil
- **Antal billeder:** Typisk 6-12 for en fin visning
- **Header:** Vis/skjul profilbillede og bio
- **Farver:** Arv fra tema eller sæt manuelt
- **Hover-effekt:** Vis likes/kommentarer ved hover

## Opsætning: Facebook Feed

### Trin 1: Installation
1. Søg efter "Smash Balloon Custom Facebook Feed"
2. Installér og aktivér

### Trin 2: Forbind Facebook-side
1. Gå til **Facebook Feed → Settings**
2. Klik **Add Source**
3. Log ind med Facebook og vælg den side du vil forbinde
4. Godkend de nødvendige tilladelser

### Trin 3: Opret og tilpas feed
1. Vælg indholdstype: Timeline, Photos, Events, Albums
2. Tilpas layout, farver og antal opslag
3. Vælg om likes/kommentarer/delinger skal vises

## Indsæt feed på hjemmesiden

### Metode 1: Shortcode
- Kopiér shortcoden fra feed-indstillingerne (f.eks. `[instagram-feed feed=1]`)
- Indsæt i en tekst-widget, side eller indlæg

### Metode 2: WordPress Block
- I block-editoren: Tilføj blok → søg "Instagram Feed" eller "Facebook Feed"
- Vælg det ønskede feed

### Metode 3: Elementor Widget
- Smash Balloon tilføjer automatisk widgets til Elementor
- Træk widgeten ind på siden og vælg feedet

## GDPR og cookie compliance

**Vigtigt:** Smash Balloon loader indhold fra Instagram/Facebook-servere. Dette sætter 3. parts cookies og deler brugerdata med Meta.

### Opsætning med Complianz
1. Kør en cookie-scan i Complianz efter installation af Smash Balloon
2. Complianz detekterer automatisk social media cookies
3. Kategorisér cookies som **Marketing** eller **3. part**
4. Feedet blokeres indtil brugeren accepterer cookies
5. Complianz viser en placeholder med besked om at acceptere cookies

### Alternativ: GDPR-venlig løsning
- Brug Smash Balloons **GDPR compliance** indstilling
- **Instagram Feed → Settings → Advanced → GDPR**
- Aktivér "Enable GDPR Setting" — loader kun lokalt cachede billeder
- Reducerer 3. parts datadeling men begrænser funktionaliteten

## Fejlsøgning

### "Unable to retrieve" eller tomt feed
1. **Token udløbet** — gå til plugin settings og forny forbindelsen
2. Klik **Reconnect** eller **Add Source** igen
3. Instagram tokens udløber efter ~60 dage (Personal accounts)
4. Business accounts har længere tokenlevetid

### Billeder loader langsomt
- Aktivér **Image Resizing** under Advanced settings
- Smash Balloon cacher billeder lokalt — første load kan være langsom
- Tjek at cron-jobs kører korrekt (WP-Cron)

### Feed viser gamle billeder
- Klik **Clear Cache** i feed-indstillingerne
- Tjek cache-intervallet (standard: 12 timer)
- Forkortes kan sættes ned til 30 minutter (men belaster API'en mere)

### Feed vises ikke i Elementor
- Ryd Elementor-cache under **Elementor → Tools → Regenerate CSS**
- Tjek at shortcoden er korrekt indsat
- Prøv med en simpel shortcode i en HTML-widget som alternativ

## Bemærkninger

- Smash Balloon Free viser kun basale feeds med begrænset styling
- Pro-versionerne giver: Carousel, lightbox, filtrering, flere layouts
- Instagram API har rate limits — undgå for mange feeds på samme side
- Brug altid caching for at undgå langsom sideload
- Husk GDPR-compliance — social feeds kræver samtykke i EU
- Test at tokens ikke er udløbet efter plugin-opdateringer
