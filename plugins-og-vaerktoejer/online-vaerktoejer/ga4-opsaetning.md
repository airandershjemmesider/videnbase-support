# GA4 Opsætning — Komplet Guide

## Hvad er GA4

Google Analytics 4 (GA4) er Googles nuværende analyseplatform. Den erstattede Universal Analytics (UA) i juli 2023. De vigtigste forskelle:

| Egenskab | Universal Analytics (UA) | GA4 |
|----------|-------------------------|-----|
| Datamodel | Session-baseret | Event-baseret |
| Rapporter | Faste rapporter | Fleksible, tilpasselige |
| Cookies | Tredjepartscookies | Førstepartscookies |
| Machine learning | Begrænset | Indbygget (prædiktive målgrupper) |
| Consent Mode | Nej | Ja (v2 påkrævet fra marts 2024) |
| Gratis dataretention | Op til 50 måneder | Maks 14 måneder |

GA4 måler ALT som events. En sidevisning er et event (`page_view`), et scroll er et event (`scroll`), et klik er et event (`click`). Det gør trackingen mere fleksibel end UA.

## Opret GA4 Property og Data Stream

### Trin 1: Opret Property

1. Gå til [analytics.google.com](https://analytics.google.com)
2. Log ind med kundens Google-konto
3. Klik **Admin** (tandhjul nederst til venstre)
4. Klik **Create** → **Property**
5. Udfyld:
   - Property-navn: Kundens domæne (fx `eksempel.dk`)
   - Tidzone: **(GMT+01:00) Copenhagen**
   - Valuta: **DKK**

### Trin 2: Opret Data Stream

1. Under den nye property: **Data Streams** → **Add stream** → **Web**
2. Indtast domænet (fx `https://eksempel.dk`)
3. Giv streamen et navn (fx `eksempel.dk — Web`)
4. Kopiér **Measurement ID** (format: `G-XXXXXXXXXX`)
5. Slå **Enhanced Measurement** til (se nedenfor)

## Installér GA4

### Via GTM (anbefalet)

Se [gtm-opsaetning-wordpress.md](gtm-opsaetning-wordpress.md) for fuld GTM-guide.

1. Opret en **Google Analytics: GA4 Event** tag i GTM
2. Indtast Measurement ID (`G-XXXXXXXXXX`)
3. Trigger: **All Pages**
4. Publicér containeren

### Via RankMath

1. Gå til **RankMath** → **General Settings** → **Analytics**
2. Forbind med Google-kontoen
3. Vælg GA4 property
4. RankMath indsætter tracking-koden automatisk

### Via plugin

- **Site Kit by Google** — officielt Google-plugin, nemt setup
- **MonsterInsights** — brugervenlig dashboard i WordPress

**Vigtigt:** Brug KUN én metode. Dobbelt-installation giver forkerte data.

## Enhanced Measurement

Enhanced Measurement er GA4s automatiske event-tracking. Slås til under **Data Stream** → **Enhanced Measurement**. Disse events trackes automatisk:

| Event | Hvad det måler |
|-------|---------------|
| `page_view` | Sidevisninger (altid aktiv) |
| `scroll` | Scroll til 90% af sidens højde |
| `click` (outbound) | Klik på links til eksterne domæner |
| `site_search` | Brug af sidens søgefunktion |
| `video_engagement` | YouTube-videoer: start, progress, fuldført |
| `file_download` | Download af PDF, DOCX, XLSX osv. |
| `form_interaction` | Formular-interaktioner (start og indsendelse) |

## Vigtige Events at Tracke

Ud over Enhanced Measurement bør du opsætte custom events for:

- **form_submit** — kontaktformular indsendt (via GTM eller CF7/Elementor event)
- **phone_click** — klik på telefonnummer (`tel:` links)
- **email_click** — klik på e-mail links (`mailto:`)
- **cta_click** — klik på vigtige call-to-action knapper

## Konverteringer (Key Events)

Sådan markerer du et event som konvertering:

1. Gå til **Admin** → **Events**
2. Find eventet (fx `form_submit`)
3. Slå **Mark as key event** til

Typiske konverteringer for en virksomhedsside:

- Kontaktformular indsendt
- Telefonnummer klikket
- Tilbudsanmodning sendt
- Booking gennemført

## Audiences (Målgrupper)

Opret målgrupper til remarketing under **Admin** → **Audiences**:

- **Alle besøgende** — standard, bruges til bred remarketing
- **Engagerede brugere** — besøgte 3+ sider eller var på sitet 60+ sekunder
- **Konverterede** — brugere der udførte en key event
- **Besøgte specifik side** — fx prissiden eller kontaktsiden

Audiences kan deles med Google Ads til remarketing-kampagner.

## Rapporter

| Rapport | Hvad den viser |
|---------|---------------|
| **Acquisition** | Hvor trafikken kommer fra (organic, paid, social, direct) |
| **Engagement** | Sidevisninger, sessionslængde, events, scroll |
| **Monetization** | E-commerce data, omsætning (kræver opsætning) |
| **Retention** | Tilbagevendende brugere over tid |
| **Demographics** | Alder, køn, interesser, geografi |

## DebugView

Test events i realtid under **Admin** → **DebugView**:

1. Aktivér GTM Preview mode ELLER installér **Google Analytics Debugger** Chrome-extension
2. Besøg sitet — events vises live i DebugView
3. Tjek at alle events og parametre registreres korrekt
4. DebugView viser events med ca. 1 sekunds forsinkelse

## Vigtige Indstillinger

### Data Retention

- Gå til **Admin** → **Data Settings** → **Data Retention**
- Ændr fra 2 måneder til **14 måneder** (maks for gratis GA4)
- Gælder kun Exploration-rapporter — standardrapporter påvirkes ikke

### Filtrér Intern Trafik

1. **Admin** → **Data Streams** → Vælg stream → **Configure tag settings**
2. Klik **Define internal traffic**
3. Tilføj din IP-adresse (eller IP-range)
4. Gå til **Admin** → **Data Settings** → **Data Filters**
5. Aktivér filteret (det starter som "Testing" — skift til "Active")

### Forbind med Andre Tjenester

- **Google Ads:** Admin → Product Links → Google Ads — giver remarketing og konverteringsdata
- **Search Console:** Admin → Product Links → Search Console — viser søgedata direkte i GA4
- **BigQuery:** Admin → Product Links → BigQuery — til avanceret dataanalyse (gratis eksport)

## Hurtig Opsætningstjekliste

- [ ] GA4 property oprettet med korrekt tidzone og valuta
- [ ] Data Stream oprettet med korrekt domæne
- [ ] Measurement ID kopieret
- [ ] GA4 installeret via GTM (eller plugin)
- [ ] Enhanced Measurement aktiveret
- [ ] Custom events opsat (formular, telefon-klik)
- [ ] Key events markeret (konverteringer)
- [ ] Data Retention sat til 14 måneder
- [ ] Intern trafik filtreret
- [ ] Search Console forbundet
- [ ] Google Ads forbundet (hvis relevant)
- [ ] DebugView brugt til at verificere data
- [ ] Audiences oprettet til remarketing
- [ ] Consent Mode konfigureret (Complianz/CookieYes)
