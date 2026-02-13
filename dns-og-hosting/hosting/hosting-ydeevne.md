# Hosting er langsom — Fejlsøgning og optimering

## Problem

Din hjemmeside loader langsomt. Du har brug for at identificere om det er hosting, site-konfiguration, eller noget helt tredje.

## Løsning: Systematisk fejlsøgning

### Trin 1: Mål hastigheden

Brug disse værktøjer til at få et baseline:

- **Google PageSpeed Insights** (pagespeed.web.dev) — Scorer ydeevne og giver forslag
- **GTmetrix** (gtmetrix.com) — Detaljeret waterfall-analyse
- **Pingdom** (tools.pingdom.com) — Simpel hastigheds-test

Vigtige tal:
- **TTFB (Time To First Byte):** Serverens svartid. Over 600ms er langsomt
- **LCP (Largest Contentful Paint):** Under 2,5 sek er godt
- **Total loadtid:** Under 3 sek for de fleste sider

### Trin 2: Er det serveren?

#### Tjek TTFB
Hvis TTFB er høj (over 600ms):
- Problemet er sandsynligvis **serveren** eller **backend-kode**
- Prøv at åbne en simpel HTML-fil direkte — er den også langsom?
- Hvis ja: Serverens hardware eller konfiguration er problemet

#### Tjek serverbelastning
- Log ind på hosting-kontrolpanelet
- Tjek CPU- og RAM-forbrug
- Shared hosting: Du rammer måske ressource-grænsen

### Trin 3: Er det WordPress?

Hvis du kører WordPress og TTFB er høj:

#### Plugins
1. Deaktiver ALLE plugins
2. Test hastigheden igen
3. Aktivér plugins én ad gangen og test efter hver
4. Typiske syndere: Side-builders, tunge kontaktformularer, dårlige SEO-plugins, sociale medier-plugins

#### Tema
1. Skift midlertidigt til et standard-tema (Twenty Twenty-Four)
2. Er sitet hurtigere? Så er temaet problemet

#### Database
1. Installer WP-Optimize eller lignende
2. Ryd op: Revisioner, transients, spam-kommentarer, autoloaded options
3. Overvej at begrænse revisioner i `wp-config.php`:
   ```php
   define('WP_POST_REVISIONS', 5);
   ```

### Trin 4: Opsæt caching

#### Server-side caching
- **LiteSpeed Cache** (hvis LiteSpeed-server)
- **WP Super Cache** eller **W3 Total Cache** (Apache/Nginx)
- Managed WP-hosting har typisk caching indbygget

#### Object caching
- Redis eller Memcached (kræver server-support)
- Reducerer database-forespørgsler markant

### Trin 5: Optimér frontend

- **Billeder:** Komprimer med ShortPixel, Imagify eller WebP-konvertering
- **CSS/JS:** Minify og kombiner med Autoptimize eller hostingens cache-plugin
- **Lazy loading:** Billeder og iframes loader først når de er synlige
- **CDN:** Brug Cloudflare (gratis) eller BunnyCDN til at servere statiske filer fra nære servere

### Trin 6: Overvej opgradering

Hvis serveren ikke kan følge med trods optimering:

| Nuværende | Opgrader til | Forventet forbedring |
|-----------|--------------|----------------------|
| Shared hosting | Managed WP | 2-5x hurtigere |
| Shared hosting | VPS | 3-10x hurtigere |
| Gammel PHP (7.x) | PHP 8.2+ | 20-50% hurtigere |

## Bemærkninger

- **PHP-version er kritisk** — PHP 8.2 er markant hurtigere end 7.4. Opgrader altid til nyeste understøttede version
- **Billedoptimering** giver ofte den største synlige forbedring med mindst indsats
- **Cloudflare (gratis plan)** kan forbedre hastigheden mærkbart for statisk indhold
- Mål ALTID før og efter ændringer — ellers ved du ikke hvad der hjalp
- Shared hosting kan aldrig konkurrere med VPS/managed hosting på ydeevne
