# Deaktivér plugins via FTP/filhåndtering

## Problem

Du kan ikke logge ind i WordPress admin (hvid skærm, fejl, blokeret af sikkerhedsplugin) og skal deaktivere plugins udefra.

## Løsning

### Metode 1: Via FTP (FileZilla)

1. **Forbind til serveren** med en FTP-klient (FileZilla, WinSCP el.lign.)
   - Brug FTP-oplysninger fra din hostingudbyder
   - Host, brugernavn, adgangskode og port (typisk 21 eller 22 for SFTP)

2. **Navigér til plugin-mappen**
   ```
   /public_html/wp-content/plugins/
   ```
   (stien kan variere — fx `/httpdocs/` eller `/www/`)

3. **Deaktivér ALLE plugins på én gang:**
   - Omdøb mappen `plugins` til `plugins_disabled`
   - WordPress deaktiverer automatisk alle plugins når mappen ikke findes

4. **Prøv at logge ind** på WordPress admin

5. **Genaktivér plugins:**
   - Omdøb mappen tilbage til `plugins`
   - Gå til **Plugins → Installerede plugins** i admin
   - Alle plugins er nu deaktiverede men synlige — aktivér dem én ad gangen

### Metode 2: Deaktivér ét specifikt plugin

1. Navigér til `/wp-content/plugins/`
2. Find mappen for det specifikke plugin (fx `wordfence/`)
3. Omdøb mappen (fx `wordfence_disabled/`)
4. Pluginet er nu deaktiveret
5. Log ind og løs problemet
6. Omdøb mappen tilbage når du er klar

### Metode 3: Via hostingens filhåndtering

Hvis du ikke har FTP:

1. Log ind på hostingens kontrolpanel (cPanel, Plesk etc.)
2. Åbn **Filhåndtering** (File Manager)
3. Navigér til `wp-content/plugins/`
4. Højreklik på plugin-mappen → **Omdøb**
5. Følg samme fremgangsmåde som FTP-metoden

### Metode 4: Via phpMyAdmin (avanceret)

Deaktivér plugins direkte i databasen:

1. Åbn **phpMyAdmin**
2. Vælg WordPress-databasen
3. Find tabellen `wp_options`
4. Søg efter rækken med `option_name` = `active_plugins`
5. Redigér feltet `option_value`
6. Erstat indholdet med: `a:0:{}`
7. Gem — alle plugins er nu deaktiverede

### Gængse plugins der blokerer login

| Plugin | Mappenavn | Typisk problem |
|--------|-----------|----------------|
| Wordfence | `wordfence/` | Blokerer efter for mange loginforsøg |
| iThemes Security | `better-wp-security/` | Ændrer login-URL |
| All In One Security | `all-in-one-wp-security-and-firewall/` | Blokerer IP-adresser |
| Limit Login Attempts | `limit-login-attempts-reloaded/` | Blokerer efter X forsøg |

## Bemærkninger

- Brug ALTID SFTP (port 22) frem for FTP (port 21) hvis muligt — det er krypteret
- Omdøbning er sikrere end sletning — du bevarer plugin-filerne
- Husk at omdøbe mappen tilbage efter fejlsøgning
- Hvis du ikke kender FTP-oplysningerne, find dem i hostingens kontrolpanel eller kontakt support
- Nogle managed WordPress-hosts (fx WP Engine) har egne værktøjer til at deaktivere plugins
