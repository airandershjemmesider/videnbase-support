# cPanel — Oversigt

## Hvad er det

cPanel er kontrolpanelet for den enkelte hosting-konto. Her administrerer kunden filer, databaser, email, domæner, SSL og meget mere — uden at skulle bruge kommandolinjen.

## Adgang

- **URL:** `https://domæne:2083` eller via hosting-udbyderens link
- **Login:** Brugernavn og password (oprettet i WHM)
- **Alternativ:** Mange hosting-udbydere tilbyder single sign-on fra deres kundepanel

## Vigtigste sektioner

### Files
- **File Manager** — Upload, redigér, slet og flyt filer direkte i browseren
- **Disk Usage** — Se hvad der fylder på kontoen
- **FTP Accounts** — Opret FTP-adgange til udviklere

### Databases
- **MySQL Databases** — Opret databaser og brugere
- **phpMyAdmin** — Administrér databaser visuelt (SQL-forespørgsler, eksport, import)

### Domains
- **Addon Domains** — Tilføj ekstra domæner til kontoen
- **Subdomains** — Opret underdomæner (f.eks. blog.domæne.dk)
- **Redirects** — Opsæt omdirigeringer

### Email
- **Email Accounts** — Opret og administrér email-konti
- **Forwarders** — Videresend email
- **Email Deliverability** — Tjek SPF, DKIM, rDNS

### Security
- **SSL/TLS** — Administrér SSL-certifikater
- **IP Blocker** — Blokér specifikke IP-adresser
- **Hotlink Protection** — Beskyt billeder mod hotlinking

### Software
- **Softaculous** — Installér WordPress, Joomla, PrestaShop m.fl. med ét klik
- **MultiPHP Manager** — Vælg PHP-version per domæne
- **MultiPHP INI Editor** — Juster PHP-indstillinger

### Metrics
- **Visitors** — Log over besøgende
- **Errors** — PHP- og server-fejllog
- **Resource Usage** — CPU, RAM og I/O-forbrug

## File Manager — hurtig guide

1. Åbn **File Manager** i cPanel
2. Naviger til `public_html` (webroot for hoveddomænet)
3. **Upload:** Klik Upload-knappen — træk filer ind eller vælg fra computeren
4. **Redigér:** Højreklik → Edit (til hurtige ændringer i .htaccess, wp-config.php osv.)
5. **Rettigheder:** Højreklik → Change Permissions

## Bemærkninger

- `public_html` er webroden — alt der ligger her, er tilgængeligt via domænet
- Addon-domæner opretter undermapper i `public_html` (f.eks. `public_html/ekstradomæne.dk`)
- cPanel har temaet "Jupiter" (nyere versioner) eller "paper_lantern" (ældre)
- Søgefeltet øverst i cPanel finder hurtigt den funktion du leder efter
