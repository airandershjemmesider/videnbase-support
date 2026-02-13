# Complianz + Google Consent Mode v2

## Hvad er det

Google Consent Mode v2 er en teknologi der sender brugerens cookie-samtykke til Google. Når en besøgende accepterer eller afviser cookies via Complianz-banneret, kommunikerer Consent Mode dette til Google Analytics og Google Ads. Det sikrer korrekt dataindsamling OG GDPR-overholdelse.

## Hvorfor er det vigtigt

- Google kræver Consent Mode v2 for annoncører i EU/EØS (fra marts 2024)
- Uden Consent Mode mister du remarketing- og konverteringsdata
- Consent Mode giver Google mulighed for at modellere data selv uden samtykke (consent-less pings)

## Forudsætninger

- Complianz plugin installeret og konfigureret (se `complianz-opsaetning.md`)
- Google Tag Manager ELLER direkte gtag.js på hjemmesiden
- Google Analytics 4 property oprettet

## Opsætning

### Trin 1: Aktivér Consent Mode i Complianz
1. Gå til **Complianz → Integrations**
2. Find **Google Consent Mode**
3. Aktivér integrationen
4. Vælg implementeringsmetode:
   - **Google Tag Manager** (anbefalet hvis GTM allerede bruges)
   - **gtag.js** (hvis Analytics er indsat direkte)

### Trin 2: Konfigurér consent-parametre
Complianz sætter automatisk disse Google Consent Mode parametre:

| Parameter | Beskrivelse | Standard (før samtykke) |
|-----------|-------------|------------------------|
| `ad_storage` | Cookies til annoncering | `denied` |
| `analytics_storage` | Cookies til statistik | `denied` |
| `ad_user_data` | Deling af brugerdata med Google Ads | `denied` |
| `ad_personalization` | Personaliserede annoncer | `denied` |
| `functionality_storage` | Funktionelle cookies | `denied` |
| `personalization_storage` | Personaliseringscookies | `denied` |
| `security_storage` | Sikkerhedscookies | `granted` |

### Trin 3: Verificér i Google Tag Manager (hvis brugt)
1. Åbn Google Tag Manager
2. Gå til **Admin → Container Settings**
3. Kontrollér at "Enable consent overview" er aktiveret
4. Tjek at dine tags har korrekte consent-indstillinger:
   - Google Analytics tag: Kræver `analytics_storage`
   - Google Ads tag: Kræver `ad_storage` + `ad_user_data` + `ad_personalization`

## Test af Consent Mode

### Med Google Tag Assistant
1. Installér **Google Tag Assistant** Chrome-extension
2. Besøg hjemmesiden i et inkognito-vindue
3. Afvis cookies i banneret → tjek at consent states viser "denied"
4. Acceptér cookies → tjek at consent states skifter til "granted"

### Med browser DevTools
1. Åbn DevTools → Console
2. Skriv `dataLayer` og tryk Enter
3. Søg efter `consent` events
4. Verificér at `default` consent er "denied" og opdateres efter brugerinteraktion

### Med Google Analytics 4
1. Gå til **GA4 → Admin → Data Streams**
2. Tjek at der kommer data ind
3. Under **Reports → Realtime** kan du se aktive brugere
4. Consent Mode events bør vises i DebugView

## Fejlsøgning

### Consent states opdateres ikke
- Ryd cache (WP Rocket, browser, CDN)
- Tjek at Complianz-integrationen er aktiveret korrekt
- Verificér at GTM-containeren er publiceret efter ændringer

### Google Ads viser "Consent Mode not detected"
- Sørg for at `ad_user_data` og `ad_personalization` er inkluderet
- Disse to parametre er nye krav i Consent Mode v2
- Tjek at Complianz er opdateret til nyeste version

### Data mangler i Google Analytics
- Consent Mode sender "consent-less pings" til Google selv uden samtykke
- Google bruger modelleret data til at udfylde huller
- Det kan tage 24-48 timer før modelleret data vises

## Bemærkninger

- Consent Mode v2 er et krav fra Google for EU-annoncører
- Complianz håndterer automatisk kommunikationen mellem cookie-banner og Google
- Opdatér Complianz regelmæssigt for at sikre kompatibilitet med Googles krav
- Test altid efter opdateringer af enten Complianz eller GTM
- Advanced Consent Mode (standard i Complianz) sender anonyme pings selv uden samtykke
- Basic Consent Mode blokerer alt indtil samtykke gives (mere restriktivt)
