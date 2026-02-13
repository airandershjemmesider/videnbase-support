# Distributionsgrupper i Exchange Online

## Problem

Du skal oprette og administrere distributionsgrupper (maillister) i Exchange Online — tilføje/fjerne medlemmer, sætte afsendelsestilladelser og konvertere mellem gruppetyper.

## Løsning

### Komplet script: Opret og administrer distributionsgruppe

```powershell
# =============================================================
# Distributionsgrupper — Opret, administrer, konvertér
# =============================================================

# --- Forbind til Exchange Online ---
Import-Module ExchangeOnlineManagement
Connect-ExchangeOnline -UserPrincipalName admin@ditdomaene.dk

# --- Opret ny distributionsgruppe ---
New-DistributionGroup `
    -Name "Salg" `
    -DisplayName "Salgsafdelingen" `
    -PrimarySmtpAddress "salg@ditdomaene.dk" `
    -ManagedBy "admin@ditdomaene.dk"

Write-Host "Distributionsgruppe oprettet: salg@ditdomaene.dk" -ForegroundColor Green

# --- Tilføj medlemmer ---
$Medlemmer = @(
    "bruger1@ditdomaene.dk",
    "bruger2@ditdomaene.dk",
    "bruger3@ditdomaene.dk"
)

foreach ($Medlem in $Medlemmer) {
    Add-DistributionGroupMember -Identity "salg@ditdomaene.dk" -Member $Medlem
    Write-Host "Tilføjet: $Medlem" -ForegroundColor Green
}

# --- Fjern et medlem ---
Remove-DistributionGroupMember -Identity "salg@ditdomaene.dk" `
    -Member "bruger3@ditdomaene.dk" `
    -Confirm:$false

# --- Vis alle medlemmer ---
Get-DistributionGroupMember -Identity "salg@ditdomaene.dk" |
    Format-Table DisplayName, PrimarySmtpAddress

# --- Afbryd forbindelsen ---
Disconnect-ExchangeOnline -Confirm:$false
```

### Sæt SendAs-tilladelse på gruppen

```powershell
# --- Forbind til Exchange Online ---
Import-Module ExchangeOnlineManagement
Connect-ExchangeOnline -UserPrincipalName admin@ditdomaene.dk

# Giv en bruger lov til at sende mails SOM gruppen
Add-RecipientPermission -Identity "salg@ditdomaene.dk" `
    -Trustee "bruger@ditdomaene.dk" `
    -AccessRights SendAs `
    -Confirm:$false

# Tjek hvem der har SendAs-tilladelse
Get-RecipientPermission -Identity "salg@ditdomaene.dk" |
    Where-Object { $_.Trustee -notlike "NT AUTHORITY*" } |
    Format-Table Trustee, AccessRights

# --- Afbryd forbindelsen ---
Disconnect-ExchangeOnline -Confirm:$false
```

### Konvertér distributionsgruppe til Microsoft 365 Group

```powershell
# --- Forbind til Exchange Online ---
Import-Module ExchangeOnlineManagement
Connect-ExchangeOnline -UserPrincipalName admin@ditdomaene.dk

# Konvertér fra distributionsgruppe til Microsoft 365 Group
# OBS: Dette giver gruppen et delt SharePoint, OneNote, Teams-kanal, osv.
Upgrade-DistributionGroup -DlIdentities "salg@ditdomaene.dk"

# Tjek status på konverteringen
Get-UnifiedGroup -Identity "salg@ditdomaene.dk" |
    Format-List DisplayName, PrimarySmtpAddress, GroupType

# --- Afbryd forbindelsen ---
Disconnect-ExchangeOnline -Confirm:$false
```

### List alle distributionsgrupper

```powershell
# --- Forbind til Exchange Online ---
Import-Module ExchangeOnlineManagement
Connect-ExchangeOnline -UserPrincipalName admin@ditdomaene.dk

# Alle distributionsgrupper
Get-DistributionGroup -ResultSize Unlimited |
    Format-Table DisplayName, PrimarySmtpAddress, GroupType

# Alle Microsoft 365 Groups
Get-UnifiedGroup -ResultSize Unlimited |
    Format-Table DisplayName, PrimarySmtpAddress

# --- Afbryd forbindelsen ---
Disconnect-ExchangeOnline -Confirm:$false
```

### Tillad eksterne afsendere

```powershell
# --- Forbind til Exchange Online ---
Import-Module ExchangeOnlineManagement
Connect-ExchangeOnline -UserPrincipalName admin@ditdomaene.dk

# Tillad at eksterne afsendere (uden for organisationen) kan sende til gruppen
Set-DistributionGroup -Identity "salg@ditdomaene.dk" `
    -RequireSenderAuthenticationEnabled $false

# Begræns igen til kun interne afsendere
Set-DistributionGroup -Identity "salg@ditdomaene.dk" `
    -RequireSenderAuthenticationEnabled $true

# --- Afbryd forbindelsen ---
Disconnect-ExchangeOnline -Confirm:$false
```

## Bemærkninger

### Forskel på gruppetyper

| Type | Beskrivelse | Ekstra funktioner |
|---|---|---|
| **Distributionsgruppe** | Simpel mailliste til at sende til flere modtagere | Kun mail |
| **Sikkerhedsgruppe med mail** | Mailliste + kan bruges til tilladelser i Azure AD | Mail + adgangsstyring |
| **Microsoft 365 Group** | Moderne gruppe med delt postkasse, kalender, filer | Mail + SharePoint + Teams + OneNote |

- **Konvertering** fra distributionsgruppe til Microsoft 365 Group kan ikke fortrydes. Den gamle distributionsgruppe slettes.
- **ManagedBy** angiver hvem der kan redigere gruppens medlemmer via Exchange Admin Center.
- **RequireSenderAuthenticationEnabled**: Standard er `$true` (kun interne afsendere). Sæt til `$false` for grupper der skal modtage mails udefra (f.eks. support@ditdomaene.dk).
- Dynamiske distributionsgrupper (der automatisk inkluderer brugere baseret på attributter) oprettes med `New-DynamicDistributionGroup` — se Microsofts dokumentation.
