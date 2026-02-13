# Mixed Content advarsler (HTTP/HTTPS blanding)

## Problem

Din side har SSL-certifikat og bruger HTTPS, men browseren viser advarsler, hængelåsen mangler, eller du ser "Mixed Content" fejl i konsollen. Sitet loader ressourcer (billeder, scripts, stylesheets) via usikkert HTTP i stedet for HTTPS.

## Hvad er Mixed Content?

Når en HTTPS-side indlæser ressourcer via HTTP, opstår mixed content. Browseren advarer fordi den sikre forbindelse brydes.

### Typer

- **Mixed Active Content** (blokeres): Scripts, stylesheets, iframes, AJAX-kald via HTTP. Browseren blokerer dette helt
- **Mixed Passive Content** (advarsel): Billeder, video, lyd via HTTP. Vises men hængelåsen fjernes

## Løsning

### Trin 1: Find mixed content

#### Browser DevTools
1. Åbn sitet i Chrome
2. Tryk F12 → fanen "Console"
3. Kig efter advarsler med "Mixed Content"
4. Fejlmeddelelsen viser præcis hvilke ressourcer der er problemet

#### Online værktøj
- **whynopadlock.com** — Scanner siten og viser alle HTTP-ressourcer

### Trin 2: Ret kilderne

#### WordPress — Really Simple SSL plugin (hurtig løsning)
1. Installer og aktivér **Really Simple SSL**
2. Pluginet fikser automatisk de fleste mixed content-problemer
3. Det er en midlertidig løsning — ret de reelle kilder bagefter

#### WordPress — Opdater URL'er i databasen
Brug **Better Search Replace** plugin:
1. Installer og aktivér pluginet
2. Søg efter: `http://example.dk`
3. Erstat med: `https://example.dk`
4. Vælg ALLE tabeller
5. Kør først med "Dry Run" for at se antal ændringer
6. Kør derefter rigtigt

#### Hardkodede URL'er i tema/plugins
1. Tjek tema-filer for hardkodede `http://` URL'er
2. Ret dem til `https://` eller brug protocol-relative `//`
3. Tjek `functions.php`, `header.php`, `footer.php`

#### Eksternt indhold
- Billeder, scripts eller fonts der hentes fra **andre domæner** via HTTP
- Ret URL'en til HTTPS (de fleste tjenester understøtter det)
- Hvis tjenesten ikke understøtter HTTPS: Host ressourcen selv

### Trin 3: Tving HTTPS med redirect

#### .htaccess (Apache)
```apache
RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

#### Nginx
```nginx
server {
    listen 80;
    server_name example.dk www.example.dk;
    return 301 https://$host$request_uri;
}
```

#### WordPress wp-config.php
```php
define('FORCE_SSL_ADMIN', true);
```

### Trin 4: Tilføj Content-Security-Policy header (valgfrit)

For at automatisk opgradere HTTP til HTTPS:
```
Content-Security-Policy: upgrade-insecure-requests
```

I .htaccess:
```apache
Header always set Content-Security-Policy "upgrade-insecure-requests"
```

### Trin 5: Verificer

1. Besøg sitet — hængelåsen skal vises uden advarsler
2. Tjek DevTools Console for mixed content-fejl
3. Test alle undersider — mixed content kan være på specifikke sider
4. Kør **whynopadlock.com** igen for at bekræfte

## Typiske kilder til mixed content

| Kilde | Løsning |
|-------|---------|
| Billeder i indlæg/sider | Search & Replace i database |
| Hardkodede URL'er i temaet | Ret i tema-filerne |
| Eksterne scripts (analytics, fonts) | Opdater til HTTPS-version |
| Iframe-embeds (kort, video) | Opdater embed-koden til HTTPS |
| CSS background-images | Ret i stylesheet |
| Gammel CDN-konfiguration | Opdater CDN til HTTPS |

## Bemærkninger

- **Better Search Replace er den grundigste løsning** for WordPress — den fixer alt i databasen
- Tag ALTID backup inden du kører Search & Replace
- Really Simple SSL er god som akutløsning, men det er bedre at rette problemerne permanent
- `upgrade-insecure-requests` headeren er en god ekstra sikkerhed, men erstatter ikke at rette kilderne
- Tjek ALLE undersider — mixed content er ofte kun på specifikke sider med gammelt indhold
