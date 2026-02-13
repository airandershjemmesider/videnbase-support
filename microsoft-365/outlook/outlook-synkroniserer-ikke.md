# Outlook synkroniserer ikke email

## Problem

Outlook modtager eller sender ikke nye mails. Mails sidder fast i udbakken, eller indbakken opdateres ikke. Statuslinjen viser "Afbrudt", "Forsøger at oprette forbindelse" eller "Arbejder offline".

## Løsning

### 1. Tjek om Outlook er i offline-tilstand

1. Åbn Outlook
2. Gå til fanen **Send/modtag**
3. Tjek om knappen **Arbejd offline** er aktiv (fremhævet)
4. Hvis ja: klik på **Arbejd offline** for at deaktivere den
5. Statuslinjen nederst skal vise **Tilsluttet til: Microsoft Exchange** (eller lignende)

### 2. Tving en manuel synkronisering

1. Gå til fanen **Send/modtag**
2. Klik **Send/modtag alle mapper** (eller tryk **F9**)
3. Vent og se om mails kommer igennem

### 3. Reparer Outlook-profilen

1. Luk Outlook helt
2. Åbn **Kontrolpanel** → **Mail (Microsoft Outlook)**
3. Klik **Email-konti** → vælg kontoen
4. Klik **Reparer**
5. Følg guiden og genstart Outlook

### 4. Ryd Outlook-cachen

1. Luk Outlook helt
2. Tryk **Win + R**, skriv `%localappdata%\Microsoft\Outlook` og tryk Enter
3. Slet indholdet af mappen **RoamCache**
4. Start Outlook igen — cachen genopbygges automatisk

### 5. Opret en ny Outlook-profil

Hvis intet andet virker:

1. Åbn **Kontrolpanel** → **Mail (Microsoft Outlook)**
2. Klik **Vis profiler** → **Tilføj**
3. Giv profilen et navn og tilføj din email-konto
4. Sæt den nye profil som standard
5. Start Outlook og vent på at mails synkroniserer

### 6. Tjek i Outlook på web

1. Gå til [outlook.office.com](https://outlook.office.com)
2. Log ind med din arbejdskonto
3. Hvis mails vises her men ikke i desktop-Outlook, er problemet lokalt

## Bemærkninger

- Outlook-cachen (OST-filen) kan blive korrupt ved strømafbrydelser eller tvangslukning
- Store postkasser (over 50 GB) kan give synkroniseringsproblemer — arkivér gamle mails
- Tjek altid internetforbindelsen først
- Antivirus/firewall kan blokere Outlook — prøv midlertidigt at deaktivere
- Hvis problemet rammer flere brugere samtidig, tjek Microsoft 365 servicestatus på [status.office.com](https://status.office.com)
