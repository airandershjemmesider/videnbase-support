# DNS Zone Editor i cPanel

## Hvad er det

cPanels Zone Editor giver mulighed for at administrere DNS-records for domæner på kontoen. Her kan du tilføje, redigere og slette A-, CNAME-, MX- og TXT-records.

## Trin-for-trin

### Åbn Zone Editor

1. Log ind på cPanel (`https://domæne:2083`)
2. Gå til **Domains → Zone Editor**
3. Find domænet og klik **Manage**

### Tilføj en record

1. Klik **Add Record**
2. Vælg record-type og udfyld felterne:

#### A-record
- **Name:** `subdomain.domæne.dk` (eller `domæne.dk` for roden)
- **TTL:** 14400 (standard)
- **Type:** A
- **Record:** IP-adresse (f.eks. `185.60.40.10`)

#### CNAME-record
- **Name:** `www.domæne.dk`
- **Type:** CNAME
- **Record:** `domæne.dk` (peger til hoveddomænet)

#### MX-record
- **Name:** `domæne.dk`
- **Type:** MX
- **Priority:** 0 (lavest = højest prioritet)
- **Record:** `mail.domæne.dk`

#### TXT-record (SPF, DKIM, DMARC)
- **Name:** `domæne.dk`
- **Type:** TXT
- **Record:** Indholdet af TXT-recorden

### Redigér eksisterende record

1. Find recorden i listen
2. Klik **Edit**
3. Ændr værdien og klik **Save Record**

### Slet en record

1. Find recorden
2. Klik **Delete**
3. Bekræft sletning

## Email-autentificering via DNS

### SPF (Sender Policy Framework)
- Gå til **Email → Email Deliverability** — cPanel anbefaler korrekt SPF automatisk
- Typisk SPF-record: `v=spf1 +a +mx +ip4:SERVER-IP ~all`
- Klik **Repair** hvis Email Deliverability viser problemer

### DKIM (DomainKeys Identified Mail)
- Gå til **Email → Email Deliverability**
- Klik **Repair** for at generere og tilføje DKIM-record
- DKIM-recorden er en lang TXT-record på `default._domainkey.domæne.dk`

### DMARC
- Tilføj TXT-record manuelt:
- **Name:** `_dmarc.domæne.dk`
- **Record:** `v=DMARC1; p=none; rua=mailto:admin@domæne.dk`
- `p=none` (overvåg), `p=quarantine` (karantæne), `p=reject` (afvis)

## Bemærkninger

- **Vigtigt:** Hvis DNS styres eksternt (f.eks. hos Cloudflare, Simply eller Gratisdns), skal ændringer laves DÉR — ikke i cPanel
- DNS-ændringer kan tage op til 24-48 timer at propagere (oftest 1-4 timer)
- TTL (Time To Live) angiver hvor længe DNS-servere cacher recorden — lavere TTL = hurtigere opdatering
- Vær forsigtig med at slette MX-records — det stopper email-levering
- Brug **Email Deliverability** i cPanel som førstevalg til SPF og DKIM — det foreslår de korrekte records
