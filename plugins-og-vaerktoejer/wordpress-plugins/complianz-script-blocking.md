# Complianz — Script blocking og integrations

## Oversigt

Complianz er et GDPR/ePrivacy cookie-consent plugin til WordPress. Det håndterer automatisk blokering af tredjepartsscripts indtil brugeren giver samtykke. Denne guide dækker hvordan script-blocking fungerer, hvad der auto-blokeres, og hvad du skal håndtere manuelt.

## Auto-blokerede tjenester vs. manuelle

Complianz scanner dit site og genkender mange populære tjenester automatisk. Men ikke alt fanges.

| Tjeneste | Auto-blokering | Manuel tjek nødvendig | Bemærkninger |
|----------|---------------|----------------------|--------------|
| Google Analytics 4 (GA4) | Ja | Ja, ved GTM setups | gtag.js blokeres automatisk. Ved GTM-opsætning: tjek at GA4-tags inde i GTM også respekterer consent |
| Meta Pixel (Facebook) | Ja | Ja, ved custom scripts | Standardpixel fanges. Custom events via manuel kode skal tjekkes separat |
| YouTube embeds | Ja | Nej | Viser placeholder med consent-knap. Understøtter no-cookie embed URL |
| Vimeo embeds | Ja | Nej | Samme placeholder-løsning som YouTube |
| Hotjar | Ja | Nej | Session recording kræver consent i kategorien "statistics" |
| HubSpot | Ja | Nej | Chat widget og tracking blokeres. Tjek at forms også respekterer consent |
| Google Maps embeds | Ja | Nej | Viser placeholder med kort-ikon |
| Elementor custom HTML | Nej | Ja | Scripts i HTML widgets scannes ikke — skal håndteres manuelt |
| WPBakery custom code | Nej | Ja | Samme som Elementor — manuelt |
| Inline JavaScript | Nej | Ja | Script-tags i header/footer via temaet scannes sjældent korrekt |
| Tredjepartsformularer (Typeform, Jotform) | Delvist | Ja | Embeds kan fanges, men API-kald inde i formularen kontrolleres ikke |

## Content Blocker

Content Blocker er Complianz' funktion til at blokere embeds (iframes) indtil brugeren giver samtykke.

### Sådan virker det

1. Complianz erstatter `<iframe>` med en placeholder
2. Placeholderen viser en besked om, at indholdet kræver samtykke
3. Brugeren klikker "Acceptér" eller giver samtykke via cookie-banneret
4. Det originale embed indlæses

### Konfiguration

- Gå til **Complianz > Integrations > Content Blocker**
- Aktivér/deaktivér blokering per tjeneste
- Tilpas placeholder-tekst og styling
- Vælg om placeholder skal vise preview-billede (YouTube thumbnails)

### Typiske tjenester der bruger Content Blocker

- YouTube og Vimeo videoer
- Google Maps
- Social media embeds (Facebook, Instagram, Twitter)
- Tredjepartsformularer

## Script Center

Script Center giver dig fuld kontrol over hvilke scripts der blokeres, og i hvilken consent-kategori de hører til.

### Consent-kategorier

| Kategori | Beskrivelse | Eksempler |
|----------|-------------|-----------|
| Functional | Nødvendige for sidens drift | WordPress session cookies |
| Statistics | Anonymiseret tracking | GA4, Hotjar |
| Marketing | Annoncering og retargeting | Meta Pixel, Google Ads remarketing |
| Preferences | Brugerpræferencer | Sprogvalg, layout-indstillinger |

### Tilføj et script manuelt

1. Gå til **Complianz > Integrations > Script Center**
2. Klik **Add Script**
3. Udfyld:
   - **Navn:** Beskrivende navn (fx "Custom Facebook Event")
   - **Script URL eller snippet:** Indsæt URL eller inline script
   - **Kategori:** Vælg den korrekte consent-kategori
   - **Placering:** Header, body eller footer
4. Gem og test

### Blokér et script via attribut

Du kan også blokere scripts direkte i HTML med Complianz' data-attributter:

```html
<script type="text/plain" data-category="statistics" data-service="google-analytics">
  // Dit script her — indlæses først efter consent
</script>
```

**Vigtigt:** `type="text/plain"` forhindrer browseren i at køre scriptet. Complianz ændrer det til `text/javascript` efter consent.

## Re-scan — glem det aldrig

Complianz scanner dit site for cookies og scripts. Men scanningen sker ikke automatisk efter ændringer.

### Hvornår skal du re-scanne?

- Efter installation af nyt plugin
- Efter tilføjelse af nye scripts (GTM tags, custom code)
- Efter ændring af tema
- Efter tilføjelse af nye embeds (YouTube, Maps, formularer)
- Mindst én gang om måneden som standard vedligeholdelse

### Sådan re-scanner du

1. Gå til **Complianz > Wizard > Cookies**
2. Klik **Scan again**
3. Vent til scanningen er færdig
4. Gennemgå resultaterne — tjek at nye cookies/scripts er kategoriseret korrekt
5. Gem og opdatér cookie-erklæringen

## Typiske fejl og faldgruber

### 1. Over-tillid til auto-scan

Auto-scan fanger de mest populære tjenester, men den er ikke perfekt. Custom kode, nyere plugins og atypiske implementeringer bliver ofte overset. **Tjek altid manuelt** at alle scripts blokeres korrekt.

### 2. Glemmer custom code i Elementor/WPBakery

HTML-widgets med tracking-scripts scannes ikke. Tilføj dem manuelt i Script Center, eller brug `type="text/plain"` med data-attributter.

### 3. GTM-scripts der omgår consent

Hvis du bruger Google Tag Manager, skal du sikre at:

- Complianz blokerer GTM-containeren indtil consent
- ELLER du bruger GTM's built-in consent mode (recommended)
- Tags inde i GTM respekterer consent-signalet

### 4. Glemmer re-scan efter ændringer

Nye plugins tilføjer ofte cookies og scripts. Uden re-scan ved Complianz ikke at de eksisterer, og de blokeres ikke.

### 5. Forkert consent-kategori

Et marketing-script i "statistics"-kategorien overtræder GDPR. Dobbelttjek altid kategoriseringen.

## Hurtig tjekliste

- [ ] Auto-scan kørt og gennemgået
- [ ] Custom scripts tilføjet manuelt i Script Center
- [ ] Content Blocker aktiv for alle embeds
- [ ] GTM consent mode konfigureret korrekt
- [ ] Cookie-erklæring opdateret
- [ ] Test: Besøg sitet i incognito og tjek at scripts først loader efter consent
- [ ] Re-scan planlagt som månedlig opgave
