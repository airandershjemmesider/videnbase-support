# Google Tag Manager (GTM)

## Hvad er det

Google Tag Manager er et gratis tag management system fra Google. Det gør det muligt at tilføje og administrere tracking-koder (tags) på en hjemmeside uden at redigere kildekoden. Alt styres fra et webinterface med tags, triggers og variabler.

## Opsætning

### Opret GTM container

1. Gå til [tagmanager.google.com](https://tagmanager.google.com)
2. Log ind med kundens Google-konto
3. Klik **Create Account**
4. Udfyld kontonavn (kundens navn) og containernavn (kundens domæne)
5. Vælg **Web** som målplatform
6. Acceptér servicevilkår
7. Du får to kode-snippets: én til `<head>` og én til `<body>`

### Installer på WordPress

**Metode 1: Plugin (anbefalet)**
1. Installer plugin: **GTM4WP** (Google Tag Manager for WordPress)
2. Gå til **Indstillinger → Google Tag Manager**
3. Indtast container-ID (format: `GTM-XXXXXXX`)
4. Vælg placeringsmetode: "Custom" (footer + codeless injection) eller "Off" med manuelt snippet
5. Gem

**Metode 2: Manuelt**
1. Indsæt første snippet i `<head>` (via child theme functions.php eller Customizer)
2. Indsæt andet snippet lige efter `<body>`
3. Mindre anbefalet da det kræver kodeændringer

### Verificér installation

1. Gå til GTM → klik **Preview**
2. Indtast kundens URL
3. Tag Assistant åbner — bekræft at GTM-containeren er fundet
4. Tjek at "Container Found" vises og at tags fyrer korrekt

## Daglig brug

### Grundlæggende struktur

- **Tags** — hvad der skal eksekveres (fx GA4 tracking, Facebook Pixel, custom scripts)
- **Triggers** — hvornår tags skal fyre (fx alle sidevisninger, klik på knap, formular sendt)
- **Variables** — data der bruges af tags og triggers (fx side-URL, klik-tekst, dataLayer-variabler)

### Standard GA4 opsætning

1. Klik **Tags** → **New**
2. Vælg tag-type: **Google Analytics: GA4 Configuration**
3. Indtast Measurement ID (`G-XXXXXXXXXX`)
4. Trigger: **All Pages**
5. Gem og navngiv tagget (fx "GA4 - Configuration")
6. Klik **Submit** → **Publish** for at aktivere

### Facebook Pixel via GTM

1. Klik **Tags** → **New**
2. Vælg **Custom HTML**
3. Indsæt Facebook Pixel base-kode
4. Trigger: **All Pages**
5. Opret separate tags for specifikke events (Purchase, Lead, etc.)

### Consent Mode

- Integrer med Complianz, CookieYes eller lignende consent-plugin
- Tags kan sættes til at kræve consent før de fyrer
- Built-in consent: GA4 tags har consent-indstillinger direkte i GTM
- Se pluginnets dokumentation for præcis GTM-integration

## Fejlsøgning

### Tags fyrer ikke

1. **Tjek triggers** — er triggeren sat korrekt? Brug Preview mode til at se hvilke triggers der aktiveres
2. **Tjek consent** — er tagget blokeret af consent mode?
3. **Tjek at containeren er publiceret** — ændringer i GTM kræver **Submit → Publish**
4. **Tjek GTM installation** — er snippets korrekt indsat? Brug Tag Assistant

### Dobbelt-tracking

- Symptom: Alle tal i GA4 er fordoblet
- Årsag: GA4 er installeret både via GTM OG direkte (plugin eller kode)
- Løsning: Fjern direkte installation — brug KUN GTM til GA4

### Preview mode virker ikke

- Ryd browser-cache og cookies
- Deaktivér ad blockers midlertidigt
- Prøv i incognito-vindue
- Tjek at popups ikke er blokeret

## Bemærkninger

- **Publicér altid** efter ændringer — draft-tilstand er kun synlig i Preview
- Brug **Workspaces** hvis flere personer arbejder i samme container
- Opret en **Version** med beskrivelse ved hver publicering for nem rollback
- GTM har et **versionerings-system** — du kan altid rulle tilbage til en tidligere version
- Hold containeren organiseret med konsistent navngivning (fx "GA4 - Event - Scroll", "FB - PageView")
- Undgå at bruge Custom HTML tags til ting der har dedikerede tag-typer
- GTM Debug-konsollen i Preview mode viser præcis hvilke tags der fyrer og hvornår
