# DNS Propagation — Hvornår træder ændringer i kraft?

## Problem

Du har ændret DNS records, men ændringerne virker ikke endnu. Sitet viser stadig den gamle side, eller email fungerer ikke.

## Forklaring

DNS propagation er den tid det tager for DNS-ændringer at sprede sig til alle DNS-servere verden over. Hver DNS-server cacher (husker) records i en periode bestemt af **TTL-værdien**.

### Typiske ventetider

| Ændring              | Typisk tid       | Maksimal tid  |
|----------------------|------------------|---------------|
| A/AAAA record        | 15 min – 4 timer | 48 timer      |
| CNAME record         | 15 min – 4 timer | 48 timer      |
| MX record            | 15 min – 4 timer | 48 timer      |
| TXT record           | 15 min – 4 timer | 48 timer      |
| NS record (navneserver) | 2 – 48 timer  | 72 timer      |
| Nyt domæne           | 1 – 24 timer     | 48 timer      |

## Løsning: Gør propagation hurtigere

### Før ændringen
1. Sæt TTL til **300** (5 minutter) på den record du vil ændre
2. Vent mindst den nuværende TTL-tid (f.eks. 1 time hvis TTL er 3600)
3. Nu har alle caches den lave TTL
4. Lav selve ændringen — den spredes nu på ca. 5 minutter

### Efter ændringen
1. Verificer at ændringen er spredt (se nedenfor)
2. Sæt TTL tilbage til **3600** (1 time) eller højere

## Tjek propagation-status

### Kommandolinje
```
nslookup example.dk
nslookup -type=MX example.dk
```

For at tjekke mod en specifik DNS-server:
```
nslookup example.dk 8.8.8.8
nslookup example.dk 1.1.1.1
```

### Online værktøjer
- **whatsmydns.net** — viser status fra DNS-servere verden over
- **dnschecker.org** — tilsvarende global propagation-tjek
- **mxtoolbox.com** — god til MX og email-relaterede records

## Flush lokal DNS-cache

Hvis din egen computer stadig viser gamle data:

### Windows
```
ipconfig /flushdns
```

### Mac
```
sudo dscacheutil -flushcache; sudo killall -HUP mDNSResponder
```

### Browser
- Chrome: Gå til `chrome://net-internals/#dns` → "Clear host cache"
- Prøv også at rydde browser-cache eller test i inkognito-vindue

## Bemærkninger

- **48 timer er worst case** — de fleste ændringer virker inden for 1-4 timer
- NS-ændringer (navneserver-skift) tager længst tid, fordi de skal propagere fra TLD-serverne
- Forskellige ISP'er opdaterer i forskelligt tempo — det er normalt at ændringen virker for nogle, men ikke alle
- Hvis det stadig ikke virker efter 48 timer, er det sandsynligvis en konfigurationsfejl — ikke propagation
