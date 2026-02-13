# Fejlsøgning i cPanel

## Hvad er det

Denne guide dækker de mest almindelige fejl og problemer man støder på i cPanel, og hvordan de løses.

## Error Logs (fejllog)

1. Gå til cPanel → **Metrics → Errors**
2. Viser de seneste PHP-fejl og advarsler
3. Typiske fejl:
   - `Fatal error: Allowed memory size exhausted` → Forøg memory_limit
   - `Warning: include(): Failed opening` → Fil mangler eller forkert sti
   - `Parse error: syntax error` → Syntaksfejl i PHP-kode

## Diskforbrug

1. Gå til cPanel → **Files → Disk Usage**
2. Find hvilke mapper der fylder mest
3. Typiske syndere:
   - `/mail` — store emailpostkasser
   - `/public_html/wp-content/uploads` — mediefiler i WordPress
   - `/tmp` eller `/logs` — midlertidige filer og logfiler
4. Løsning: Slet unødvendige filer, komprimér billeder, ryd mailboks

## PHP-version og -indstillinger

### Skift PHP-version
1. Gå til cPanel → **Software → MultiPHP Manager**
2. Vælg domænet
3. Vælg ønsket PHP-version (f.eks. 8.1, 8.2, 8.3)
4. Klik **Apply**

### Justér PHP-indstillinger
1. Gå til cPanel → **Software → MultiPHP INI Editor**
2. Vælg domænet
3. Justér de vigtigste indstillinger:

| Indstilling | Standard | Anbefalet for WordPress |
|-------------|----------|------------------------|
| `memory_limit` | 128M | 256M eller 512M |
| `upload_max_filesize` | 2M | 64M |
| `post_max_size` | 8M | 128M |
| `max_execution_time` | 30 | 300 |
| `max_input_vars` | 1000 | 3000 |

4. Klik **Apply**

## Blokeret IP-adresse

### cPanel IP Blocker
- Gå til **Security → IP Blocker** for at se og administrere blokerede IP'er
- Tilføj eller fjern IP-adresser manuelt

### WHM cPHulk (brute force beskyttelse)
- WHM → **Security Center → cPHulk Brute Force Protection**
- Tjek om kundens IP er blokeret pga. for mange mislykkede login-forsøg
- Klik **Flush DB** for at fjerne alle blokeringer (brug med forsigtighed)

## 500 Internal Server Error

Tjek i denne rækkefølge:

1. **`.htaccess`** — Omdøb til `.htaccess_backup` og test. Hvis sitet virker, er fejlen i .htaccess
2. **PHP-fejl** — Tjek Error Logs (se ovenfor)
3. **Fil-rettigheder** — Mapper skal være `755`, filer `644`. Forkerte rettigheder giver 500-fejl
4. **PHP-version** — Prøv at skifte PHP-version (ældre plugins kan fejle på nye PHP-versioner)
5. **Plugins (WordPress)** — Omdøb `/wp-content/plugins/` via File Manager for at deaktivere alle plugins

## 403 Forbidden

- Tjek fil-rettigheder (755/644)
- Tjek at `public_html` har en `index.html` eller `index.php`
- Tjek **Indexes** er slået til i cPanel hvis directory listing er ønsket
- Tjek ModSecurity-regler (WHM → Security Center → ModSecurity) — kan blokere legitime forespørgsler

## Langsom hjemmeside

1. **Resource Usage:** cPanel → **Metrics → Resource Usage** — tjek om CPU/RAM/I/O er maxet
2. **Database:** Optimér database via phpMyAdmin → Vælg alle tabeller → **Repair** og **Optimize**
3. **Caching:** Installér caching-plugin i WordPress (f.eks. WP Super Cache, LiteSpeed Cache)
4. **Billeder:** Komprimér store billeder (brug ShortPixel, Imagify el.lign.)
5. **PHP-version:** Nyere PHP-versioner er hurtigere — opgradér hvis muligt
6. **Logfiler:** Store error-logs kan bremse serveren — ryd dem jævnligt

## Bemærkninger

- Tag altid backup før du ændrer .htaccess, PHP-version eller fil-rettigheder
- Mange WordPress-fejl løses ved at deaktivere plugins og genaktivere én ad gangen
- Error Logs viser kun de seneste fejl — for ældre fejl, tjek `/home/brugernavn/logs/error.log`
- Kontakt hosting-udbyder hvis problemet er server-relateret (hardware, netværk, server-software)
