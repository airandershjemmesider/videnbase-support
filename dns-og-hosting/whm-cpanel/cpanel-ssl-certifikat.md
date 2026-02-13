# SSL-certifikat i cPanel

## Hvad er det

SSL (Secure Sockets Layer) krypterer trafikken mellem besøgendes browser og serveren. Det vises som hængelåsen og `https://` i adresselinjen. Uden SSL viser browsere "Ikke sikker"-advarsler.

## AutoSSL (gratis Let's Encrypt)

### Sådan fungerer det
- cPanel installerer automatisk gratis Let's Encrypt-certifikater via AutoSSL
- Certifikater fornyes automatisk hver 60-90 dag
- Dækker hoveddomæne, www-version og mail-subdomæne

### Tjek AutoSSL-status
1. Log ind på cPanel
2. Gå til **Security → SSL/TLS Status**
3. Grøn lås = certifikat installeret og gyldigt
4. Rød/gul = problem med certifikatet

### Kør AutoSSL manuelt
- I cPanel: **SSL/TLS Status → Run AutoSSL**
- I WHM: **SSL/TLS → Manage AutoSSL → Run AutoSSL for en specifik bruger**

## Force HTTPS (omdiriger HTTP til HTTPS)

### Via .htaccess
Tilføj øverst i `.htaccess` i `public_html`:

```apache
RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

### Via WordPress
- Installér plugin: **Really Simple SSL** (aktivér og det klarer resten)
- Eller manuelt: Ændr WordPress Address og Site Address i **Indstillinger → Generelt** til `https://`

## Fejlsøgning

### "AutoSSL DCV check failed"
- **Årsag:** DNS peger ikke til serveren, eller domænet er bag en proxy (f.eks. Cloudflare)
- **Løsning:** Tjek at A-record peger til serverens IP. Hvis Cloudflare: sæt midlertidigt til "DNS only" (grå sky)

### "SSL certificate is expired"
- Kør AutoSSL manuelt
- Tjek at domænet stadig peger til serveren
- Tjek WHM → Manage AutoSSL for fejlbeskeder

### "Mixed content" advarsler
- Siden loader HTTP-ressourcer (billeder, scripts) på en HTTPS-side
- Løsning i WordPress: Brug **Better Search Replace** plugin til at erstatte `http://` med `https://` i databasen

## Manuelt certifikat (købt)

Bruges kun hvis kunden har købt et certifikat (f.eks. Wildcard eller EV):

1. Gå til **Security → SSL/TLS → Install and Manage SSL**
2. Indsæt:
   - **Certificate (CRT):** Certifikatet fra udbyderen
   - **Private Key (KEY):** Den private nøgle
   - **Certificate Authority Bundle (CA):** Mellemliggende certifikat
3. Klik **Install Certificate**

## Bemærkninger

- AutoSSL dækker de fleste behov — købt certifikat er sjældent nødvendigt
- Wildcard-certifikater (`*.domæne.dk`) kræver DNS-validering og kan ikke udstedes af AutoSSL
- EV-certifikater (Extended Validation) med grøn adresselinje er udgået i moderne browsere
- Tjek altid at **alle** domæner/subdomæner peger til serveren, ellers fejler AutoSSL for dem
