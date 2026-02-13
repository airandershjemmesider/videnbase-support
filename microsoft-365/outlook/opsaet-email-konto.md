# Opsæt ny email-konto i Outlook (Microsoft 365)

## Problem

En bruger skal have opsat sin Microsoft 365 email-konto i Outlook desktop-klienten for første gang, eller kontoen skal tilføjes på en ny computer.

## Løsning

### Metode 1: Automatisk opsætning (anbefalet)

1. Åbn Outlook
2. Hvis det er første gang: guiden starter automatisk
3. Skriv din email-adresse (f.eks. `bruger@firma.dk`)
4. Klik **Opret forbindelse**
5. Outlook finder automatisk serverindstillingerne via Autodiscover
6. Indtast din adgangskode når du bliver bedt om det
7. Hvis MFA (multifaktor-godkendelse) er aktiveret: godkend med Authenticator-appen eller SMS
8. Klik **Udfør** — Outlook begynder at synkronisere

### Metode 2: Tilføj en ekstra konto

Hvis Outlook allerede har en konto og du vil tilføje en ny:

1. Gå til **Filer** → **Tilføj konto**
2. Skriv email-adressen og klik **Opret forbindelse**
3. Indtast adgangskode og godkend MFA hvis påkrævet
4. Klik **Udfør**
5. Genstart Outlook for at fuldføre opsætningen

### Metode 3: Manuel opsætning (sjældent nødvendigt)

Hvis automatisk opsætning fejler:

1. Gå til **Filer** → **Tilføj konto**
2. Klik **Avancerede indstillinger** → markér **Lad mig konfigurere min konto manuelt**
3. Vælg **Microsoft 365** som kontotype
4. Skriv email-adressen
5. Indtast adgangskode og godkend MFA
6. Outlook opretter forbindelse via Exchange Online

### Serverindstillinger (til reference)

| Indstilling | Værdi |
|-------------|-------|
| Kontotype | Exchange / Microsoft 365 |
| Server | outlook.office365.com |
| Port (IMAP) | 993 (SSL) |
| Port (SMTP) | 587 (TLS) |
| Godkendelse | OAuth 2.0 / Modern Authentication |

### Fejlfinding ved opsætning

**"Vi kan ikke oprette forbindelse lige nu":**
- Tjek internetforbindelsen
- Prøv at logge ind på [outlook.office.com](https://outlook.office.com) først
- Sørg for at adgangskoden er korrekt

**Outlook beder om adgangskode igen og igen:**
- Slet gemte legitimationsoplysninger: **Kontrolpanel** → **Legitimationsadministrator** → slet Microsoft Office-poster
- Genstart Outlook

**MFA-loop (bliver ved med at bede om godkendelse):**
- Opdater Outlook til seneste version
- Sørg for at Modern Authentication er aktiveret i din M365-tenant

## Bemærkninger

- Outlook synkroniserer som standard de seneste 12 måneder — dette kan ændres under **Filer** → **Kontoindstillinger** → **Skift** → **Offlineindstillinger**
- Første synkronisering kan tage lang tid for store postkasser
- Basic Authentication er udfaset — alle M365-konti bruger nu Modern Authentication (OAuth 2.0)
- Nye Outlook-klienten kræver ingen manuel opsætning — log blot ind med din M365-konto
- Outlook-appen til mobil opsættes tilsvarende: åbn appen, skriv email, godkend med MFA
