# Outlook søgefunktion virker ikke

## Problem

Søgningen i Outlook finder ikke mails, selv om de findes i postkassen. Søgeresultaterne er ufuldstændige, eller der vises "Ingen resultater fundet" for mails man ved eksisterer.

## Løsning

### 1. Genopbyg søgeindekset i Outlook

1. Åbn Outlook
2. Gå til **Filer** → **Indstillinger** → **Søg**
3. Klik **Indekseringsindstillinger**
4. Klik **Avanceret**
5. Under **Fejlfinding** klik **Genopbyg**
6. Klik **OK** og vent — genopbygning kan tage fra 15 minutter til flere timer afhængigt af postkassens størrelse
7. Genstart Outlook når den er færdig

### 2. Tjek at Outlook er inkluderet i søgeindekset

1. Åbn **Windows-indstillinger** → **Søgning** → **Søgning i Windows**
2. Klik **Avancerede indstillinger for søgeindeksering**
3. Klik **Rediger**
4. Tjek at **Microsoft Outlook** er markeret med flueben
5. Hvis ikke: markér den og klik **OK**

### 3. Kør Outlook i fejlsikret tilstand

1. Luk Outlook
2. Tryk **Win + R**, skriv `outlook.exe /safe` og tryk Enter
3. Prøv søgningen i fejlsikret tilstand
4. Hvis søgning virker her, er et tilføjelsesprogram skyld i problemet

### 4. Deaktiver problematiske tilføjelsesprogrammer

1. Gå til **Filer** → **Indstillinger** → **Tilføjelsesprogrammer**
2. Vælg **COM-tilføjelsesprogrammer** i bunden og klik **Start**
3. Fjern flueben fra alle tilføjelser
4. Genstart Outlook og test søgning
5. Aktivér tilføjelser én ad gangen for at finde synderen

### 5. Reparer Office-installationen

1. Åbn **Indstillinger** → **Apps** → **Installerede apps**
2. Find **Microsoft 365** og klik de tre prikker → **Rediger**
3. Vælg **Onlinereparation** og klik **Reparer**
4. Vent til reparationen er færdig og genstart computeren

### 6. Nulstil søgeindekset via Registry (avanceret)

1. Tryk **Win + R**, skriv `regedit` og tryk Enter
2. Naviger til `HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Outlook\Search`
3. Højreklik på **Search** → **Ny** → **DWORD (32-bit) værdi**
4. Navngiv den `ResetSearchCriteria` og sæt værdien til `1`
5. Genstart Outlook

## Bemærkninger

- Genopbygning af indeks bruger meget CPU — gør det gerne ved fyraften
- Søgeindekset fylder typisk 1-5 % af postkassens størrelse
- Nye Outlook (den nye version) bruger cloud-baseret søgning og har sjældent dette problem
- Hvis problemet kun gælder delte postkasser, kan det skyldes at de ikke er fuldt cachet lokalt
- Windows Search-tjenesten (WSearch) skal køre — tjek i `services.msc`
