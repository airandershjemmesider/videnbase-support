# Udskriftskøen sidder fast

## Problem

Udskriftsjobs hænger i køen og kan ikke slettes eller udskrives. Nye udskriftsjobs hænger også fast.

## Løsning

### 1. Annullér alle udskriftsjobs

1. Åbn **Indstillinger** → **Bluetooth og enheder** → **Printere og scannere**
2. Klik på den pågældende printer
3. Klik **Åbn udskriftskø**
4. Klik **Printer** i menuen → **Annuller alle dokumenter**

### 2. Genstart Print Spooler-tjenesten

Hvis annullering ikke virker:

1. Tryk **Win + R**, skriv `services.msc` og tryk Enter
2. Find **Print Spooler** i listen
3. Højreklik → **Stop**
4. Vent 10 sekunder
5. Højreklik → **Start**
6. Prøv at udskrive igen

### 3. Ryd printerkøen manuelt (hvis trin 2 ikke virker)

Åbn **Kommandoprompt som administrator** og kør følgende kommandoer:

```cmd
net stop spooler
del /Q /F /S "%systemroot%\System32\spool\PRINTERS\*.*"
net start spooler
```

Dette stopper tjenesten, sletter alle ventende udskriftsjobs, og starter tjenesten igen.

### 4. Genstart printeren

1. Sluk printeren helt (ikke bare standby)
2. Vent 30 sekunder
3. Tænd printeren
4. Vent til den er klar (lys holder op med at blinke)
5. Prøv at udskrive igen

### 5. Opret en hurtig genvej (til gentagne problemer)

Opret en batch-fil på skrivebordet med navnet `ryd-printer.bat`:

```bat
@echo off
net stop spooler
timeout /t 3
del /Q /F /S "%systemroot%\System32\spool\PRINTERS\*.*"
net start spooler
echo Printerkøen er ryddet!
pause
```

Højreklik → **Kør som administrator** når det er nødvendigt.

## Bemærkninger

- Udskriftskøen sidder typisk fast pga. korrupte udskriftsfiler, driverproblemer eller kommunikationsfejl med printeren
- Hvis problemet gentager sig ofte, opdatér eller geninstallér printerdriveren
- Store udskriftsjobs (mange sider, høj opløsning) har større chance for at sætte køen fast
- Tjek at printeren ikke er i fejltilstand (papirstop, tomt blæk/toner, åben klap)
- Nogle printere har en egen kø internt — sluk og tænd printeren for at rydde den
