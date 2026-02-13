# Delt postkasse — Administrer tilladelser

## Problem

Du skal give eller fjerne brugeres adgang til en delt postkasse i Exchange Online. Typisk skal AutoMapping slås fra, så postkassen ikke automatisk dukker op i Outlook.

## Løsning

### Komplet script: Administrer tilladelser på delt postkasse

```powershell
# =============================================================
# Delt postkasse — Tilføj og fjern tilladelser
# =============================================================

# --- Forbind til Exchange Online ---
Import-Module ExchangeOnlineManagement
Connect-ExchangeOnline -UserPrincipalName admin@ditdomaene.dk

# --- Variabel: Den delte postkasse ---
$DeltPostkasse = "info@ditdomaene.dk"

# --- Tjek eksisterende tilladelser ---
Get-MailboxPermission -Identity $DeltPostkasse |
    Where-Object { $_.User -notlike "NT AUTHORITY*" } |
    Format-Table User, AccessRights, IsInherited

# --- Fjern eksisterende tilladelse for en bruger ---
Remove-MailboxPermission -Identity $DeltPostkasse `
    -User "bruger@ditdomaene.dk" `
    -AccessRights FullAccess `
    -Confirm:$false

# --- Tilføj FullAccess UDEN AutoMapping ---
# AutoMapping $false = postkassen tilføjes IKKE automatisk i Outlook
Add-MailboxPermission -Identity $DeltPostkasse `
    -User "bruger@ditdomaene.dk" `
    -AccessRights FullAccess `
    -AutoMapping $false

# --- Tilføj tilladelse for flere brugere på én gang ---
$Brugere = @(
    "bruger1@ditdomaene.dk",
    "bruger2@ditdomaene.dk",
    "bruger3@ditdomaene.dk"
)

foreach ($Bruger in $Brugere) {
    # Fjern først eventuel eksisterende tilladelse
    Remove-MailboxPermission -Identity $DeltPostkasse `
        -User $Bruger `
        -AccessRights FullAccess `
        -Confirm:$false -ErrorAction SilentlyContinue

    # Tilføj med AutoMapping slået fra
    Add-MailboxPermission -Identity $DeltPostkasse `
        -User $Bruger `
        -AccessRights FullAccess `
        -AutoMapping $false

    Write-Host "Tilladelse tilføjet for: $Bruger" -ForegroundColor Green
}

# --- Bekræft de nye tilladelser ---
Get-MailboxPermission -Identity $DeltPostkasse |
    Where-Object { $_.User -notlike "NT AUTHORITY*" } |
    Format-Table User, AccessRights, IsInherited

# --- Afbryd forbindelsen ---
Disconnect-ExchangeOnline -Confirm:$false
```

### Fjern tilladelse med AutoMapping og gentilføj uden

```powershell
# Hvis en bruger allerede har FullAccess MED AutoMapping,
# skal du fjerne og gentilføje for at slå AutoMapping fra.
# Der er ingen måde at ændre AutoMapping uden at fjerne/tilføje.

Remove-MailboxPermission -Identity "info@ditdomaene.dk" `
    -User "bruger@ditdomaene.dk" `
    -AccessRights FullAccess `
    -Confirm:$false

Add-MailboxPermission -Identity "info@ditdomaene.dk" `
    -User "bruger@ditdomaene.dk" `
    -AccessRights FullAccess `
    -AutoMapping $false
```

## Bemærkninger

- **AutoMapping**: Når `$true` (standard), tilføjer Outlook automatisk den delte postkasse som en ekstra postkasse. Dette er ofte uønsket, fordi:
  - Det fylder i brugerens Outlook-profil
  - Det kan forvirre brugere der ikke forventer postkassen
  - Brugeren kan i stedet tilføje den manuelt via "Åbn en anden postkasse"
- **FullAccess** giver brugeren fuld adgang til at læse, slette og organisere mails i postkassen — men IKKE til at sende som postkassen. Brug `SendAs` til det (se `opret-delt-postkasse.md`).
- Ændringer i tilladelser kan tage op til 60 minutter at slå igennem.
- Brugeren skal muligvis genstarte Outlook for at se ændringerne.
