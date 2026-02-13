# DNS Record-typer — Oversigt

## Hvad er DNS records?

DNS records er instruktioner der fortæller internettet, hvordan dit domæne skal opføre sig. Hver record-type har et specifikt formål.

## Record-typer

### A Record (Address)
- Peger et domæne til en **IPv4-adresse** (f.eks. `203.0.113.50`)
- Den mest basale record — forbinder dit domæne med din server
- Eksempel: `example.dk → 203.0.113.50`

### AAAA Record (IPv6 Address)
- Samme som A record, men for **IPv6-adresser** (f.eks. `2001:0db8:85a3::8a2e:0370:7334`)
- Bruges i stigende grad, men mange sider kører stadig fint uden

### CNAME Record (Canonical Name)
- Peger et domæne til **et andet domæne** (alias)
- Eksempel: `www.example.dk → example.dk`
- **Begrænsning:** Kan IKKE bruges på rod-domænet (naked domain). Kun på subdomæner
- Typisk brug: `www`-subdomain, CDN-opsætning, SaaS-tjenester

### MX Record (Mail Exchange)
- Fortæller hvor email til dit domæne skal sendes hen
- Har en **prioritet** (lavere tal = højere prioritet)
- Eksempel: `example.dk MX 10 mail.example.dk`
- Du kan have flere MX records som fallback

### TXT Record (Text)
- Indeholder fritekst — bruges til verifikation og sikkerhed
- Typiske anvendelser:
  - **SPF** — hvem må sende email fra dit domæne
  - **DKIM** — digital signatur på email
  - **DMARC** — politik for email-autentificering
  - **Domæne-verifikation** — Google Search Console, M365, osv.

### NS Record (Name Server)
- Angiver hvilke **navneservere** der er autoritative for dit domæne
- Ændres typisk kun når du flytter domæne eller skifter DNS-udbyder
- Eksempel: `ns1.hosting.dk`, `ns2.hosting.dk`

### SRV Record (Service)
- Peger på en specifik service og port
- Bruges af f.eks. Microsoft 365, VoIP, og andre tjenester
- Format: `_service._proto.name TTL class SRV priority weight port target`
- Eksempel: `_sip._tcp.example.dk SRV 10 60 5060 sipserver.example.dk`

## Hurtig reference

| Type  | Peger på         | Typisk brug                        |
|-------|------------------|------------------------------------|
| A     | IPv4-adresse     | Hjemmeside → server                |
| AAAA  | IPv6-adresse     | Hjemmeside → server (IPv6)         |
| CNAME | Andet domæne     | www-alias, CDN, SaaS               |
| MX    | Mailserver       | Email-routing                      |
| TXT   | Fritekst         | SPF, DKIM, DMARC, verifikation     |
| NS    | Navneserver      | DNS-delegation                     |
| SRV   | Service + port   | M365, VoIP, chat                   |

## Bemærkninger

- **TTL (Time To Live):** Alle records har en TTL-værdi (i sekunder) der bestemmer hvor længe cachen husker værdien. Lavere TTL = hurtigere opdatering, men mere trafik til DNS-serveren
- Typisk TTL: 3600 (1 time). Sæt til 300 (5 min) før planlagte ændringer
- Brug `nslookup` eller `dig` til at tjekke dine records
