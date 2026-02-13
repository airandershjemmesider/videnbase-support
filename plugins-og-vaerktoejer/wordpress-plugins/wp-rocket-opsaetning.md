# WP Rocket Cache og Performance — Opsætning

## Hvad er det

WP Rocket er et premium cache-plugin der gør WordPress-hjemmesider markant hurtigere. Det cacher sider som statisk HTML, optimerer CSS/JS-filer, lazy-loader billeder og tilbyder database-oprydning. WP Rocket er betalt software — der er ingen gratis version.

## Installation

1. Køb licens på wp-rocket.me
2. Download plugin-filen (.zip) fra din konto
3. Gå til **Plugins → Tilføj nyt → Upload Plugin**
4. Upload zip-filen og aktivér pluginet
5. WP Rocket aktiverer automatisk page caching ved aktivering

## Grundopsætning

Gå til **Indstillinger → WP Rocket** for at konfigurere:

### Cache-fanen
- **Enable caching for mobile devices** — aktivér (vigtigt for mobil-hastighed)
- **Separate cache files for mobile** — aktivér hvis temaet har et separat mobil-layout
- **Cache Lifespan** — 10 timer er standard (fint for de fleste sider)

### Preloading
- **Activate Preloading** — aktivér. Genererer cache proaktivt i baggrunden
- **Activate sitemap-based cache preloading** — aktivér. Bruger sitemap til at finde alle sider
- **Prefetch DNS Requests** — tilføj domæner for eksterne ressourcer:
  - `//fonts.googleapis.com`
  - `//www.google-analytics.com`
  - `//www.googletagmanager.com`
  - `//connect.facebook.net` (hvis Facebook Pixel bruges)

### File Optimization

#### CSS
- **Minify CSS Files** — aktivér (fjerner whitespace og kommentarer)
- **Combine CSS Files** — test forsigtigt (kan ødelægge layout på nogle sider)
- **Optimize CSS Delivery** — aktivér (eliminerer render-blocking CSS)
- **Remove Unused CSS** — aktivér med forsigtighed, test alle sider

#### JavaScript
- **Minify JavaScript Files** — aktivér
- **Combine JavaScript Files** — test forsigtigt (kan bryde funktionalitet)
- **Load JavaScript Deferred** — aktivér (loader JS efter sidens indhold)
- **Delay JavaScript Execution** — aktivér for yderligere hastighed, men test grundigt

**Vigtigt:** Aktivér filoptimering én indstilling ad gangen og test hjemmesiden efter hver ændring.

## LazyLoad

- **Images** — aktivér (billeder loades først når de scrolles til)
- **Iframes/Videos** — aktivér (YouTube-embeds loades on-demand)
- **Replace YouTube iframe with preview image** — aktivér (stor hastighedsgevinst)
- **CSS background images** — aktivér i Pro (cacher og lazy-loader baggrundsbilleder)

## CDN-opsætning

### Cloudflare
1. Gå til **WP Rocket → CDN → Cloudflare**
2. Indtast Cloudflare API-credentials
3. WP Rocket rydder automatisk Cloudflare-cache ved ændringer
4. Aktivér **Optimal Settings** for automatisk konfiguration

### Andet CDN (BunnyCDN, KeyCDN osv.)
1. Gå til **WP Rocket → CDN**
2. Aktivér CDN
3. Indtast CDN URL (f.eks. `cdn.domæne.dk`)
4. WP Rocket omskriver automatisk URL'er til CDN

## Database optimering

Gå til **WP Rocket → Database**:
- **Revisions** — slet gamle revisioner (behold de seneste 2-3)
- **Auto Drafts** — slet automatiske kladder
- **Trashed Posts** — tøm papirkurven
- **Spam Comments** — slet spam-kommentarer
- **Transients** — slet udløbne transients
- **Optimize Tables** — optimer databasetabeller

**Tip:** Kør database-optimering månedligt eller opsæt automatisk schedule.

## Undtagelser — sider der IKKE skal caches

Gå til **WP Rocket → Advanced Rules**:

### Sider der altid skal undtages
- `/cart/` eller `/kurv/` (WooCommerce indkøbskurv)
- `/checkout/` eller `/kasse/` (WooCommerce checkout)
- `/min-konto/` eller `/my-account/` (WooCommerce konto)
- Login-sider og password-beskyttede sider

### Cookies der forhindrer caching
- WP Rocket undtager automatisk indloggede brugere
- WooCommerce-cookies (kurv, session) håndteres automatisk

### URL'er med query strings
- Standard: Sider med query strings caches IKKE
- Tilføj specifikke parametre under "Cache Query Strings" hvis nødvendigt

## Fejlsøgning

### Layout er ødelagt efter aktivering
1. **Ryd cachen:** WP Rocket → Dashboard → Clear Cache
2. **Deaktiver "Combine CSS"** — dette er den hyppigste årsag
3. **Deaktiver "Combine JavaScript"** — næsthyppigste årsag
4. Test med én indstilling ad gangen for at finde problemet
5. Tilføj problematiske filer til undtagelseslisten

### Hjemmesiden virker langsom trods WP Rocket
- Tjek at preloading er aktiveret
- Kontrollér at cachen faktisk virker: Se kildekode → bunden skal have en WP Rocket kommentar
- Test med GTmetrix eller PageSpeed Insights
- Tjek server-responstid (TTFB) — dette er hosting-relateret, ikke cache

### WooCommerce: Kurv/checkout fungerer ikke
- Sørg for at kurv- og checkout-sider er undtaget fra cache
- WP Rocket gør dette automatisk for standard WooCommerce-URL'er
- Ved custom URL'er: Tilføj dem manuelt under Advanced Rules

### Cache ryddes ikke automatisk
- Tjek at WP-Cron kører korrekt
- Kontrollér at disk-plads er tilgængelig
- Manuelt: Klik "Clear Cache" i admin-baren

## Vigtige indstillinger — hurtig tjekliste

| Indstilling | Anbefalet | Note |
|-------------|-----------|------|
| Page Caching | Aktiveret | Grundlæggende cache |
| Mobile Cache | Aktiveret | Separat mobil-cache |
| Preloading | Aktiveret | Proaktiv cache-opbygning |
| Minify CSS | Aktiveret | Sjældent problematisk |
| Minify JS | Aktiveret | Sjældent problematisk |
| Combine CSS | Test først | Kan ødelægge layout |
| Combine JS | Test først | Kan bryde scripts |
| Defer JS | Aktiveret | God hastighedsgevinst |
| LazyLoad | Aktiveret | Vigtigt for billedtunge sider |

## Bemærkninger

- WP Rocket er betalt — ca. $59/år for én site
- Det er det mest brugervenlige cache-plugin til WordPress
- Altid tag backup inden du ændrer filoptimering-indstillinger
- WP Rocket er kompatibelt med de fleste temaer og plugins
- Kør PageSpeed Insights test før OG efter opsætning for at måle forbedring
- Ved hostingskift: Ryd cache og preload igen
- Undgå at bruge flere cache-plugins samtidigt
