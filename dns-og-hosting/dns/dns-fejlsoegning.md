# DNS Fejlsøgning — Domain peger forkert eller site loader ikke

## Problem

Domænet viser forkert side, loader slet ikke, eller du får fejlmeddelelser når du besøger dit domæne.

## Løsning: Systematisk fejlsøgning

### Trin 1: Tjek hvad domænet peger på

```
nslookup example.dk
```

Sammenlign IP-adressen med din servers IP. Matcher de ikke, peger DNS forkert.

For at se alle DNS records:
```
nslookup -type=ANY example.dk
```

### Trin 2: Tjek navneservere

```
nslookup -type=NS example.dk
```

Spørgsmål at stille:
- Peger NS-records til den rigtige DNS-udbyder?
- Har du ændret NS men glemt at oprette records hos den nye udbyder?

### Trin 3: Identificer fejltypen

#### "Denne side kan ikke nås" / DNS_PROBE_FINISHED_NXDOMAIN
- Domænet har **ingen A-record** eller den er forkert
- Tjek: Findes der en A-record? Peger den til en gyldig IP?
- Løsning: Opret/ret A-record hos din DNS-udbyder

#### "Serverfejl" / 500-fejl
- DNS er sandsynligvis korrekt — fejlen er på serveren
- Tjek: Server-logs, .htaccess, PHP-fejl

#### "Forbindelsen blev nægtet" / ERR_CONNECTION_REFUSED
- DNS peger rigtigt, men serveren afviser forbindelsen
- Tjek: Kører webserveren (Apache/Nginx)? Er porten åben?

#### Forkert hjemmeside vises
- A-record peger til **en forkert server** eller gammel IP
- Tjek: Er IP-adressen den rigtige? Er der et vhost-problem på serveren?

#### "DNS-adressen blev ikke fundet" / ERR_NAME_NOT_RESOLVED
- Domænet eksisterer ikke i DNS
- Tjek: Er domænet udløbet? Er NS-records opsat?

### Trin 4: Tjek mod forskellige DNS-servere

Din lokale ISP kan have cached gammel data. Test mod offentlige DNS-servere:

```
nslookup example.dk 8.8.8.8       (Google DNS)
nslookup example.dk 1.1.1.1       (Cloudflare DNS)
nslookup example.dk 208.67.222.222 (OpenDNS)
```

Hvis resultatet er forskelligt, er det et propagation- eller cache-problem.

### Trin 5: Flush DNS-cache

```
ipconfig /flushdns
```

Test derefter i et inkognito-vindue.

### Trin 6: Tjek for CNAME-konflikter

- CNAME på rod-domænet (`@`) er **ikke tilladt** — brug A-record i stedet
- Flere records af samme type på samme navn kan skabe konflikter
- CNAME og andre record-typer på samme navn er ugyldigt

## Typiske fejlscenarier

### Scenarie: Domæne efter hosting-skift
1. Du har skiftet hosting, men glemt at opdatere A-record
2. Løsning: Opdater A-record til den nye servers IP

### Scenarie: www virker, men naked domain gør ikke
1. `www.example.dk` har CNAME → men `example.dk` mangler A-record
2. Løsning: Tilføj A-record for `@` (rod-domænet)

### Scenarie: Email virker ikke efter DNS-ændring
1. MX records er blevet slettet eller overskrevet
2. Løsning: Tjek og genopret MX records

## Bemærkninger

- Brug **whatsmydns.net** til at tjekke propagation globalt
- Husk at DNS-ændringer kan tage op til 48 timer (se dns-propagation.md)
- Tjek altid **både** www og naked domain — de kan pege forskellige steder
- Når alt andet fejler: Tjek om domænet er udløbet hos registraren
