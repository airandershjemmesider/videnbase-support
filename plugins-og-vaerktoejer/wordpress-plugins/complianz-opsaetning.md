# Complianz GDPR Cookie Consent — Fuld Opsætningsguide

## Hvad er Complianz

Complianz er et GDPR/ePrivacy cookie-consent plugin til WordPress. Det scanner hjemmesiden for cookies, viser en cookie-banner, blokerer scripts indtil samtykke og genererer en cookie-politik. Det er det foretrukne valg til danske/EU-sites fordi det håndterer dansk lovgivning korrekt ud af boksen.

### Hvorfor Complianz

- Automatisk cookie-scanning (opdager de fleste 3. parts-cookies)
- Blokerer scripts automatisk (GA4, Meta Pixel, YouTube osv.) indtil samtykke
- Google Consent Mode v2 integration (krav for EU-annoncører)
- Dansk sprog og EU-region som standard
- Genererer cookie-politik automatisk
- Gratis version dækker de fleste behov

## Installation og Wizard

1. **Plugins → Tilføj nyt** → søg "Complianz" → installér **Complianz – GDPR/CCPA Cookie Consent**
2. Aktivér pluginet
3. Gå til **Complianz → Wizard**

### Wizard trin-for-trin

**Trin 1 — Generelt:**
- Region: **Europe (EU)**
- Virksomhedens land: **Denmark**
- Udfyld virksomhedsnavn og kontaktinfo

**Trin 2 — Cookies:**
- Klik **Start Scan** — Complianz scanner alle sider for cookies og scripts
- Gennemgå resultaterne og kategorisér ukendte cookies
- Re-scan er nødvendig efter enhver ny plugin-installation

**Trin 3 — Consent:**
- Vælg opt-in (påkrævet i EU — besøgende skal aktivt acceptere)
- Konfigurér hvilke consent-kategorier der skal vises

**Trin 4 — Cookie Policy:**
- Complianz genererer en cookie-politik automatisk
- Gennemgå og tilpas teksten til virksomheden
- Vælg en eksisterende side eller lad Complianz oprette en ny

## Cookie Scanner

Scanneren crawler hjemmesiden og identificerer alle cookies og scripts fra tredjeparter.

### Sådan virker det
- Complianz besøger siderne som en browser og registrerer hvilke cookies der sættes
- Kendte tjenester (GA4, YouTube, Facebook osv.) genkendes automatisk
- Ukendte cookies skal kategoriseres manuelt

### Hvornår skal du re-scanne
- Efter installation af nyt plugin
- Efter tilføjelse af nye scripts (GTM tags, custom kode)
- Efter ændring af tema
- Mindst én gang om måneden som vedligeholdelse

## Cookie Banner Opsætning

### Dansk tekst
- **Complianz → Cookie Banner → Texts**
- Standardtekster er på engelsk — skift til dansk
- Anbefalet bannertekst: Kort og klar. F.eks. "Vi bruger cookies til at forbedre din oplevelse. Vælg hvilke cookies du vil tillade."
- Knaptekster: "Acceptér alle", "Kun nødvendige", "Indstillinger"

### Design og placering
- **Complianz → Cookie Banner → Design**
- Vælg position: Bund (banner), center (popup), eller top
- Tilpas farver til kundens branding (baggrund, tekst, knapper)
- Primær-knap ("Acceptér alle") bør have en fremhævet farve
- Test på både desktop og mobil — banneret skal være læsbart og klikbart

### Consent-kategorier

| Kategori | Beskrivelse | Eksempler | Kan afvises? |
|----------|-------------|-----------|-------------|
| Funktionel | Nødvendige for sidens drift | WordPress sessions, WooCommerce kurv | Nej (altid aktiv) |
| Statistik | Anonymiseret tracking | Google Analytics, Hotjar | Ja |
| Marketing | Annoncering og retargeting | Meta Pixel, Google Ads remarketing | Ja |
| Præferencer | Brugertilpasning | Sprogvalg, dark mode | Ja |

## Integration med Google Analytics

Complianz blokerer automatisk GA4-cookies indtil besøgende giver samtykke:

1. **Complianz → Integrations** → find Google Analytics
2. Aktivér integrationen
3. Complianz genkender gtag.js og blokerer det automatisk
4. Når brugeren accepterer "Statistik"-kategorien, indlæses GA4
5. Aktivér **Google Consent Mode v2** for modelleret data (se `complianz-consent-mode.md`)

## Integration med Google Tag Manager

GTM kræver lidt mere opmærksomhed fordi scripts indlæses via GTM-containeren:

1. **Complianz → Integrations** → aktivér Google Tag Manager
2. Vælg metode:
   - **Consent Mode via GTM** (anbefalet) — GTM-containeren indlæses altid, men tags respekterer consent-signaler
   - **Blokér hele GTM** — containeren blokeres helt indtil samtykke (enklere men mister consent-less pings)
3. I GTM: Sørg for at alle tags har korrekte consent-indstillinger
4. Se detaljer i `complianz-consent-mode.md` og `complianz-script-blocking.md`

## Integration med Facebook/Meta Pixel

1. **Complianz → Integrations** → find Meta Pixel / Facebook
2. Aktivér integrationen
3. Complianz blokerer pixelen automatisk indtil "Marketing"-samtykke
4. Standard-pixelen fanges automatisk — custom events via manuel kode skal tilføjes i Script Center
5. Test i Meta Events Manager at events kun fyrer efter samtykke

## Cookie Policy Side

- Complianz genererer en cookie-erklæring automatisk med alle fundne cookies
- Siden opdateres automatisk når du re-scanner
- Link til cookie-policyen fra:
  - Footer (navigations-link)
  - Cookie-banneret (link i teksten)
  - Privatlivspolitik-siden

## Geo-restriction

- **Complianz → Settings → Regions**
- EU-besøgende: Fuld opt-in banner (påkrævet af GDPR)
- USA: Kan konfigureres som opt-out (CCPA)
- Resten af verden: Vælg mellem opt-in, opt-out eller ingen banner
- Geo-detection bruger IP-adresse til at bestemme region
- **Bemærk:** Caching kan påvirke geo-detection — se afsnittet om LiteSpeed Cache herunder

## A/B Testing af Cookie Banner (Pro)

Complianz Pro kan teste forskellige banner-designs mod hinanden:

- Test farver, tekst, placering og knap-layout
- Måler accept-rate per variant
- Hjælper med at optimere samtykke-raten uden at bryde GDPR
- Kræver Complianz Premium-licens

## Complianz + LiteSpeed Cache

LiteSpeed Cache kan skabe problemer med cookie-banneret hvis caching er for aggressiv:

### Problem
- Cached sider viser ikke banneret korrekt
- Consent gemmes ikke fordi siden serveres fra cache
- Geo-restriction virker ikke (alle får samme cachede version)

### Løsning
1. **LiteSpeed Cache → Cache → Excludes**
2. Tilføj Complianz-cookies til "Do Not Cache Cookies": `cmplz_consent_status`, `cmplz_policy_id`
3. Aktivér **ESI (Edge Side Includes)** hvis LiteSpeed-serveren understøtter det
4. Alternativt: Brug Complianz' JavaScript-baserede banner (standard) som ikke påvirkes af page cache
5. Test i inkognito-vindue at banneret vises og gemmer samtykke korrekt

## Typiske problemer og løsninger

### Scripts blokeres ikke korrekt
1. Kør en ny cookie-scan
2. Tjek at scripts er registreret under **Complianz → Integrations**
3. Custom scripts i Elementor HTML-widgets fanges IKKE automatisk — tilføj dem i Script Center
4. Test med browser DevTools → Network tab: Tjek om scripts indlæses før samtykke

### Consent registreres ikke (banner vises hver gang)
1. Ryd al cache: LiteSpeed, CDN, browser
2. Tjek at Complianz-cookies ikke er på en blokerings-liste
3. Test i inkognito — hvis det virker der, er det et cache-problem
4. Tjek at "Acceptér"-knappen er synlig og klikbar på mobil

### Banner vises ikke overhovedet
1. Tjek at banneret er aktiveret under **Complianz → Cookie Banner**
2. Ryd cache (alle lag)
3. Admins ser ikke banneret som standard — test i inkognito eller udlogget
4. Tjek for JavaScript-fejl i browser console der kan blokere banneret

### Cookie scanner finder ingen cookies
- Sørg for at sitet har indhold med embeds, tracking-scripts osv.
- Et tomt site uden 3. parts-scripts vil naturligt have få cookies
- Tilføj Google Analytics, YouTube embeds osv. før du scanner

## Hurtig tjekliste for ny-site opsætning

- [ ] Installér Complianz og kør Wizard (EU region, dansk)
- [ ] Kør cookie scanner og gennemgå resultater
- [ ] Konfigurér banner: Dansk tekst, kundens farver, mobilvenligt
- [ ] Aktivér Google Analytics integration
- [ ] Aktivér Google Consent Mode v2
- [ ] Aktivér Meta Pixel integration (hvis relevant)
- [ ] Konfigurér GTM consent (hvis GTM bruges)
- [ ] Opret/gennemgå cookie policy-side
- [ ] Link cookie policy fra footer og banner
- [ ] Konfigurér geo-restriction (EU opt-in)
- [ ] Test LiteSpeed Cache kompatibilitet
- [ ] Test i inkognito: Banner vises → afvis → tjek at scripts IKKE loader
- [ ] Test i inkognito: Banner vises → acceptér → tjek at scripts loader
- [ ] Planlæg månedlig re-scan af cookies
