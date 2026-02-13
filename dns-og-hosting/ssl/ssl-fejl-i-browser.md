# SSL-fejl i browseren — Fejlsøgning

## Problem

Besøgende ser en advarsel eller fejlside i browseren når de besøger din hjemmeside. Typiske fejlmeddelelser:

- "Din forbindelse er ikke privat"
- "NET::ERR_CERT_DATE_INVALID"
- "NET::ERR_CERT_AUTHORITY_INVALID"
- "NET::ERR_CERT_COMMON_NAME_INVALID"
- "SSL_ERROR_BAD_CERT_DOMAIN"

## Løsning: Identificer og løs fejlen

### Fejl: Certifikatet er udløbet (ERR_CERT_DATE_INVALID)

**Årsag:** SSL-certifikatet er ikke fornyet i tide.

**Løsning:**
1. Log ind på hosting-kontrolpanelet
2. Gå til SSL/certifikat-indstillinger
3. Forny eller geninstaller certifikatet
4. Hvis Let's Encrypt: Kør `sudo certbot renew` eller tjek at automatisk fornyelse virker
5. Tjek at serverens ur/dato er korrekt (forkert tid = fornyelse fejler)

### Fejl: Ukendt certifikatudsteder (ERR_CERT_AUTHORITY_INVALID)

**Årsag:** Certifikatet er selvsigneret eller udstedt af en CA som browseren ikke kender.

**Løsning:**
1. Brug et certifikat fra en anerkendt CA (Let's Encrypt er gratis og anerkendt)
2. Tjek at hele certifikatkæden er installeret (root + intermediate + certifikat)
3. Test med **ssllabs.com/ssltest/** — den viser om kæden er ufuldstændig

### Fejl: Domænet matcher ikke (ERR_CERT_COMMON_NAME_INVALID)

**Årsag:** Certifikatet er udstedt til et andet domæne end det browseren besøger.

**Løsning:**
1. Tjek hvilke domæner certifikatet dækker:
   - Klik på hængelåsen i browseren → "Certifikat" → se "Subject" og "SAN"
2. Generer et nyt certifikat der inkluderer det korrekte domæne
3. Husk at inkludere BÅDE `example.dk` og `www.example.dk`

### Fejl: Redirect-loop (ERR_TOO_MANY_REDIRECTS)

**Årsag:** Serveren hopper mellem HTTP og HTTPS i en uendelig loop.

**Løsning:**
1. **Cloudflare:** Sæt SSL-mode til "Full (Strict)" i stedet for "Flexible"
2. **WordPress:** Tjek at Site URL og WordPress URL begge bruger `https://`
3. **Nginx/Apache:** Tjek at redirect-regler ikke konflikter
4. Ryd browser-cache og cookies for domænet

### Fejl: Forbindelsen blev afbrudt (ERR_SSL_PROTOCOL_ERROR)

**Årsag:** SSL-konfigurationen på serveren er forkert.

**Løsning:**
1. Tjek at SSL-certifikatet er korrekt installeret
2. Tjek at port 443 er åben i firewall
3. Tjek at webserveren (Apache/Nginx) lytter på port 443
4. Test konfigurationen med **ssllabs.com/ssltest/**

### Fejl: Blandet indhold (Mixed Content)

Ikke en SSL-fejl som sådan, men hængelåsen vises ikke korrekt:
- Se mixed-content.md for løsning

## Diagnosticeringsværktøjer

| Værktøj | URL | Hvad det tjekker |
|---------|-----|------------------|
| SSL Labs | ssllabs.com/ssltest/ | Fuld SSL-analyse og scoring |
| Why No Padlock | whynopadlock.com | Mixed content og certifikat |
| SSL Checker | sslshopper.com/ssl-checker.html | Certifikatkæde og udløb |

## Hurtig fejlsøgning via kommandolinje

Tjek certifikatdetaljer:
```
openssl s_client -connect example.dk:443 -servername example.dk
```

Tjek udløbsdato:
```
openssl s_client -connect example.dk:443 -servername example.dk 2>/dev/null | openssl x509 -noout -dates
```

## Bemærkninger

- **Ryd browser-cache** som første skridt — browseren kan cache gamle certifikater
- Test altid i **inkognito-vindue** for at undgå cache-problemer
- SSL Labs giver en score fra A+ til F — sigter efter mindst A
- Husk at tjekke BÅDE `example.dk` og `www.example.dk` — de kan have forskellige certifikater
- Nogle antivirusprogrammer (Avast, Kaspersky) kan forstyrre SSL — test med antivirus deaktiveret
