# Opsæt MX Records for Email

## Problem

Du skal opsætte eller ændre MX records så email til dit domæne leveres korrekt — f.eks. til Microsoft 365, Google Workspace eller en anden mailserver.

## Hvad er MX records?

MX (Mail Exchange) records fortæller andre mailservere **hvor email til dit domæne skal leveres**. Uden korrekte MX records modtager du ingen email.

## Løsning

### Trin 1: Find de korrekte MX records

#### Microsoft 365
| Prioritet | Mailserver                                    |
|-----------|-----------------------------------------------|
| 0         | `example-dk.mail.protection.outlook.com`      |

(Erstat `example-dk` med dit domæne med bindestreg i stedet for punktum)

Microsoft angiver den præcise værdi i Admin Center → Settings → Domains.

#### Google Workspace
| Prioritet | Mailserver                |
|-----------|---------------------------|
| 1         | `aspmx.l.google.com`     |
| 5         | `alt1.aspmx.l.google.com`|
| 5         | `alt2.aspmx.l.google.com`|
| 10        | `alt3.aspmx.l.google.com`|
| 10        | `alt4.aspmx.l.google.com`|

#### Simply.com (egen mailserver)
| Prioritet | Mailserver                |
|-----------|---------------------------|
| 10        | `mx1.simply.com`         |
| 20        | `mx2.simply.com`         |

(Tjek altid Simply.com's aktuelle anbefalinger i deres kontrolpanel)

#### one.com
| Prioritet | Mailserver                |
|-----------|---------------------------|
| 10        | `mx.one.com`             |

### Trin 2: Opdater DNS

1. Log ind hos din DNS-udbyder
2. **Slet eksisterende MX records** (hvis du skifter email-udbyder)
3. Tilføj nye MX records:
   - **Navn:** `@` (rod-domænet)
   - **Type:** MX
   - **Prioritet:** Som angivet ovenfor
   - **Værdi:** Mailserver-adressen
   - **TTL:** 3600
4. Gem

### Trin 3: Vent på propagation

MX record-ændringer tager typisk 15 min – 4 timer. I mellemtiden kan email leveres til enten den gamle eller nye server.

### Trin 4: Verificer

```
nslookup -type=MX example.dk
```

Tjek med **mxtoolbox.com** for fuld diagnostik.

### Trin 5: Test

Send en email fra en ekstern adresse (f.eks. Gmail) til din domæne-email og bekræft at den modtages.

## Om prioritet

- **Lavere tal = højere prioritet** (0 er højest)
- Mailservere med samme prioritet bruges tilfældigt (load balancing)
- Hvis den primære server er nede, prøves den næste prioritet

## Bemærkninger

- **Slet ALTID gamle MX records** når du skifter email-udbyder — ellers kan email ende det forkerte sted
- Husk at opdatere **SPF-record** når du skifter email-udbyder (se spf-record.md)
- Husk at opsætte **DKIM** hos den nye email-udbyder (se dkim-record.md)
- MX records skal pege til et **hostname** (ikke en IP-adresse)
- Sæt TTL ned til 300 FØR du laver ændringer for hurtigere propagation
- Under skift: Sæt op på den nye server FØRST, skift MX bagefter — så er du klar til at modtage
