# White Screen of Death (WSOD) — hvid skærm

## Problem

Sitet viser en helt hvid skærm uden fejlmeddelelse — hverken forsiden eller admin-panelet virker. Dette kaldes "White Screen of Death" (WSOD) og er en af de mest gængse WordPress-fejl.

## Løsning

### Trin 1: Aktivér debug-mode

1. Forbind til serveren via FTP eller hosting-filhåndtering
2. Åbn `wp-config.php`
3. Find linjen `define('WP_DEBUG', false);`
4. Ændr til:
   ```php
   define('WP_DEBUG', true);
   define('WP_DEBUG_LOG', true);
   define('WP_DEBUG_DISPLAY', true);
   ```
5. Gem filen og genindlæs sitet
6. Nu bør du se en fejlmeddelelse der fortæller hvad der er galt

### Trin 2: Tjek PHP-hukommelse

WSOD skyldes ofte for lidt PHP-hukommelse. Tilføj i `wp-config.php`:
```php
define('WP_MEMORY_LIMIT', '256M');
```

### Trin 3: Deaktivér plugins

Hvis fejlmeddelelsen peger på et plugin, eller hvis du ikke kan se fejlen:

1. Via FTP — navigér til `wp-content/`
2. Omdøb mappen `plugins` til `plugins_disabled`
3. Genindlæs sitet — virker det nu?
4. Hvis ja — omdøb mappen tilbage og aktivér plugins én ad gangen

### Trin 4: Skift til standardtema

Hvis plugins ikke er problemet:

1. Via FTP — navigér til `wp-content/themes/`
2. Omdøb dit aktive temas mappe (fx `mit-tema` → `mit-tema_disabled`)
3. WordPress falder automatisk tilbage til et standardtema
4. Genindlæs sitet

### Trin 5: Tjek .htaccess

En korrupt `.htaccess` kan give WSOD:

1. Via FTP — find `.htaccess` i roden
2. Omdøb den til `.htaccess_backup`
3. Genindlæs sitet
4. Hvis det virker — gå til **Indstillinger → Permalinks** og klik **Gem** for at generere en ny `.htaccess`

### Trin 6: Geninstallér WordPress core

Hvis intet af ovenstående virker:

1. Download seneste WordPress fra wordpress.org
2. Upload alle filer UNDTAGEN `wp-content/` og `wp-config.php`
3. Overskriv de eksisterende core-filer
4. Genindlæs sitet

### Trin 7: Tjek fejlloggen

Tjek serverens fejllog for mere information:

- **cPanel:** Fejllog under **Metrics → Errors**
- **wp-content/debug.log** (hvis WP_DEBUG_LOG er aktiveret)
- **PHP-fejllog:** Stien vises i phpinfo() under `error_log`

### Gængse årsager til WSOD

| Årsag | Løsning |
|-------|---------|
| Plugin-konflikt | Deaktivér plugins trinvist |
| Tema-fejl | Skift til standardtema |
| PHP-hukommelse | Øg WP_MEMORY_LIMIT |
| Korrupt .htaccess | Omdøb og generér ny |
| PHP-syntaxfejl | Tjek debug-log for fil og linjenummer |
| Forældet PHP | Opdatér PHP-version |

## Bemærkninger

- WSOD på kun forsiden (admin virker) = typisk tema-problem
- WSOD på kun admin (forsiden virker) = typisk plugin-problem
- WSOD på alt = PHP-hukommelse, core-fejl eller .htaccess
- Husk at slå debug-mode FRA igen efter fejlsøgning (sæt WP_DEBUG til false)
- Tag backup af `wp-config.php` før du ændrer i den
