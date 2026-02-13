# Opsæt gratis SSL med Let's Encrypt

## Problem

Du har brug for et SSL-certifikat til din hjemmeside, men vil ikke betale for det.

## Hvad er Let's Encrypt?

Let's Encrypt er en gratis, automatisk Certificate Authority (CA). De udsteder DV-certifikater (Domain Validation) der er anerkendt af alle browsere. Certifikaterne udløber efter 90 dage, men fornyes automatisk.

## Løsning

### Via hosting-kontrolpanel (nemmest)

De fleste hosting-udbydere har Let's Encrypt integreret:

#### cPanel
1. Log ind på cPanel
2. Gå til "SSL/TLS" eller "Let's Encrypt SSL"
3. Vælg dit domæne
4. Klik "Issue" eller "Udsted certifikat"
5. Certifikatet installeres og fornyes automatisk

#### Plesk
1. Log ind på Plesk
2. Gå til "Websites & Domains" → dit domæne
3. Klik "SSL/TLS Certificates"
4. Klik "Install" under Let's Encrypt
5. Vælg om www-subdomæne skal inkluderes
6. Klik "Install"

#### Simply.com
1. Log ind → Kontrolpanel
2. Vælg domænet
3. Gå til "SSL-certifikat"
4. Let's Encrypt er typisk allerede aktiveret

#### one.com
1. Log ind → Kontrolpanel
2. SSL er typisk aktiveret automatisk for alle domæner

#### Cloudflare
1. Log ind → vælg dit domæne
2. Gå til "SSL/TLS"
3. Vælg "Full (Strict)" under encryption mode
4. Cloudflare udsteder automatisk et Universal SSL-certifikat

### Via kommandolinje (VPS/egen server)

#### Certbot (Ubuntu/Debian + Nginx)
```bash
sudo apt update
sudo apt install certbot python3-certbot-nginx
sudo certbot --nginx -d example.dk -d www.example.dk
```

#### Certbot (Ubuntu/Debian + Apache)
```bash
sudo apt update
sudo apt install certbot python3-certbot-apache
sudo certbot --apache -d example.dk -d www.example.dk
```

Certbot opsætter automatisk fornyelse via systemd timer.

#### Test automatisk fornyelse
```bash
sudo certbot renew --dry-run
```

### Trin efter installation

1. **Tving HTTPS:** Sørg for at al trafik redirectes fra HTTP til HTTPS

   WordPress — tilføj i `wp-config.php`:
   ```php
   define('FORCE_SSL_ADMIN', true);
   ```

   Opdater også Site URL og WordPress URL i Indstillinger → Generelt til `https://`

2. **Tjek mixed content:** Se mixed-content.md

3. **Verificer certifikatet:**
   - Besøg sitet — tjek hængelås-ikonet
   - Brug **ssllabs.com/ssltest/** for en detaljeret test

## Fejlsøgning

### "Let's Encrypt kan ikke verificere domænet"
- Tjek at A-record peger til den server du installerer på
- Tjek at port 80 er åben (Let's Encrypt bruger HTTP-01 challenge)
- Tjek at `.well-known/acme-challenge/` er tilgængelig

### "Certifikatet er udløbet"
- Tjek at automatisk fornyelse er aktiveret
- Kør `sudo certbot renew` manuelt
- Tjek cron/systemd timer: `systemctl status certbot.timer`

### "Certifikatet matcher ikke domænet"
- Certifikatet er udstedt til et andet domæne
- Geninstaller certifikatet med det korrekte domænenavn

## Bemærkninger

- Let's Encrypt certifikater er **lige så sikre** som betalte DV-certifikater
- Fornyelse sker automatisk — men tjek det en gang imellem
- Wildcard-certifikater kræver DNS-01 challenge (kræver DNS-API adgang)
- Grænse: Maks 50 certifikater per domæne per uge (sjældent et problem)
- Let's Encrypt er en non-profit sponseret af bl.a. Mozilla, Google og Cisco
