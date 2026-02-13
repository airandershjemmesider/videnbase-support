# Backup af WordPress

## Problem

Uden backup kan du miste alt indhold hvis noget går galt — hackerangreb, fejlslagen opdatering, hostingproblemer eller menneskelige fejl.

## Løsning

### Hvad skal sikkerhedskopieres

En komplet WordPress-backup indeholder:

1. **Databasen** — indlæg, sider, indstillinger, brugere, kommentarer
2. **wp-content/uploads/** — alle uploadede billeder og filer
3. **wp-content/plugins/** — installerede plugins
4. **wp-content/themes/** — temaer (inkl. tilpasninger)
5. **wp-config.php** — databaseforbindelse og indstillinger
6. **.htaccess** — permalink- og serverregler

### Metode 1: Backup med UpdraftPlus (anbefalet)

1. Installér og aktivér **UpdraftPlus** (gratis version)
2. Gå til **Indstillinger → UpdraftPlus Backups**
3. Klik **Backup nu**
4. Markér både "Inkludér din database" og "Inkludér dine filer"
5. Klik **Backup nu**

**Automatiske backups:**
1. Under fanen **Indstillinger** i UpdraftPlus
2. Sæt tidsplan for filer og database (ugentligt eller dagligt)
3. Vælg fjernlager (Google Drive, Dropbox, etc.)
4. Gem ændringer

### Metode 2: Backup via hosting

De fleste hostingudbydere tilbyder backup:

- **cPanel:** Gå til **Filer → Backup** eller **Backup Wizard**
- **Plesk:** Gå til **Websites & Domains → Backup Manager**
- **SiteGround/one.com:** Automatisk daglig backup med gendan-funktion

Tjek din hosting — mange tager automatisk daglig backup.

### Metode 3: Manuel backup

**Database:**
1. Log ind på **phpMyAdmin** via hosting-panel
2. Vælg WordPress-databasen
3. Klik **Eksportér**
4. Vælg format: **SQL**
5. Klik **Udfør** og gem filen

**Filer:**
1. Forbind til serveren via FTP (FileZilla el.lign.)
2. Download hele `wp-content/` mappen
3. Download `wp-config.php` og `.htaccess`

### Gendan fra backup

**Med UpdraftPlus:**
1. Gå til **Indstillinger → UpdraftPlus Backups**
2. Find den ønskede backup under **Eksisterende backups**
3. Klik **Gendan**
4. Vælg hvilke komponenter der skal gendannes
5. Klik **Gendan**

**Manuelt:**
1. Upload filer via FTP til de korrekte mapper
2. Importér databasen via phpMyAdmin → **Importér**
3. Opdatér `wp-config.php` hvis databasenavne har ændret sig

### Backup-strategi

| Hvad | Hvor ofte | Hvor |
|------|-----------|------|
| Database | Dagligt | Fjernlager (cloud) |
| Filer | Ugentligt | Fjernlager (cloud) |
| Komplet backup | Før opdateringer | Lokalt + cloud |

## Bemærkninger

- Gem ALDRIG backups kun på serveren — hvis serveren dør, mister du også backup
- Brug fjernlager: Google Drive, Dropbox, Amazon S3 eller lignende
- Test din backup regelmæssigt — en backup er kun god hvis den kan gendannes
- Hold mindst 3 versioner af backups (så du kan gå flere uger tilbage)
- Tag ALTID manuel backup før store ændringer (opdateringer, plugin-skift, tema-skift)
