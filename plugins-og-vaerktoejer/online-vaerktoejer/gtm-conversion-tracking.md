# Google Tag Manager — Conversion tracking

## Oversigt

Conversion tracking måler hvornår en bruger udfører en værdifuld handling — fx indsender en formular, gennemfører et køb eller klikker på et telefonnummer. Denne guide dækker opsætning via GTM for både Google Ads og GA4.

## Google Ads conversion tracking

### Trin 1: Opret conversion i Google Ads

1. Log ind på **Google Ads**
2. Gå til **Goals > Conversions > Summary**
3. Klik **New conversion action**
4. Vælg **Website**
5. Udfyld:
   - **Conversion name:** Beskrivende navn (fx "Kontaktformular indsendt")
   - **Value:** Fast værdi eller variabel (fx 500 DKK per lead)
   - **Count:** "One" for leads, "Every" for køb
   - **Click-through window:** 30 dage (standard)
   - **View-through window:** 1 dag (standard)
6. Vælg **Use Google Tag Manager**
7. Kopiér **Conversion ID** og **Conversion Label**

### Trin 2: Conversion Linker tag (påkrævet)

Conversion Linker sikrer at klikdata fra Google Ads-annoncer overføres korrekt. Det skal være på alle sider.

1. Gå til **Tags** i GTM
2. Klik **New**
3. Tag type: **Conversion Linker**
4. Trigger: **All Pages**
5. Navngiv: `Google Ads - Conversion Linker`
6. Gem

**Vigtigt:** Uden Conversion Linker mister du klikattribution, og dine conversions tælles ikke korrekt.

### Trin 3: Opret conversion tag i GTM

1. Gå til **Tags** i GTM
2. Klik **New**
3. Tag type: **Google Ads Conversion Tracking**
4. Udfyld:
   - **Conversion ID:** Indsæt fra trin 1
   - **Conversion Label:** Indsæt fra trin 1
   - **Conversion Value:** Fast værdi eller GTM-variabel
   - **Currency Code:** DKK
5. Trigger: Se næste trin
6. Navngiv: `Google Ads - Conversion - [Beskrivelse]`
7. Gem

### Trin 4: Opsæt trigger

Triggeren bestemmer hvornår conversionen registreres. Typiske setups:

**Tak-side (Page View trigger):**
1. Opret ny trigger: **Page View**
2. Vælg "Some Page Views"
3. Betingelse: `Page URL contains /tak` eller `Page Path equals /tak-for-din-besked`

**Formular indsendt (Custom Event trigger):**
1. Opret ny trigger: **Custom Event**
2. Event name: `form_submit` (skal matche dit dataLayer.push event)
3. Tilføj betingelse hvis nødvendigt (fx `form_id equals kontakt`)

**Knap-klik (Click trigger):**
1. Opret ny trigger: **Click - All Elements** eller **Click - Just Links**
2. Betingelse: `Click Text contains Send` eller `Click ID equals submit-btn`

## GA4 event tracking for conversions

GA4 bruger events til alt — også conversions. Du markerer specifikke events som conversions inde i GA4 efter de er oprettet.

### Klik-tracking

**Alle udgående klik:**
1. Gå til **Triggers > New**
2. Type: **Click - Just Links**
3. Vælg "Some Link Clicks"
4. Betingelse: `Click URL does not contain [dit domæne]`
5. Opret GA4 Event tag med event name `outbound_click`

**Specifikke knapper:**
1. Trigger type: **Click - All Elements**
2. Betingelse: `Click Classes contains cta-button` eller `Click ID equals book-meeting`
3. GA4 Event tag med relevant event name

### Scroll depth tracking

1. Gå til **Triggers > New**
2. Type: **Scroll Depth**
3. Vælg **Vertical Scroll Depths**
4. Percentages: `25, 50, 75, 90`
5. Opret GA4 Event tag:
   - Event name: `scroll`
   - Parameter: `percent_scrolled` = `{{Scroll Depth Threshold}}`
6. Trigger: Din nye scroll depth trigger

**Husk:** Aktivér den built-in variabel `Scroll Depth Threshold` under Variables først.

### Form submission tracking

**Med Element Visibility (tak-besked):**
1. Trigger type: **Element Visibility**
2. Selection method: CSS Selector
3. Selector: `.wpcf7-mail-sent-ok` (Contact Form 7) eller `.elementor-message-success`
4. GA4 Event: `form_submit`

**Med Custom Event (dataLayer):**
1. Tilføj `dataLayer.push({'event': 'form_submit', 'form_id': 'kontakt'})` i formularens success callback
2. Trigger: Custom Event med event name `form_submit`
3. GA4 Event tag med parametre fra Data Layer

### Element visibility tracking

Nyttigt til at spore om brugere ser vigtige sektioner:

1. Trigger type: **Element Visibility**
2. Selection method: **CSS Selector** eller **ID**
3. Selector: `#priser` eller `.testimonials-section`
4. Indstillinger:
   - **Minimum Percent Visible:** 50%
   - **Observe DOM changes:** Ja (for dynamisk indhold)
   - **Fire once per page:** Ja (undgår gentagne events)
5. GA4 Event: `section_viewed` med parameter `section_name`

## Markér events som conversions i GA4

Når dine events sender data til GA4:

1. Gå til **GA4 > Admin > Events**
2. Find dit event i listen
3. Slå **Mark as conversion** til
4. Eventet tæller nu som conversion i rapporter

**Bemærk:** Det kan tage op til 24 timer før nye events vises i GA4.

## Export og import af GTM containers

### Eksport

1. Gå til **Admin** i GTM
2. Klik **Export Container**
3. Vælg version eller workspace
4. Download JSON-filen
5. Gem filen med beskrivende navn og dato

### Import

1. Gå til **Admin** i GTM
2. Klik **Import Container**
3. Vælg JSON-filen
4. Vælg workspace
5. Vælg **Merge** (tilføj til eksisterende) eller **Overwrite** (erstat alt)
6. Gennemgå ændringer og bekræft

**Tip:** Brug export/import til at kopiere opsætninger mellem kunder eller som backup før store ændringer.

## Preview og test workflow

Følg altid denne rækkefølge:

1. **Preview mode:** Klik Preview i GTM — åbner Tag Assistant
2. **Naviger:** Besøg de sider hvor conversions skal ske
3. **Udløs handlingen:** Indsend formularen, klik knappen, besøg tak-siden
4. **Tjek Tag Assistant:** Se at dit conversion tag fyrer med korrekte værdier
5. **Tjek GA4 DebugView:** Gå til GA4 > Admin > DebugView og se events i realtid
6. **Publicér:** Når alt virker, klik **Submit** i GTM
7. **Verificér i produktion:** Vent 24-48 timer og tjek at conversions registreres

## Fejlsøgning

### Tag fyrer ikke

- Tjek at triggeren matcher den korrekte URL, event eller klik
- Verificér at Consent Mode ikke blokerer tagget (tjek Complianz-integration)
- Se om tagget er i den publicerede version (ikke kun workspace)

### Conversion tælles ikke i Google Ads

- Tjek at Conversion Linker tag er aktivt på alle sider
- Verificér at Conversion ID og Label er korrekte (ingen mellemrum, korrekte værdier)
- Vent mindst 24 timer — der er forsinkelse i Google Ads rapportering
- Tjek at Google Ads-kontoen er aktiv og har impressions

### GA4 event vises ikke

- Brug **DebugView** i GA4 til realtidsdata
- Tjek at GA4 Measurement ID er korrekt i GTM
- Verificér at eventet ikke filtreres af ad-blockers
- Sørg for at consent er givet (test i incognito uden ad-blocker)

### Preview mode virker ikke

- Ryd browser-cache og cookies
- Prøv en anden browser
- Tjek at GTM-container snippet er installeret korrekt på sitet
- Deaktivér ad-blockers midlertidigt
