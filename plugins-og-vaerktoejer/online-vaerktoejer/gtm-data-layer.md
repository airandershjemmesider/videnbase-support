# Google Tag Manager — Data Layer og avanceret tracking

## Hvad er Data Layer?

Data Layer er et JavaScript-objekt som GTM bruger til at modtage og videresende data fra dit website. Det fungerer som en mellemmand mellem din hjemmeside og GTM — sitet skubber data ind, og GTM læser det og sender det videre til fx GA4, Google Ads eller Meta.

Data Layer oprettes automatisk af GTM-containeren, men du kan også initialisere det selv før GTM loader:

```javascript
window.dataLayer = window.dataLayer || [];
```

## Grundlæggende dataLayer struktur

Data Layer er et array af objekter. Hvert objekt repræsenterer en "besked" til GTM:

```javascript
// Eksempel: Brugerdata ved sidevisning
dataLayer.push({
  'event': 'page_view',
  'page_title': 'Kontakt os',
  'page_type': 'contact',
  'user_type': 'returning_customer',
  'user_id': '12345'
});
```

### Vigtige principper

- **Brug altid `dataLayer.push()`** — skriv aldrig direkte til arrayet
- **Event-nøglen** er det GTM lytter efter i triggers
- **Data persisterer** i Data Layer indtil siden genindlæses
- **Nyere data overskriver ældre** med samme nøgle

## Nested data (ecommerce)

GA4 ecommerce-events bruger nested objekter i Data Layer. Strukturen følger GA4's standardskema:

```javascript
// Eksempel: Produkt tilføjet til kurv
dataLayer.push({
  'event': 'add_to_cart',
  'ecommerce': {
    'currency': 'DKK',
    'value': 299.00,
    'items': [
      {
        'item_id': 'SKU-001',
        'item_name': 'Løbesko Model X',
        'item_category': 'Sko',
        'item_brand': 'SportsBrand',
        'price': 299.00,
        'quantity': 1
      }
    ]
  }
});
```

### Adgang til nested data i GTM

For at læse `ecommerce.currency` i GTM opretter du en **Data Layer Variable**:

- Variabelnavn: `ecommerce.currency`
- GTM bruger dot-notation til at navigere ned i objektet

## Custom Events via dataLayer.push()

Custom events er din primære måde at kommunikere handlinger fra sitet til GTM.

### Typiske custom events

```javascript
// Formular indsendt
dataLayer.push({
  'event': 'form_submit',
  'form_id': 'kontakt-formular',
  'form_name': 'Kontakt os',
  'form_destination': '/tak-for-din-besked'
});

// Klik på telefonnummer
dataLayer.push({
  'event': 'phone_click',
  'phone_number': '+45 12 34 56 78'
});

// Video afspillet
dataLayer.push({
  'event': 'video_play',
  'video_title': 'Produktvideo 2025',
  'video_provider': 'youtube',
  'video_percent': 0
});

// CTA-knap klikket
dataLayer.push({
  'event': 'cta_click',
  'cta_text': 'Få et tilbud',
  'cta_location': 'hero_section'
});
```

## Opsæt User-Defined Variables fra Data Layer

For at bruge Data Layer-data i dine tags skal du oprette variabler i GTM.

### Trin-for-trin

1. Gå til **Variables** i GTM
2. Klik **New** under User-Defined Variables
3. Vælg variabeltype: **Data Layer Variable**
4. Udfyld:
   - **Data Layer Variable Name:** Den præcise nøgle fra dit dataLayer.push() (fx `form_id`)
   - **Data Layer Version:** Version 2 (standard)
   - **Set Default Value:** Valgfrit — brug hvis værdien kan mangle
5. Navngiv variablen tydeligt (fx `DLV - form_id`)
6. Gem

### Navngivningskonvention

Brug konsistent navngivning for overblik:

| Præfiks | Type | Eksempel |
|---------|------|----------|
| DLV | Data Layer Variable | DLV - form_id |
| CJS | Custom JavaScript | CJS - page_hostname |
| CEV | Custom Event Variable | CEV - click_text |

## Triggers for custom events

For at fyre et tag når et custom event sker, opretter du en **Custom Event trigger**.

### Opsætning

1. Gå til **Triggers** i GTM
2. Klik **New**
3. Vælg trigger type: **Custom Event**
4. Udfyld:
   - **Event name:** Præcis det event-navn du bruger i `dataLayer.push()` (fx `form_submit`)
   - **Use regex matching:** Kun hvis du vil matche flere events med ét mønster
   - **Fire on:** Alle custom events med det navn, eller tilføj betingelser
5. Navngiv triggeren (fx `CE - form_submit`)
6. Gem

### Betingelser på triggers

Du kan filtrere yderligere med betingelser:

- `form_id equals kontakt-formular` — fyr kun for én specifik formular
- `cta_location contains hero` — fyr kun for CTA'er i hero-sektionen

## GA4 event med Data Layer parametre

Når du har variabler og triggers, kobler du det sammen i et GA4 Event tag.

### Praktisk eksempel: add_to_cart

**Forudsætning:** dataLayer.push() med `add_to_cart` event (se kodeeksempel ovenfor).

1. **Opret Data Layer Variables:**
   - `DLV - ecommerce.currency`
   - `DLV - ecommerce.value`
   - `DLV - ecommerce.items`

2. **Opret trigger:**
   - Type: Custom Event
   - Event name: `add_to_cart`

3. **Opret GA4 Event tag:**
   - Tag type: Google Analytics: GA4 Event
   - Event name: `add_to_cart`
   - Event Parameters:
     - `currency` = `{{DLV - ecommerce.currency}}`
     - `value` = `{{DLV - ecommerce.value}}`
     - `items` = `{{DLV - ecommerce.items}}`
   - Trigger: `CE - add_to_cart`

4. Gem og test

## Tips og best practices

### Test altid i Preview mode

- Klik **Preview** i GTM inden du publicerer
- GTM Tag Assistant åbner i et nyt vindue
- Naviger rundt på sitet og se hvilke tags der fyrer
- Tjek Data Layer-fanen for at se præcis hvad der sendes
- Fejl vises med røde advarsler

### Brug Tag Assistant til debugging

- Tag Assistant viser alle Data Layer events kronologisk
- Klik på et event for at se variabler, triggers og tags
- Tjek at variabelværdier matcher det forventede
- Brug "Values" fanen til at se alle variabler på et givent tidspunkt

### Undgå typiske fejl

- **Forkert event-navn:** GTM er case-sensitive. `form_submit` og `Form_Submit` er to forskellige events
- **Manglende dataLayer.push():** Tagget fyrer ikke hvis eventet aldrig sendes
- **Timing:** Sørg for at `dataLayer.push()` kører FØR GTM-containeren loader, eller brug event-baserede triggers
- **Overskrivning:** Gentagne push() med samme nøgle overskriver tidligere data — brug unikke event-navne
- **Test i incognito:** Undgå at dine egne consent-valg eller browsercache forstyrrer testen
