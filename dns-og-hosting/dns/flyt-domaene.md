# Flyt et domæne mellem udbydere

## Problem

Du vil flytte dit domæne fra én registrar til en anden (f.eks. fra GoDaddy til Simply.com eller Namecheap).

## Løsning

### Før flytningen — forberedelse

1. **Tjek at domænet kan flyttes:**
   - Domænet skal være mindst 60 dage gammelt
   - Domænet må ikke være låst (transfer lock)
   - Domænet må ikke være udløbet

2. **Sæt DNS TTL ned til 300** på alle vigtige records (A, MX, CNAME)
   - Vent mindst den gamle TTL-tid før du fortsætter

3. **Notér alle eksisterende DNS records:**
   - Tag screenshots eller eksportér records fra den nuværende udbyder
   - Du skal genoprette dem hos den nye udbyder

### Trin-for-trin flytning

#### Trin 1: Fjern transfer lock hos nuværende registrar
- Log ind hos den nuværende udbyder
- Find domæneindstillinger → "Transfer lock" eller "Domain lock"
- Slå låsen FRA

#### Trin 2: Få autorisationskode (EPP/Auth code)
- Hos den nuværende registrar: Anmod om en **EPP-kode** (også kaldet auth code eller transfer key)
- Koden sendes typisk til domænets kontakt-email
- Koden er gyldig i en begrænset periode (ofte 5-14 dage)

#### Trin 3: Start overførslen hos den nye registrar
- Log ind hos den nye udbyder
- Find "Overfør domæne" / "Transfer domain"
- Indtast domænenavnet og EPP-koden
- Betal for overførslen (typisk 1 års forlængelse)

#### Trin 4: Godkend overførslen
- Den nuværende registrar sender en bekræftelses-email
- **Godkend overførslen** — ellers afvises den automatisk efter 5 dage
- Nogle registrarer kræver godkendelse fra begge sider

#### Trin 5: Vent på overførslen
- Typisk 1-7 dage afhængigt af TLD og registrar
- .dk-domæner: Ofte hurtigere (1-2 dage via DK Hostmaster)
- .com/.net: Op til 5-7 dage

#### Trin 6: Opsæt DNS hos den nye udbyder
- Genopret alle DNS records fra dine noter
- Tjek at A, MX, CNAME, TXT records er korrekte
- Verificer med `nslookup` at alt peger rigtigt

### Særligt for .dk-domæner

.dk-domæner håndteres via **DK Hostmaster** (dk-hostmaster.dk):

1. Log ind på DK Hostmaster med NemID/MitID
2. Skift registrar under domæneindstillinger
3. Den nye registrar skal være DK Hostmaster-godkendt
4. Selve DNS kan styres uafhængigt af registraren

## Flyt kun DNS (uden domæne-overførsel)

Hvis du bare vil ændre hvor DNS styres (uden at flytte selve domænet):

1. Opret alle DNS records hos den nye DNS-udbyder først
2. Skift NS-records hos din registrar til de nye navneservere
3. Vent på propagation (kan tage op til 48 timer)

## Bemærkninger

- **Tag ALTID backup af DNS records** inden flytning — records kan gå tabt under overførslen
- Email er det mest kritiske — sørg for at MX records er korrekte med det samme
- Planlæg flytningen i en rolig periode (ikke fredag eftermiddag)
- Domænet forlænges typisk med 1 år ved overførsel — du mister ikke resterende tid
- Nogle registrarer forsøger at gøre det svært at flytte væk — vær tålmodig
