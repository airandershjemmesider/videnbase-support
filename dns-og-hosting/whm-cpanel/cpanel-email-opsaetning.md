# Email-opsætning i cPanel

## Hvad er det

cPanel giver mulighed for at oprette email-konti på eget domæne (f.eks. info@domæne.dk), tilgå webmail og konfigurere email-klienter som Outlook og Thunderbird.

## Opret ny email-konto

### Trin-for-trin

1. Log ind på cPanel (`https://domæne:2083`)
2. Gå til **Email → Email Accounts**
3. Klik **Create**
4. Udfyld:
   - **Username:** Den ønskede adresse (f.eks. `info`)
   - **Domain:** Vælg domænet
   - **Password:** Stærkt password
   - **Storage Space:** Kvote i MB (eller Unlimited)
5. Klik **Create**

## Webmail-adgang

- **URL:** `https://domæne:2096` eller `https://domæne/webmail`
- Standard webmail-klient: **Roundcube**
- Log ind med fuld email-adresse og password

## Konfigurér i Outlook / Thunderbird

### IMAP-indstillinger (anbefalet)

| Indstilling | Værdi |
|-------------|-------|
| **Indgående server (IMAP)** | `mail.domæne.dk` |
| **Port** | 993 |
| **Kryptering** | SSL/TLS |
| **Udgående server (SMTP)** | `mail.domæne.dk` |
| **Port** | 465 |
| **Kryptering** | SSL/TLS |
| **Brugernavn** | Fuld email-adresse |
| **Password** | Email-kontoens password |

### POP3-indstillinger (alternativ)

| Indstilling | Værdi |
|-------------|-------|
| **Indgående server (POP3)** | `mail.domæne.dk` |
| **Port** | 995 |
| **Kryptering** | SSL/TLS |

### Forskel på IMAP og POP3

- **IMAP:** Email synkroniseres mellem server og klient — anbefalet til flere enheder
- **POP3:** Email downloades og fjernes fra serveren — bruges sjældent i dag

## Forwarders (videresendelse)

1. Gå til **Email → Forwarders**
2. Klik **Add Forwarder**
3. Angiv kilde-adresse og destinations-adresse
4. Eksempel: `kontakt@domæne.dk` → `personlig@gmail.com`

## Autoresponders (automatisk svar)

1. Gå til **Email → Autoresponders**
2. Klik **Add Autoresponder**
3. Udfyld:
   - **Email:** Vælg email-konto
   - **Subject:** Emne på autosvar
   - **Body:** Beskedtekst (f.eks. "Tak for din henvendelse. Vi vender tilbage inden for 24 timer.")
   - **Start/Stop:** Valgfrit tidsinterval

## Bemærkninger

- Tjek **Email Deliverability** i cPanel for at sikre SPF, DKIM og rDNS er korrekt opsat
- Hvis email ender i spam: Tjek SPF-record, DKIM-signering og at serverens IP ikke er blacklistet
- `mail.domæne.dk` skal pege til serverens IP via A-record i DNS
- Kvote kan ændres efterfølgende via Email Accounts → Manage
