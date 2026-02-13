# Flyt en hjemmeside til ny hosting

## Problem

Du skal flytte en hjemmeside fra én hosting-udbyder til en anden med minimal nedetid.

## Løsning

### Oversigt over processen

1. Opsæt den nye hosting
2. Kopier filer og database
3. Test på den nye server
4. Skift DNS
5. Verificer og ryd op

### Trin 1: Forbered den nye hosting

1. Opret konto hos den nye hosting-udbyder
2. Opsæt domænet i kontrolpanelet (uden at ændre DNS endnu)
3. Notér den nye servers IP-adresse
4. Tjek at PHP-version og andre krav matcher

### Trin 2: Tag backup af den eksisterende side

#### WordPress (med plugin)
- Installer **All-in-One WP Migration**, **Duplicator** eller **UpdraftPlus**
- Kør en fuld backup (filer + database)
- Download backup-filen

#### WordPress (manuelt)
1. **Filer:** Download hele `public_html` / `www` mappen via FTP eller filhåndtering
2. **Database:** Eksportér via phpMyAdmin → vælg databasen → "Eksportér" → SQL-format

#### Statisk side
- Download alle filer via FTP

### Trin 3: Overfør til den nye server

#### WordPress (med plugin)
1. Installer WordPress på den nye server
2. Installer samme migrations-plugin
3. Importér backup-filen

#### WordPress (manuelt)
1. Upload filer via FTP til den nye server
2. Opret ny database i kontrolpanelet
3. Importér SQL-filen via phpMyAdmin
4. Opdater `wp-config.php` med nye database-oplysninger:
   ```php
   define('DB_NAME', 'ny_database');
   define('DB_USER', 'ny_bruger');
   define('DB_PASSWORD', 'nyt_kodeord');
   define('DB_HOST', 'localhost');
   ```

### Trin 4: Test på den nye server

Inden du skifter DNS, test at sitet virker:

#### Via hosts-fil (Windows)
1. Åbn `C:\Windows\System32\drivers\etc\hosts` som administrator
2. Tilføj: `NY.SERVER.IP.ADRESSE example.dk`
3. Gem og besøg sitet i browseren
4. **Husk at fjerne linjen igen bagefter**

#### Via midlertidigt URL
- Mange hosts giver et midlertidigt URL (f.eks. `example.dk.temp-url.com`)
- Brug dette til at teste

### Trin 5: Skift DNS

1. Sæt TTL ned til **300** på A-record (mindst et par timer i forvejen)
2. Opdater A-record til den nye servers IP
3. Hvis du bruger Cloudflare: Opdater IP-adressen i Cloudflare-dashboard
4. Vent på propagation (15 min – 4 timer)

### Trin 6: Verificer efter skift

- Tjek at sitet loader korrekt
- Tjek at email stadig fungerer (MX records uændret)
- Tjek at SSL-certifikat virker
- Tjek formularer, login, betalingsløsninger
- Kør en hastighedstest (GTmetrix, PageSpeed Insights)

### Trin 7: Ryd op

- Fjern hosts-fil ændringer
- Sæt TTL tilbage til 3600
- Behold den gamle hosting i mindst 1-2 uger som fallback
- Opsig den gamle hosting når alt er bekræftet

## Tjekliste for flytning

| Trin | Status |
|------|--------|
| Backup af filer og database | [ ] |
| Filer kopieret til ny server | [ ] |
| Database importeret | [ ] |
| wp-config.php opdateret | [ ] |
| Test via hosts-fil bestået | [ ] |
| SSL-certifikat opsat | [ ] |
| DNS opdateret | [ ] |
| Email fungerer | [ ] |
| Formularer testet | [ ] |

## Bemærkninger

- **Lav ALDRIG flytning fredag eftermiddag** — giv dig selv tid til fejlsøgning
- **Behold altid den gamle hosting** som backup i mindst 1-2 uger
- Husk at opsætte **SSL-certifikat** på den nye server (se ssl-mappen)
- Hvis sitet bruger e-handel: Planlæg flytningen i en stille periode
- Store sider med meget data: Overvej at bruge rsync eller hostingens migrations-service
