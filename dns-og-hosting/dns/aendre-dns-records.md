# Sådan ændrer du DNS records

## Problem

Du skal ændre DNS records for et domæne — f.eks. pege domænet til en ny server, tilføje email-records eller verificere domænet hos en tjeneste.

## Løsning

### Trin 1: Find ud af hvor DNS'en styres

DNS styres der hvor domænets **navneservere (NS)** peger hen. Det er IKKE nødvendigvis der du købte domænet.

Tjek navneservere:
```
nslookup -type=NS example.dk
```

### Trin 2: Log ind hos DNS-udbyderen

#### Hos DK Hostmaster (kun .dk-domæner)
- DK Hostmaster styrer IKKE selve DNS-records — de peger kun NS videre
- Du ændrer records hos den udbyder, der kører dine navneservere

#### Simply.com
1. Log ind på Simply.com → Kontrolpanel
2. Vælg domænet under "Domæner"
3. Klik "DNS" i menuen
4. Tilføj/ret records direkte i tabellen
5. Klik "Gem"

#### one.com
1. Log ind på one.com → Kontrolpanel
2. Gå til "DNS-indstillinger"
3. Klik "Tilføj record" eller rediger eksisterende
4. Vælg record-type og udfyld felterne
5. Gem ændringerne

#### Cloudflare
1. Log ind på Cloudflare Dashboard
2. Vælg dit domæne
3. Gå til "DNS" → "Records"
4. Klik "Add record"
5. Vælg type, udfyld navn og værdi
6. Vælg om proxy (orange sky) skal være til eller fra
7. Klik "Save"

#### GoDaddy
1. Log ind → "My Products"
2. Find domænet → klik "DNS"
3. Klik "Add" for ny record eller blyant-ikonet for at redigere
4. Udfyld felterne og gem

#### Namecheap
1. Log ind → "Domain List"
2. Klik "Manage" ud for domænet
3. Gå til fanen "Advanced DNS"
4. Tilføj eller rediger records

### Trin 3: Udfyld record-felterne

Alle DNS records har disse felter:

| Felt     | Beskrivelse                                    |
|----------|------------------------------------------------|
| Type     | A, CNAME, MX, TXT osv.                        |
| Navn     | Subdomæne eller `@` for rod-domænet            |
| Værdi    | IP-adresse, domæne eller tekststreng            |
| TTL      | Cache-tid i sekunder (standard: 3600)           |
| Prioritet| Kun for MX og SRV records                      |

### Trin 4: Verificer ændringen

Tjek at din record er oprettet korrekt:
```
nslookup -type=A example.dk
nslookup -type=MX example.dk
nslookup -type=TXT example.dk
```

Eller brug online værktøjer som:
- whatsmydns.net (tjek propagation globalt)
- mxtoolbox.com (tjek MX og email-records)
- dnschecker.org

## Bemærkninger

- Sæt TTL til **300 sekunder** (5 min) et par timer FØR du laver ændringer — så spreder den nye værdi sig hurtigere
- Husk at sætte TTL tilbage til 3600 bagefter
- DNS-ændringer kan tage op til **48 timer** at sprede sig globalt, men typisk 15 min til et par timer
- Hvis du bruger Cloudflare som proxy (orange sky), peger A-recorden teknisk set til Cloudflare — ikke direkte til din server
