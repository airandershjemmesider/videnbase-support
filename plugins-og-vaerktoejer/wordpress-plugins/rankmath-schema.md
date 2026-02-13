# RankMath Schema Markup

## Hvad er det

Schema markup (strukturerede data) er kode der hjælper Google med at forstå indholdet på hjemmesiden. Det kan resultere i "rich snippets" i søgeresultaterne — f.eks. stjerner, priser, FAQ-sektioner eller virksomhedsinfo direkte i Google.

RankMath tilføjer automatisk schema markup og giver mulighed for at tilpasse det per side.

## Automatisk schema

RankMath tilføjer automatisk schema baseret på indholdstypen:

| Indholdstype | Standard schema | Bruges til |
|--------------|----------------|------------|
| Blogindlæg | Article | Artikler og blogposts |
| Sider | WebPage | Almindelige undersider |
| Produkter | Product | WooCommerce produkter |
| Forside | WebSite + Organization | Virksomhedens hovedside |

### Konfigurér standard schema
1. Gå til **RankMath → Titles & Meta**
2. Vælg indholdstypen (Posts, Pages osv.)
3. Scroll ned til **Schema Type**
4. Vælg den ønskede standard schema-type

## LocalBusiness schema — vigtigt for lokale virksomheder

LocalBusiness schema er afgørende for virksomheder der betjener et lokalt område. Det viser virksomhedsinfo direkte i Google-søgninger.

### Opsætning
1. Gå til **RankMath → Titles & Meta → Local SEO**
2. Udfyld alle felter:
   - **Virksomhedsnavn** — præcist som det skal vises i Google
   - **Adresse** — fuld adresse med postnummer og by
   - **Telefonnummer** — med landekode (+45)
   - **Email** — kontakt-email
   - **Åbningstider** — udfyld for alle ugedage
   - **Logo** — virksomhedens logo
   - **Geo-koordinater** — latitude/longitude (find på Google Maps)

### NAP-konsistens
- **NAP** = Name, Address, Phone
- Virksomhedsinfo SKAL være identisk overalt: hjemmeside, Google Business Profile, Facebook, Krak osv.
- Selv små forskelle (f.eks. "Vej" vs "vej") kan forvirre Google

## Manuelt schema per side

For sider der kræver specifik schema:

1. Åbn siden/indlægget i WordPress editor
2. Scroll ned til **RankMath SEO → Schema**
3. Klik **Schema Generator**
4. Vælg schema-type:
   - **FAQ** — til FAQ-sider (vises som dropdown i Google)
   - **HowTo** — til trin-for-trin guides
   - **Event** — til begivenheder med dato og sted
   - **Recipe** — til opskrifter
   - **Video** — til sider med video
   - **Service** — til serviceydelser
5. Udfyld de relevante felter
6. Gem og opdatér siden

### FAQ schema — populær og effektiv
1. Vælg **FAQ** i Schema Generator
2. Tilføj spørgsmål og svar
3. Google viser spørgsmålene direkte i søgeresultaterne som dropdowns
4. Kan give markant mere plads i søgeresultaterne

## Test schema markup

### Google Rich Results Test
1. Gå til **search.google.com/test/rich-results**
2. Indsæt sidens URL
3. Klik **Test URL**
4. Tjek for fejl og advarsler
5. Gennemgå de detekterede schema-typer

### Schema Markup Validator
1. Gå til **validator.schema.org**
2. Indsæt URL eller kode
3. Giver mere detaljeret validering end Googles værktøj

### I RankMath selv
- Under **RankMath → Schema** kan du se en forhåndsvisning
- Brug **Code Preview** for at se den rå JSON-LD kode

## Fejlsøgning

### Schema vises ikke i Googles testværktøj
- Tjek at siden er offentligt tilgængelig (ikke password-beskyttet)
- Ryd cache og test igen
- Tjek at der ikke er konfliktende schema fra andre plugins eller temaet

### Rich snippets vises ikke i Google
- Google garanterer IKKE at rich snippets vises
- Det kan tage uger før Google henter og viser schema
- Sørg for at schema er korrekt og fejlfri
- Sider med lav autoritet får sjældnere rich snippets

### Konflikter med andre schema-plugins
- Deaktivér andre schema-plugins (Schema Pro, Yoast osv.)
- Dobbelt schema kan forvirre Google og give fejl
- Brug kun én kilde til schema markup

## Bemærkninger

- Schema markup er en SEO-fordel, men IKKE en ranking-faktor i sig selv
- Det vigtigste er korrekt og relevant schema — ikke mængden
- LocalBusiness schema er næsten et krav for lokale virksomheder
- FAQ schema kan øge CTR (click-through rate) markant
- Hold schema opdateret — forældede åbningstider eller priser er værre end ingen schema
- RankMath Pro tilbyder avancerede schema-typer og mulighed for at oprette custom schema
