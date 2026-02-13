# Complianz GDPR Cookie Consent — Opsætning

## Hvad er det

Complianz er et GDPR/cookie compliance plugin til WordPress. Det scanner hjemmesidens cookies, viser en cookie-banner til besøgende og kan generere en privatlivspolitik. Pluginet sikrer at hjemmesiden overholder EU's cookielovgivning.

## Installation

1. Gå til **Plugins → Tilføj nyt** i WordPress admin
2. Søg efter "Complianz"
3. Installér og aktivér **Complianz – GDPR/CCPA Cookie Consent**
4. Gå til **Complianz → Wizard** for at starte opsætningen

## Wizard-gennemgang

Wizarden guider dig igennem hele opsætningen trin for trin:

### Trin 1: Generelle indstillinger
- Vælg **region: EU** (dækker GDPR)
- Vælg sprog: **Dansk**
- Angiv virksomhedens kontaktinfo

### Trin 2: Cookie scanner
- Klik **Start Scan** — pluginet scanner alle sider for cookies
- Gennemgå de fundne cookies
- Kategorisér cookies korrekt: Nødvendige, Statistik, Marketing, Præferencer
- Ukendte cookies skal undersøges og kategoriseres manuelt

### Trin 3: Cookie banner
- Vælg bannertype (opt-in er påkrævet i EU)
- Tilpas tekst, farver og design til kundens branding
- Forhåndsvis banneret inden du gemmer

### Trin 4: Privatlivspolitik
- Complianz kan generere en privatlivspolitik-side
- Gennemgå og tilpas teksten så den matcher virksomheden
- Link til privatlivspolitikken fra footer og cookie banner

## Vigtige indstillinger

### Cookie banner — design og tekst
- **Complianz → Cookie Banner** for at tilpasse udseende
- Vælg farver der passer til hjemmesidens branding
- Tilpas knaptekster (f.eks. "Acceptér alle", "Kun nødvendige")
- Test at banneret vises korrekt på mobil og desktop

### Cookie scanner — vedligeholdelse
- Kør en ny scan efter installation af nye plugins
- Kør scan regelmæssigt (månedligt) for at fange nye cookies
- Kontrollér at alle cookies er korrekt kategoriseret

### Google Analytics / Tag Manager integration
- Gå til **Complianz → Integrations**
- Aktivér integration med Google Analytics eller Google Tag Manager
- Sørg for at statistik-cookies først sættes efter brugerens samtykke
- Se separat guide: `complianz-consent-mode.md`

### Geo-restriction
- Under **Settings → Regions** kan du vælge hvilke regioner der skal se banneret
- EU-besøgende: Fuld cookie banner med opt-in
- Andre regioner: Kan konfigureres separat (f.eks. opt-out for USA)

## Fejlsøgning

### Banner vises ikke
1. **Ryd cache** — WP Rocket, server-cache, CDN cache
2. Tjek at banneret er aktiveret under **Complianz → Cookie Banner**
3. Tjek om du er logget ind — banneret skjules som standard for admins
4. Åbn i privat/inkognito vindue for at teste

### Cookies blokeres ikke korrekt
1. Kør en ny cookie-scan under **Complianz → Cookie Scanner**
2. Tjek at cookies er korrekt kategoriseret
3. Kontrollér at scripts fra 3. part (Analytics, Facebook Pixel) er registreret
4. Test med browser DevTools → Application → Cookies

### Banner vises på hver side-load
- Tjek at "Accept"-knappen faktisk gemmer samtykket (cookie)
- Kan skyldes cache-plugin der cacher siden med banneret
- Tilføj en undtagelse i cache-pluginet for Complianz-cookies

## Bemærkninger

- Complianz Free dækker de fleste behov for danske sider
- Complianz Premium tilføjer: A/B testing af banner, geo-targeting, flere regioner
- Opdatér pluginet regelmæssigt — cookie-lovgivning ændrer sig
- Cookie scanneren bør køres igen efter enhver plugin-installation eller -opdatering
- Complianz arbejder sammen med de fleste cache-plugins (WP Rocket, LiteSpeed)
