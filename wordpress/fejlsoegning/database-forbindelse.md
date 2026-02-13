# "Error establishing a database connection"

## Problem

WordPress viser fejlmeddelelsen "Error establishing a database connection". Sitet er helt nede — hverken forside eller admin virker. WordPress kan ikke oprette forbindelse til MySQL-databasen.

## Løsning

### Trin 1: Tjek om problemet er midlertidigt

1. Vent 2-5 minutter og prøv igen
2. Det kan være et midlertidigt serverproblem (overbelastning, vedligeholdelse)
3. Hvis det fortsætter — gå videre til næste trin

### Trin 2: Tjek wp-config.php

Forbind via FTP og åbn `wp-config.php`. Kontrollér disse fire værdier:

```php
define('DB_NAME', 'database_navn');     // Databasenavn
define('DB_USER', 'database_bruger');   // Databasebruger
define('DB_PASSWORD', 'adgangskode');   // Databaseadgangskode
define('DB_HOST', 'localhost');         // Databasehost
```

Sammenlign med de korrekte oplysninger fra hosting-panelet:

**cPanel:**
1. Log ind → **Databaser → MySQL Databases**
2. Tjek databasenavn, brugernavn og at brugeren er tilknyttet databasen

**Plesk:**
1. Log ind → **Websites & Domains → Databases**
2. Tjek oplysningerne

### Trin 3: Tjek at databasebrugeren har rettigheder

I hosting-panelet:
1. Gå til **MySQL Databases**
2. Scroll ned til **Add User To Database**
3. Vælg brugeren og databasen
4. Tildel **ALL PRIVILEGES**
5. Klik **Tilføj**

### Trin 4: Tjek DB_HOST

`DB_HOST` er normalt `localhost`, men på nogle hosts er det anderledes:

| Host | DB_HOST |
|------|---------|
| De fleste hosts | `localhost` |
| one.com | Specifikt hostnavn (ses i kontrolpanelet) |
| GoDaddy | Specifikt hostnavn |
| WP Engine | `localhost` |

Tjek din hostings dokumentation eller kontrolpanel for den korrekte værdi.

### Trin 5: Tjek om MySQL kører

Hvis du har SSH-adgang:
```bash
mysqladmin -u root -p status
```

Hvis MySQL er nede — kontakt hostingudbyderen.

### Trin 6: Reparér databasen

WordPress har et indbygget reparationsværktøj:

1. Tilføj i `wp-config.php`:
   ```php
   define('WP_ALLOW_REPAIR', true);
   ```
2. Besøg: `ditsite.dk/wp-admin/maint/repair.php`
3. Klik **Repair Database** (eller **Repair and Optimize Database**)
4. Fjern linjen fra `wp-config.php` bagefter (den kræver ikke login — sikkerhedsrisiko)

### Trin 7: Tjek databasen manuelt via phpMyAdmin

1. Log ind på phpMyAdmin via hosting-panelet
2. Hvis du kan se databasen og tabellerne — databasen virker
3. Hvis tabeller er markeret som "crashed" eller "corrupt":
   - Markér de korrupte tabeller
   - Vælg **Reparér tabel** fra dropdown-menuen

### Trin 8: Import fra backup

Hvis databasen er alvorligt beskadiget:
1. Slet den beskadigede database (eller opret en ny)
2. Importér seneste backup via phpMyAdmin → **Importér**
3. Opdatér `wp-config.php` hvis databasenavn har ændret sig

### Tjek om problemet kun er wp-admin

Hvis forsiden virker men admin giver databasefejl:

1. Åbn phpMyAdmin
2. Find tabellen `wp_options`
3. Tjek at `siteurl` og `home` har de korrekte URL'er
4. Ryd browsercache og prøv igen

## Bemærkninger

- Denne fejl skyldes ALTID databaseforbindelsen — aldrig plugins eller temaer
- De tre hyppigste årsager: forkerte loginoplysninger, databaseserver nede, korrupt database
- Kontakt hostingudbyderen tidligt — de kan hurtigt tjekke om MySQL-serveren kører
- Overvej et overvågningsværktøj (fx UptimeRobot) der advarer dig når sitet er nede
- Tag regelmæssig backup af databasen — den indeholder ALT dit indhold
