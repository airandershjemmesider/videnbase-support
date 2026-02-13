# Best practices for kanaler og teams-struktur

## Problem

Organisationen har brug for en fornuftig struktur i Microsoft Teams, så kommunikationen er organiseret og nem at finde rundt i. Uden plan ender man med for mange teams, døde kanaler og forvirring.

## Løsning

### Grundprincipper for god struktur

1. **Færre teams, flere kanaler** — opret kun teams for reelle grupper/projekter
2. **Hvert team har ét formål** — f.eks. en afdeling, et projekt eller et emne
3. **Kanaler er emner inden for teamet** — ikke separate teams for hvert emne
4. **Brug General-kanalen sparsomt** — den er til vigtige meddelelser, ikke daglig snak
5. **Arkivér inaktive teams** — ryd op løbende

### Anbefalet struktur for en typisk virksomhed

```
IT-afdelingen (team)
  ├── General          → Vigtige meddelelser
  ├── Helpdesk         → Support-sager og spørgsmål
  ├── Infrastruktur    → Servere, netværk, cloud
  ├── Projekter        → Igangværende IT-projekter
  └── Vidensdeling     → Tips, guides, nyheder

Salg (team)
  ├── General          → Fælles beskeder
  ├── Leads            → Nye kundehenvendelser
  ├── Pipeline         → Igangværende salg
  └── Resultater       → KPI'er og rapporter

Projekt: Ny hjemmeside (team)
  ├── General          → Overblik og status
  ├── Design           → Mockups og design-diskussion
  ├── Udvikling        → Teknisk diskussion
  └── Indhold          → Tekster og billeder
```

### Opret et nyt team

1. Klik **Teams** i venstre side → **Opret eller deltag i et team**
2. Klik **Opret team**
3. Vælg **Fra bunden** eller **Fra en eksisterende gruppe/team**
4. Vælg **Privat** (kun inviterede) eller **Offentligt** (alle i organisationen)
5. Giv teamet et klart navn og en beskrivelse
6. Tilføj medlemmer

### Opret en kanal

1. Klik **...** ved teamnavnet → **Tilføj kanal**
2. Giv kanalen et kort, beskrivende navn
3. Vælg type:
   - **Standard**: synlig for alle team-medlemmer
   - **Privat**: kun synlig for udvalgte medlemmer
   - **Delt**: kan deles med folk udenfor teamet
4. Tilføj en beskrivelse så folk ved hvad kanalen er til

### Hvornår skal man oprette et nyt team vs. en kanal?

| Opret et NYT TEAM når... | Opret en NY KANAL når... |
|---------------------------|--------------------------|
| Det er en ny afdeling/gruppe | Det er et emne inden for en eksisterende gruppe |
| Medlemmerne er helt forskellige | Samme folk skal se indholdet |
| Det kræver egne tilladelser | Standard tilladelser er fine |
| Det er et stort, langsigtet projekt | Det er en del af et eksisterende projekts arbejde |

### Arkivér et team

Når et team ikke længere er aktivt:

1. Klik **...** ved teamnavnet → **Administrer team**
2. Klik **Indstillinger** → **Arkivér team**
3. Markér evt. **Gør SharePoint-stedet skrivebeskyttet**
4. Klik **Arkivér**

Arkiverede teams kan stadig søges i og læses, men der kan ikke skrives nye beskeder.

### Navngivningskonventioner

- Brug korte, klare navne: "IT-Support" ikke "IT-Afdelingens Support-Team til Alle Medarbejdere"
- Brug præfiks for projektteams: "Projekt: Ny hjemmeside"
- Undgå personnavne i teamnavne — folk skifter job
- Hold kanalnavne under 3 ord

## Bemærkninger

- Hvert team opretter automatisk en Microsoft 365-gruppe, et SharePoint-site og en delt postkasse
- Der er en grænse på 250 kanaler per team (200 standard + 30 private + 30 delte)
- Et team kan have op til 25.000 medlemmer
- Administratorer kan oprette navngivningspolitikker og skabeloner i Teams Admin Center
- Private kanaler har deres eget SharePoint-site — filer her deles ikke med resten af teamet
- Tab og apps kan tilføjes per kanal for at samle værktøjer ét sted
