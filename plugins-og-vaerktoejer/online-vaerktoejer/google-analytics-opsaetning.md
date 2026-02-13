# Google Analytics 4 (GA4) opsætning

## Hvad er det

Google Analytics 4 (GA4) er Googles analyseplatform til at måle trafik og brugeradfærd på hjemmesider. Det erstatter Universal Analytics (UA) og er baseret på en event-drevet datamodel. GA4 giver indsigt i hvor besøgende kommer fra, hvad de gør på sitet, og om de konverterer.

## Opsætning

### Opret GA4 property

1. Gå til [analytics.google.com](https://analytics.google.com)
2. Log ind med kundens Google-konto
3. Klik **Admin** (tandhjul nederst til venstre)
4. Klik **Create** → **Property**
5. Udfyld property-navn (fx kundens domæne), tidzone (Copenhagen) og valuta (DKK)
6. Opret en **Web** data stream med kundens URL
7. Kopiér **Measurement ID** (format: `G-XXXXXXXXXX`)

### Installer på WordPress

**Metode 1: Via Google Tag Manager (anbefalet)**
- Se [google-tag-manager.md](google-tag-manager.md) for GTM-opsætning
- Opret en GA4 Configuration tag i GTM med Measurement ID
- Trigger: All Pages
- Publicér containeren

**Metode 2: Via plugin (enklere)**
- Installer plugin: **Site Kit by Google** (officielt fra Google)
- Forbind med Google-konto og vælg GA4 property
- Alternativt: **MonsterInsights** eller **GA Google Analytics** plugin

**Metode 3: Manuelt**
- Indsæt GA4 gtag.js snippet i `<head>` via Customizer eller child theme
- Ikke anbefalet da det er sværere at vedligeholde

## Daglig brug

### Grundlæggende rapporter

- **Realtime** — se hvem der er på sitet lige nu, hvad de kigger på
- **Acquisition** — hvor kommer trafikken fra (organic, paid, social, direct, referral)
- **Engagement** — hvilke sider besøges, hvor lang tid bruger folk, events
- **Retention** — hvor mange brugere vender tilbage
- **Monetization** — omsætning og e-commerce data (kræver opsætning)

### Events

**Automatiske events (Enhanced Measurement):**
- page_view, scroll, outbound click, site search, video engagement, file download
- Slås til under Data Stream → Enhanced Measurement

**Custom events:**
- Oprettes via GTM eller gtag.js
- Eksempler: formular-indsendelse, klik på telefonnummer, tilføj til kurv

### Konverteringer

1. Gå til **Admin** → **Events**
2. Find det event du vil bruge som konvertering
3. Slå **Mark as key event** til
4. Typiske konverteringer:
   - `form_submit` — kontaktformular sendt
   - `purchase` — køb gennemført
   - Custom event for telefon-klik

## Fejlsøgning

### Ingen data i GA4

1. **Tjek Measurement ID** — er det korrekt indsat?
2. **Tjek GTM** — er containeren publiceret? Brug GTM Preview mode
3. **Tjek consent** — blokerer cookie-consent GA4 før accept?
4. **Tjek ad blockers** — mange brugere blokerer GA4
5. **Vent 24-48 timer** — GA4 standard-rapporter har forsinkelse (Realtime virker med det samme)

### Dobbelt-tracking

- Symptom: Unormalt høje sidevisninger, bounce rate tæt på 0%
- Årsag: GA4 er installeret BÅDE via GTM og direkte (plugin eller kode)
- Løsning: Fjern den ene — brug KUN GTM-metoden

### Consent Mode

- GA4 respekterer Google Consent Mode v2
- Uden cookie-consent sendes "cookieless pings" (begrænset data)
- Med consent: Fuld tracking aktiveres
- Integrer med Complianz eller CookieYes for automatisk håndtering

## Bemærkninger

- GA4 data kan IKKE overføres til Universal Analytics (UA er lukket)
- Standard dataretention er 2 måneder — ændr til 14 måneder under Admin → Data Settings → Data Retention
- GDPR kræver cookie consent FØR GA4 tracking aktiveres — brug Consent Mode
- Link GA4 med Google Search Console for at se søgedata direkte i GA4
- Link GA4 med Google Ads for at bruge GA4-audiences i annoncering
- Opret en **Test property** til at eksperimentere uden at forurene produktionsdata
