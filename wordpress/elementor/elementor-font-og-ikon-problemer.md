# Font og ikon problemer i Elementor

## Problem

Google Fonts loader ikke, custom fonts vises forkert, eller ikoner vises som firkanter eller mangler helt.

## Løsning

### Google Fonts loader ikke

**Årsag:** GDPR-krav eller browser-blokering af Google-servere.

**Løsning — host fonts lokalt:**

1. Gå til **Elementor → Settings → Advanced**
2. Sæt **Google Fonts Load** til **Local** (eller brug plugin som OMGF)
3. Klik **Elementor → Tools → Regenerate CSS & Data**

Dette downloader fontene til din server så de ikke hentes fra Google.

### Custom fonts virker ikke (Elementor Pro)

1. Gå til **Elementor → Custom Fonts**
2. Tilføj fonten med korrekte filformater:
   - **WOFF2** — anbefalet, bedst komprimeret
   - **WOFF** — god fallback
   - **TTF** — ældre browsers
3. Upload mindst WOFF2 + WOFF for bedst dækning
4. Sæt korrekt **font-weight** for hver variation (Regular = 400, Bold = 700 osv.)
5. Regenerér CSS under **Elementor → Tools**

**Typiske fejl:**
- Kun ét filformat uploadet — brug minimum WOFF2
- Forkert font-weight tildelt — tjek at Bold faktisk er sat til 700
- Font-filerne er korrupte — download dem igen fra kilden

### Ikoner vises som firkanter

1. Gå til **Elementor → Tools → General**
2. Klik **Regenerate CSS & Data** — dette genopbygger også ikon-cachen
3. Ryd browser-cache og server-cache
4. Tjek at ikon-fontene (eicons) loader korrekt i browser-konsollen (F12 → Network)

### Font Awesome vs Elementor ikoner

Elementor bruger som standard sine egne ikoner (Elementor Icons). Font Awesome kan aktiveres:

1. Gå til **Elementor → Settings → Advanced**
2. Under **Load Font Awesome 4 Support** — aktivér hvis du bruger ældre FA4-ikoner
3. Font Awesome 5/6 kan bruges via **Icon widget** → vælg **Font Awesome** som bibliotek

### Fonts ser anderledes ud i editor vs frontend

1. Regenerér CSS under **Elementor → Tools**
2. Ryd alle caches (plugin-cache, server-cache, CDN-cache)
3. Tjek at ingen CSS-optimerings-plugin overskriver Elementor-styles
4. Hard refresh i browseren: **Ctrl+Shift+R**

## Bemærkninger

- Lokalt hostede Google Fonts er bedst for GDPR-compliance og performance
- WOFF2 er det foretrukne format — det er 30% mindre end WOFF
- Custom fonts kræver Elementor Pro
- Ikon-problemer skyldes ofte aggressiv caching — ryd altid cache efter ændringer
