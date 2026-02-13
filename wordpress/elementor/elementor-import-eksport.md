# Import og eksport af Elementor templates

## Problem

Du skal flytte Elementor templates mellem sites, importere andres templates, eller eksportere hele dit site-kit.

## Løsning

### Eksportér en enkelt template

1. Gå til **Elementor → My Templates** (eller **Templates → Saved Templates**)
2. Find den template du vil eksportere
3. Klik på de tre prikker (**...**) til højre for templaten
4. Vælg **Export**
5. En `.json`-fil downloades til din computer

### Importér en template

1. Gå til **Elementor → My Templates**
2. Klik **Import Templates** øverst
3. Vælg `.json`-filen fra din computer
4. Templaten er nu tilgængelig i dit bibliotek

### Eksportér hele site-kit (Elementor Pro)

Et site-kit inkluderer templates, site settings, og globale indstillinger:

1. Gå til **Elementor → Tools → Import / Export**
2. Klik **Export**
3. Vælg hvad der skal inkluderes (templates, content, site settings)
4. Klik **Export** — en `.zip`-fil downloades

### Importér site-kit

1. Gå til **Elementor → Tools → Import / Export**
2. Klik **Import**
3. Upload `.zip`-filen
4. Vælg hvad der skal importeres
5. Klik **Import** og vent til processen er færdig

### "Sorry, you are not allowed to import this file type"

Denne fejl skyldes at WordPress blokerer upload af JSON-filer:

**Løsning 1:** Tilføj til `wp-config.php`:
```php
define('ALLOW_UNFILTERED_UPLOADS', true);
```
Importér templaten, og **fjern linjen igen** bagefter af sikkerhedshensyn.

**Løsning 2:** Brug et plugin som **WP Extra File Types** til at tillade JSON-uploads.

### Billeder i eksport

- Billeder inkluderes automatisk i `.zip`-eksporter (site-kit)
- Enkelte `.json`-templates refererer til billede-URLs — billederne skal eksistere på det nye site
- Hvis billeder mangler efter import: tjek at de originale billede-URLs er tilgængelige

## Bemærkninger

- Templates eksporteret fra Elementor Pro kan kun fuldt bruges på sites med Elementor Pro
- Global Fonts og Global Colors følger med i site-kit eksport
- Ved import til et site med eksisterende indhold: vælg om du vil overskrive eller flette
- Store site-kits kan tage lang tid at importere — øg PHP `max_execution_time` hvis nødvendigt
