# LiteSpeed Cache — Opsætning og optimering

## Hvad er LiteSpeed Cache?

LiteSpeed Cache (LSCache) er et gratis caching- og optimeringsplugin til WordPress. Det fungerer bedst på LiteSpeed-webservere, hvor det udnytter server-level caching direkte. På andre servere (Apache/Nginx) virker de fleste funktioner stadig — men uden den fulde server-level integration.

Pluginet dækker:
- **Page Cache** — gemmer færdige HTML-sider
- **Object Cache** — cacher databaseforespørgsler (kræver Redis/Memcached)
- **Browser Cache** — instruerer browseren i at gemme statiske filer lokalt
- **CSS/JS-optimering** — minify, combine og defer
- **Billedoptimering** — WebP-konvertering via QUIC.cloud
- **Database-oprydning** — fjerner revisioner, transients og spam
- **Crawler/Preload** — opvarmer cachen automatisk

## Installation

1. Gå til **Plugins → Tilføj nyt** i WordPress admin
2. Søg efter "LiteSpeed Cache"
3. Installér og aktivér pluginet
4. Gå til **LiteSpeed Cache → Dashboard** for at bekræfte det kører

### QUIC.cloud-konto (valgfrit men anbefalet)

QUIC.cloud giver adgang til billedoptimering, CDN og avanceret caching — selv på ikke-LiteSpeed servere.

1. Gå til **LiteSpeed Cache → General → QUIC.cloud**
2. Klik "Request Domain Key"
3. Bekræft domænet via e-mail eller DNS
4. Gratis-planen dækker de fleste små sites

## Grundopsætning

### General Settings
- **Automatically Upgrade:** OFF (opdatér manuelt for kontrol)
- **Domain Key:** Hent fra QUIC.cloud hvis du vil bruge billedoptimering/CDN
- **Server IP:** Udfyld kun hvis QUIC.cloud beder om det

## Cache-indstillinger

### Cache → Cache
- **Enable Cache:** ON
- **Cache Logged-in Users:** OFF (medmindre sitet har mange faste brugere)
- **Cache Commenters:** OFF
- **Cache REST API:** ON
- **Cache Login Page:** ON
- **Cache favicon.ico:** ON
- **Cache PHP Resources:** ON
- **Cache Mobile:** OFF (medmindre sitet bruger separat mobil-tema)

### Cache → TTL (Time To Live)
- **Default Public Cache TTL:** 604800 (7 dage)
- **Default Private Cache TTL:** 1800 (30 min)
- **Default Front Page TTL:** 604800
- **Default Feed TTL:** 604800

### Cache → Purge
- **Purge All On Upgrade:** ON
- **Auto Purge Rules:** Behold standardindstillinger (purge ved post-opdatering)

### Cache → Excludes
- Tilføj sider der IKKE skal caches:
  - `/cart/` og `/checkout/` (WooCommerce)
  - `/min-konto/` eller `/my-account/`
  - Sider med formularer der kræver friske tokens
  - Medlemssider med dynamisk indhold

### Cache → Browser
- **Browser Cache:** ON
- **Browser Cache TTL:** 31557600 (1 år — statiske filer versioneres alligevel)

### Cache → Object (kræver Redis/Memcached på serveren)
- **Object Cache:** ON (kun hvis serveren understøtter det)
- **Method:** Redis (foretrukket) eller Memcached
- **Host:** 127.0.0.1
- **Port:** 6379 (Redis standard)
- Tjek med din hosting om Redis/Memcached er tilgængeligt

## Billedoptimering

### Image Optimization → Image Optimization Settings
- **Auto Request Cron:** ON (sender automatisk billeder til QUIC.cloud)
- **Auto Pull Cron:** ON (henter optimerede billeder automatisk)
- **Original Image Optimization:** ON
- **Remove Original Backups:** OFF (behold backup indtil du er tilfreds)
- **Optimize WebP Versions:** ON
- **WebP Attribute To Replace:** Behold standard (img.src, div.data-thumb osv.)
- **WebP For Extra srcset:** ON
- **WordPress Image Quality Control:** 82 (god balance mellem kvalitet og størrelse)

### Billeder — vigtige noter
- QUIC.cloud har en daglig kvota på gratis-planen — store sites kan tage flere dage
- Optimerede billeder erstattes direkte — originaler gemmes som backup
- WebP serveres automatisk til browsere der understøtter det

## CDN

### CDN → CDN Settings
- **QUIC.cloud CDN:** ON (hvis du bruger QUIC.cloud)
- **Use CDN Mapping:** Kun relevant hvis du bruger eksternt CDN (Cloudflare, BunnyCDN)
- **CDN URL:** Udfyld med dit CDN-domæne hvis relevant

### Cloudflare-brugere
- Brug **LiteSpeed Cache + Cloudflare** sammen — de supplerer hinanden
- Sæt Cloudflare til "Standard" caching (ikke Tiered Cache konflikter)
- Deaktivér Cloudflares Rocket Loader (konflikter med LSCache JS-optimering)
- Overvej at bruge Cloudflares APO som alternativ til QUIC.cloud CDN

## CSS/JS Optimering

### Page Optimization → CSS Settings
- **CSS Minify:** ON
- **CSS Combine:** OFF (moderne HTTP/2 håndterer flere filer fint)
- **Generate Critical CSS:** ON (kræver QUIC.cloud — fjerner render-blocking CSS)
- **CSS Async Load:** ON (loader CSS asynkront efter critical CSS)
- **Font Display Optimization:** Swap (viser fallback-font mens webfont loader)

### Page Optimization → JS Settings
- **JS Minify:** ON
- **JS Combine:** OFF (samme grund som CSS — HTTP/2)
- **JS Defer:** ON (defer loader scripts efter HTML er parset)
- **JS Delay:** Tænd forsigtigt — kan ødelægge interaktive elementer
  - Tilføj specifikke scripts til delay-listen manuelt
  - Test grundigt efter aktivering

### Page Optimization → HTML Settings
- **HTML Minify:** ON
- **DNS Prefetch:** Tilføj domæner du loader fra (Google Fonts, analytics osv.)
- **Remove Query Strings:** ON (bedre caching af statiske filer)
- **Load Google Fonts Asynchronously:** ON
- **Remove Google Fonts:** OFF (medmindre du self-hoster alle fonte)
- **Lazy Load Images:** ON
- **Lazy Load Iframes:** ON
- **Add Missing Image Dimensions:** ON
- **Viewport Images:** Angiv antal billeder "above the fold" der IKKE skal lazy-loades (typisk 2-4)

## Database-optimering

### Database → Manage
- **Clean All:** Kør manuelt en gang om måneden
- Eller sæt automatisk oprydning op:
  - **Post Revisions:** ON (slet gamle revisioner)
  - **Auto Drafts:** ON
  - **Trashed Posts:** ON
  - **Spam Comments:** ON
  - **Trashed Comments:** ON
  - **Expired Transients:** ON
  - **Optimize Tables:** ON

### Database → DB Optimization Settings
- **Revisions Max Number:** 5 (behold de seneste 5)
- **Revisions Max Age:** 30 (slet revisioner ældre end 30 dage)

## Crawler/Preload

### Crawler → General Settings
- **Crawler:** ON (opvarmer cachen ved at besøge alle sider)
- **Delay:** 500ms (vær venlig mod serveren)
- **Run Duration:** 400 sekunder
- **Interval Between Runs:** 600 sekunder
- **Crawl Interval:** 302400 (3,5 dage — matcher TTL)
- **Threads:** 3 (øg kun på dedikerede servere)

### Crawler → Sitemap Settings
- **Custom Sitemap:** Angiv dit sitemap-URL (f.eks. fra Rank Math)
- **Drop Domain from Sitemap:** ON

**Bemærk:** Crawleren kræver en cron-job. Mange shared hosting-udbydere begrænser dette. Tjek at WP-Cron kører korrekt.

## WooCommerce-overvejelser

- **Ekskludér fra cache:** /cart/, /checkout/, /my-account/, /wishlist/
- **Cache Logged-in Users:** OFF (WooCommerce bruger sessions)
- **Private Cached URIs:** Tilføj /shop/ hvis priser varierer per bruger
- **Cache → ESI (Edge Side Includes):** ON for dynamiske widgets (kurv-ikon, login-status)
  - ESI kræver LiteSpeed-server — virker ikke på Apache/Nginx
- **JS Delay:** Test grundigt — kan ødelægge "Tilføj til kurv"-knapper

## Fejlsøgning

### Layout er ødelagt efter aktivering
1. Slå **CSS Combine** og **JS Combine** fra
2. Slå **JS Delay** fra
3. Ryd cache: **LiteSpeed Cache → Toolbox → Purge All**
4. Aktivér én indstilling ad gangen og test

### Cache virker ikke (sider er stadig langsomme)
1. Tjek response headers — kig efter `X-LiteSpeed-Cache: hit`
2. Hvis headeren mangler: serveren er muligvis ikke LiteSpeed
3. Tjek at siden ikke er ekskluderet i Cache → Excludes
4. Tjek at crawleren kører (Crawler → Summary)

### QUIC.cloud problemer
- **Domain Key fejler:** Tjek DNS — QUIC.cloud skal kunne nå dit domæne
- **Billedoptimering hænger:** Tjek QUIC.cloud dashboard for kø-status
- **CDN virker ikke:** Bekræft at CNAME/DNS er sat korrekt op
- **Kvota opbrugt:** Vent til næste dag eller opgrader planen

### Generelle fejlsøgningstrin
1. **Purge All** cache (Toolbox → Purge All)
2. Test i inkognitovindue (undgå browser-cache)
3. Brug Debug-log: **Toolbox → Debug Settings → Debug Log → ON**
4. Tjek loggen i `/wp-content/debug.log`
5. Deaktivér andre cache-plugins (kun ét cache-plugin ad gangen!)

## Hurtig tjekliste

| Indstilling | Anbefalet | Bemærkning |
|---|---|---|
| Page Cache | ON | Grundlæggende caching |
| Object Cache | ON | Kræver Redis/Memcached |
| Browser Cache | ON | TTL: 1 år |
| CSS Minify | ON | Altid sikkert |
| CSS Combine | OFF | HTTP/2 gør det unødvendigt |
| Critical CSS | ON | Kræver QUIC.cloud |
| JS Minify | ON | Altid sikkert |
| JS Combine | OFF | HTTP/2 gør det unødvendigt |
| JS Defer | ON | Test efter aktivering |
| JS Delay | Forsigtigt | Test grundigt — kan ødelægge JS |
| HTML Minify | ON | Altid sikkert |
| Lazy Load (billeder) | ON | Undtag above-the-fold |
| Lazy Load (iframes) | ON | YouTube, Google Maps osv. |
| WebP Optimization | ON | Via QUIC.cloud |
| Image Quality | 82 | God balance |
| Database Cleanup | Månedligt | Eller automatisk via cron |
| Crawler | ON | Delay: 500ms, 3 threads |
| WooCommerce excludes | /cart/, /checkout/ | Altid ekskludér dynamiske sider |
| Query Strings | Fjern | Bedre cache-hit rate |
| DNS Prefetch | ON | Tilføj eksterne domæner |
| Font Display | Swap | Undgår usynlig tekst under load |
