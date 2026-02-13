# Wordfence Sikkerhed — Opsætning

## Hvad er det

Wordfence er det mest populære sikkerhedsplugin til WordPress. Det tilbyder en Web Application Firewall (WAF), malware-scanner, login-sikkerhed med to-faktor-autentificering (2FA) og realtids IP-blokering. Wordfence beskytter mod brute force-angreb, malware og kendte sårbarheder.

## Installation

1. Gå til **Plugins → Tilføj nyt**
2. Søg efter "Wordfence Security"
3. Installér og aktivér **Wordfence Security – Firewall & Malware Scan**
4. Indtast en emailadresse til sikkerhedsadvarsler
5. Acceptér licensbetingelserne

## Grundopsætning

### Firewall — Learning Mode
Ved første aktivering kører firewallen i **Learning Mode** i én uge:

1. Gå til **Wordfence → Firewall**
2. Status viser "Learning Mode" — dette er normalt
3. Wordfence lærer sidens normale trafik og adfærd
4. Efter ~7 dage skifter den automatisk til **Enabled and Protecting**
5. Du kan manuelt skifte til "Enabled" før tid, men vent gerne den fulde periode

### Optimér firewallen
1. Wordfence viser ofte en besked: "Wordfence firewall is not optimized"
2. Klik **Click here to configure** eller gå til **Firewall → All Firewall Options**
3. Klik **Optimize the Wordfence Firewall**
4. Vælg den korrekte serverkonfiguration (typisk Apache + mod_php eller LiteSpeed)
5. Download backup af .htaccess inden du anvender ændringerne
6. Klik **Continue** — Wordfence tilføjer firewall-kode til .htaccess/.user.ini

## Malware Scanner

### Kør en scan
1. Gå til **Wordfence → Scan**
2. Klik **Start New Scan**
3. Scanningen tjekker:
   - WordPress core-filer mod originaler
   - Plugin- og tema-filer mod kendte versioner
   - Ukendte filer der ikke hører til WordPress
   - Kendte malware-signaturer
   - Ændrede filer

### Gennemgå resultater
- **Critical** — kræver øjeblikkelig handling (malware fundet, ændrede core-filer)
- **Warning** — bør undersøges (ukendte filer, forældede plugins)
- **Informational** — ingen handling nødvendig

### Håndtér fund
- **Core-filer ændret:** Klik "Repair" for at gendanne originale filer
- **Ukendte filer:** Undersøg filen — slet kun hvis du er sikker på at den er skadelig
- **Plugin-filer ændret:** Opdatér eller geninstallér pluginet
- **Malware:** Følg Wordfences anbefalinger og kontakt hosting hvis nødvendigt

## Login Security

### To-faktor-autentificering (2FA)
1. Gå til **Wordfence → Login Security**
2. Scan QR-koden med en autentificeringsapp (Google Authenticator, Authy osv.)
3. Indtast koden for at bekræfte
4. Download recovery codes og gem dem sikkert
5. Aktivér 2FA for alle admin-brugere

### Limit Login Attempts
- **Wordfence → All Options → Brute Force Protection**
- **Lock out after X login failures:** 5 (standard, fint for de fleste)
- **Lock out after X forgot password attempts:** 3
- **Count failures over what time period:** 4 timer
- **Amount of time a user is locked out:** 4 timer

### reCAPTCHA
1. Gå til **Wordfence → Login Security → Settings**
2. Aktivér reCAPTCHA v3
3. Indtast Site Key og Secret Key fra Google reCAPTCHA admin
4. reCAPTCHA tilføjes automatisk til login- og registreringsformularer

## Firewall — avancerede indstillinger

### WAF-regler
- Wordfence opdaterer automatisk WAF-regler (Premium: realtid, Free: 30 dages forsinkelse)
- Undlad at deaktivere regler medmindre de giver specifikke problemer
- Tjek **Wordfence → Firewall → Blocking** for blokerede IP'er

### IP-blokering
1. Gå til **Wordfence → Firewall → Blocking**
2. Klik **Create a Blocking Rule**
3. Vælg type:
   - **IP Address** — blokér en specifik IP
   - **Country** (Premium) — blokér hele lande
   - **Custom Pattern** — blokér baseret på user agent, referrer osv.

### Rate Limiting
- **Wordfence → All Options → Rate Limiting**
- Begræns antal forespørgsler fra en enkelt IP
- Hjælper mod crawlers og DDoS-lignende trafik
- Standard-indstillingerne er fine for de fleste sider

## Email-alerts

### Konfigurér notifikationer
1. Gå til **Wordfence → All Options → Email Alert Preferences**
2. Vælg hvad du vil have besked om:
   - **Aktivér:** Scan-resultater, blokerede IP'er, login-forsøg fra admin
   - **Overvej at deaktivere:** Hver enkelt blokeret IP (kan give mange emails)
3. Tilføj flere email-modtagere hvis nødvendigt

### Anbefalede alert-indstillinger
| Alert | Anbefalet | Grund |
|-------|-----------|-------|
| Scan-resultater med fund | Aktiveret | Vigtigt at vide om malware |
| Admin-login fra ny enhed | Aktiveret | Sikkerhed |
| Plugin-opdateringer tilgængelige | Aktiveret | Holde WordPress opdateret |
| Hver blokeret IP | Deaktiveret | For mange emails på travle sider |
| Brute force-angreb | Aktiveret | Vigtig sikkerhedsinfo |

## Fejlsøgning

### "Wordfence firewall not optimized"
1. Gå til **Wordfence → Firewall**
2. Klik **Optimize the Wordfence Firewall**
3. Vælg korrekt serverkonfiguration
4. Download backup og anvend ændringerne
5. Tjek at hjemmesiden stadig virker bagefter

### Scan kører langsomt eller timer ud
- Gå til **Wordfence → All Options → Scan Options**
- Aktivér **Low Resource Scanning** (bruger mindre server-ressourcer)
- Reducér scan-frekvens til ugentlig i stedet for daglig
- Kontakt hosting hvis serveren har meget begrænsede ressourcer

### Wordfence blokerer legitime brugere
1. Gå til **Wordfence → Firewall → Blocking**
2. Find den blokerede IP og fjern blokeringen
3. Tilføj IP'en til **Wordfence → Firewall → Whitelisting** hvis det er en fast bruger
4. Justér rate limiting-indstillingerne hvis problemet gentager sig

### Konflikt med cache-plugin
- Wordfence og WP Rocket kan normalt sameksistere
- Hvis firewall-optimeringen fejler: Ryd cachen og prøv igen
- Sørg for at Wordfence loader BEFORE cache-pluginet i load-ordenen

## Vigtige indstillinger — tjekliste

| Indstilling | Anbefalet |
|-------------|-----------|
| Firewall | Enabled and Protecting |
| Firewall optimeret | Ja |
| Malware scan | Ugentlig (minimum) |
| 2FA for admins | Aktiveret |
| Login attempts limit | 5 forsøg |
| Email alerts (scan) | Aktiveret |
| reCAPTCHA | Aktiveret |
| Auto-update | Aktiveret for Wordfence |

## Bemærkninger

- Wordfence Free giver solid beskyttelse for de fleste sider
- Wordfence Premium tilføjer: Realtids firewall-regler, landblokering, realtids IP-blacklist
- Brug kun ét sikkerhedsplugin — kør IKKE Wordfence sammen med Sucuri eller iThemes
- Firewall-optimering kræver .htaccess-adgang — virker ikke på alle hosts (f.eks. nginx uden .htaccess)
- Tag altid backup inden firewall-optimering
- Scan-frekvens: Daglig for webshops og sider med brugere, ugentlig for statiske sider
- 2FA er den vigtigste enkeltstående sikkerhedsforanstaltning — aktivér det altid
