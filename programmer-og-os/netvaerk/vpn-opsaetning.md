# VPN opsætning og fejlsøgning

## Problem

Du skal opsætte en VPN-forbindelse til arbejdspladsen, eller en eksisterende VPN-forbindelse fungerer ikke.

## Løsning

### 1. Opsæt VPN i Windows (indbygget)

Windows har en indbygget VPN-klient til L2TP, PPTP, SSTP og IKEv2:

1. Åbn **Indstillinger** → **Netværk og internet** → **VPN**
2. Klik **Tilføj VPN**
3. Udfyld:
   - **VPN-udbyder:** Windows (indbygget)
   - **Forbindelsesnavn:** Et beskrivende navn (f.eks. "Arbejde VPN")
   - **Servernavn eller -adresse:** Adressen fra din IT-afdeling
   - **VPN-type:** Spørg IT-afdelingen (typisk L2TP/IPsec eller IKEv2)
   - **Loginoplysninger:** Brugernavn og adgangskode eller certifikat
4. Klik **Gem**

### 2. Opret forbindelse

1. Klik på **netværksikonet** i proceslinjen
2. Klik på **VPN**-forbindelsen
3. Klik **Opret forbindelse**
4. Indtast evt. brugernavn og adgangskode

### 3. Tredjeparts VPN-klienter

Mange virksomheder bruger dedikerede VPN-klienter:

- **Cisco AnyConnect:** Download fra virksomhedens portal eller IT-afdelingen
- **GlobalProtect (Palo Alto):** Typisk leveret af IT-afdelingen
- **OpenVPN:** Download fra openvpn.net og importér konfigurationsfilen (.ovpn)
- **WireGuard:** Download fra wireguard.com og importér konfigurationen

Følg IT-afdelingens vejledning for den specifikke klient.

## Fejlsøgning

### VPN forbinder ikke

1. **Tjek internetforbindelsen:** VPN kræver en aktiv internetforbindelse først
2. **Tjek credentials:** Er brugernavn og adgangskode korrekte? Er kontoen aktiv?
3. **Tjek serveradressen:** Er den stavet korrekt?
4. **Prøv en anden VPN-type:** Skift mellem L2TP, IKEv2, SSTP i VPN-indstillingerne
5. **Firewall:** Tjek om din firewall blokerer VPN-trafik

### VPN-forbindelse falder ud

1. **Deaktivér strømbesparelse for netværksadapter:**
   - Åbn **Enhedshåndtering** → **Netværkskort**
   - Højreklik på din adapter → **Egenskaber** → **Strømstyring**
   - Fjern flueben ved **Tillad, at computeren slukker denne enhed**

2. **Skift VPN-protokol:** Nogle protokoller er mere stabile end andre. IKEv2 er generelt stabil

3. **Tjek for konflikter:** Andre VPN-klienter eller sikkerhedssoftware kan konflikte

### VPN er forbundet men internet virker ikke

1. **Split tunneling:** Spørg IT-afdelingen om split tunneling er aktiveret. Uden det går AL trafik gennem VPN
2. **DNS-problemer:** Prøv at skifte DNS (se netvaerks-fejlsoegning.md)
3. **Nulstil TCP/IP:**
   ```cmd
   netsh int ip reset
   netsh winsock reset
   ```
   Genstart computeren.

### L2TP-forbindelse fejler bag NAT

Hvis L2TP/IPsec fejler bag en router, kan det skyldes NAT-traversal:

1. Åbn **Registreringseditor** (regedit)
2. Gå til: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\PolicyAgent`
3. Opret ny DWORD (32-bit) værdi: `AssumeUDPEncapsulationContextOnSendRule`
4. Sæt værdien til `2`
5. Genstart computeren

## Bemærkninger

- Virksomheds-VPN kræver ofte MFA (multi-faktor-godkendelse) — hav din telefon klar
- VPN reducerer internethastigheden — det er normalt, især ved forbindelse til fjerne servere
- Hvis VPN bruges til at tilgå firmanetværk, kontakt altid IT-afdelingen ved problemer — de har logs og kan fejlsøge fra serversiden
- Gem aldrig VPN-credentials i usikre notater — brug Windows' indbyggede credential-manager
- Nogle offentlige netværk (hoteller, lufthavne) blokerer VPN-trafik — prøv at bruge mobil-hotspot i stedet
