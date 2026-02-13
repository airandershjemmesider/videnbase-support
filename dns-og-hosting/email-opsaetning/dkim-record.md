# Opsæt DKIM Record (DomainKeys Identified Mail)

## Problem

Emails fra dit domæne mangler digital signatur, hvilket gør det sværere for modtagere at verificere at emailen faktisk kommer fra dig og ikke er forfalsket.

## Hvad er DKIM?

DKIM tilføjer en **kryptografisk signatur** til hver email du sender. Modtageren kan verificere signaturen mod en offentlig nøgle i din DNS. Det beviser at emailen ikke er ændret undervejs og faktisk er sendt fra en autoriseret server.

## Løsning

### Trin 1: Generer DKIM-nøgle hos din email-udbyder

DKIM-nøglen genereres af den tjeneste der sender din email.

#### Microsoft 365
1. Gå til Microsoft 365 Defender → Policies → DKIM
2. Vælg dit domæne
3. Microsoft giver dig **2 CNAME-records** at oprette:
   - `selector1._domainkey.example.dk`
   - `selector2._domainkey.example.dk`

#### Google Workspace
1. Gå til Google Admin → Apps → Google Workspace → Gmail → Authenticate email
2. Klik "Generate new record"
3. Vælg DKIM key bit length (2048 anbefalet)
4. Google giver dig en **TXT-record** at oprette

#### Mailchimp
1. Gå til Account → Domains → Authenticate
2. Mailchimp giver dig en CNAME-record til DKIM

### Trin 2: Opret DNS-record

**For Microsoft 365 (CNAME):**
- **Navn:** `selector1._domainkey`
- **Type:** CNAME
- **Værdi:** `selector1-example-dk._domainkey.example.onmicrosoft.com`

**For Google Workspace (TXT):**
- **Navn:** `google._domainkey`
- **Type:** TXT
- **Værdi:** Den lange nøgle Google genererede (starter med `v=DKIM1; k=rsa; p=...`)

### Trin 3: Aktivér DKIM hos email-udbyderen

- **Microsoft 365:** Gå tilbage til DKIM-indstillingerne og slå DKIM til
- **Google Workspace:** Klik "Start authentication" efter DNS-recorden er oprettet
- Vent 15-60 minutter på DNS propagation inden aktivering

### Trin 4: Verificer

Tjek din DKIM-record:
```
nslookup -type=TXT selector1._domainkey.example.dk
```

Eller brug: **mxtoolbox.com/dkim.aspx**

Send en test-email til **mail-tester.com** — den viser om DKIM er korrekt.

## Sådan virker DKIM

1. Afsenderserveren signerer emailen med en **privat nøgle**
2. Den offentlige nøgle ligger i DNS som TXT/CNAME-record
3. Modtagerserveren henter den offentlige nøgle fra DNS
4. Signaturen verificeres — matcher den, er emailen ægte

## Bemærkninger

- DKIM-nøglen er specifik per afsender-tjeneste. Hvis du bruger både M365 og Mailchimp, skal begge have deres egen DKIM-record
- Brug **2048-bit nøgler** hvor muligt (mere sikker end 1024-bit)
- Nogle DNS-udbydere har en grænse på TXT-record længde. Hvis nøglen er for lang, split den i to strenge
- DKIM kræver IKKE ændringer i eksisterende SPF-record — det er en separat mekanisme
- Kombiner SPF + DKIM + DMARC for bedst mulig email-sikkerhed
