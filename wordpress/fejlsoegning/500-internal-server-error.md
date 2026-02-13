# 500 Internal Server Error

## Problem

Sitet viser "500 Internal Server Error". Dette er en generel serverfejl der kan have mange årsager. Fejlen kommer fra serveren — ikke fra WordPress direkte.

## Løsning

### Trin 1: Tjek .htaccess

En korrupt `.htaccess`-fil er den hyppigste årsag:

1. Forbind via FTP eller hosting-filhåndtering
2. Find `.htaccess` i WordPress-roden
3. Omdøb den til `.htaccess_backup`
4. Genindlæs sitet
5. Hvis det virker — log ind i WordPress admin
6. Gå til **Indstillinger → Permalinks** og klik **Gem ændringer**
7. WordPress genererer en ny, korrekt `.htaccess`

### Trin 2: Øg PHP-hukommelse

Tilføj i `wp-config.php`:
```php
define('WP_MEMORY_LIMIT', '256M');
```

Eller i `.htaccess`:
```apache
php_value memory_limit 256M
```

### Trin 3: Deaktivér plugins

1. Via FTP — omdøb `wp-content/plugins/` til `plugins_disabled/`
2. Genindlæs sitet
3. Hvis det virker — omdøb tilbage og aktivér plugins én ad gangen
4. Det plugin der genskaber fejlen er synderen

### Trin 4: Skift tema

1. Via FTP — omdøb dit aktive temas mappe
2. WordPress falder tilbage til standardtema
3. Genindlæs sitet

### Trin 5: Tjek PHP-version

Forkert PHP-version kan give 500-fejl:

1. Log ind på hosting-panelet
2. Tjek PHP-version (skal være mindst 7.4, helst 8.1+)
3. Prøv at skifte til en anden PHP-version
4. Test sitet

### Trin 6: Tjek filrettigheder

Forkerte rettigheder giver 500-fejl:

| Hvad | Korrekt rettighed |
|------|-------------------|
| Mapper | 755 |
| Filer | 644 |
| wp-config.php | 600 eller 640 |

Rettigheder ændres via FTP-klienten (højreklik → Rettigheder/Permissions).

### Trin 7: Tjek serverens fejllog

Fejlloggen fortæller den præcise årsag:

- **cPanel:** **Metrics → Errors** eller **Logfiler → Fejllog**
- **Plesk:** **Websites & Domains → Logs**
- **Via FTP:** Tjek `error_log` i WordPress-roden
- **WordPress debug:** Aktivér `WP_DEBUG_LOG` og tjek `wp-content/debug.log`

### Trin 8: Geninstallér WordPress core

Hvis intet virker:

1. Download WordPress fra wordpress.org
2. Upload og overskriv alle filer UNDTAGEN:
   - `wp-content/` (dit indhold)
   - `wp-config.php` (dine indstillinger)
3. Genindlæs sitet

### Trin 9: Kontakt hosting

Hvis ingen af trinene virker:

- Problemet kan ligge på serversiden (ressourcebegrænsning, serveropsætning)
- Hostingudbyderen kan se den fulde fejllog
- Bed dem tjekke: PHP-version, mod_security regler, serverlogs

### Gængse årsager

| Årsag | Hyppighed |
|-------|-----------|
| Korrupt .htaccess | Meget hyppig |
| Plugin-konflikt | Hyppig |
| PHP-hukommelsesbegrænsning | Hyppig |
| Forkerte filrettigheder | Moderat |
| Forældet PHP-version | Moderat |
| Korrupte WordPress core-filer | Sjælden |
| Server-konfigurationsfejl | Sjælden |

## Bemærkninger

- 500-fejlen viser IKKE den egentlige fejl — du skal finde den i logfilerne
- Hvis fejlen kun opstår på bestemte sider, er det sandsynligvis et plugin eller tema-problem
- Hvis fejlen opstår efter en opdatering, rul opdateringen tilbage
- Gentagne 500-fejl kan indikere at du har overskredet hostingens ressourcegrænser
- Overvej at opgradere hosting-planen hvis fejlen skyldes ressourcemangel
