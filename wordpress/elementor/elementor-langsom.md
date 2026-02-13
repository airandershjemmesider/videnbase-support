# Elementor editor er langsom eller crasher

## Problem

Elementor editoren loader langsomt, fryser eller crasher helt. Siden kan tage lang tid om at gemme, og widgets reagerer trægt.

## Løsning

### 1. Ryd Elementor cache

Gå til **Elementor → Tools → General** og klik:

- **Regenerate CSS & Data** — genopbygger alle Elementor stylesheets
- **Sync Library** — opdaterer template-biblioteket

### 2. Deaktivér ubrugte widgets

Gå til **Elementor → Settings → Features** og slå ubrugte widgets fra. Hver aktiv widget loader JavaScript og CSS, selv hvis den ikke bruges på siden.

### 3. Aktivér Improved Asset Loading

Gå til **Elementor → Settings → Features** (eller **Experiments**) og aktivér **Improved Asset Loading**. Dette loader kun CSS/JS for widgets der faktisk bruges på siden.

### 4. Tjek server resources

Disse PHP-indstillinger påvirker Elementor performance:

| Indstilling | Anbefalet minimum |
|-------------|-------------------|
| `memory_limit` | 256M (helst 512M) |
| `max_execution_time` | 300 |
| `upload_max_filesize` | 64M |
| `post_max_size` | 64M |

Tjek via **WordPress → Værktøjer → Webstedsintegritet** eller **Elementor → System Info**.

### 5. Opdatér Elementor og addons

Forældet software er en hyppig årsag til performance-problemer. Opdatér:

- Elementor (gratis)
- Elementor Pro
- Alle tredjeparts Elementor-addons

### 6. Tjek for plugin-konflikter

Deaktivér alle andre plugins midlertidigt og test om Elementor editoren bliver hurtigere. Aktivér plugins én ad gangen for at identificere konflikten.

Typiske syndere:

- Optimerings-plugins (Autoptimize, WP Rocket i editor-mode)
- Sikkerhedsplugins der scanner requests
- Andre page builders eller theme builders

### 7. Browser og hardware

- Ryd browser-cache og cookies
- Prøv i incognito-mode (udelukker browser-extensions)
- Brug Chrome eller Firefox (bedst understøttet)
- Luk unødvendige browser-tabs for at frigøre RAM

## Bemærkninger

- Sider med mange widgets (+50) vil altid være langsommere i editoren
- Overvej at opdele lange sider i sektioner med Elementor templates
- Hosting-kvalitet har stor betydning — shared hosting er ofte for langsomt
