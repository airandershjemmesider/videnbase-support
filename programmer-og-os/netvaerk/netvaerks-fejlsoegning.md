# Generel netværksfejlsøgning (ping, tracert, ipconfig)

## Problem

Netværket fungerer ikke korrekt, og du har brug for at fejlsøge systematisk for at finde årsagen.

## Løsning

### 1. ipconfig — se din netværkskonfiguration

Åbn **Kommandoprompt** og kør:

```cmd
ipconfig
```

Tjek følgende:
- **IPv4-adresse:** Din computers IP (typisk 192.168.x.x). Hvis den starter med 169.254.x.x har computeren IKKE fået en IP fra routeren
- **Undernetmaske:** Typisk 255.255.255.0
- **Standardgateway:** Din routers IP (typisk 192.168.1.1 eller 192.168.0.1)

For mere detaljer:

```cmd
ipconfig /all
```

Viser også DNS-server, DHCP-server, MAC-adresse og mere.

### 2. ping — test forbindelsen

**Test forbindelse til routeren:**

```cmd
ping 192.168.1.1
```

(Erstat med din gateways IP fra ipconfig)

- **Svar:** Forbindelsen til routeren er OK
- **Timeout:** Problem mellem computer og router (kabel, Wi-Fi, driver)

**Test forbindelse til internettet:**

```cmd
ping 8.8.8.8
```

- **Svar:** Internetforbindelsen virker
- **Timeout:** Routeren har ikke forbindelse til internettet

**Test DNS:**

```cmd
ping google.com
```

- **Svar:** DNS virker korrekt
- **"Værtsnavn ikke fundet":** DNS-problem (ping 8.8.8.8 virker men domænenavne gør ikke)

### 3. Fejlsøgningsrækkefølge (systematisk)

Kør disse i rækkefølge for at isolere problemet:

| Trin | Kommando | Fejler → årsag |
|------|----------|----------------|
| 1 | `ping 127.0.0.1` | TCP/IP-stakken er defekt |
| 2 | `ping [din IP]` | Netværksadapter problem |
| 3 | `ping [gateway IP]` | Problem mellem computer og router |
| 4 | `ping 8.8.8.8` | Problem mellem router og internet |
| 5 | `ping google.com` | DNS-problem |

### 4. tracert — spor ruten til en server

```cmd
tracert google.com
```

Viser hvert hop mellem dig og serveren. Nyttigt til at se HVOR forbindelsen er langsom eller fejler:

- **Timeout ved hop 1:** Problem med din router
- **Timeout ved hop 2-3:** Problem hos internetudbyderen
- **Timeout langt ude:** Problem hos destinationen eller en mellemliggende udbyder

### 5. nslookup — test DNS-opslag

```cmd
nslookup google.com
```

Viser hvilken DNS-server der svarer og den opløste IP-adresse. Hvis dette fejler:

```cmd
nslookup google.com 8.8.8.8
```

Hvis det virker med 8.8.8.8 men ikke din standard DNS, er din DNS-server problemet.

### 6. Nulstil netværksstakken

Hvis basale kommandoer fejler, prøv at nulstille. Åbn **Kommandoprompt som administrator**:

```cmd
ipconfig /release
ipconfig /flushdns
ipconfig /renew
netsh int ip reset
netsh winsock reset
```

Genstart computeren bagefter.

### 7. netstat — se aktive forbindelser

```cmd
netstat -an
```

Viser alle aktive netværksforbindelser og lyttende porte. Nyttigt til at se om et program bruger en bestemt port.

For at se hvilke programmer der bruger netværket:

```cmd
netstat -b
```

(Kræver administrator)

### 8. Kør Windows netværksdiagnostik

1. Højreklik på netværksikonet i proceslinjen
2. Vælg **Diagnosticér netværksproblemer**
3. Følg vejledningen

## Bemærkninger

- Brug altid **systematisk fejlsøgning** (trin 3 ovenfor) — det sparer tid og peger direkte på årsagen
- `ping -t [adresse]` kører kontinuerligt ping (stop med Ctrl+C) — nyttigt til at se om forbindelsen er ustabil
- `pathping [adresse]` kombinerer ping og tracert og viser pakketab ved hvert hop
- Alle kommandoer kører i Kommandoprompt — PowerShell kan også bruges men syntaksen kan variere
- Gem output fra fejlsøgningen hvis du skal kontakte IT-support eller internetudbyder
