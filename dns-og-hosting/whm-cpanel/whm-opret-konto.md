# Opret ny hosting-konto i WHM

## Hvad er det

Når en ny kunde skal have hosting, oprettes en cPanel-konto via WHM. Kontoen får sit eget filsystem, database-adgang, email og DNS-zone.

## Trin-for-trin

### 1. Åbn Create a New Account

- Log ind på WHM (`https://server-ip:2087`)
- Gå til **Account Functions → Create a New Account**

### 2. Udfyld domæne-info

- **Domain:** Kundens primære domæne (f.eks. `eksempel.dk`)
- **Username:** Genereres automatisk fra domænet — kan tilpasses (maks 8 tegn)
- **Password:** Stærkt password (eller brug generatoren)
- **Email:** Kundens kontakt-email (bruges til notifikationer)

### 3. Vælg pakke

- **Package:** Vælg en foruddefineret hosting-pakke
- Pakken bestemmer: diskplads, båndbredde, antal email-konti, antal domæner, antal databaser
- Hvis ingen pakke passer: Vælg "Select Options Manually" og sæt grænser manuelt

### 4. Indstillinger

- **cPanel Theme:** paper_lantern (standard)
- **Locale:** da (dansk) eller en (engelsk)
- **Enable CGI Access:** Normalt ja
- **Enable SpamAssassin:** Anbefalet ja
- **Enable SPF og DKIM:** Anbefalet ja — forbedrer email-levering

### 5. DNS-opsætning

- WHM opretter automatisk en DNS-zone for domænet
- Zonen indeholder: A-record (peger til serverens IP), MX-record (mail), NS-records
- **Vigtigt:** Kundens domæne skal pege til serverens nameservere (eller A-record) hos domæneudbyderen

### 6. Opret kontoen

- Klik **Create**
- WHM viser en bekræftelse med alle detaljer
- Notér login-info til kunden

## Verificér kontoen

- Gå til **Account Functions → List Accounts**
- Find kontoen og tjek:
  - Domæne vises korrekt
  - Diskforbrug er 0 MB (ny konto)
  - Status er aktiv (ikke suspenderet)
- Test cPanel-login: `https://domæne:2083` med de oprettede credentials

## Bemærkninger

- Brugernavn kan **ikke** ændres efter oprettelse — vælg det rigtigt første gang
- Slet aldrig en konto uden backup — brug Suspend i stedet hvis kunden skal deaktiveres midlertidigt
- Pakker oprettes under **Packages → Add a Package** i WHM
- Ændr pakke efterfølgende via **Account Functions → Upgrade/Downgrade an Account**
