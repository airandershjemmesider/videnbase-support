# Opsæt automatisk svar / Out of Office i Outlook

## Problem

En bruger skal opsætte automatisk svar (Out of Office / fravær) i Outlook, så afsendere får besked om at brugeren ikke er tilgængelig.

## Løsning

### Metode 1: Outlook desktop

1. Åbn Outlook
2. Gå til **Filer** → **Automatiske svar (Ikke til stede)**
3. Vælg **Send automatiske svar**
4. Valgfrit: sæt **Start tidspunkt** og **Slut tidspunkt** for perioden
5. Skriv din besked i fanen **Inden for organisationen** (til kolleger)
6. Skift til fanen **Uden for organisationen** og skriv en besked til eksterne afsendere
7. Vælg om eksterne svar skal sendes til **Kun mine kontakter** eller **Alle uden for organisationen**
8. Klik **OK**

### Metode 2: Outlook på web

1. Gå til [outlook.office.com](https://outlook.office.com)
2. Klik tandhjulet øverst til højre → **Vis alle Outlook-indstillinger**
3. Gå til **Mail** → **Automatiske svar**
4. Slå **Automatiske svar til**
5. Sæt tidsperiode hvis ønsket
6. Skriv besked til interne og eksterne afsendere
7. Klik **Gem**

### Metode 3: Outlook mobil-app

1. Åbn Outlook-appen
2. Tryk på dit profilbillede øverst til venstre
3. Tryk tandhjulet (Indstillinger)
4. Tryk på din email-konto
5. Tryk **Automatiske svar**
6. Slå det til og skriv din besked

### Eksempel på intern besked

```
Tak for din mail. Jeg er fraværende fra [dato] til [dato] og har begrænset adgang til email.

Ved hastende henvendelser kontakt venligst [navn] på [email/telefon].

Jeg vender tilbage til dig hurtigst muligt efter min tilbagekomst.

Venlig hilsen
[Navn]
```

### Eksempel på ekstern besked

```
Tak for din henvendelse. Jeg er fraværende fra kontoret i perioden [dato] til [dato].

Jeg har ikke adgang til email i perioden. Ved hastende sager kontakt venligst [navn] på [email/telefon].

Jeg besvarer din mail, når jeg er tilbage.

Med venlig hilsen
[Navn]
[Firma]
```

### Deaktiver automatisk svar

- Outlook viser en gul bjælke øverst: klik **Deaktiver** for at slå det fra
- Eller gå til **Filer** → **Automatiske svar** → vælg **Send ikke automatiske svar**
- Hvis du har sat et sluttidspunkt, slås det automatisk fra

## Bemærkninger

- Automatisk svar sendes kun én gang per afsender i perioden (for at undgå spam-loops)
- Administratorer kan opsætte automatisk svar for andre brugere via Exchange Admin Center eller PowerShell
- Regler kan kombineres med automatisk svar (f.eks. videresend hastende mails til en kollega)
- Tjek altid at sluttidspunktet er korrekt — glemte automatiske svar er en klassiker
- Den eksterne besked bør ikke indeholde følsomme oplysninger om hvorfor du er væk
