# Support Videnbase — CLAUDE.md

## Projektbeskrivelse
Kundesupport videnbase med fejlsøgning, opsætning og guides til:
- Microsoft 365 (Outlook, Teams, OneDrive, SharePoint, Excel, Word)
- DNS & Hosting (DNS-records, domæner, SSL, email-opsætning)
- Programmer & OS (Windows, printere, netværk, gængse programmer)
- WordPress (admin, plugins, sikkerhed, fejlsøgning)

## Lokal sti
`D:\Videnbase\Support\`

## GitHub repo
`airandershjemmesider/videnbase-support`

## RAG-server
- MCP-navn: `mcp__rag-support__`
- Data: `D:\Videnbase\Support`
- LanceDB: `D:\AI-Data\rag\support\lancedb\`

## Afgrænsning
- KUN support-dokumentation og fejlsøgning
- IKKE kode, templates eller designfiler (det er Elementor-videnbasen)
- IKKE SEO-tekster (det er SEO-videnbasen)
- WordPress-viden her er SUPPORT-orienteret (fejlsøgning, admin, sikkerhed)
- WordPress MCP-integration og Elementor-specifikt hører i Elementor-videnbasen

## Videnbase-standard
- Granulære filer (~200 linjer maks)
- Én ting per fil
- Maks ~10 filer per mappe
- Filnavne: lowercase, bindestreg, æ→ae, ø→oe, å→aa
- Indhold: Overskrift → Problem/Løsning → Eksempler

## Filformat for support-artikler
```
# [Titel]

## Problem
[Kort beskrivelse af problemet]

## Løsning
[Trin-for-trin løsning]

## Bemærkninger
[Ekstra kontekst, advarsler, relaterede problemer]
```

## Session logs
`D:\Videnbase\MCP\session-logs\support\`

## Fejl-rapportering
`D:\Videnbase\MCP\fejl\mcp\` (del af MCP-projektet)

## Python/Subagent-stier
- Python: `D:\AI-Data\venv\Scripts\python.exe`
- Node.js: `C:\PROGRA~1\nodejs\node.exe`
