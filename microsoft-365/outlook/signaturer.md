# Opret og administrer email-signaturer i Outlook

## Problem

En bruger vil oprette, redigere eller administrere email-signaturer i Outlook, så de automatisk indsættes i nye mails og svar.

## Løsning

### Opret signatur i Outlook desktop

1. Åbn Outlook
2. Gå til **Filer** → **Indstillinger** → **Mail**
3. Klik **Signaturer** under afsnittet "Opret eller rediger signaturer"
4. Klik **Ny**
5. Giv signaturen et navn (f.eks. "Standard" eller "Kort")
6. Skriv din signatur i editoren:
   - Brug formateringsværktøjerne til skrifttype, farve og størrelse
   - Indsæt billede via billedikonet (f.eks. firmalogo)
   - Indsæt link via linkikonet (f.eks. til firmaets hjemmeside)
7. Under **Vælg standardsignatur**:
   - **Nye meddelelser:** vælg din signatur
   - **Svar/videresendelser:** vælg signatur eller "(ingen)"
8. Klik **OK**

### Opret signatur i Outlook på web

1. Gå til [outlook.office.com](https://outlook.office.com)
2. Klik tandhjulet → **Vis alle Outlook-indstillinger**
3. Gå til **Mail** → **Skriv og svar**
4. Under **Email-signatur** skriv din signatur
5. Vælg om den skal bruges til nye mails og/eller svar
6. Klik **Gem**

### Eksempel på professionel signatur

```
Med venlig hilsen

Jens Jensen
IT-konsulent

Firma A/S
Telefon: +45 12 34 56 78
Email: jens@firma.dk
Web: www.firma.dk
```

### Tips til god signatur-design

- **Hold det kort** — navn, titel, firma, telefon, email er nok
- **Undgå store billeder** — de fylder i hver eneste mail og blokeres ofte
- **Brug max 2 skriftfarver** — sort tekst med firma-farve på firmanavn
- **Brug ikke for mange skrifttyper** — én skrifttype er bedst
- **Tilføj ikke citater eller reklamer** i professionelle signaturer
- **Mobil-signatur:** husk at opsætte en kortere signatur i Outlook-appen

### Skift mellem flere signaturer

1. Opret flere signaturer (f.eks. "Fuld", "Kort", "Engelsk")
2. Sæt én som standard
3. I en ny mail: klik **Indsæt** → **Signatur** → vælg den ønskede

### Signatur med HTML (avanceret)

Signaturfiler gemmes her:
```
%appdata%\Microsoft\Signatures\
```

Hver signatur har tre filer:
- `.htm` — HTML-version
- `.rtf` — Rich Text-version
- `.txt` — Ren tekst-version

Du kan redigere `.htm`-filen direkte med en HTML-editor for mere kontrol over layoutet.

### Central signatur-styring (administrator)

Administratorer kan opsætte fælles signaturer for hele organisationen via:

1. **Exchange transportregler** — tilføjer signatur server-side
2. **Exchange Admin Center** → **Mailflow** → **Regler** → **Anvend ansvarsfraskrivelser**
3. Tredjepartsløsninger som **CodeTwo**, **Exclaimer** eller **Signatures365**

## Bemærkninger

- Outlook desktop og Outlook på web har separate signaturer — de synkroniserer ikke automatisk
- Nye Outlook synkroniserer signaturer via skyen (roaming signatures) fra version 2024+
- Billeder i signaturer bør hostes online (URL) fremfor at være indlejret — reducerer mailstørrelse
- Ved signaturskift: eksisterende mails i udbakken beholder den gamle signatur
- Test altid signaturen ved at sende en mail til dig selv og tjek den på mobil
