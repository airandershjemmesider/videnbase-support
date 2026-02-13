# RankMath SEO Plugin — Fuld Opsætningsguide

## Hvad er RankMath

RankMath er et SEO-plugin til WordPress der samler alt SEO-arbejde ét sted: meta titles/descriptions, XML sitemaps, schema markup, 404-overvågning, redirects og SEO-analyse. Det erstatter behovet for flere separate plugins.

### Gratis vs Pro

| Funktion | Free | Pro |
|----------|------|-----|
| Focus keywords per side | 5 | Ubegrænset |
| Schema-typer | Grundlæggende (Article, LocalBusiness, FAQ, HowTo) | Alle typer + custom schema |
| Redirections | Grundlæggende | Avanceret med auto-detection |
| Google Analytics integration | Nej | Ja (direkte i dashboard) |
| Keyword rank tracking | Nej | Ja |
| Content AI (AI-forslag) | Begrænset | Fuld adgang |
| SEO email-rapporter | Nej | Ja |
| IndexNow (Instant Indexing) | Ja | Ja |

**Anbefaling:** Free dækker de fleste danske virksomhedssider. Pro er relevant for webshops og sider med mange redirects.

## Installation og Setup Wizard

1. **Plugins → Tilføj nyt** → søg "Rank Math SEO" → installér og aktivér
2. Opret gratis RankMath-konto (kræves for fuld funktionalitet)
3. Setup Wizard starter automatisk

### Easy vs Advanced Mode

- **Easy** — færre muligheder, hurtigere opsætning. Anbefales til simple kundesites
- **Advanced** — giver adgang til 404 Monitor, Redirections, Schema-tilpasning, Role Manager. Brug dette til professionelle opsætninger

**Tip:** Du kan altid skifte mellem Easy og Advanced under **RankMath → Dashboard → Modules**.

### Wizard-trin

1. **Site-information:** Vælg site-type (virksomhed, webshop, personlig), udfyld navn, logo, social media
2. **Search Console:** Forbind Google Search Console direkte (kræver Google-login)
3. **Sitemap:** XML Sitemap aktiveres automatisk — URL: `domæne.dk/sitemap_index.xml`
4. **Import:** Kan importere fra Yoast SEO, All in One SEO, SEOPress. Deaktivér og slet det gamle plugin bagefter

## Vigtige indstillinger efter Wizard

### Titles & Meta

- **RankMath → Titles & Meta → Global**
- Standard title-format: `%title% %sep% %sitename%`
- Separator: Vælg `|` eller `–` (kundepræference)
- **Posts/Pages:** Tilpas standard meta description-skabelon
- **Noindex disse:** Tagarkiver, forfatterarkiver, datoarkiver, mediebilag — medmindre de har SEO-værdi

### Sitemap Settings

- **RankMath → Sitemap Settings**
- Inkludér: Sider, indlæg, produkter (WooCommerce)
- Ekskludér: Tags, forfattere, mediefiler
- Indsend sitemap i Google Search Console efter opsætning
- Ping søgemaskiner: Aktivér (sender automatisk besked ved nye sider)

### 404 Monitor (Advanced mode)

- **RankMath → 404 Monitor**
- Logger alle 404-fejl besøgende rammer
- Brug til at identificere døde links og oprette redirects
- Ryd loggen jævnligt for at holde den overskuelig

### Redirections (Advanced mode)

- **RankMath → Redirections**
- Opret 301-redirects (permanent) for slettede/flyttede sider
- Aktivér auto-redirect: Fanger URL-ændringer og opretter redirect automatisk
- Importér redirects fra .htaccess eller Redirection-plugin

## Focus Keyword Optimering

RankMath Free giver op til 5 focus keywords per side/indlæg. Brug dem strategisk:

1. **Primært keyword** i det første felt — dette er dit vigtigste søgeord
2. **Sekundære keywords** i felt 2-5 — variationer og relaterede søgeord
3. RankMath tjekker hvert keyword mod:
   - Title tag og meta description
   - URL (slug)
   - Første afsnit af brødteksten
   - Underoverskrifter (H2/H3)
   - Alt-tekst på billeder
   - Keyword-densitet (sigter mod 1-1,5%)

**Vigtigt:** Skriv naturligt for mennesker, IKKE for pluginet. En grøn score med unaturlig tekst er værdiløs.

## SEO Score

| Score | Farve | Handling |
|-------|-------|----------|
| 0-50 | Rød | Mangler grundlæggende SEO — tilføj keyword i titel, meta, brødtekst |
| 51-80 | Orange | Grundlaget er på plads — optimer detaljer (billeder, links, længde) |
| 81-100 | Grøn | God optimering — publicér med god samvittighed |

Scoren er en rettesnor. Den garanterer IKKE ranking. God SEO kræver også godt indhold, teknisk hastighed og backlinks.

## Google Search Console Integration

1. **RankMath → General Settings → Search Console**
2. Klik **Connect Google Account** og godkend adgang
3. Vælg den korrekte Search Console property
4. Efter forbindelse kan du se direkte i WordPress:
   - Søgeord der driver trafik
   - Sidevisninger og klik
   - Gennemsnitlig position per keyword
   - Crawl-fejl og dækningsproblemer

## Schema Markup

RankMath håndterer schema automatisk, men du kan tilpasse per side. De vigtigste typer:

| Schema-type | Bruges til | Rich snippet i Google |
|-------------|------------|----------------------|
| LocalBusiness | Lokale virksomheder | Virksomhedsinfo, åbningstider, kort |
| Article | Blogindlæg og artikler | Forfatter, dato, billede |
| FAQ | FAQ-sider | Dropdown-spørgsmål i søgeresultat |
| HowTo | Trin-for-trin guides | Trinvis visning med billeder |

Se separat detaljeret guide: `rankmath-schema.md`

## Instant Indexing (IndexNow)

RankMath integrerer med IndexNow-protokollen der sender nye/opdaterede sider direkte til Bing og Yandex:

1. **RankMath → Instant Indexing**
2. Aktivér IndexNow
3. API-nøgle genereres automatisk
4. Nye og opdaterede sider sendes automatisk til søgemaskiner
5. Google understøtter ikke IndexNow direkte endnu, men Bing og Yandex gør

## SEO Analysis Tool

- **RankMath → SEO Analysis**
- Scanner hele sitet for SEO-problemer
- Tjekker: Meta tags, links, billeder, hastighed, mobilvenlighed
- Giver en samlet SEO-score for hele sitet
- Kør analysen efter opsætning og derefter månedligt

## Hurtig tjekliste for ny-site opsætning

- [ ] Installér og kør Setup Wizard (Advanced mode)
- [ ] Forbind Google Search Console
- [ ] Konfigurér Titles & Meta (noindex på irrelevante arkiver)
- [ ] Aktivér og indsend XML Sitemap
- [ ] Opsæt LocalBusiness schema (lokal virksomhed)
- [ ] Aktivér 404 Monitor og Redirections
- [ ] Aktivér Instant Indexing (IndexNow)
- [ ] Kør SEO Analysis og ret fundne fejl
- [ ] Sæt focus keyword på alle vigtige sider
- [ ] Test schema med Googles Rich Results Test
- [ ] Deaktivér evt. gammelt SEO-plugin efter import

## Typiske fejl og løsninger

### Redirect loops (side omdirigerer i ring)
- Tjek **RankMath → Redirections** for cirkulære redirects (A → B → A)
- Tjek også .htaccess og andre redirect-plugins for konflikter
- Deaktivér RankMath-redirects midlertidigt for at isolere problemet

### Duplicate schema markup
- Kun ét plugin bør levere schema. Deaktivér schema fra Yoast, temaet eller andre plugins
- Brug Googles Rich Results Test til at identificere duplikater
- Tjek temaets kode for hardcodede schema-tags

### Sitemap giver 404
1. **Indstillinger → Permalinks** → klik Gem (genopbygger rewrite-regler)
2. Tjek at sitemap er aktiveret under RankMath → Sitemap Settings
3. Tjek for konflikter med andre sitemap-plugins

### SEO-score vises ikke i editor
- Tjek at RankMath-metaboksen er synlig (Screen Options øverst i editoren)
- I Gutenberg: Klik RankMath-ikonet i sidebar
- Ryd browser-cache og prøv igen

### Google viser ikke din meta description
- Google vælger selv om den bruger din meta description — det er forventet
- Ændringer kan tage dage til uger at slå igennem
- Brug Search Console → URL-inspektion → Anmod om indeksering for at fremskynde
