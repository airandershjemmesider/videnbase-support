# Elementor Pro formular problemer

## Problem

Elementor Pro formularer sender ikke emails, notifikationer går i spam, submissions gemmes ikke, eller reCAPTCHA/redirect virker ikke.

## Løsning

### Formularer sender ikke email

WordPress bruger som standard `wp_mail()` via PHP `mail()`, som ofte blokeres af hosting.

**Løsning — installér SMTP-plugin:**

1. Installér **WP Mail SMTP** (eller FluentSMTP)
2. Konfigurér med din email-udbyders SMTP-indstillinger
3. Send en test-email fra plugin'ets indstillinger
4. Test formularen igen

**Typiske SMTP-indstillinger:**

| Udbyder | Server | Port | Kryptering |
|---------|--------|------|------------|
| Gmail | smtp.gmail.com | 587 | TLS |
| Outlook/365 | smtp.office365.com | 587 | TLS |
| Custom | Spørg hosting | 587 | TLS |

### Notifikationer går i spam

Selv med SMTP kan emails lande i spam. Opsæt disse DNS-records:

- **SPF** — fortæller modtageren hvilke servere der må sende email fra dit domæne
- **DKIM** — digital signatur der beviser emailen er ægte
- **DMARC** — politik for hvad der sker med fejlede emails

Tjek din opsætning med [mail-tester.com](https://www.mail-tester.com) eller MXToolbox.

**Derudover:**
- Brug en afsender-adresse der matcher dit domæne (ikke @gmail.com)
- Undgå spam-ord i email-emnelinjen

### Submissions gemmes ikke

1. Tjek at **Submissions** er aktiveret: Gå til formular-widgeten → **Actions After Submit** → tilføj **Collect Submissions**
2. Se submissions under **Elementor → Submissions**
3. Tjek at databasen har plads og ikke er korrupt
4. Tjek PHP error-log for database-fejl

### reCAPTCHA virker ikke

1. Gå til **Elementor → Settings → Integrations**
2. Tjek at **reCAPTCHA Site Key** og **Secret Key** er korrekte
3. Tjek at nøglerne matcher den rigtige reCAPTCHA-version:
   - **reCAPTCHA v2** — checkbox "I'm not a robot"
   - **reCAPTCHA v3** — usynlig scoring
4. Tjek at dit domæne er registreret i Google reCAPTCHA admin
5. Ryd cache efter ændring af nøgler

**"ERROR for site owner: Invalid key type"** — du bruger v2-nøgler i v3-feltet (eller omvendt). Generér nye nøgler til den korrekte version.

### Redirect efter submit virker ikke

1. Tjek at **Redirect** er tilføjet i **Actions After Submit**
2. Brug **fuld URL** inklusiv `https://` (f.eks. `https://ditsite.dk/tak/`)
3. Tjek at redirect-siden eksisterer og ikke giver 404
4. Hvis redirect ignoreres: tjek browser-konsollen for JavaScript-fejl
5. Deaktivér cache-plugins midlertidigt og test igen

### Formular-felter vises ikke korrekt

1. Regenerér CSS under **Elementor → Tools**
2. Tjek for CSS-konflikter med temaet
3. Prøv med et standard-tema (Hello Elementor) for at udelukke tema-konflikter

## Bemærkninger

- SMTP er praktisk talt et krav for pålidelig email-afsendelse fra WordPress
- Elementor Submissions kræver Elementor Pro 3.4+
- reCAPTCHA v3 er brugervenligst (ingen checkbox), men kræver tuning af score-tærsklen
- Test altid formularer efter opsætning — send til en rigtig email-adresse og tjek at alt kommer frem
