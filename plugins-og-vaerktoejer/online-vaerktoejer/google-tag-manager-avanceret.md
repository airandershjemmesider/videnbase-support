# Google Tag Manager — avancerede opsætninger

## Hvad er det

Denne guide dækker avancerede GTM-opsætninger ud over standard GA4 og Facebook Pixel. Det inkluderer custom events, e-commerce tracking, formular-tracking, telefon-klik og cross-domain tracking.

## Custom events

### Scroll tracking

1. Gå til **Variables** → **Configure Built-In Variables**
2. Aktivér: Scroll Depth Threshold, Scroll Depth Units, Scroll Direction
3. Opret trigger: **Scroll Depth** → Vertical → Percentages: 25, 50, 75, 90
4. Opret GA4 Event tag:
   - Event name: `scroll_depth`
   - Parameter: `percent_scrolled` = `{{Scroll Depth Threshold}}`
   - Trigger: Scroll Depth triggeren

### Outbound clicks

1. Aktivér built-in variable: **Click URL**
2. Opret trigger: **Click - Just Links**
   - Betingelse: Click URL does not contain `ditdomæne.dk`
3. Opret GA4 Event tag:
   - Event name: `outbound_click`
   - Parameter: `link_url` = `{{Click URL}}`

### Video tracking (YouTube)

1. Opret trigger: **YouTube Video**
   - Capture: Start, Complete, Pause, Seeking, Progress (25%, 50%, 75%)
2. Aktivér built-in variables: Video Title, Video URL, Video Percent, Video Status
3. Opret GA4 Event tag med relevante parametre

## Enhanced ecommerce (WooCommerce)

### DataLayer integration

1. Installer plugin: **GTM4WP** med WooCommerce-integration aktiveret
2. Under GTM4WP indstillinger → **Integration** → slå WooCommerce til
3. Vælg dataLayer-format: **GA4**
4. GTM4WP pusher automatisk e-commerce events til dataLayer:
   - `view_item`, `add_to_cart`, `begin_checkout`, `purchase`

### GTM tags til e-commerce

1. Opret GA4 Event tags for hvert e-commerce event
2. Brug **Data Layer Variable** til at hente e-commerce data
3. Eller brug GA4 Event tag med "Send Ecommerce data" aktiveret
4. Trigger: Custom Event med eventnavnet fra dataLayer

## Formular-tracking

### Contact Form 7

1. CF7 sender automatisk et `wpcf7mailsent` event til DOM
2. Opret trigger: **Custom Event** → Event name: `wpcf7mailsent`
3. Opret GA4 Event tag:
   - Event name: `form_submit`
   - Parameter: `form_name` = `contact_form_7`

### Elementor Forms

1. Elementor Forms sender ikke standard dataLayer events
2. Løsning A: Brug GTM4WP som fanger Elementor form submissions
3. Løsning B: Tilføj custom JavaScript i Elementor form success action:
   - After Submit → Custom Code der pusher til dataLayer
4. Opret Custom Event trigger i GTM

### Gravity Forms

1. Gravity Forms har en `gform_confirmation_loaded` event
2. Opret trigger: **Custom Event** → Event name: `gform_confirmation_loaded`
3. Brug Data Layer variabler til at fange form-ID og felter

## Telefon-klik tracking

### tel: links som konverteringer

1. Aktivér built-in variable: **Click URL**
2. Opret trigger: **Click - Just Links**
   - Betingelse: Click URL starts with `tel:`
3. Opret GA4 Event tag:
   - Event name: `phone_click`
   - Parameter: `phone_number` = `{{Click URL}}`
4. Markér `phone_click` som key event i GA4 for konverteringssporing

## Cross-domain tracking

### Hvornår det er relevant

- Kunden har flere domæner der deler trafik (fx `shop.dk` og `blog.dk`)
- Kunden bruger et eksternt betalingssystem på et andet domæne
- Uden cross-domain tracking tælles brugere som nye ved domæneskift

### Opsætning

1. Gå til GA4 → **Admin** → **Data Streams** → vælg streamen
2. Klik **Configure tag settings** → **Configure your domains**
3. Tilføj alle domæner der skal deles (match type: "contains")
4. GA4 tilføjer automatisk en `_gl` parameter til links mellem domænerne
5. Tjek med Preview mode at parameteren sendes korrekt

## Server-side tagging

### Hvad er det

- Standard GTM kører i brugerens browser (client-side)
- Server-side GTM kører på en server du kontrollerer (typisk Google Cloud)
- Data sendes først til din server, derefter videre til Google/Facebook etc.

### Hvornår er det relevant

- Bedre datakvalitet (ad blockers blokerer ikke server-side requests)
- Bedre performance (færre scripts i browseren)
- Mere kontrol over data (GDPR compliance)
- Typisk relevant for større kunder med budget til hosting

### Opsætning (oversigt)

1. Opret en Server container i GTM
2. Deploy til Google Cloud Run (eller anden hosting)
3. Konfigurér client-side GTM til at sende data til server-containeren
4. Opsæt server-side tags til at videresende til GA4, Facebook etc.

## Bemærkninger

- Test ALTID i Preview mode før publicering
- Avancerede opsætninger kræver ofte fejlsøgning — brug browser DevTools Console og Network tab
- DataLayer-variabler er case-sensitive — dobbelttjek stavning
- Hold containeren dokumenteret — brug noter i tags og versioner
- Server-side tagging koster penge (Google Cloud hosting) — typisk 30-100 kr/måned
