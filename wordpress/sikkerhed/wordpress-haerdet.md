# Hærdning af WordPress — grundlæggende sikkerhed

## Problem

En standard WordPress-installation har flere kendte svagheder som hackere udnytter. Grundlæggende hærdning reducerer risikoen markant.

## Løsning

### 1. Hold alt opdateret

- WordPress core, plugins og temaer skal ALTID være opdaterede
- Slet plugins og temaer du ikke bruger — de er en angrebsflade
- Slet standardtemaer du ikke bruger (behold ét som fallback)

### 2. Brug stærke adgangskoder

- Minimum 12 tegn med bogstaver, tal og specialtegn
- Brug en adgangskodemanager (Bitwarden, 1Password el.lign.)
- Forskellige adgangskoder til WP-admin, FTP, database og hosting

### 3. Ændr standard brugernavn

- Brug ALDRIG "admin" som brugernavn
- Opret en ny administrator-konto med unikt brugernavn
- Slet den gamle "admin" konto (overfør indhold til den nye)

### 4. Beskyt wp-config.php

Flyt `wp-config.php` en mappe op (WordPress finder den automatisk):
```
/public_html/wp-config.php → /wp-config.php
```

Eller begræns adgang via `.htaccess`:
```apache
<files wp-config.php>
order allow,deny
deny from all
</files>
```

### 5. Deaktivér filredigering i admin

Tilføj i `wp-config.php`:
```php
define('DISALLOW_FILE_EDIT', true);
```
Dette forhindrer redigering af tema- og pluginfiler via admin-panelet.

### 6. Begræns login-forsøg

- Installér **Limit Login Attempts Reloaded** eller **Wordfence**
- Standard: bloker efter 3-5 fejlslagne forsøg
- Blokeringstid: minimum 15 minutter

### 7. Tilføj 2-faktor-godkendelse (2FA)

- Installér et 2FA-plugin (fx **Two Factor Authentication**)
- Konfigurér for alle administrator-konti
- Brug en autentificeringsapp (Google Authenticator, Authy)

### 8. Beskyt wp-admin med HTTP-godkendelse

Tilføj ekstra password-beskyttelse via hosting:

1. I cPanel: **Mappeadgangskoder** (Directory Privacy)
2. Vælg mappen `wp-admin`
3. Opret brugernavn og adgangskode
4. Nu kræves to logins — ekstra sikkerhedslag

### 9. Skjul WordPress-version

Tilføj i `functions.php` eller et custom plugin:
```php
remove_action('wp_head', 'wp_generator');
```

### 10. Deaktivér XML-RPC (hvis ikke nødvendigt)

XML-RPC bruges til pingbacks og fjernpublicering, men er også en angrebsflade:

```php
// Tilføj i functions.php
add_filter('xmlrpc_enabled', '__return_false');
```

Eller via `.htaccess`:
```apache
<Files xmlrpc.php>
order deny,allow
deny from all
</Files>
```

### 11. Sæt korrekte filrettigheder

| Fil/mappe | Rettighed |
|-----------|-----------|
| Mapper | 755 |
| Filer | 644 |
| wp-config.php | 600 eller 640 |

### 12. Brug SSL/HTTPS

- Installér et SSL-certifikat (de fleste hosts tilbyder gratis Let's Encrypt)
- Tving HTTPS i `wp-config.php`:
  ```php
  define('FORCE_SSL_ADMIN', true);
  ```

## Bemærkninger

- Ingen sikkerhedsforanstaltning er 100% — brug backup som sikkerhedsnet
- Hosting-kvalitet spiller en stor rolle — vælg en host med god sikkerhed
- Overvåg sitet med et sikkerhedsplugin der scanner for malware
- Gennemgå sikkerhedsindstillinger mindst én gang i kvartalet
- WordPress' egen sikkerhedsguide: Hardening WordPress (i WordPress Codex)
