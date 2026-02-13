# WHM (Web Host Manager) — Oversigt

## Hvad er det

WHM (Web Host Manager) er serveradministrationspanelet til cPanel-servere. Det bruges til at oprette og administrere individuelle cPanel-konti (hosting-kunder), konfigurere serveren og overvåge services.

WHM er server-niveau — cPanel er konto-niveau. Én WHM kan administrere mange cPanel-konti.

## Adgang

- **URL:** `https://server-ip:2087` eller `https://hostname:2087`
- **Login:** root-bruger eller reseller-konto
- **Sikkerhed:** Adgang kræver enten root-password eller SSH-nøgle

## Vigtigste funktioner

### Account Functions
- Create a New Account — opret hosting-konto
- List Accounts — oversigt over alle konti
- Modify an Account — ændr pakke, kvote, features
- Suspend/Unsuspend — suspendér konti (f.eks. manglende betaling)
- Terminate an Account — slet konto permanent

### DNS Functions
- DNS Zone Manager — administrér DNS-zoner for alle domæner
- Add a DNS Zone — opret ny zone manuelt
- Edit DNS Zone — redigér eksisterende records

### Server Configuration
- Basic WebHost Manager Setup — grundlæggende serveropsætning
- Tweak Settings — finjuster server-adfærd
- MultiPHP Manager — administrér PHP-versioner

### Service Status
- Oversigt over kørende services: Apache, MySQL/MariaDB, DNS (named/BIND), Exim (mail), FTP, cPanel
- Genstart individuelle services

## Forskel på WHM og cPanel

| Emne | WHM | cPanel |
|------|-----|--------|
| Niveau | Server | Konto |
| Adgang | root / reseller | Hosting-kunde |
| Port | 2087 | 2083 |
| Formål | Administrér alle konti | Administrér én konto |
| DNS | Alle zoner | Kun egne domæner |
| Backup | Server-dækkende | Kun egen konto |

## Bemærkninger

- WHM og cPanel opdateres samlet — versionen styres via WHM → Update Preferences
- Resellere har begrænset WHM-adgang (kun deres egne kunder)
- WHM kræver licens — enten direkte fra cPanel Inc. eller via hosting-udbyder
