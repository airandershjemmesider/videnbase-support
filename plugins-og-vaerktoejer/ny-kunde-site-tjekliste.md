# Ny kunde site — Komplet opsætningstjekliste

## Formål

Denne tjekliste dækker ALT der skal opsættes når en ny kundes hjemmeside går live. Følg trinene i rækkefølge — nogle afhænger af hinanden.

---

## Fase 0: Kundeinfo og server

Udfyld FØRST — det styrer resten af tjeklisten:

- [ ] **Domæne:** ____________________
- [ ] **Hosting:** WHM/cPanel server / Managed WP / Andet: ________
- [ ] **SEO-pakke:** ☐ Ja → udfør Fase 4 komplet ☐ Nej → spring Fase 4 over (undtagen sitemap)
- [ ] **Email-løsning:** ☐ M365 ☐ Google Workspace ☐ cPanel email ☐ Andet
- [ ] **Sociale medier:** ☐ Instagram ☐ Facebook ☐ YouTube ☐ Ingen feeds

### Hvis WHM/cPanel server:
- [ ] **Opret cPanel-konto** i WHM (Account Functions → Create New Account)
- [ ] **DNS zone** → Oprettet automatisk ved kontoen, men tjek A-record peger korrekt
- [ ] **PHP version** → MultiPHP Manager → Vælg 8.2+ for domænet
- [ ] **PHP indstillinger** → MultiPHP INI Editor:
  - `memory_limit` = 256M
  - `upload_max_filesize` = 64M
  - `max_execution_time` = 300
  - `post_max_size` = 64M
- [ ] **AutoSSL** → Tjek at SSL er aktivt (SSL/TLS Status)
- [ ] **Installér WordPress** → Softaculous eller manuelt

> Se: `dns-og-hosting/whm-cpanel/` mappen

---

## Fase 1: WordPress grundopsætning

- [ ] **WordPress sprog** → Indstillinger → Generelt → Dansk
- [ ] **Tidszone** → Europe/Copenhagen (UTC+1)
- [ ] **Datoformat** → j. F Y (dansk: "13. februar 2026")
- [ ] **Tidsformat** → H:i (24-timers)
- [ ] **Ugestart** → Mandag
- [ ] **Permalinks** → Indstillinger → Permalinks → "Indlægsnavn" (`/%postname%/`)
- [ ] **Fjern standard-indhold** → Slet "Hello World" indlæg, eksempelside, standard-kommentar
- [ ] **Brugerroller** → Opret kunden som "Redaktør" (ikke Admin)
- [ ] **Admin konto** → Stærkt password, evt. 2FA

> Se: `wordpress/admin/wordpress-dansk-opsaetning.md` og `wordpress/admin/bruger-roller.md`

---

## Fase 2: Sikkerhed (FØR lancering!)

- [ ] **Wordfence** → Installér og aktivér
  - [ ] Firewall → Learning Mode → skift til "Enabled" efter 1 uge
  - [ ] Login Security → Aktivér 2FA for admin-brugere
  - [ ] Scan → Kør første scan
- [ ] **Brute force** → Limit login attempts (via Wordfence)
- [ ] **Opdatér PHP** → Minimum 8.1, helst 8.2+ (tjek hos hosting)
- [ ] **SSL** → Bekræft at HTTPS virker og HTTP redirecter til HTTPS
- [ ] **WordPress hærdning** → Deaktivér fil-redigering, skjul version

> Se: `wordpress/sikkerhed/` mappen

---

## Fase 3: Performance

- [ ] **WP Rocket** → Installér og aktivér
  - [ ] Cache → Aktivér caching
  - [ ] File Optimization → Minify CSS og JS
  - [ ] LazyLoad → Aktivér for billeder og iframes
  - [ ] Preloading → Aktivér sitemap-baseret preload
  - [ ] Database → Ryd transients og revisioner
  - [ ] CDN → Opsæt hvis kunden bruger CDN
- [ ] **Billeder** → Konverter til WebP (ShortPixel, Imagify eller Smush)
- [ ] **Test hastighed** → GTmetrix + PageSpeed Insights

> Se: `plugins-og-vaerktoejer/wordpress-plugins/wp-rocket-opsaetning.md`

---

## Fase 4: SEO ⚠️ Kun hvis kunden har SEO-pakke (se Fase 0)

> **Uden SEO-pakke:** Installér stadig RankMath (grundopsætning + sitemap), men spring Search Console, Analytics og Tag Manager over.

- [ ] **RankMath** → Installér og kør setup wizard
  - [ ] Site type og business info
  - [ ] Titles & Meta → Standardtitler og -beskrivelser
  - [ ] Sitemap → Aktivér og tjek at den virker (`/sitemap.xml`)
  - [ ] Schema → LocalBusiness for lokale virksomheder
- [ ] **Google Search Console** → Tilføj property
  - [ ] Verificér via DNS TXT record
  - [ ] Indsend sitemap.xml
- [ ] **Google Analytics 4** → Opret property, få Measurement ID
- [ ] **Google Tag Manager** → Opret container
  - [ ] Installér GTM på WordPress (GTM4WP plugin eller manuelt)
  - [ ] Tilføj GA4 tag via GTM
  - [ ] Opsæt Consent Mode (til Complianz)

> Se: `plugins-og-vaerktoejer/wordpress-plugins/rankmath-opsaetning.md` og `plugins-og-vaerktoejer/online-vaerktoejer/` mappen

---

## Fase 5: GDPR / Cookie consent

- [ ] **Complianz** → Installér og kør wizard
  - [ ] Region → EU
  - [ ] Sprog → Dansk
  - [ ] Kør cookie scan
  - [ ] Gennemgå og kategorisér fundne cookies
  - [ ] Tilpas cookie banner (farver, tekst, position)
  - [ ] Aktivér Google Consent Mode v2
- [ ] **Privatlivspolitik** → Generer via Complianz eller lav custom
- [ ] **Cookie-erklæring** → Tilføj side med cookie-oversigt

> Se: `plugins-og-vaerktoejer/wordpress-plugins/complianz-opsaetning.md` og `complianz-consent-mode.md`

---

## Fase 6: Email

- [ ] **WP Mail SMTP** → Installér og opsæt
  - [ ] Vælg mailer (SMTP, SendLayer, eller M365)
  - [ ] Send testmail — bekræft at den ankommer
- [ ] **DNS email records** (hos kundens DNS-udbyder):
  - [ ] SPF record
  - [ ] DKIM record
  - [ ] DMARC record
  - [ ] MX records (hvis M365 eller Google Workspace)

> Se: `plugins-og-vaerktoejer/wordpress-plugins/wp-mail-smtp-opsaetning.md` og `dns-og-hosting/email-opsaetning/` mappen

---

## Fase 7: Indhold og sociale medier

- [ ] **Smash Balloon** → Hvis kunden vil vise sociale feeds
  - [ ] Forbind Instagram/Facebook konto
  - [ ] Vælg feed-type og styling
  - [ ] Husk GDPR: Feeds kræver cookie consent
- [ ] **Kontaktformular** → Elementor Form eller Contact Form 7
  - [ ] Test at formularer sender korrekt
  - [ ] Opsæt notifikationer til kunden
  - [ ] reCAPTCHA eller honeypot mod spam

---

## Fase 8: Backup og vedligeholdelse

- [ ] **Backup** → UpdraftPlus eller hostingens backup
  - [ ] Daglig automatisk backup
  - [ ] Backup til ekstern lokation (Google Drive, Dropbox)
  - [ ] Test gendannelse mindst én gang
- [ ] **Opdateringsstrategi** → Aftal med kunden
  - [ ] Automatiske minor-opdateringer (WordPress core)
  - [ ] Manuelle major-opdateringer (test først)
  - [ ] Plugin-opdateringer: Månedligt eller efter behov

> Se: `wordpress/admin/wordpress-backup.md` og `wordpress/admin/wordpress-opdateringer.md`

---

## Fase 9: Lanceringstjek

- [ ] **Alle sider** → Gennemgå for stavefejl, manglende billeder, broken links
- [ ] **Mobil** → Test alle sider på mobil
- [ ] **Formularer** → Test ALLE formularer (send testbesked)
- [ ] **Hastighed** → GTmetrix score + PageSpeed score (gem som baseline)
- [ ] **SEO** → Alle sider har meta-titel og -beskrivelse
- [ ] **Favicon** → Er der et favicon?
- [ ] **404-side** → Virker 404-siden korrekt?
- [ ] **Robots.txt** → Tillader indeksering (ingen "Disallow: /")
- [ ] **Search Console** → Ingen fejl i dækning
- [ ] **Analytics** → Verificér at data registreres (Realtime-rapport)

---

## Fase 10: Overdragelse til kunden

- [ ] **Login-info** → Send til kunden (sikkert, IKKE i ren email)
- [ ] **Hurtigguide** → Vis kunden hvordan de redigerer indhold
- [ ] **Support-aftale** → Afklar vedligeholdelse og support-omfang
- [ ] **Dokumentér** → Noter alle logins, plugins, DNS-opsætning et centralt sted

---

## Bemærkninger

- Denne tjekliste er en **rækkefølge** — følg den fra top til bund
- Spring trin over der ikke er relevante for kunden (f.eks. Smash Balloon hvis ingen sociale feeds)
- **Tag backup FØR hver større ændring** (plugin-installation, opdatering, tema-skift)
- Gem denne tjekliste som reference — kopiér den til et nyt dokument per kunde hvis nødvendigt
