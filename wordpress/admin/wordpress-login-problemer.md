# Kan ikke logge ind i WordPress admin

## Problem

Du kan ikke logge ind på WordPress admin-panelet. Mulige symptomer:
- Login-siden genindlæser uden fejlmeddelelse
- "Ugyldigt brugernavn eller adgangskode"
- Login-siden vises ikke (404 eller hvid skærm)
- Du bliver logget ud med det samme efter login

## Løsning

### 1. Nulstil adgangskode via email

1. Gå til `ditsite.dk/wp-login.php`
2. Klik **Mistet din adgangskode?**
3. Indtast email eller brugernavn
4. Tjek email (og spam-mappe) for nulstillingslink
5. Følg linket og opret ny adgangskode

### 2. Nulstil adgangskode via phpMyAdmin

Hvis email ikke virker:

1. Log ind på hostingens kontrolpanel (cPanel, Plesk etc.)
2. Åbn **phpMyAdmin**
3. Vælg WordPress-databasen
4. Find tabellen `wp_users` (præfikset kan variere)
5. Klik **Redigér** ud for din bruger
6. I feltet `user_pass` — vælg funktionen **MD5**
7. Indtast din nye adgangskode i værdi-feltet
8. Klik **Udfør**

### 3. Login-siden genindlæser (cookies-problem)

1. Ryd browserens cookies og cache
2. Prøv i inkognito/privat vindue
3. Prøv en anden browser
4. Tilføj i `wp-config.php`:
   ```php
   define('COOKIE_DOMAIN', 'ditsite.dk');
   define('ADMIN_COOKIE_PATH', '/');
   ```

### 4. Login-siden giver 404

1. Prøv at gå direkte til `ditsite.dk/wp-admin/`
2. Tjek at WordPress er installeret korrekt
3. Tjek `.htaccess`-filen — omdøb den midlertidigt og besøg **Indstillinger → Permalinks** for at regenerere

### 5. Bliver logget ud med det samme

Ofte et problem med WordPress URL-indstillinger:

1. Åbn `wp-config.php` via FTP
2. Tilføj disse linjer (erstat med dit domæne):
   ```php
   define('WP_HOME', 'https://ditsite.dk');
   define('WP_SITEURL', 'https://ditsite.dk');
   ```
3. Gem filen og prøv at logge ind igen

### 6. For mange login-forsøg (blokeret)

Hvis et sikkerhedsplugin blokerer dig:

1. Vent den angivne tid (typisk 15-60 minutter)
2. Eller deaktivér sikkerhedsplugin via FTP:
   - Omdøb plugin-mappen (fx `wordfence` → `wordfence_disabled`)
3. Log ind og konfigurér plugin korrekt
4. Omdøb mappen tilbage

## Bemærkninger

- Standard login-URL er `ditsite.dk/wp-login.php` — nogle sikkerhedsplugins ændrer denne
- Brug en adgangskodemanager for at undgå glemt password
- Hvis intet virker, kontakt hostingudbyderen — de kan hjælpe med database-adgang
- Hav altid mindst to administrator-konti som backup
