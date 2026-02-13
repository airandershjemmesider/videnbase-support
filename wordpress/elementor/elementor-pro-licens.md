# Elementor Pro licens problemer

## Problem

Elementor Pro licens kan ikke aktiveres, viser fejlmeddelelser, eller Pro-funktioner virker ikke efter fornyelse eller domæneskift.

## Løsning

### Licens aktivering fejler

1. Tjek at dit site kan nå **license.elementor.com** — firewalls eller sikkerhedsplugins kan blokere
2. Tjek at din licens ikke allerede er aktiveret på det maksimale antal sites
3. Log ind på **my.elementor.com** og verificér at licensen er aktiv
4. Prøv at deaktivere og genaktivere licensen under **Elementor → License**

### "Mismatch between your plan and the current version"

Denne fejl opstår når plugin-versionen er nyere end hvad din licens dækker:

1. Opdatér Elementor Pro til nyeste version
2. Hvis licensen er udløbet, kan du ikke opdatere — forny licensen først
3. Alternativt: rollback til en ældre version der matcher din licensperiode

### Flyt licens til nyt domæne

1. Gå til det **gamle site** → Elementor → License → Disconnect
2. Alternativt: log ind på **my.elementor.com** → Subscriptions → Manage Sites → fjern det gamle domæne
3. Aktivér licensen på det nye domæne under **Elementor → License**

### Licens udløbet — hvad sker der?

Når licensen udløber:

- **Pro widgets deaktiveres** — de vises som tomme pladsholdere på frontend
- **Data bevares** — alt indhold ligger stadig i databasen
- **Ingen opdateringer** — du modtager ikke nye versioner eller sikkerhedspatches
- **Support ophører** — ingen adgang til Elementor Pro support

Genaktivering af licensen genopretter alle Pro-widgets og data med det samme.

### API-forbindelsesproblemer

Hvis licensen slet ikke kan valideres:

1. Tjek at `wp-cron.php` kører korrekt
2. Tilføj til `wp-config.php` hvis nødvendigt:
   ```php
   define('ELEMENTOR_LICENCE_KEY', 'din-licens-nøgle');
   ```
3. Kontakt Elementor support hvis problemet fortsætter

## Bemærkninger

- Elementor Pro licenser er årlige — sæt en påmindelse om fornyelse
- Essential-planen dækker 1 site, Advanced dækker 3, Agency dækker 1000
- Ved domæneskift (f.eks. staging → produktion) skal licensen flyttes manuelt
