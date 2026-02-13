# Problemer ved opdatering af Elementor

## Problem

Opdatering af Elementor eller Elementor Pro fejler, giver hvid skærm, eller bryder sitet.

## Løsning

### ALTID tag backup FØR opdatering

Før enhver Elementor-opdatering:

1. Tag fuld backup (filer + database) via dit backup-plugin eller hosting-panel
2. Test opdateringen på et staging-site først hvis muligt
3. Notér den nuværende versionsnummer så du kan rulle tilbage

### Hvid skærm efter opdatering (White Screen of Death)

1. **Via FTP/filhåndtering:** Gå til `wp-content/plugins/`
2. Omdøb mappen `elementor` til `elementor-disabled`
3. Omdøb mappen `elementor-pro` til `elementor-pro-disabled` (hvis relevant)
4. Log ind i WordPress — sitet skulle nu loade
5. Enten: opdatér Elementor manuelt, eller geninstallér den forrige version

### "Failed to update plugin"

Typiske årsager og løsninger:

| Årsag | Løsning |
|-------|---------|
| Manglende filrettigheder | Sæt `wp-content/plugins/` til 755, filer til 644 |
| Ikke nok diskplads | Ryd op i gamle backups, logs, eller ubrugte uploads |
| PHP memory limit | Øg `memory_limit` i php.ini til mindst 256M |
| Timeout under download | Øg `max_execution_time` til 300 |

### Rollback til tidligere version

**Metode 1: WP Rollback plugin**

1. Installér plugin'et **WP Rollback**
2. Gå til **Plugins → Installed Plugins**
3. Klik **Rollback** ved siden af Elementor
4. Vælg den ønskede version og klik **Rollback**

**Metode 2: Manuelt via FTP**

1. Download den ønskede version fra wordpress.org/plugins/elementor/advanced/
2. Slet mappen `wp-content/plugins/elementor/` via FTP
3. Upload den downloadede version til `wp-content/plugins/`
4. Aktivér pluginet i WordPress

For Elementor Pro: download fra my.elementor.com → Previous Versions.

### Opdatering hænger eller stopper

1. Gå til `wp-content/` og slet `.maintenance`-filen hvis den findes
2. Prøv opdateringen igen
3. Hvis det gentager sig, opdatér manuelt via FTP

## Bemærkninger

- Opdatér altid i rækkefølgen: WordPress → Elementor (gratis) → Elementor Pro → Addons
- Major Elementor-versioner (fx 3.x → 4.x) har større risiko for breaking changes
- Hold altid en fungerende backup tilgængelig i mindst 7 dage efter opdatering
- Tjek Elementor changelogs før opdatering for kendte problemer
