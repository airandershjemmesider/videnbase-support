# Exchange Online — Fejlsøgning

## Problem

Gængse fejl og problemer ved administration af Exchange Online via PowerShell.

## Løsning

### Fejl: "Forbindelsen blev afbrudt" / session timeout

```powershell
# Exchange Online-sessioner udløber efter inaktivitet.
# Løsning: Afbryd og opret ny forbindelse.

Disconnect-ExchangeOnline -Confirm:$false
Import-Module ExchangeOnlineManagement
Connect-ExchangeOnline -UserPrincipalName admin@ditdomaene.dk
```

### Fejl: "Modulet ExchangeOnlineManagement er ikke fundet"

```powershell
# Modulet er ikke installeret eller ikke tilgængeligt.

# Tjek om modulet er installeret
Get-Module ExchangeOnlineManagement -ListAvailable

# Installér modulet (hvis det mangler)
Install-Module ExchangeOnlineManagement -Scope CurrentUser -Force

# Opdatér modulet (hvis versionen er for gammel)
Update-Module ExchangeOnlineManagement -Force

# Tjek at execution policy tillader moduler
Get-ExecutionPolicy
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser -Force
```

### Fejl: Tilladelser virker ikke / bruger kan ikke se postkassen

```powershell
# --- Forbind til Exchange Online ---
Import-Module ExchangeOnlineManagement
Connect-ExchangeOnline -UserPrincipalName admin@ditdomaene.dk

# --- Tjek FullAccess-tilladelser på postkassen ---
Get-MailboxPermission -Identity "info@ditdomaene.dk" |
    Where-Object { $_.User -notlike "NT AUTHORITY*" } |
    Format-Table User, AccessRights, IsInherited

# --- Tjek SendAs-tilladelser ---
Get-RecipientPermission -Identity "info@ditdomaene.dk" |
    Where-Object { $_.Trustee -notlike "NT AUTHORITY*" } |
    Format-Table Trustee, AccessRights

# --- Tjek SendOnBehalf-tilladelser ---
Get-Mailbox -Identity "info@ditdomaene.dk" |
    Select-Object GrantSendOnBehalfTo

# --- Tjek om postkassen overhovedet eksisterer ---
Get-Mailbox -Identity "info@ditdomaene.dk" |
    Format-List Name, PrimarySmtpAddress, RecipientTypeDetails

# --- Afbryd forbindelsen ---
Disconnect-ExchangeOnline -Confirm:$false
```

**Typiske årsager:**
- Tilladelser kan tage op til 60 minutter at slå igennem
- Brugeren skal genstarte Outlook
- AutoMapping er slået fra — brugeren skal tilføje postkassen manuelt

### Fejl: Mail leveres ikke / sporring af mails

```powershell
# --- Forbind til Exchange Online ---
Import-Module ExchangeOnlineManagement
Connect-ExchangeOnline -UserPrincipalName admin@ditdomaene.dk

# --- Message Trace: Spor en specifik mail (sidste 10 dage) ---
Get-MessageTrace `
    -SenderAddress "afsender@eksempel.dk" `
    -RecipientAddress "bruger@ditdomaene.dk" `
    -StartDate (Get-Date).AddDays(-10) `
    -EndDate (Get-Date) |
    Format-Table Received, SenderAddress, RecipientAddress, Subject, Status

# --- Alle mails til en bestemt modtager ---
Get-MessageTrace `
    -RecipientAddress "bruger@ditdomaene.dk" `
    -StartDate (Get-Date).AddDays(-2) `
    -EndDate (Get-Date) |
    Format-Table Received, SenderAddress, Subject, Status

# --- Alle fejlede leveringer ---
Get-MessageTrace `
    -StartDate (Get-Date).AddDays(-7) `
    -EndDate (Get-Date) `
    -Status Failed |
    Format-Table Received, SenderAddress, RecipientAddress, Subject

# --- Afbryd forbindelsen ---
Disconnect-ExchangeOnline -Confirm:$false
```

### Diagnostik: Nyttige kommandoer til fejlsøgning

```powershell
# --- Forbind til Exchange Online ---
Import-Module ExchangeOnlineManagement
Connect-ExchangeOnline -UserPrincipalName admin@ditdomaene.dk

# --- Tjek postkassens størrelse og kvote ---
Get-MailboxStatistics -Identity "bruger@ditdomaene.dk" |
    Select-Object DisplayName, TotalItemSize, ItemCount

# --- Tjek postkassens type (User, Shared, Room, etc.) ---
Get-Mailbox -Identity "bruger@ditdomaene.dk" |
    Select-Object DisplayName, RecipientTypeDetails, PrimarySmtpAddress

# --- List alle delte postkasser ---
Get-Mailbox -RecipientTypeDetails SharedMailbox -ResultSize Unlimited |
    Format-Table DisplayName, PrimarySmtpAddress

# --- Tjek om postkassen er blokeret ---
Get-Mailbox -Identity "bruger@ditdomaene.dk" |
    Select-Object DisplayName, AccountDisabled

# --- Tjek mail-flow regler (transport rules) ---
Get-TransportRule | Format-Table Name, State, Priority

# --- Afbryd forbindelsen ---
Disconnect-ExchangeOnline -Confirm:$false
```

## Bemærkninger

- **Message Trace** dækker de seneste 10 dage. For ældre mails skal du bruge "Historical Search" i Exchange Admin Center.
- **Status-værdier** i Message Trace: `Delivered` (leveret), `Failed` (fejlet), `Pending` (afventer), `Filtered` (filtreret som spam/malware), `Quarantined` (sat i karantæne).
- Kør altid `Disconnect-ExchangeOnline` inden du opretter en ny forbindelse — ellers risikerer du at ramme grænsen på 3 samtidige sessioner.
- Ved vedvarende leveringsproblemer: Tjek MX-records og SPF/DKIM/DMARC-opsætning i DNS.
