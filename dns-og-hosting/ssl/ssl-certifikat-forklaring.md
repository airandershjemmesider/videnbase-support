# Hvad er SSL/TLS og hvorfor er det vigtigt?

## Hvad er SSL/TLS?

SSL (Secure Sockets Layer) og TLS (Transport Layer Security) er krypteringsprotokoller der sikrer forbindelsen mellem en brugers browser og din webserver. TLS er den nyere, sikrere version — men termen "SSL" bruges stadig i daglig tale.

Når SSL er aktivt, vises:
- **https://** i stedet for http:// i URL'en
- Et **hængelås-ikon** i browseren

## Hvorfor er SSL vigtigt?

### 1. Sikkerhed
- Krypterer al data mellem browser og server
- Beskytter passwords, kreditkortoplysninger og persondata
- Forhindrer man-in-the-middle-angreb

### 2. SEO
- Google bruger HTTPS som **ranking-faktor**
- Sider uden SSL rangerer lavere i søgeresultaterne

### 3. Tillid
- Browsere viser **"Ikke sikker"** på sider uden SSL
- Besøgende stoler mere på sider med hængelås-ikonet
- Særligt vigtigt for webshops og sider med formularer

### 4. Lovkrav
- GDPR kræver passende sikkerhedsforanstaltninger for persondata
- SSL er i praksis et minimum for alle sider der indsamler data

## Typer af SSL-certifikater

### Domain Validation (DV)
- **Verificerer:** At du ejer domænet
- **Pris:** Gratis (Let's Encrypt) til ca. 100 kr/år
- **Udstedelsestid:** Minutter
- **Passer til:** De fleste hjemmesider

### Organization Validation (OV)
- **Verificerer:** Domæne + at virksomheden eksisterer
- **Pris:** Ca. 500-2.000 kr/år
- **Udstedelsestid:** 1-3 dage
- **Passer til:** Virksomhedssider der vil vise ekstra tillid

### Extended Validation (EV)
- **Verificerer:** Domæne + virksomhed + grundig baggrundskontrol
- **Pris:** Ca. 1.000-5.000 kr/år
- **Udstedelsestid:** 1-2 uger
- **Passer til:** Banker, store webshops (dog mindre relevant i dag, da browsere ikke længere viser grøn adresselinje)

### Wildcard-certifikat
- Dækker domænet **og alle subdomæner** (*.example.dk)
- Praktisk hvis du har mange subdomæner
- Fås som DV eller OV

## Løsning: Hvad skal du vælge?

| Situation | Anbefaling |
|-----------|------------|
| Simpel hjemmeside | Let's Encrypt (gratis DV) |
| WordPress-side | Let's Encrypt (gratis DV) |
| Webshop | Let's Encrypt eller OV |
| Bank / finansiel side | EV |
| Mange subdomæner | Wildcard |

**For de fleste:** Let's Encrypt er gratis, automatisk og helt tilstrækkeligt.

## Bemærkninger

- **SSL og TLS bruges synonymt** i daglig tale, men TLS er den korrekte tekniske term for moderne versioner
- Let's Encrypt certifikater udløber efter **90 dage** — men fornyes automatisk
- Et SSL-certifikat er IKKE nok alene — du skal også sørge for at sitet **kun bruger HTTPS** (se mixed-content.md)
- Alle moderne hosting-udbydere tilbyder Let's Encrypt gratis og med automatisk fornyelse
