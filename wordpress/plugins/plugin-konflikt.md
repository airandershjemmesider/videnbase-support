# Fejlsøg plugin-konflikter

## Problem

Plugins kan konflikte med hinanden eller med temaet, hvilket giver:
- Hvid skærm (White Screen of Death)
- PHP-fejlmeddelelser
- Funktioner der stopper med at virke
- Sitet bliver langsomt eller ustabilt

## Løsning

### Trin 1: Identificér problemet

Spørgsmål til dig selv:
- Hvornår startede problemet? (efter installation/opdatering af et plugin?)
- Påvirker det hele sitet eller kun bestemte sider?
- Virker admin-panelet stadig?

### Trin 2: Deaktivér alle plugins

**Hvis du kan logge ind i admin:**

1. Gå til **Plugins → Installerede plugins**
2. Markér alle plugins med checkbox øverst
3. Vælg **Deaktivér** i bulk-handlinger
4. Klik **Anvend**
5. Tjek om problemet er løst

**Hvis du IKKE kan logge ind:**
- Se separat guide: "Deaktivér plugins via FTP"

### Trin 3: Aktivér plugins én ad gangen

1. Aktivér ét plugin
2. Tjek sitet — virker det stadig?
3. Gentag for næste plugin
4. Når problemet vender tilbage, har du fundet det skyldige plugin

### Trin 4: Løs konflikten

Når du har fundet det problematiske plugin:

1. **Tjek for opdateringer** — er pluginet opdateret til nyeste version?
2. **Tjek kompatibilitet** — er det kompatibelt med din WordPress-version?
3. **Søg efter kendte problemer** — tjek pluginets support-forum på wordpress.org
4. **Kontakt pluginudvikleren** — rapportér fejlen med detaljer
5. **Find alternativ** — søg efter et andet plugin med samme funktion

### Tema-konflikt

Hvis problemet fortsætter efter deaktivering af alle plugins:

1. Gå til **Udseende → Temaer**
2. Skift til et standardtema (Twenty Twenty-Four)
3. Tjek om problemet er løst
4. Hvis ja — problemet er i dit tema. Kontakt temaudvikleren

### Hurtig test med WordPress debug

Aktivér debug-mode for at se præcis fejlmeddelelse:

```php
// I wp-config.php
define('WP_DEBUG', true);
define('WP_DEBUG_LOG', true);
define('WP_DEBUG_DISPLAY', false);
```

Fejlloggen gemmes i `wp-content/debug.log`.

## Bemærkninger

- De mest konfliktsøgende plugins er typisk: cache-plugins, sikkerhedsplugins og billedoptimering
- Undgå at bruge to plugins der gør det samme (fx to SEO-plugins)
- Hold altid plugins opdaterede — ældre versioner har flere konflikter
- Slet deaktiverede plugins du ikke bruger — de er en sikkerhedsrisiko
- Før du installerer et nyt plugin, tjek "Sidst opdateret" og "Testet op til" på wordpress.org
