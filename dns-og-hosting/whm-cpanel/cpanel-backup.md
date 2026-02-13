# Backup i cPanel

## Hvad er det

cPanel tilbyder backup af filer, databaser og email-konfiguration. Full backups kan kun gendannes via WHM, mens partial backups kan gendannes direkte i cPanel.

## Full Backup (komplet konto)

### Download full backup

1. Log ind på cPanel
2. Gå til **Files → Backup**
3. Klik **Download a Full Account Backup**
4. Vælg destination:
   - **Home Directory** — gem på serveren (under `/home/brugernavn/`)
   - **Remote FTP Server** — send til ekstern server
   - **SCP** — send via sikker kopi
5. Klik **Generate Backup**
6. Du får en email når backuppen er klar til download

### Gendannelse af full backup
- Kræver **WHM-adgang** (root eller reseller)
- WHM → **Backup → Restore a Full Backup/cpmove File**
- Upload backup-filen og vælg gendannelsesindstillinger

## Partial Backup (enkeltdele)

### Download partial backups

Under **Files → Backup** kan du downloade separat:

- **Home Directory** — alle filer (public_html, emails, indstillinger)
- **MySQL Databases** — hver database som SQL-dump
- **Email Forwarders & Filters** — email-konfiguration

### Gendannelse af partial backups

- **Filer:** Upload via File Manager til den korrekte mappe, eller brug **Restore a Home Directory Backup**
- **Database:** Gå til **phpMyAdmin → Import → Vælg SQL-fil → Klik Go**
- **Email:** Upload via **Restore Email Forwarders/Filters** i Backup-sektionen

## Automatisk backup (WHM)

Opsættes af serveradministrator i WHM:

1. WHM → **Backup → Backup Configuration**
2. Aktivér backup og vælg:
   - **Frekvens:** Daglig, ugentlig, månedlig
   - **Retention:** Hvor mange backups der gemmes
   - **Backup-type:** Compressed (tar.gz) eller uncompressed
   - **Destination:** Lokal, remote FTP, Amazon S3, Google Drive (med plugin)
3. Vælg hvilke konti der skal inkluderes/ekskluderes

## JetBackup (populær addon)

Mange hosting-udbydere bruger JetBackup som WHM-addon:

- **Point-in-time restore** — gendannelse til et specifikt tidspunkt
- **Granulær restore** — gendannelse af individuelle filer, mapper, databaser eller email-konti
- Tilgængelig direkte i cPanel for slutbrugeren
- Klik på filen/databasen → vælg backup-dato → klik Restore

### JetBackup i cPanel
1. Gå til **Files → JetBackup** (hvis installeret)
2. Vælg kategori: Files, Databases, Emails, DNS Zones
3. Vælg backup-dato
4. Vælg hvad der skal gendannes
5. Klik **Restore**

## Bemærkninger

- Lav ALTID backup før større ændringer (WordPress-opdatering, plugin-installation, server-migrering)
- Full backups kan være store — tjek diskplads før generering
- cPanel-backups inkluderer IKKE server-konfiguration (Apache, PHP, WHM-indstillinger)
- Opbevar backups eksternt (ikke kun på serveren) — beskytter mod serverfejl
- Automatisk backup bør køre natligt for at minimere server-belastning
