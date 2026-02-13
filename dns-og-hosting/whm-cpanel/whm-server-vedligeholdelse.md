# Server-vedligeholdelse i WHM

## Hvad er det

Løbende vedligeholdelse af en cPanel/WHM-server sikrer stabilitet, sikkerhed og god ydeevne. Denne guide dækker de vigtigste vedligeholdelsesopgaver.

## Opdateringer

### cPanel/WHM opdatering
1. WHM → **cPanel → Update Preferences**
2. Vælg opdateringsniveau:
   - **RELEASE** — stabil (anbefalet til produktion)
   - **CURRENT** — nyeste stabile
   - **EDGE** — beta (kun til test)
3. Automatiske opdateringer kører dagligt (kan sættes til manuelt)

### PHP-versioner
1. WHM → **Software → MultiPHP Manager**
2. Installér nye PHP-versioner via **EasyApache 4**
3. Fjern forældede versioner (f.eks. PHP 7.4) når ingen konti bruger dem
4. Anbefaling: Hold mindst PHP 8.1+ tilgængeligt

## Diskforbrug

1. WHM → **Account Information → List Accounts**
2. Sortér efter **Disk Used** for at finde konti der fylder mest
3. Kontakt kunder der nærmer sig deres kvote
4. Tjek også serverens egen disk: WHM → **Server Status → Service Status**

## Suspenderede konti

1. WHM → **Account Information → List Suspended Accounts**
2. Gennemgå årsagen til suspendering
3. Ususpendér via **Account Functions → Unsuspend an Account**
4. Slet konti der ikke længere er aktive via **Terminate an Account**

## Backup-konfiguration

1. WHM → **Backup → Backup Configuration**
2. Anbefalet opsætning:
   - **Backup Status:** Enabled
   - **Backup Type:** Compressed
   - **Daglig backup:** Aktivér — behold 5 dage
   - **Ugentlig backup:** Aktivér — behold 4 uger
   - **Månedlig backup:** Aktivér — behold 2 måneder
3. Vælg **Additional Destinations** for off-site backup (FTP, S3, Google Drive)
4. Ekskludér store konti kun hvis nødvendigt

## Service Status

1. WHM → **Server Status → Service Status**
2. Tjek at alle kritiske services kører:

| Service | Funktion |
|---------|----------|
| Apache (httpd) | Webserver |
| MySQL/MariaDB | Database |
| named (BIND) | DNS-server |
| Exim | Mail-server (udgående) |
| Dovecot | Mail-server (IMAP/POP3) |
| Pure-FTPd | FTP-server |
| cPanel/WHM | Kontrolpanel |
| cPHulk | Brute force beskyttelse |

3. Genstart fejlende services via klik på **Restart**

## EasyApache 4

1. WHM → **Software → EasyApache 4**
2. Administrér Apache- og PHP-moduler
3. Typiske moduler der kan være nødvendige:
   - **mod_rewrite** — URL-rewriting (kræves af WordPress)
   - **mod_headers** — HTTP headers
   - **PHP extensions:** imagick, memcached, opcache, redis
4. Klik **Customize** → vælg moduler → **Review** → **Provision**

## Firewall (CSF/LFD)

ConfigServer Security & Firewall er standard-firewall for cPanel-servere:

1. WHM → **Plugins → ConfigServer Security & Firewall**
2. **Tjek blokerede IP'er:** Quick Unblock — indtast IP for at fjerne blokering
3. **Firewall Allow:** Tilføj kunders eller udvikleres IP'er til whitelist
4. **LFD (Login Failure Daemon):** Blokerer automatisk IP'er efter gentagne mislykkede login
5. **Email-alarmer:** CSF sender email ved blokerede IP'er, mistænkelig aktivitet osv.

### Vigtige CSF-indstillinger
- `DENY_IP_LIMIT` — maks antal blokerede IP'er (standard 200)
- `LF_TRIGGER` — antal mislykkede login før blokering
- `CT_LIMIT` — maks samtidige forbindelser fra én IP

## Bemærkninger

- Kør ikke opdateringer i myldretid — planlæg dem om natten eller i weekenden
- Overvåg serverens load via WHM → **Server Status → Server Information**
- Hold altid en fungerende backup klar før større ændringer (PHP-opgradering, EasyApache-ændringer)
- Sæt monitoring op (f.eks. UptimeRobot) så du får besked hvis serveren er nede
- Gennemgå CSF-blokeringer jævnligt — legitime brugere kan blive blokeret ved fejlindtastning
