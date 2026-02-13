# Dansk opsætning af Microsoft Teams

## Problem

Teams viser engelske menuer og indstillinger. Tastatur-genveje passer ikke til dansk tastaturlayout.

## Løsning

### Teams desktop (Windows)

1. Klik på de **tre prikker (...)** ved dit profilbillede øverst til højre
2. Vælg **Indstillinger** (eller **Settings** hvis sproget er engelsk)
3. Gå til **Generelt → Sprog**
4. Vælg **Dansk** i dropdown-menuen
5. Klik **Gem og genstart** — Teams skal genstartes for at sprogændringen træder i kraft

I nyere versioner af Teams (New Teams):

1. Klik på de **tre prikker (...)** ved dit profilbillede
2. Vælg **Indstillinger → Generelt**
3. Under **Sprog** — vælg **Dansk**
4. Teams genstarter automatisk

### Teams web (teams.microsoft.com)

Teams web bruger det sprog, der er indstillet i browseren. For at få dansk Teams web:

1. Sæt browserens foretrukne sprog til **Dansk** (se browserens sprogindstillinger)
2. Genindlæs Teams-siden
3. Alternativt: Skift sproget via Microsoft 365-profilen på **myaccount.microsoft.com → Indstillinger → Sprog og område**

### Tidszone

Teams henter tidszonen fra operativsystemet (Windows). Kontrollér at Windows er sat til:

- **Tidszone:** (UTC+01:00) Bruxelles, København, Madrid, Paris
- **Justér automatisk for sommertid:** Slået til

Tidszonen kan også sættes direkte i Outlook (som deles med Teams-kalenderen).

### Tastatur-genveje med dansk layout

Nogle genveje ændrer sig når man bruger dansk tastaturlayout, fordi æøå-tasterne optager pladser der bruges anderledes på engelsk layout.

Vigtige genveje der virker uændret:

| Funktion | Genvej |
|----------|--------|
| Søg | Ctrl + E |
| Ny chat | Ctrl + N |
| Slå mikrofon til/fra | Ctrl + Shift + M |
| Slå kamera til/fra | Ctrl + Shift + O |
| Ræk hånden op | Ctrl + Shift + K |
| Del skærm | Ctrl + Shift + E |

Genveje der kan give problemer med dansk layout:

| Funktion | Engelsk layout | Bemærkning |
|----------|---------------|------------|
| Gå til kommandofeltet | Ctrl + / | Skråstreg ligger anderledes på dansk tastatur (Shift + 7) |
| Vedhæft fil | Ctrl + O | Virker normalt, men kan konflikte med æ-tasten i visse apps |

### Stavekontrol

Teams bruger Windows' stavekontrol. Sørg for at dansk stavekontrol er installeret:

1. **Windows Indstillinger → Tid og sprog → Sprog og område**
2. Kontrollér at **Dansk** er tilføjet som sprog
3. Klik på **Dansk → Sprogindstillinger** og installér **Stavekontrol**

## Bemærkninger

- Sprogændringen i Teams desktop kræver altid en genstart af programmet
- Teams web følger browserens sprog — ikke Teams' egne indstillinger
- Kalender-tidspunkter i Teams styres af Outlook/Exchange-indstillingerne
- Sommertid håndteres automatisk af Windows
- Hvis Teams er udrullet via virksomhedens MDM/Intune, kan sprogindstillingen være låst af administratoren
