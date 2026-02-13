# Opdatér PHP-version på hosting

## Problem

WordPress anbefaler minimum PHP 7.4 og anbefaler PHP 8.0+. En forældet PHP-version giver:
- Sikkerhedshuller (ældre PHP-versioner modtager ikke sikkerhedsopdateringer)
- Dårligere ydeevne (nyere PHP er markant hurtigere)
- Plugin-kompatibilitetsproblemer (nye plugins kræver nyere PHP)
- WordPress-advarsler i admin om forældet PHP

## Løsning

### Trin 1: Tjek nuværende PHP-version

**I WordPress:**
1. Gå til **Værktøjer → Website sundhed**
2. Klik fanen **Info**
3. Åbn sektionen **Server** — PHP-version vises her

**Eller via phpinfo:**
1. Opret en fil `phpinfo.php` i roden:
   ```php
   <?php phpinfo(); ?>
   ```
2. Besøg `ditsite.dk/phpinfo.php`
3. **Slet filen bagefter** — den viser følsomme serveroplysninger

### Trin 2: Tjek kompatibilitet

Før du skifter PHP-version:

1. **Installér pluginet PHP Compatibility Checker**
2. Gå til **Værktøjer → PHP Compatibility**
3. Vælg den ønskede PHP-version
4. Klik **Scan site**
5. Gennemgå resultater — ret eventuelle inkompatible plugins/temaer

### Trin 3: Tag backup

Tag ALTID komplet backup før PHP-opdatering. Hvis noget går galt, kan du rulle tilbage.

### Trin 4: Skift PHP-version

**cPanel (de fleste hosts):**
1. Log ind på cPanel
2. Find **MultiPHP Manager** eller **PHP Version**
3. Vælg dit domæne
4. Vælg den nye PHP-version (8.0, 8.1, 8.2 eller 8.3)
5. Klik **Anvend**

**Plesk:**
1. Log ind på Plesk
2. Gå til **Websites & Domains**
3. Klik **PHP Settings** ud for dit domæne
4. Vælg den nye PHP-version
5. Klik **OK** / **Anvend**

**one.com:**
1. Log ind på one.com kontrolpanel
2. Gå til **PHP og database-indstillinger**
3. Vælg PHP-version
4. Gem ændringer

**SiteGround:**
1. Log ind på Site Tools
2. Gå til **Devs → PHP Manager**
3. Vælg den ønskede version
4. Klik **Bekræft**

### Trin 5: Test sitet

Efter PHP-opdatering:

1. Besøg forsiden — vises den korrekt?
2. Tjek admin-panelet — kan du logge ind?
3. Test vigtige funktioner (formularer, WooCommerce etc.)
4. Tjek **Værktøjer → Website sundhed** for nye advarsler
5. Tjek fejlloggen for PHP-fejl

### Hvis noget går galt

1. **Skift tilbage til den gamle PHP-version** via hosting-panelet
2. Opdatér de inkompatible plugins/temaer
3. Prøv at skifte PHP-version igen
4. Kontakt hostingudbyderen hvis du ikke kan ændre PHP-version

### Anbefalede PHP-versioner (2025-2026)

| PHP-version | Status | Anbefalet? |
|-------------|--------|------------|
| 7.4 | End of life | Nej — opdatér snarest |
| 8.0 | End of life | Nej — opdatér snarest |
| 8.1 | Sikkerhedsopdateringer | Acceptabel |
| 8.2 | Aktiv support | Anbefalet |
| 8.3 | Aktiv support | Anbefalet |

## Bemærkninger

- PHP 8.x er markant hurtigere end 7.x — du vil mærke en hastighedsforbedring
- Ændr ALDRIG PHP-version på et live site uden backup
- Nogle ældre plugins virker ikke med PHP 8.x — opdatér eller erstat dem
- PHP-indstillinger som `memory_limit` og `upload_max_filesize` kan nulstilles ved versionsskift — tjek dem bagefter
- Managed WordPress-hosts (fx Kinsta, WP Engine) opdaterer ofte PHP automatisk
