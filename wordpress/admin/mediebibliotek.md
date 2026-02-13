# Mediebibliotek problemer

## Problem

Problemer med WordPress mediebiblioteket kan vise sig som:
- Upload fejler med fejlmeddelelse
- Filstørrelsesgrænse forhindrer upload
- Billeder vises ikke korrekt
- Mediebiblioteket er tomt eller indlæser ikke

## Løsning

### Upload fejler — "HTTP-fejl"

1. **Ryd browsercache** og prøv igen
2. **Prøv en anden browser**
3. **Reducér filstørrelsen** — komprimér billedet før upload
4. **Øg PHP-hukommelse** — tilføj i `wp-config.php`:
   ```php
   define('WP_MEMORY_LIMIT', '256M');
   ```
5. **Deaktivér plugins** — især billedoptimerings- og sikkerhedsplugins kan blokere upload

### Filstørrelsesgrænse for stor

Standard upload-grænse er ofte 2-8 MB. Øg den på én af disse måder:

**Via .htaccess** (Apache):
```apache
php_value upload_max_filesize 64M
php_value post_max_size 64M
php_value max_execution_time 300
php_value max_input_time 300
```

**Via php.ini** (hvis du har adgang):
```ini
upload_max_filesize = 64M
post_max_size = 64M
max_execution_time = 300
```

**Via wp-config.php**:
```php
@ini_set('upload_max_filesize', '64M');
@ini_set('post_max_size', '64M');
```

**Via hosting-panel**: De fleste hosts har en PHP-indstilling under cPanel → "PHP Version" eller "PHP Settings" hvor du kan ændre grænsen direkte.

### Billeder vises ikke (ødelagte thumbnails)

1. Installér pluginet **Regenerate Thumbnails**
2. Gå til **Værktøjer → Regenerate Thumbnails**
3. Klik **Regenerér alle thumbnails**
4. Vent til processen er færdig

### Mediebiblioteket indlæser ikke

1. **Ryd cache** i browser og evt. cache-plugin
2. **Deaktivér plugins** trinvist for at finde konflikten
3. **Skift til standardtema** (Twenty Twenty-Four) midlertidigt
4. **Tjek JavaScript-fejl** — åbn browserens konsol (F12) og kig efter røde fejl
5. **Øg PHP-hukommelse** (se ovenfor)

### Tilladt filtyper

WordPress tillader som standard kun bestemte filtyper. For at tillade fx SVG:

```php
// Tilføj i functions.php eller et custom plugin
function tilfoej_filtyper($mimes) {
    $mimes['svg'] = 'image/svg+xml';
    return $mimes;
}
add_filter('upload_mimes', 'tilfoej_filtyper');
```

**OBS:** SVG-filer kan indeholde skadelig kode. Brug et plugin som **Safe SVG** i stedet.

### Filadgangsrettigheder

Forkerte rettigheder på upload-mappen forhindrer upload:

- `wp-content/uploads/` skal have rettigheder **755** (mapper) og **644** (filer)
- Rettigheder ændres via FTP-klient eller hosting-filhåndtering
- Spørg hostingudbyderen hvis du er usikker

## Bemærkninger

- WordPress opretter undermapper per år/måned i `wp-content/uploads/` (fx `2026/02/`)
- Store billeder bør komprimeres FØR upload — brug TinyPNG eller ShortPixel
- WordPress genererer automatisk flere størrelser per billede (thumbnail, medium, large)
- Slet ubrugte billeder løbende for at spare diskplads
