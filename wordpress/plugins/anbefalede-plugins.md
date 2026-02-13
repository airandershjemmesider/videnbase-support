# Anbefalede plugins til sikkerhed, ydeevne og backup

## Problem

Der findes over 60.000 WordPress-plugins. Det kan være svært at vælge de rigtige, og for mange plugins gør sitet langsomt og usikkert.

## Løsning

### Sikkerhed

| Plugin | Formål | Gratis/Premium |
|--------|--------|----------------|
| **Wordfence Security** | Firewall, malware-scanning, login-beskyttelse | Gratis (premium tilgængelig) |
| **Sucuri Security** | Sikkerhedsovervågning, firewall | Gratis (premium tilgængelig) |
| **Limit Login Attempts Reloaded** | Begrænser login-forsøg mod brute force | Gratis |
| **Two Factor Authentication** | 2FA til login | Gratis |

**Anbefaling:** Wordfence til de fleste sites. Let at opsætte og god gratis version.

### Ydeevne og cache

| Plugin | Formål | Gratis/Premium |
|--------|--------|----------------|
| **WP Super Cache** | Side-caching (simpelt) | Gratis |
| **W3 Total Cache** | Avanceret caching (mange indstillinger) | Gratis |
| **LiteSpeed Cache** | Cache for LiteSpeed-servere | Gratis |
| **ShortPixel** | Billedkomprimering | Gratis (begrænset) |
| **Autoptimize** | Minificér CSS/JS | Gratis |

**Anbefaling:** Brug den cache-plugin din host anbefaler. LiteSpeed Cache hvis du er på LiteSpeed-server. Ellers WP Super Cache for enkelhed.

### Backup

| Plugin | Formål | Gratis/Premium |
|--------|--------|----------------|
| **UpdraftPlus** | Komplet backup til cloud | Gratis (premium tilgængelig) |
| **All-in-One WP Migration** | Eksportér/importér hele sitet | Gratis (størrelsesbegrænset) |
| **Duplicator** | Site-migrering og backup | Gratis |

**Anbefaling:** UpdraftPlus til løbende backup. All-in-One WP Migration til flytning af sites.

### SEO

| Plugin | Formål | Gratis/Premium |
|--------|--------|----------------|
| **Yoast SEO** | On-page SEO, sitemaps, meta-tags | Gratis (premium tilgængelig) |
| **Rank Math** | Alternativ til Yoast, flere gratis funktioner | Gratis (premium tilgængelig) |

**Anbefaling:** Vælg ét SEO-plugin — ALDRIG begge på samme tid.

### Anti-spam

| Plugin | Formål | Gratis/Premium |
|--------|--------|----------------|
| **Antispam Bee** | Spam-beskyttelse for kommentarer (GDPR-venlig) | Gratis |
| **Akismet** | Spam-filtrering (kræver API-nøgle) | Gratis for personlige sites |

### Vedligeholdelse

| Plugin | Formål | Gratis/Premium |
|--------|--------|----------------|
| **WP-Optimize** | Ryd database, komprimér billeder | Gratis |
| **Health Check** | Fejlsøgning og site-sundhed | Gratis |

### Vigtige regler for plugins

1. **Mindre er mere** — installér kun det du har brug for (10-15 plugins er normalt)
2. **Slet deaktiverede plugins** — de er en sikkerhedsrisiko
3. **Tjek anmeldelser og opdateringer** — vælg plugins der opdateres regelmæssigt
4. **Undgå duplikater** — aldrig to plugins med samme funktion
5. **Test først** — installér på staging hvis muligt

## Bemærkninger

- Premium-versioner er sjældent nødvendige for små til mellemstore sites
- Din hosting kan allerede tilbyde caching og backup — tjek før du installerer plugins
- Fjern altid "Hello Dolly" og "Akismet" hvis du ikke bruger dem
- Hold plugins opdaterede — sårbare plugins er den mest gængse hackingmetode
