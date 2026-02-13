# WordPress er hacket — hvad gør du

## Problem

Dit WordPress-site er kompromitteret. Tegn på hacking:
- Sitet omdirigerer til et andet domæne
- Ukendt indhold eller links på sitet (spam, reklamer)
- Google viser "Denne side kan skade din computer"
- Ukendte administrator-konti
- Filer er ændret uden din viden
- Hostingudbyderen har blokeret dit site

## Løsning

### Trin 1: Bevar roen og tag backup

1. **Tag backup af det hackede site** — du kan have brug for det til analyse
2. **Notér** hvornår du opdagede problemet
3. **Skriv ned** alle ændringer du har bemærket

### Trin 2: Sæt sitet i vedligeholdelsestilstand

Tilføj i `.htaccess` midlertidigt (eller brug et maintenance-plugin):
```apache
RewriteEngine On
RewriteCond %{REMOTE_ADDR} !^DIN\.IP\.ADRESSE$
RewriteRule .* - [R=503,L]
```

### Trin 3: Skift ALLE adgangskoder

Skift adgangskoder til:
- Alle WordPress-brugerkonti (især administratorer)
- FTP/SFTP-adgang
- Database (opdatér også `wp-config.php`)
- Hosting kontrolpanel (cPanel, Plesk)
- Email-konti tilknyttet sitet

### Trin 4: Scan for malware

**Med plugin:**
1. Installér **Wordfence** (hvis du kan logge ind)
2. Kør en fuld scanning
3. Gennemgå og fjern fundne trusler

**Manuelt:**
1. Download alle filer via FTP
2. Sammenlign WordPress core-filer med en ren installation (download fra wordpress.org)
3. Søg efter mistænkelige filer:
   - Filer med tilfældige navne i `wp-content/`
   - PHP-filer i `wp-content/uploads/` (bør kun indeholde mediefiler)
   - Filer med `eval()`, `base64_decode()`, `gzinflate()` i koden

### Trin 5: Geninstallér WordPress core

1. Download seneste WordPress fra wordpress.org
2. Upload og overskriv alle core-filer via FTP (IKKE `wp-content/` og `wp-config.php`)
3. Dette erstatter eventuelle inficerede core-filer

### Trin 6: Tjek og ryd databasen

1. Åbn **phpMyAdmin**
2. Tjek `wp_users` — slet ukendte administrator-konti
3. Tjek `wp_options` — kontrollér `siteurl` og `home` (er de korrekte?)
4. Søg efter mistænkeligt indhold i `wp_posts` (injiceret JavaScript/iframes)

### Trin 7: Geninstallér plugins og temaer

1. Slet alle plugins og temaer via FTP
2. Geninstallér fra wordpress.org eller den officielle kilde
3. Brug ALDRIG piratkopierede/nullede plugins — de indeholder næsten altid malware

### Trin 8: Opdatér alt

1. Opdatér WordPress til seneste version
2. Opdatér alle plugins og temaer
3. Opdatér PHP til seneste understøttede version

### Trin 9: Hærd sitet

Se guiden "Hærdning af WordPress" for at forhindre fremtidige angreb.

### Trin 10: Kontakt Google (hvis blokeret)

Hvis Google har markeret dit site:
1. Gå til **Google Search Console**
2. Verificér dit site (hvis ikke allerede gjort)
3. Under **Sikkerhed og manuelle handlinger** → **Sikkerhedsproblemer**
4. Klik **Anmod om gennemgang** efter oprydning

## Bemærkninger

- De fleste hacks skyldes: forældede plugins, svage adgangskoder eller nullede temaer/plugins
- Hvis du har en ren backup fra FØR hacket, er gendan fra backup ofte hurtigere end oprydning
- Professionel malware-fjernelse: Sucuri og Wordfence tilbyder betalte oprydningstjenester
- Kontakt din hostingudbyder — de kan ofte hjælpe med scanning og oprydning
- Opsæt overvågning efter oprydning for at opdage tilbagefald hurtigt
