# WordPress brugerroller og tilladelser

## Problem

WordPress har flere brugerroller med forskellige tilladelser. Det er vigtigt at tildele den rigtige rolle så brugere ikke får mere adgang end nødvendigt.

## Løsning

### De 5 standard-roller

| Rolle | Kan | Kan IKKE |
|-------|-----|----------|
| **Administrator** | Alt — fuld kontrol over sitet | Intet begrænset |
| **Redaktør** | Redigér og publicér ALLE indlæg og sider | Ændre tema, plugins, indstillinger |
| **Forfatter** | Skriv og publicér egne indlæg | Redigér andres indlæg, ændre sider |
| **Bidragyder** | Skriv indlæg (kræver godkendelse) | Publicere, uploade filer |
| **Abonnent** | Læse indhold, redigere egen profil | Oprette eller redigere indhold |

### Opret ny bruger

1. Gå til **Brugere → Tilføj ny**
2. Udfyld brugernavn, email og adgangskode
3. Vælg den korrekte rolle
4. Klik **Tilføj ny bruger**

### Ændr en brugers rolle

1. Gå til **Brugere → Alle brugere**
2. Klik på brugerens navn
3. Ændr rollen i dropdown-menuen
4. Klik **Opdatér bruger**

### Ændr flere brugere på én gang

1. Gå til **Brugere → Alle brugere**
2. Markér de ønskede brugere med checkboxes
3. Vælg **Ændr rolle til...** i bulk-handlinger
4. Klik **Anvend**

### Anbefalinger

- **Kunden** bør typisk være **Redaktør** — kan redigere indhold men ikke ødelægge sitet
- **Gæsteskribenter** bør være **Bidragyder** — kræver godkendelse før publicering
- **Hold antallet af administratorer lavt** — kun den teknisk ansvarlige
- **Brug aldrig "admin" som brugernavn** — det er det første hackere prøver

### Brugerdefinerede roller (med plugin)

Hvis standardrollerne ikke passer, brug pluginet **User Role Editor**:

1. Installér og aktivér User Role Editor
2. Gå til **Brugere → User Role Editor**
3. Vælg en rolle at redigere eller opret en ny
4. Tilføj/fjern specifikke tilladelser
5. Gem ændringer

## Bemærkninger

- I multisite-installationer findes også rollen **Super Admin** med adgang til alle sites
- WooCommerce tilføjer rollerne **Kunde** og **Butikschef** automatisk
- Slet aldrig den oprindelige administrator-konto uden at have en anden administrator
- Brugere kan kun se deres egen profil som Abonnent — velegnet til medlemssites
