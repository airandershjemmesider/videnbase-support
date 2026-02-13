# Regional opsætning af postkasser (dansk)

## Problem

Nye postkasser i Exchange Online har som standard engelsk sprog og amerikanske dato/tidsformater. Du skal sætte dansk sprog, dansk tidszone og danske formater.

## Løsning

### Komplet script: Sæt dansk regional konfiguration

```powershell
# =============================================================
# Regional opsætning — Dansk sprog og formater på postkasser
# =============================================================

# --- Forbind til Exchange Online ---
Import-Module ExchangeOnlineManagement
Connect-ExchangeOnline -UserPrincipalName admin@ditdomaene.dk

# --- Sæt dansk konfiguration på én enkelt postkasse ---
Set-MailboxRegionalConfiguration -Identity "bruger@ditdomaene.dk" `
    -Language da-DK `
    -TimeZone "W. Europe Standard Time" `
    -DateFormat "dd-MM-yyyy" `
    -TimeFormat "HH:mm" `
    -LocalizeDefaultFolderName:$true

Write-Host "Regional konfiguration sat for: bruger@ditdomaene.dk" -ForegroundColor Green

# --- Tjek den aktuelle regionale konfiguration ---
Get-MailboxRegionalConfiguration -Identity "bruger@ditdomaene.dk" |
    Format-List Language, TimeZone, DateFormat, TimeFormat

# --- Bulk: Sæt dansk konfiguration på ALLE postkasser ---
Get-Mailbox -ResultSize Unlimited | ForEach-Object {
    Set-MailboxRegionalConfiguration -Identity $_.UserPrincipalName `
        -Language da-DK `
        -TimeZone "W. Europe Standard Time" `
        -DateFormat "dd-MM-yyyy" `
        -TimeFormat "HH:mm" `
        -LocalizeDefaultFolderName:$true

    Write-Host "Konfigureret: $($_.UserPrincipalName)" -ForegroundColor Green
}

# --- Bulk: Kun delte postkasser ---
Get-Mailbox -RecipientTypeDetails SharedMailbox -ResultSize Unlimited | ForEach-Object {
    Set-MailboxRegionalConfiguration -Identity $_.UserPrincipalName `
        -Language da-DK `
        -TimeZone "W. Europe Standard Time" `
        -DateFormat "dd-MM-yyyy" `
        -TimeFormat "HH:mm" `
        -LocalizeDefaultFolderName:$true

    Write-Host "Delt postkasse konfigureret: $($_.DisplayName)" -ForegroundColor Green
}

# --- Bekræft alle postkassers regionale indstillinger ---
Get-Mailbox -ResultSize Unlimited | ForEach-Object {
    $Config = Get-MailboxRegionalConfiguration -Identity $_.UserPrincipalName
    [PSCustomObject]@{
        Postkasse  = $_.DisplayName
        Sprog      = $Config.Language
        Tidszone   = $Config.TimeZone
        Datoformat = $Config.DateFormat
        Tidsformat = $Config.TimeFormat
    }
} | Format-Table -AutoSize

# --- Afbryd forbindelsen ---
Disconnect-ExchangeOnline -Confirm:$false
```

## Bemærkninger

- **Language da-DK**: Sætter sproget til dansk. Påvirker bl.a. mappenavne i Outlook Web (Indbakke, Sendt post, osv.).
- **LocalizeDefaultFolderName**: Når `$true`, oversættes standardmapper (Inbox → Indbakke, Sent Items → Sendt post, osv.). Virker kun i Outlook Web — Outlook-klienten bruger sin egen lokalisering.
- **TimeZone "W. Europe Standard Time"**: Dansk tidszone (CET/CEST) med automatisk sommertid.
- **DateFormat "dd-MM-yyyy"**: Dansk datoformat (dag-måned-år), f.eks. 13-02-2026.
- **TimeFormat "HH:mm"**: 24-timers format, f.eks. 14:30.
- Bulk-operationen kan tage lang tid ved mange postkasser. PowerShell viser fremskridt med `Write-Host`.
- Kør bulk-scriptet efter oprettelse af nye postkasser, da nye postkasser ikke arver regionale indstillinger automatisk.
