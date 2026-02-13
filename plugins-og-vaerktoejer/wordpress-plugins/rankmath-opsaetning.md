# RankMath SEO Plugin — Opsætning

## Hvad er det

RankMath er et SEO-plugin til WordPress der håndterer meta titles og descriptions, XML sitemaps, schema markup og SEO-analyse. Det giver en SEO-score per side/indlæg og hjælper med at optimere indholdet til søgemaskiner.

## Installation

1. Gå til **Plugins → Tilføj nyt**
2. Søg efter "Rank Math SEO"
3. Installér og aktivér pluginet
4. Opret en gratis RankMath-konto (kræves for fuld funktionalitet)

## Setup Wizard

### Trin 1: Vælg profil
- **Easy** — grundlæggende indstillinger (anbefalet til de fleste)
- **Advanced** — flere muligheder (for erfarne brugere)
- **Custom** — fuld kontrol over alle indstillinger

### Trin 2: Site-information
- Angiv site-type: Personlig blog, virksomhed, webshop osv.
- Udfyld virksomhedsnavn og logo
- Angiv social media profiler (Facebook, Instagram osv.)

### Trin 3: Import fra andet SEO-plugin
- Hvis kunden brugte Yoast SEO før, kan RankMath importere alle data
- Vælg **Yoast SEO** og klik Import
- Verificér at meta titles/descriptions er korrekt overført
- Deaktivér og slet Yoast efter vellykket import

### Trin 4: Sitemap
- XML Sitemap aktiveres automatisk
- Sitemap URL: `domæne.dk/sitemap_index.xml`
- Indsend sitemap i Google Search Console

## Vigtige indstillinger

### Titles & Meta
- **Gå til RankMath → Titles & Meta**
- Sæt standard title-format for indlæg og sider
- Anbefalet format: `%title% %sep% %sitename%`
- Tilpas meta description-skabeloner
- Sæt noindex på arkivsider, tags og forfattersider (hvis ikke relevante)

### Sitemap
- **RankMath → Sitemap Settings**
- Inkludér: Sider, indlæg, produkter (WooCommerce)
- Ekskludér: Tags, forfatterarkiver, mediefiler
- Maks antal URL'er per sitemap: 200 (standard er fint)

### Schema
- **RankMath → Titles & Meta → Posts/Pages**
- Vælg standard schema-type per indholdstype
- Se separat guide: `rankmath-schema.md`

### Redirects (Pro)
- **RankMath → Redirections**
- Opret 301-redirects for slettede/flyttede sider
- Aktivér automatisk redirect-overvågning for 404-fejl
- Importér redirects fra .htaccess eller andre plugins

## SEO Score — hvad betyder det

RankMath giver en SEO-score fra 0-100 per side/indlæg:

| Score | Farve | Betydning |
|-------|-------|-----------|
| 0-50 | Rød | Dårlig SEO — flere forbedringer nødvendige |
| 51-80 | Orange | Okay SEO — kan forbedres |
| 81-100 | Grøn | God SEO — de vigtigste ting er på plads |

**Vigtig note:** Scoren er en rettesnor, IKKE en garanti for ranking. En score på 100 betyder ikke automatisk førstepladsen i Google.

## Focus Keyword — korrekt brug

1. Vælg ét primært keyword per side/indlæg
2. Skriv keywordet i **Focus Keyword**-feltet i RankMath-boksen
3. RankMath tjekker om keywordet bruges i:
   - Titel (H1)
   - Meta title og meta description
   - URL (slug)
   - Første afsnit
   - Underoverskrifter (H2/H3)
   - Alt-tekst på billeder
4. Følg anbefalingerne — men skriv naturligt, ikke kun for pluginet

## Fejlsøgning

### Sitemap giver 404-fejl
1. Gå til **Indstillinger → Permalinks** og klik **Gem ændringer** (uden at ændre noget)
2. Dette genopbygger rewrite-reglerne
3. Tjek at sitemap er aktiveret under **RankMath → Sitemap Settings**

### Meta titles/descriptions vises ikke i Google
- Google vælger selv om den bruger din meta description
- Det kan tage dage/uger før ændringer vises i søgeresultaterne
- Brug Google Search Console → URL-inspektion → Anmod om indeksering

### RankMath konflikter med andet plugin
- Deaktivér andre SEO-plugins (Yoast, All in One SEO)
- Kun ét SEO-plugin bør være aktivt ad gangen
- Tjek for JavaScript-fejl i browser console

## Bemærkninger

- RankMath Free dækker de fleste behov for danske virksomhedssider
- RankMath Pro tilføjer: Redirect Manager, Advanced Schema, Google Analytics integration
- Opdatér pluginet regelmæssigt for at følge Googles ændringer
- Brug altid Google Search Console sammen med RankMath for det fulde billede
