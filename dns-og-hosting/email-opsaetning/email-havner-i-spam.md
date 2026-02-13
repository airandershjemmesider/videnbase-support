# Email havner i spam — Fejlsøgning

## Problem

Emails sendt fra dit domæne havner i modtagerens spam-mappe i stedet for indbakken.

## Løsning: Systematisk fejlsøgning

### Trin 1: Tjek email-autentificering

De tre vigtigste ting at have styr på:

#### SPF
```
nslookup -type=TXT example.dk
```
- Tjek at SPF-recorden inkluderer alle dine afsender-tjenester
- Se spf-record.md for opsætning

#### DKIM
```
nslookup -type=TXT selector1._domainkey.example.dk
```
- Tjek at DKIM er aktiveret hos din email-udbyder
- Se dkim-record.md for opsætning

#### DMARC
```
nslookup -type=TXT _dmarc.example.dk
```
- Tjek at DMARC-record eksisterer
- Se dmarc-record.md for opsætning

### Trin 2: Test din email-konfiguration

Send en test-email til disse tjenester:

- **mail-tester.com** — Giver en score fra 1-10 med detaljer om hvad der mangler
- **learndmarc.com** — Visualiserer SPF/DKIM/DMARC-flowet

### Trin 3: Tjek sortlister (blacklists)

Dit domæne eller din servers IP kan være på en sortliste:

1. Gå til **mxtoolbox.com/blacklists.aspx**
2. Indtast dit domæne eller din servers IP
3. Hvis du er på en liste — følg listens aflistnings-procedure

### Trin 4: Tjek email-indhold

Spam-filtre reagerer på:
- **Spammy emnelinjer** — Store bogstaver, mange udråbstegn, ord som "GRATIS", "TILBUD"
- **For mange billeder, for lidt tekst** — Hold en god tekst-til-billede ratio
- **Mange links** — Især til suspekte domæner
- **Manglende afmeld-link** — Påkrævet i nyhedsbreve (og lovpligtigt)
- **Ingen plain-text version** — Send altid både HTML og plain text

### Trin 5: Tjek afsender-reputation

- **Google Postmaster Tools** (postmaster.google.com) — Vis dit domænes reputation hos Gmail
- **Microsoft SNDS** (sendersupport.olc.protection.outlook.com) — Vis reputation hos Outlook
- Ny domæner har ingen reputation og kan opleve lavere levering i starten

### Trin 6: Tjek tekniske forhold

- **Reverse DNS (PTR):** Din servers IP skal have en PTR-record der matcher
- **HELO/EHLO:** Mailserverens hostname skal matche DNS
- **TLS:** Serveren skal understøtte krypteret forbindelse

## Hurtig tjekliste

| Tjek | Status |
|------|--------|
| SPF record opsat korrekt | [ ] |
| DKIM aktiveret og verificeret | [ ] |
| DMARC record opsat | [ ] |
| Ikke på sortlister | [ ] |
| mail-tester.com score over 7 | [ ] |
| Reverse DNS (PTR) korrekt | [ ] |
| Afmeld-link i nyhedsbreve | [ ] |

## Tips til bedre levering

- **Opvarm nye domæner/IP'er gradvist** — start med små mængder og øg over uger
- **Ryd op i din mailliste** — fjern bounces og inaktive modtagere regelmæssigt
- **Brug en dedikeret sending-IP** for bulk-email (adskilt fra transaktionsmail)
- **Autentificer ALT** — SPF + DKIM + DMARC er minimum

## Bemærkninger

- Gmail og Outlook har de strengeste spam-filtre — test mod begge
- Google kræver DMARC, SPF og DKIM for afsendere med over 5.000 emails/dag
- Spam-filtre er proprietære og ændrer sig løbende — der er ingen garanti for 100% levering
- Hvis du sender nyhedsbreve: Brug en professionel tjeneste (Mailchimp, ActiveCampaign osv.) frem for din egen mailserver
