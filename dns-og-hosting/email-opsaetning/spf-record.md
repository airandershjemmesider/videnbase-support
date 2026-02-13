# Opsæt SPF Record (Sender Policy Framework)

## Problem

Emails sendt fra dit domæne havner i spam eller bliver afvist, fordi modtagernes mailservere ikke kan verificere at afsenderen er legitim.

## Hvad er SPF?

SPF er en DNS TXT-record der fortæller verden, hvilke servere der har **tilladelse til at sende email** fra dit domæne. Modtagerens mailserver tjekker SPF-recorden og afviser email fra uautoriserede servere.

## Løsning

### Trin 1: Identificer dine afsenderservere

Find alle tjenester der sender email fra dit domæne:
- Din hostings mailserver
- Microsoft 365 / Google Workspace
- Nyhedsbrevstjenester (Mailchimp, ActiveCampaign osv.)
- Transaktionsmail (SendGrid, Mailgun, Amazon SES)
- CRM-systemer, fakturasystemer osv.

### Trin 2: Byg din SPF-record

SPF-recorden er en TXT-record på rod-domænet (`@`).

**Grundstruktur:**
```
v=spf1 [afsendere] -all
```

**Eksempler:**

Kun din egen server:
```
v=spf1 a mx -all
```

Microsoft 365:
```
v=spf1 include:spf.protection.outlook.com -all
```

Google Workspace:
```
v=spf1 include:_spf.google.com -all
```

Microsoft 365 + Mailchimp:
```
v=spf1 include:spf.protection.outlook.com include:servers.mcsv.net -all
```

### Trin 3: Opret TXT-record i DNS

1. Log ind hos din DNS-udbyder
2. Tilføj ny TXT-record:
   - **Navn:** `@` (rod-domænet)
   - **Type:** TXT
   - **Værdi:** Din SPF-streng (se ovenfor)
   - **TTL:** 3600
3. Gem

### Trin 4: Verificer

Tjek din SPF-record:
```
nslookup -type=TXT example.dk
```

Eller brug: **mxtoolbox.com/spf.aspx**

## SPF mekanismer

| Mekanisme   | Betydning                                      |
|-------------|-------------------------------------------------|
| `a`         | Domænets A-record IP må sende                   |
| `mx`        | Domænets MX-servere må sende                    |
| `ip4:X.X.X.X` | Specifik IPv4-adresse må sende               |
| `include:X` | Inkludér en anden tjenestes SPF-record          |
| `-all`      | Afvis alt andet (hard fail — anbefalet)         |
| `~all`      | Soft fail — marker som suspekt men afvis ikke   |

## Bemærkninger

- Du må kun have **én SPF-record** per domæne. Kombiner alt i én record
- Maks **10 DNS-lookups** i en SPF-record (include tæller som lookup). Overstiger du 10, fejler SPF
- Brug `-all` (hard fail) i produktion — `~all` er kun til test
- Brug **mxtoolbox.com/spf.aspx** til at validere din SPF-record og tælle lookups
- SPF alene er ikke nok — kombiner med DKIM og DMARC for fuld beskyttelse
