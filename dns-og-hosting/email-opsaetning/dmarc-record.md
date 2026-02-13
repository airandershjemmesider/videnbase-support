# Opsæt DMARC Record (Domain-based Message Authentication)

## Problem

Trods SPF og DKIM kan svindlere stadig forfalske dit domæne i emails. Du har brug for en politik der fortæller modtagere hvad de skal gøre med emails der fejler autentificering.

## Hvad er DMARC?

DMARC bygger oven på SPF og DKIM. Den fortæller modtagerens mailserver:
1. **Hvad skal der ske** med emails der fejler SPF/DKIM-tjek
2. **Hvor skal rapporter sendes** om fejlede emails

DMARC beskytter mod email-spoofing og phishing der misbruger dit domæne.

## Løsning

### Forudsætninger

- SPF-record skal være opsat og fungere (se spf-record.md)
- DKIM-record skal være opsat og fungere (se dkim-record.md)

### Trin 1: Start med en overvågningspolitik

Begynd ALTID med `p=none` så du kan se rapporter uden at påvirke email-levering:

```
v=DMARC1; p=none; rua=mailto:dmarc@example.dk; ruf=mailto:dmarc@example.dk
```

### Trin 2: Opret TXT-record i DNS

1. Log ind hos din DNS-udbyder
2. Tilføj ny TXT-record:
   - **Navn:** `_dmarc`
   - **Type:** TXT
   - **Værdi:** Din DMARC-streng
   - **TTL:** 3600
3. Gem

### Trin 3: Overvåg rapporter (2-4 uger)

- Du modtager daglige XML-rapporter fra store mailservere (Google, Microsoft osv.)
- Brug en gratis DMARC-rapporterings-tjeneste til at læse dem:
  - **dmarcian.com** (gratis for lavt volumen)
  - **postmark.com/dmarc** (gratis DMARC-rapporter)
  - **mxtoolbox.com/dmarc.aspx**
- Identificer om der er legitime afsendere der fejler

### Trin 4: Stram politikken gradvist

Når du har bekræftet at alle legitime afsendere passer SPF/DKIM:

**Fase 1 — Karantæne 10%:**
```
v=DMARC1; p=quarantine; pct=10; rua=mailto:dmarc@example.dk
```

**Fase 2 — Karantæne 100%:**
```
v=DMARC1; p=quarantine; rua=mailto:dmarc@example.dk
```

**Fase 3 — Afvis (fuld beskyttelse):**
```
v=DMARC1; p=reject; rua=mailto:dmarc@example.dk
```

### Trin 5: Verificer

```
nslookup -type=TXT _dmarc.example.dk
```

Eller brug: **mxtoolbox.com/dmarc.aspx**

## DMARC-parametre

| Parameter | Betydning                                        |
|-----------|--------------------------------------------------|
| `v=DMARC1` | Version (påkrævet)                             |
| `p=none`  | Gør intet — kun overvågning                      |
| `p=quarantine` | Send til spam/karantæne                     |
| `p=reject` | Afvis emailen helt                              |
| `pct=XX`  | Anvend politik på XX% af emails (standard: 100)  |
| `rua=`    | Email til aggregerede rapporter (daglige)        |
| `ruf=`    | Email til forensic-rapporter (per fejlet email)  |
| `sp=`     | Politik for subdomæner                           |

## Bemærkninger

- Gå **ALDRIG** direkte til `p=reject` — start med `p=none` og overvåg først
- DMARC-rapporter kan fylde — brug en dedikeret email eller rapporterings-tjeneste
- `pct`-parameteren lader dig gradvist øge enforcement
- Husk at tjekke subdomæner — de kan have separate behov
- Fuld email-sikkerhed kræver alle tre: **SPF + DKIM + DMARC**
- Google og Yahoo kræver DMARC for bulk-afsendere (fra 2024)
