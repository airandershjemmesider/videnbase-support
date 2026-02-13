# Backup-strategi for hjemmesider

## Problem

Du har brug for en pålidelig backup-strategi så du kan gendanne din hjemmeside hvis noget går galt — hack, fejl, mistet data eller hostingproblemer.

## Løsning

### De tre backup-niveauer

En god backup-strategi har **mindst 2 uafhængige backup-metoder:**

#### 1. Hosting-backup (automatisk)
- De fleste hosting-udbydere laver daglige backups
- Tjek: Hvor mange dage gemmes backups? Kan du gendanne selv?
- **Stol ALDRIG kun på hosting-backup** — den forsvinder hvis du mister kontoen

#### 2. Plugin-backup (WordPress)
- Automatisk backup via plugin til ekstern lagring
- Anbefalede plugins:
  - **UpdraftPlus** (gratis + premium) — Backup til Google Drive, Dropbox, S3
  - **BlogVault** (betalt) — Inkrementelle backups, staging, nem gendannelse
  - **All-in-One WP Migration** (manuel) — Nem eksport/import

#### 3. Ekstern backup (offsite)
- Kopier backups til et helt andet sted end din hosting
- Muligheder: Google Drive, Dropbox, Amazon S3, lokal computer
- **Kritisk:** Backups på samme server som sitet beskytter IKKE mod server-fejl

### Opsæt automatisk backup (WordPress + UpdraftPlus)

1. Installer og aktivér **UpdraftPlus** i WordPress
2. Gå til Indstillinger → UpdraftPlus Backups
3. Under "Settings":
   - **Files backup schedule:** Dagligt, behold 14 kopier
   - **Database backup schedule:** Dagligt, behold 30 kopier
4. Vælg **fjernlagring** (Google Drive, Dropbox eller lignende)
5. Forbind til din lagringskonto
6. Klik "Save Changes"
7. Kør en test-backup og verificer at filen dukker op i fjernlagringen

### Backup-skema anbefaling

| Type | Hyppighed | Opbevaring | Sted |
|------|-----------|------------|------|
| Database | Dagligt | 30 dage | Ekstern (Cloud) |
| Filer | Dagligt eller ugentligt | 14 dage | Ekstern (Cloud) |
| Fuld site | Ugentligt | 4 uger | Ekstern (Cloud) |
| Manuel fuld backup | Før store ændringer | Permanent | Lokal + Cloud |

### Hvornår skal du tage manuel backup?

Tag ALTID manuel backup **inden:**
- WordPress core-opdatering
- Plugin- eller tema-opdateringer
- Store indholdsændringer
- Designændringer
- Flytning af hosting
- Ændringer i wp-config.php eller .htaccess

### Test dine backups

Backups er værdiløse hvis du ikke kan gendanne dem.

1. **Månedligt:** Verificer at backup-filer rent faktisk ligger i fjernlagringen
2. **Kvartalsvist:** Test en fuld gendannelse på en staging-server eller lokalt
3. **Tjek filstørrelser:** Hvis backup-filen pludselig er meget mindre, er noget galt

## Gendannelse

### Via UpdraftPlus
1. Gå til UpdraftPlus → "Existing Backups"
2. Vælg den backup du vil gendanne
3. Klik "Restore" og vælg hvad der skal gendannes (filer, database, eller begge)

### Manuel gendannelse
1. Upload filer via FTP
2. Importér database via phpMyAdmin
3. Opdater wp-config.php hvis database-oplysninger er ændret

## Bemærkninger

- **3-2-1 reglen:** 3 kopier af data, på 2 forskellige medier, 1 offsite
- **Hosting-backup alene er IKKE nok** — du har ingen kontrol over den
- **Test gendannelse** — en backup du ikke kan gendanne er ingen backup
- Gem **login-oplysninger til backup-lagring** et sikkert sted (password manager)
- For webshops: Overvej backup før HVER ordre-relateret ændring
- Database-backups er små og billige — tag dem dagligt
