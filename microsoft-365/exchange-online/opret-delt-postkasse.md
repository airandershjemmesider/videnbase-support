# Opret delt postkasse i Exchange Online

## Problem

Du skal oprette en ny delt postkasse (shared mailbox), give brugere adgang og konfigurere afsendelsestilladelser.

## Løsning

### Komplet script: Opret delt postkasse med tilladelser

```powershell
# =============================================================
# Opret delt postkasse og konfigurér tilladelser
# =============================================================

# --- Forbind til Exchange Online ---
Import-Module ExchangeOnlineManagement
Connect-ExchangeOnline -UserPrincipalName admin@ditdomaene.dk

# --- Opret den delte postkasse ---
New-Mailbox -Shared `
    -Name "Info" `
    -DisplayName "Info - Ditdomaene" `
    -PrimarySmtpAddress "info@ditdomaene.dk"

# --- Tilføj FullAccess for brugere (uden AutoMapping) ---
$Brugere = @(
    "bruger1@ditdomaene.dk",
    "bruger2@ditdomaene.dk"
)

foreach ($Bruger in $Brugere) {
    # FullAccess — adgang til at læse og administrere mails
    Add-MailboxPermission -Identity "info@ditdomaene.dk" `
        -User $Bruger `
        -AccessRights FullAccess `
        -AutoMapping $false

    # SendAs — adgang til at sende mails SOM postkassen
    Add-RecipientPermission -Identity "info@ditdomaene.dk" `
        -Trustee $Bruger `
        -AccessRights SendAs `
        -Confirm:$false

    Write-Host "FullAccess + SendAs tilføjet for: $Bruger" -ForegroundColor Green
}

# --- Bekræft opsætningen ---
Write-Host "`n--- Postkasse-info ---" -ForegroundColor Cyan
Get-Mailbox -Identity "info@ditdomaene.dk" |
    Format-List Name, DisplayName, PrimarySmtpAddress, RecipientTypeDetails

Write-Host "`n--- FullAccess-tilladelser ---" -ForegroundColor Cyan
Get-MailboxPermission -Identity "info@ditdomaene.dk" |
    Where-Object { $_.User -notlike "NT AUTHORITY*" } |
    Format-Table User, AccessRights

Write-Host "`n--- SendAs-tilladelser ---" -ForegroundColor Cyan
Get-RecipientPermission -Identity "info@ditdomaene.dk" |
    Where-Object { $_.Trustee -notlike "NT AUTHORITY*" } |
    Format-Table Trustee, AccessRights

# --- Afbryd forbindelsen ---
Disconnect-ExchangeOnline -Confirm:$false
```

### Tilføj SendOnBehalf-tilladelse

```powershell
# SendOnBehalf — brugeren sender "på vegne af" postkassen
# Modtageren ser: "Bruger på vegne af Info"
Set-Mailbox -Identity "info@ditdomaene.dk" `
    -GrantSendOnBehalfTo "bruger@ditdomaene.dk"

# Tilføj flere brugere til SendOnBehalf
Set-Mailbox -Identity "info@ditdomaene.dk" `
    -GrantSendOnBehalfTo @{Add="bruger2@ditdomaene.dk"}
```

## Bemærkninger

### Forskel på tilladelsestyper

| Tilladelse | Hvad den gør | Modtager ser |
|---|---|---|
| **FullAccess** | Læse, slette, organisere mails i postkassen | — (gælder ikke afsendelse) |
| **SendAs** | Sende mails som postkassen | Fra: info@ditdomaene.dk |
| **SendOnBehalf** | Sende på vegne af postkassen | Fra: bruger@ditdomaene.dk på vegne af info@ditdomaene.dk |

- **FullAccess** alene giver IKKE ret til at sende mails fra postkassen. Du skal altid tilføje enten SendAs eller SendOnBehalf separat.
- **SendAs** er mest brugt til delte postkasser — modtageren ser postkassens adresse som afsender.
- **SendOnBehalf** viser tydeligt hvem der faktisk sendte mailen — nyttigt til sporing.
- En delt postkasse kræver ikke en licens, medmindre den skal have mere end 50 GB lagerplads eller et online-arkiv.
- Det kan tage op til 60 minutter før tilladelserne er aktive.
