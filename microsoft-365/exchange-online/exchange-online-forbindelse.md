# Exchange Online — Forbindelse og opsætning

## Problem

Du skal forbinde til Exchange Online via PowerShell for at administrere postkasser, tilladelser og mailflow. Modulet skal installeres og konfigureres korrekt først.

## Løsning

### Komplet script: Installer og forbind

```powershell
# =============================================================
# Exchange Online Management — Installation og forbindelse
# =============================================================

# --- Trin 1: Sæt execution policy så scripts kan køre ---
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser -Force

# --- Trin 2: Installér Exchange Online Management-modulet ---
# Kør kun første gang (eller ved opdatering)
Install-Module ExchangeOnlineManagement -Scope CurrentUser -Force

# --- Trin 3: Importér modulet ---
Import-Module ExchangeOnlineManagement

# --- Trin 4: Forbind til Exchange Online ---
# Metode A: Interaktivt login (åbner browservindue)
Connect-ExchangeOnline -UserPrincipalName admin@ditdomaene.dk

# Metode B: Med credential-objekt (til scripts)
$Credential = Get-Credential
Connect-ExchangeOnline -Credential $Credential

# --- Trin 5: Bekræft forbindelsen ---
# Hent en postkasse for at teste at forbindelsen virker
Get-Mailbox -ResultSize 1

# --- Trin 6: Afbryd forbindelsen når du er færdig ---
Disconnect-ExchangeOnline -Confirm:$false
```

### Opdatér modulet

```powershell
# Opdatér til nyeste version af modulet
Update-Module ExchangeOnlineManagement -Force

# Tjek hvilken version der er installeret
Get-Module ExchangeOnlineManagement -ListAvailable | Select-Object Version
```

### Forbind til specifik tenant

```powershell
# Hvis du administrerer flere tenants, angiv Organisation
Connect-ExchangeOnline -UserPrincipalName admin@ditdomaene.dk -Organization ditdomaene.onmicrosoft.com
```

## Bemærkninger

- **Execution Policy**: `RemoteSigned` tillader lokale scripts og kræver signering af downloadede scripts. Det er den anbefalede indstilling.
- **Scope CurrentUser**: Installerer modulet kun for den aktuelle bruger — kræver ikke administratorrettigheder.
- **Interaktivt login** (Metode A) understøtter MFA og er den anbefalede metode til daglig brug.
- **Credential-objekt** (Metode B) virker kun for konti uden MFA. Bruges primært i automatiserede scripts.
- **Afbryd altid** forbindelsen med `Disconnect-ExchangeOnline` når du er færdig, så du ikke bruger unødvendige sessioner.
- Microsoft tillader maksimalt 3 samtidige Exchange Online PowerShell-sessioner per bruger.
