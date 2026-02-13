# WP Mail SMTP — Opsætning

## Hvad er det

WP Mail SMTP er et plugin der sikrer at emails fra WordPress sendes korrekt via en rigtig SMTP-server eller email-API. Uden dette plugin bruger WordPress PHP `mail()` funktionen, som ofte resulterer i at emails havner i spam eller slet ikke bliver leveret.

## Hvorfor er det nødvendigt

- WordPress' standard PHP `mail()` mangler korrekt autentificering
- Emails fra kontaktformularer, ordrebekræftelser og notifikationer ryger i spam
- Mange hostingservere har begrænset eller deaktiveret PHP mail
- SMTP-levering giver bedre deliverability og fejllogning

## Installation

1. Gå til **Plugins → Tilføj nyt**
2. Søg efter "WP Mail SMTP"
3. Installér og aktivér **WP Mail SMTP by WPForms**
4. Gå til **WP Mail SMTP → Settings** for at konfigurere

## Opsætning — vælg mailer

### Tilgængelige mailere

| Mailer | Pris | Bedst til |
|--------|------|-----------|
| **Other SMTP** | Gratis | Brug eksisterende SMTP-server |
| **SendLayer** | Fra $5/md | Dedikeret email-service |
| **Brevo (Sendinblue)** | Gratis til 300/dag | Gratis løsning med god levering |
| **Gmail / Google Workspace** | Gratis | Google-konti |
| **Outlook / Microsoft 365** | Gratis | M365-konti |
| **Amazon SES** | Pay per use | Store mængder emails |

### Generel SMTP-opsætning
1. Vælg **Other SMTP** under mailer
2. Udfyld:
   - **SMTP Host:** f.eks. `smtp.office365.com` eller `smtp.gmail.com`
   - **Encryption:** TLS (anbefalet) eller SSL
   - **SMTP Port:** 587 (TLS) eller 465 (SSL)
   - **SMTP Username:** emailadresse
   - **SMTP Password:** adgangskode eller app-password
3. Sæt **From Email** til den ønskede afsenderadresse
4. Sæt **From Name** til virksomhedens navn
5. Gem indstillinger

### Microsoft 365 / Outlook opsætning
Denne metode bruger OAuth i stedet for brugernavn/adgangskode:

1. Vælg **Outlook / Microsoft 365** som mailer
2. Du skal oprette en **App Registration** i Azure:
   - Gå til **portal.azure.com → Azure Active Directory → App registrations**
   - Klik **New registration**
   - Navn: "WP Mail SMTP" (eller passende navn)
   - Supported account types: "Accounts in this organizational directory only"
   - Redirect URI: Kopiér fra WP Mail SMTP settings
3. Under App Registration:
   - Kopiér **Application (client) ID** → indsæt i WP Mail SMTP
   - Gå til **Certificates & secrets → New client secret**
   - Kopiér secret value → indsæt i WP Mail SMTP
4. Under **API permissions**:
   - Tilføj **Microsoft Graph → Delegated → Mail.Send**
   - Klik **Grant admin consent**
5. Gem indstillinger i WP Mail SMTP
6. Klik **Authorize** og log ind med M365-kontoen

### Gmail / Google Workspace opsætning
1. Vælg **Gmail / Google Workspace** som mailer
2. Opret OAuth credentials i Google Cloud Console:
   - Opret et projekt
   - Aktivér Gmail API
   - Opret OAuth 2.0 Client ID
3. Indsæt Client ID og Client Secret i WP Mail SMTP
4. Klik **Authorize** og godkend adgangen

## Test email

1. Gå til **WP Mail SMTP → Email Test**
2. Indtast en modtager-emailadresse
3. Klik **Send Test**
4. Tjek at emailen modtages korrekt (også i spam-mappen)
5. Resultatet viser om afsendelsen lykkedes eller fejlede

## Fejlsøgning

### "Could not authenticate" fejl
- Tjek brugernavn og adgangskode
- For Gmail: Brug en **App Password** (ikke den almindelige adgangskode)
- For M365: Kontrollér at OAuth-opsætningen er korrekt
- Tjek at SMTP-porten ikke er blokeret af hosting-firewallet

### Emails havner stadig i spam
- Kontrollér at domænets DNS har korrekte email-records:
  - **SPF** — tillader SMTP-serveren at sende på domænets vegne
  - **DKIM** — digital signatur på emails
  - **DMARC** — politik for håndtering af fejlede emails
- Brug **mail-tester.com** til at tjekke email-score
- Sørg for at From Email matcher domænet

### Test-email fejler med timeout
- SMTP-porten kan være blokeret af hostingudbyderen
- Prøv port 465 (SSL) i stedet for 587 (TLS)
- Kontakt hostingudbyderen og spørg om SMTP er tilgængeligt
- Overvej at skifte til en API-baseret mailer (SendLayer, Brevo)

### OAuth-token udløber (M365/Gmail)
- Tokens skal forny sig automatisk
- Hvis de fejler: Gå til WP Mail SMTP settings og klik **Authorize** igen
- Tjek at Client Secret ikke er udløbet i Azure/Google Console

## Vigtige indstillinger

### From Email og From Name
- **From Email:** Brug en rigtig emailadresse på kundens domæne
- **From Name:** Virksomhedens navn
- **Force From Email:** Aktivér hvis andre plugins overskriver afsenderadressen
- **Force From Name:** Aktivér for konsistent afsendernavn

### Email Logging (Pro)
- Logfører alle afsendte emails
- Nyttigt til fejlsøgning og dokumentation
- Viser status (leveret/fejlet) og indhold

## Bemærkninger

- WP Mail SMTP er kritisk for pålidelig email-levering
- Opsæt det som noget af det første på en ny WordPress-installation
- OAuth-metoden (M365/Gmail) er mere sikker end brugernavn/adgangskode
- Husk at opsætte SPF, DKIM og DMARC i DNS for bedst mulig levering
- Test emaillevering efter enhver hostingmigration eller DNS-ændring
- Brevo er et godt gratis alternativ hvis SMTP er blokeret af hostingudbyderen
