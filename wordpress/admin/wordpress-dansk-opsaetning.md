# Dansk opsætning af WordPress

## Problem

WordPress viser engelske menuer, forkert datoformat eller forkert tidszone. Indlæg og sider viser tidspunkter i forkert tidszone.

## Løsning

### Sprog

1. Log ind i WordPress-administrationen
2. Gå til **Dashboard → Indstillinger → Generelt**
3. Find **Sprog** (eller **Site Language** hvis det stadig er engelsk)
4. Vælg **Dansk** i dropdown-menuen
5. Klik **Gem ændringer**

Hele admin-panelet skifter nu til dansk.

### Tidszone

1. Gå til **Indstillinger → Generelt**
2. Find **Tidszone**
3. Vælg **Europe/Copenhagen** fra dropdown-menuen
   - Alternativt: Vælg **UTC+1** (men Europe/Copenhagen håndterer sommertid automatisk)
4. Klik **Gem ændringer**

**Vigtigt:** Brug altid **Europe/Copenhagen** fremfor UTC+1, da den automatisk skifter mellem vintertid (CET, UTC+1) og sommertid (CEST, UTC+2).

### Datoformat

1. Gå til **Indstillinger → Generelt**
2. Find **Datoformat**
3. Vælg **Brugerdefineret** og skriv: `j. F Y`
   - Dette giver dansk datoformat: **13. februar 2026**
4. Klik **Gem ændringer**

Nyttige datoformat-koder:

| Kode | Resultat | Eksempel |
|------|----------|---------|
| `j. F Y` | Dag. Måned År | 13. februar 2026 |
| `d-m-Y` | dd-mm-åååå | 13-02-2026 |
| `j. M Y` | Dag. Kort måned År | 13. feb 2026 |
| `l j. F Y` | Ugedag Dag. Måned År | torsdag 13. februar 2026 |

### Tidsformat

1. Gå til **Indstillinger → Generelt**
2. Find **Tidsformat**
3. Vælg **Brugerdefineret** og skriv: `H:i`
   - Dette giver 24-timers format: **14:30**
4. Klik **Gem ændringer**

| Kode | Resultat | Eksempel |
|------|----------|---------|
| `H:i` | 24-timers | 14:30 |
| `G:i` | 24-timers uden ledende nul | 9:30 |
| `g:i a` | 12-timers (undgå dette i DK) | 2:30 pm |

### Ugestart

1. Gå til **Indstillinger → Generelt**
2. Find **Ugen starter**
3. Vælg **Mandag**
4. Klik **Gem ændringer**

I Danmark starter ugen mandag — WordPress' standard er søndag (amerikansk).

### Sprogopdatering / oversættelser

WordPress-oversættelser opdateres løbende. For at sikre de nyeste danske oversættelser:

1. Gå til **Dashboard → Opdateringer**
2. Kig efter sektionen **Oversættelser**
3. Klik **Opdatér oversættelser** hvis der er nye tilgængelige
4. Oversættelser opdateres også automatisk sammen med WordPress-opdateringer

### Brugerprofil-sprog

Hver bruger kan have sit eget sprog:

1. Gå til **Brugere → Din profil**
2. Find **Sprog**
3. Vælg **Dansk**
4. Klik **Opdatér profil**

Dette påvirker kun admin-panelet for den pågældende bruger — ikke selve websiden.

## Bemærkninger

- Sprog-indstillingen under **Indstillinger → Generelt** påvirker hele websiden (front-end og admin)
- Brugerprofil-sprog overskriver det globale sprog, men kun i admin-panelet
- Temaer og plugins skal have danske oversættelsesfiler for at vise dansk tekst — ikke alle har det
- Datoformatet `j. F Y` kræver at WordPress har danske månedsnavne indlæst (sker automatisk når sproget er sat til dansk)
- Elementor og andre page builders kan have separate sprogindstillinger
- WooCommerce har yderligere indstillinger for valuta (DKK), vægt (kg) og mål (cm) under **WooCommerce → Indstillinger → Generelt**
