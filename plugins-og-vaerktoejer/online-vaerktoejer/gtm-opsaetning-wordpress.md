# GTM Opsætning for WordPress — Komplet Guide

## Hvad er GTM og Hvorfor Bruge Det

Google Tag Manager (GTM) er et tag management system der samler al tracking-kode ét sted. I stedet for at tilføje scripts direkte i WordPress, styrer du alt fra GTMs webinterface.

**Fordele:** Overblik over alle tags ét sted, ingen kodeændringer ved ny tracking, fuld versionering med rollback, Preview/Debug mode før publicering.

**Tommelfingerregel:** Hvis sitet har mere end bare GA4, brug GTM. Det gælder så snart der er Facebook Pixel, konverteringsscripts, remarketing eller andre tredjepartstags.

## Opret GTM Konto og Container

1. Gå til [tagmanager.google.com](https://tagmanager.google.com)
2. Log ind med kundens Google-konto
3. Klik **Create Account**
4. Udfyld:
   - **Account Name:** Kundens virksomhedsnavn
   - **Container Name:** Kundens domæne (fx `eksempel.dk`)
   - **Target Platform:** Web
5. Acceptér servicevilkår
6. Kopiér container-ID (format: `GTM-XXXXXXX`)

Du får to kode-snippets — dem skal du bruge i næste trin.

## Installér GTM på WordPress

### Via Plugin (anbefalet)

1. Installér plugin: **GTM4WP** (Google Tag Manager for WordPress)
2. Gå til **Indstillinger** → **Google Tag Manager**
3. Indtast container-ID (`GTM-XXXXXXX`)
4. Under **Container code placement** vælg en af:
   - **Codeless injection** — nemmest, virker med de fleste temaer
   - **Custom** — mere kontrol over placering
5. Gem indstillinger

### Manuelt i Theme

Kun hvis plugin ikke er en mulighed. Indsæt første snippet i `<head>` og andet snippet efter `<body>` via child theme. Kræver child theme da ændringer ellers går tabt ved tema-opdatering.

### Verificér Installation

1. Gå til GTM → Klik **Preview** → Indtast kundens URL
2. Bekræft at **Container Found** vises og at tags fyrer korrekt

## Grundlæggende Begreber

### Tags

**Hvad der skal eksekveres.** Eksempler:

- GA4 Configuration — sender data til Google Analytics
- Facebook Pixel — sender data til Meta
- Custom HTML — vilkårlig tracking-kode
- Google Ads Conversion — tracking af konverteringer

### Triggers

**Hvornår tags skal fyre.** Eksempler:

| Trigger | Bruges til |
|---------|-----------|
| All Pages | GA4 base tracking, Facebook Pixel PageView |
| Click — Just Links | Tracking af specifikke link-klik |
| Form Submission | Kontaktformular indsendt |
| Scroll Depth | Tracking af scroll-dybde |
| Timer | Tid brugt på side |
| Custom Event | Events fra dataLayer (fx `formSubmit`) |

### Variables

**Data der bruges af tags og triggers.** To typer:

- **Built-in Variables** — foruddefinerede (Page URL, Click Text, Form ID osv.)
- **User-Defined Variables** — dine egne (dataLayer-variabler, konstanter, lookup tables)

## Opsæt GA4 via GTM

### Configuration Tag

1. **Tags** → **New** → Vælg **Google Analytics: GA4 Event**
2. Measurement ID: `G-XXXXXXXXXX`
3. Trigger: **All Pages**
4. Navngiv: `GA4 — Config`
5. Gem

### Event Tags

For custom events, opret separate tags:

**Eksempel — Telefon-klik:**

1. **Tags** → **New** → **Google Analytics: GA4 Event**
2. Measurement ID: `G-XXXXXXXXXX`
3. Event Name: `phone_click`
4. Trigger: Ny trigger → **Click — Just Links** → URL contains `tel:`
5. Navngiv: `GA4 — Event — Phone Click`

## Opsæt Facebook Pixel via GTM

1. **Tags** → **New** → **Custom HTML**
2. Indsæt Facebook Pixel base-kode (fra Meta Events Manager)
3. Trigger: **All Pages**
4. Navngiv: `FB — Pixel Base`

For specifikke events (Lead, Purchase osv.) opret separate Custom HTML tags med de relevante Facebook event-kald og passende triggers.

## Built-in Variables at Aktivere

Gå til **Variables** → **Configure** og aktivér disse:

**Pages:**
- Page URL, Page Path, Page Hostname, Referrer

**Clicks:**
- Click Element, Click Classes, Click ID, Click URL, Click Text

**Forms:**
- Form Element, Form Classes, Form ID, Form URL, Form Text

**Utilities:**
- Container ID, Container Version, Debug Mode, HTML ID

## Custom Events

### Formular-indsendelse (Contact Form 7)

CF7 sender et custom event til dataLayer ved succesfuld indsendelse:

1. Opret trigger: **Custom Event** → Event name: `wpcf7mailsent`
2. Opret GA4 Event tag med event name: `form_submit`
3. Tilføj event parameters for at sende formular-detaljer

### Telefon-klik

1. Aktivér Click URL som built-in variable
2. Opret trigger: **Click — Just Links** → Click URL contains `tel:`
3. Opret GA4 Event tag med event name: `phone_click`

### Scroll Tracking (udvidet)

Enhanced Measurement tracker kun 90% scroll. For mere granulær tracking: Opret **Scroll Depth** trigger (25%, 50%, 75%, 100%) og en GA4 Event tag med event name `scroll_depth` og parameter `percent_scrolled` = `{{Scroll Depth Threshold}}`.

## Preview/Debug Mode

1. Klik **Preview** i GTM → Indtast sidens URL
2. Tag Assistant åbner og viser: **Tags Fired**, **Tags Not Fired**, **Data Layer** og **Variables**
3. Navigér rundt på sitet for at teste alle triggers
4. Tjek at GA4 DebugView også modtager events korrekt

## Publish: Versionering

1. Klik **Submit** → **Publish and Create Version**
2. Giv versionen et beskrivende navn (fx `GA4 + FB Pixel opsætning`)
3. Publicér kun testede ændringer — brug altid Preview først
4. Du kan altid rulle tilbage til en tidligere version via Versions-fanen

## GTM + Complianz: Consent-baseret Firing

Complianz (eller CookieYes) integrerer med GTM via Consent Mode v2:

### Opsætning

1. Installér og konfigurér Complianz i WordPress
2. Under Complianz → Integrations: Aktivér Google Tag Manager
3. I GTM: Tags der kræver consent (GA4, FB Pixel) skal have **Consent Settings**:
   - Klik på tagget → **Advanced Settings** → **Consent Settings**
   - Vælg **Require additional consent for tag to fire**
   - Tilføj relevant consent type (fx `analytics_storage`, `ad_storage`)

### Consent Types

| Consent Type | Bruges af |
|-------------|-----------|
| `analytics_storage` | GA4, Hotjar, Clarity |
| `ad_storage` | Google Ads, Facebook Pixel |
| `ad_user_data` | Google Ads (påkrævet fra marts 2024) |
| `ad_personalization` | Google Ads remarketing |

Uden consent sender GA4 "cookieless pings" med begrænset data (Consent Mode modellering).

## Navngivningskonvention

Hold containeren organiseret: Tags navngives `[Platform] — [Type] — [Detalje]` (fx `GA4 — Event — Phone Click`, `FB — Pixel Base`). Triggers navngives efter hvad de gør (fx `Click — Tel Links`, `Form — CF7 Submit`).

## Hurtig Tjekliste

- [ ] GTM konto og container oprettet
- [ ] GTM installeret på WordPress (GTM4WP plugin)
- [ ] Installation verificeret via Preview mode
- [ ] GA4 Configuration tag opsat med korrekt Measurement ID
- [ ] GA4 Event tags for custom events (formular, telefon, scroll)
- [ ] Facebook Pixel installeret (hvis relevant)
- [ ] Built-in variables aktiveret (Clicks, Forms, Pages)
- [ ] Consent Mode konfigureret med Complianz
- [ ] Alle tags testet i Preview/Debug mode
- [ ] GA4 DebugView bekræfter korrekt data
- [ ] Container publiceret med beskrivende versionsnavn
- [ ] Navngivningskonvention fulgt for tags og triggers
- [ ] Dobbelt-tracking tjekket (GA4 ikke installeret BÅDE via GTM og plugin)
