# Dansk opsætning af Outlook

## Problem

Outlook viser engelske menuer, mapper og datoformater. Standardmapperne hedder Inbox, Sent, Drafts og Deleted i stedet for de danske navne.

## Løsning

### Outlook desktop (Windows)

1. Åbn Outlook og gå til **Fil → Indstillinger → Sprog**
2. Under **Office-visningssprog** — tilføj **Dansk** hvis det ikke allerede er der
3. Markér **Dansk** og klik **Angiv som foretrukket**
4. Under **Office-redigeringssprog** — tilføj **Dansk** og sæt som foretrukket
5. Klik **OK** og genstart Outlook

Efter genstart bør standardmapperne skifte til danske navne:

| Engelsk | Dansk |
|---------|-------|
| Inbox | Indbakke |
| Sent Items | Sendt post |
| Drafts | Kladder |
| Deleted Items | Slettet post |
| Junk Email | Uønsket mail |
| Archive | Arkiv |

### Outlook web (outlook.office.com)

1. Klik på **tandhjulet** øverst til højre → **View all Outlook settings**
2. Gå til **General → Language and time**
3. Sæt **Language** til **Dansk**
4. Sæt **Time zone** til **(UTC+01:00) Bruxelles, København, Madrid, Paris**
5. Sæt **Date format** til **dd-MM-yyyy** (eksempel: 13-02-2026)
6. Sæt **Time format** til **HH:mm** (24-timers format)
7. Klik **Save**

### Datoformat og tidszone

Kontrollér at disse indstillinger er korrekte:

- **Tidszone:** (UTC+01:00) Bruxelles, København, Madrid, Paris
- **Datoformat:** dd-MM-yyyy (dag-måned-år med bindestreg)
- **Tidsformat:** HH:mm (24-timers ur, f.eks. 14:30)

Tidszone-indstillingen påvirker mødetidspunkter i kalenderen. Forkert tidszone giver forskudte møder.

### Hvis mapperne ikke skifter til dansk

Nogle gange fastholdes de engelske mappenavne selvom sproget er ændret. Prøv:

1. Log ind på **outlook.office.com**
2. Skift sproget til dansk der (se ovenfor)
3. Log ud og ind igen
4. Åbn Outlook desktop — mapperne bør nu være danske

Hvis det stadig ikke virker, kan en administrator køre denne PowerShell-kommando i Exchange Online:

```
Set-MailboxRegionalConfiguration -Identity bruger@domæne.dk -Language da-DK -LocalizeDefaultFolderName
```

## Bemærkninger

- Sprogændring i Outlook desktop påvirker hele Office-pakken (Word, Excel osv.)
- Outlook web og Outlook desktop har separate sprogindstillinger
- Sommertid (CEST, UTC+02:00) håndteres automatisk — du skal IKKE skifte tidszone manuelt
- Datoformatet dd-MM-yyyy er dansk standard og undgår forveksling med det amerikanske MM/dd/yyyy
