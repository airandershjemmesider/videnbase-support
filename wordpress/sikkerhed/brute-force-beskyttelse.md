# Beskyt mod brute force login-angreb

## Problem

Brute force-angreb er automatiserede forsøg på at gætte dit brugernavn og adgangskode ved at prøve tusindvis af kombinationer. Dette er den mest gængse angrebstype mod WordPress.

Tegn på brute force-angreb:
- Sitet er langsomt (serveren belastes af mange login-forsøg)
- Du bliver blokeret fra login (sikkerhedsplugin blokerer din IP)
- Logfiler viser hundredvis af fejlslagne login-forsøg
- Ukendte IP-adresser i sikkerhedsloggen

## Løsning

### 1. Begræns login-forsøg

**Med Limit Login Attempts Reloaded:**
1. Installér og aktivér pluginet
2. Gå til **Indstillinger → Limit Login Attempts**
3. Indstil:
   - Tilladt forsøg: **3**
   - Lockout-varighed: **20 minutter**
   - Lang lockout efter: **3 lockouts** i **24 timer**
   - Lang lockout-varighed: **24 timer**

**Med Wordfence:**
1. Gå til **Wordfence → Firewall → Brute Force Protection**
2. Aktivér brute force-beskyttelse
3. Indstil maks. login-forsøg og blokeringstid

### 2. Tilføj 2-faktor-godkendelse (2FA)

2FA gør adgangskoden alene ubrugelig for angribere:

1. Installér **Two Factor Authentication** plugin
2. Gå til **Brugere → Din profil**
3. Aktivér 2FA og scan QR-koden med en autentificeringsapp
4. Gem backup-koder et sikkert sted
5. Kræv 2FA for alle administratorer

### 3. Ændr login-URL

Standard login-URL (`/wp-login.php` og `/wp-admin/`) er kendt af alle angribere:

**Med WPS Hide Login:**
1. Installér og aktivér pluginet
2. Gå til **Indstillinger → WPS Hide Login**
3. Ændr login-URL til noget unikt (fx `/min-adgang`)
4. Gem — noter den nye URL!

**VIGTIGT:** Husk den nye URL — ellers kan du ikke logge ind. Gem den i din adgangskodemanager.

### 4. Bloker dårlige brugernavne

Tilføj i `functions.php`:
```php
// Bloker login med "admin" brugernavn
function bloker_admin_login($user, $username) {
    if ($username === 'admin') {
        return new WP_Error('invalid_username',
            'Dette brugernavn er blokeret.');
    }
    return $user;
}
add_filter('authenticate', 'bloker_admin_login', 30, 2);
```

### 5. Deaktivér brugernavn-optælling

Angribere kan finde brugernavne via `?author=1`. Bloker dette:

```php
// Tilføj i functions.php
function bloker_author_enum() {
    if (isset($_GET['author']) && is_numeric($_GET['author'])) {
        wp_redirect(home_url(), 301);
        exit;
    }
}
add_action('init', 'bloker_author_enum');
```

### 6. HTTP-godkendelse på wp-login.php

Tilføj et ekstra password-lag via `.htaccess`:

```apache
<Files wp-login.php>
AuthType Basic
AuthName "Begrænset adgang"
AuthUserFile /sti/til/.htpasswd
Require valid-user
</Files>
```

Opret `.htpasswd` filen via hostingens kontrolpanel eller med en htpasswd-generator online.

### 7. IP-whitelisting (kun faste IP-adresser)

Hvis du altid logger ind fra samme IP:

```apache
<Files wp-login.php>
order deny,allow
deny from all
allow from 123.456.789.0
</Files>
```

Erstat med din IP-adresse. **OBS:** Virker kun med fast IP.

## Bemærkninger

- De fleste brute force-angreb rammer `wp-login.php` og `xmlrpc.php`
- Deaktivér XML-RPC hvis du ikke bruger det (se WordPress-hærdning)
- En stærk adgangskode er det vigtigste forsvar — 16+ tegn med blandet indhold
- Cloudflare (gratis plan) kan blokere mange angreb før de rammer din server
- Tjek logfiler regelmæssigt for mistænkelig aktivitet
- Hosting med DDoS-beskyttelse hjælper mod store angreb
