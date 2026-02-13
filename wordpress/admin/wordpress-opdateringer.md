# Opdatér WordPress, plugins og temaer sikkert

## Problem

WordPress, plugins og temaer skal holdes opdateret for at undgå sikkerhedshuller og kompatibilitetsproblemer. Men opdateringer kan også give fejl hvis de gøres forkert.

## Løsning

### Før du opdaterer

1. **Tag backup** — Brug et backup-plugin (fx UpdraftPlus) eller tag backup via hosting-panelet
2. **Tjek kompatibilitet** — Læs changelogs og tjek at plugins er kompatible med den nye WordPress-version
3. **Opdatér på et tidspunkt med lav trafik** — Undgå opdateringer midt på dagen

### Rækkefølge for opdateringer

1. **Plugins først** — Opdatér alle plugins én ad gangen
2. **Temaer derefter** — Opdatér aktive og inaktive temaer
3. **WordPress core til sidst** — Opdatér selve WordPress

### Trin-for-trin

1. Gå til **Dashboard → Opdateringer**
2. Vælg ét plugin ad gangen og klik **Opdatér**
3. Tjek at sitet stadig virker efter hvert plugin
4. Gentag for temaer
5. Opdatér WordPress core når alt andet er opdateret
6. Ryd cache (hvis du bruger cache-plugin)

### Automatiske opdateringer

WordPress opdaterer automatisk minor-versioner (fx 6.4.1 → 6.4.2). For at styre dette:

- **Dashboard → Opdateringer** — Slå automatiske opdateringer til/fra per plugin
- Tilføj i `wp-config.php` for at deaktivere al auto-opdatering:
  ```php
  define('AUTOMATIC_UPDATER_DISABLED', true);
  ```
- Kun auto-opdatér minor core-versioner (standard):
  ```php
  define('WP_AUTO_UPDATE_CORE', 'minor');
  ```

### Hvis en opdatering fejler

1. Ryd browsercache og prøv igen
2. Deaktivér cache-plugin midlertidigt
3. Opdatér manuelt via FTP (download plugin fra wordpress.org, upload til `/wp-content/plugins/`)
4. Tjek at PHP-versionen er kompatibel (de fleste plugins kræver PHP 7.4+)

## Bemærkninger

- Tag ALTID backup før opdateringer — der er ingen fortryd-knap
- Staging-miljø er ideelt til at teste opdateringer først (mange hosts tilbyder dette)
- Undgå at opdatere 10+ plugins på én gang — gør det trinvist så du kan spotte problemet
- Hvis sitet crasher efter opdatering, se fejlsøgning af plugin-konflikter
