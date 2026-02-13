# Aktivér WordPress debug mode

## Problem

WordPress viser fejl (hvid skærm, uventet opførsel, fejlmeddelelser) og du har brug for mere information om hvad der er galt. Debug-mode viser detaljerede fejlmeddelelser.

## Løsning

### Aktivér debug-mode

1. Forbind til serveren via FTP eller hosting-filhåndtering
2. Åbn `wp-config.php` (ligger i WordPress-roden)
3. Find linjen:
   ```php
   define('WP_DEBUG', false);
   ```
4. Erstat med følgende:
   ```php
   // Aktivér debug-mode
   define('WP_DEBUG', true);

   // Gem fejl i logfil (wp-content/debug.log)
   define('WP_DEBUG_LOG', true);

   // Vis IKKE fejl på selve sitet (kun i logfil)
   define('WP_DEBUG_DISPLAY', false);

   // Log alle database-forespørgsler (valgfrit — kun til avanceret fejlsøgning)
   // define('SAVEQUERIES', true);
   ```
5. Gem filen

### Læs fejlloggen

Fejlene logges i `wp-content/debug.log`:

1. Via FTP — navigér til `wp-content/`
2. Åbn eller download filen `debug.log`
3. Kig efter de nyeste fejl (bunden af filen)
4. Fejlmeddelelsen fortæller:
   - **Filnavn** og **linjenummer** hvor fejlen opstår
   - **Fejltype** (Fatal error, Warning, Notice, Deprecated)
   - **Beskrivelse** af fejlen

### Forstå fejltyper

| Fejltype | Alvorlighed | Handling |
|----------|-------------|---------|
| **Fatal error** | Kritisk — sitet crasher | Skal fixes med det samme |
| **Warning** | Alvorlig — noget virker ikke korrekt | Bør fixes snart |
| **Notice** | Mindre — fungerer men ikke optimalt | Kan ignoreres midlertidigt |
| **Deprecated** | Forældet kode — virker nu, men kan stoppe | Opdatér plugin/tema |

### Eksempler på gængse fejlmeddelelser

**Fatal error — manglende fil:**
```
Fatal error: require_once(): Failed opening required
'/wp-content/plugins/mit-plugin/fil.php'
```
Løsning: Geninstallér pluginet.

**Fatal error — for lidt hukommelse:**
```
Fatal error: Allowed memory size of 67108864 bytes exhausted
```
Løsning: Øg `WP_MEMORY_LIMIT` i `wp-config.php`.

**Warning — deprecated funktion:**
```
Deprecated: Function create_function() is deprecated in
/wp-content/plugins/gammelt-plugin/fil.php
```
Løsning: Opdatér eller erstat pluginet.

### Debug-mode for specifikke formål

**Vis fejl direkte på sitet (kun til test — ALDRIG i produktion):**
```php
define('WP_DEBUG', true);
define('WP_DEBUG_DISPLAY', true);
```

**Debug scripts og styles (vis uminificerede versioner):**
```php
define('SCRIPT_DEBUG', true);
```

**Log database-forespørgsler (til ydeevne-fejlsøgning):**
```php
define('SAVEQUERIES', true);
```

### Deaktivér debug-mode igen

Når fejlsøgningen er færdig:

1. Åbn `wp-config.php`
2. Sæt tilbage til:
   ```php
   define('WP_DEBUG', false);
   ```
3. Slet eller tøm `wp-content/debug.log` (den kan blive meget stor)

## Bemærkninger

- Lad ALDRIG debug-mode være aktiveret på et live site — det afslører tekniske detaljer for besøgende
- `WP_DEBUG_DISPLAY` = false + `WP_DEBUG_LOG` = true er den sikreste kombination
- Debug-logfilen kan vokse hurtigt — slet den regelmæssigt
- Brug pluginet **Query Monitor** for avanceret debug direkte i browseren (kun for administratorer)
- Placér debug-indstillinger FØR linjen `/* That's all, stop editing! */` i wp-config.php
