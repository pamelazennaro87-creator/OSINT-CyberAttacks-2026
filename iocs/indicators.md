# Indicators of Compromise (IOCs) – 2026 Campaigns

**TLP:CLEAR** – Publicly reported indicators. Validate before blocking.

## INC Ransomware / Phantom Framework (Exposed Oct 2026)

### IP Addresses
| IP | Role | Notes |
|----|------|-------|
| 45.227.254.43 | Main hub | OpenCode AI sessions, knowledge base, Phantom source |
| 45.227.254.45 | Build & deployment | Encryptor builds |
| 45.227.254.84 | Operator VM / Kali | — |
| 179.60.149.68 | Staging / pivot | — |
| 77.110.109.248 | RevSocks host | — |
| 89.185.83.8 | Ghost C2 / delivery | — |
| 138.124.113.210 | Ghost panel | — |

### Domains
- system-strategy[.]org
- iquickline[.]com (api.iquickline[.]com – C2 beaconing)

### Related
- AS267784 (Flyservers S.A.) – hosting pattern
- Operator email linked in research: smilefacesec[@]gmail[.]com (BreachForums association)

### Exploited CVEs (operator records)
- CVE-2026-35616 – FortiClient EMS authentication bypass
- CVE-2024-57727 – SimpleHelp path traversal
- CVE-2026-41940 – cPanel/WHM authentication bypass

## APT28 (Fancy Bear) – 2026 NATO targets

| Indicator | Type | Notes |
|-----------|------|-------|
| 185.82.218.119:443 | C2 / Exfiltration | Used for tasking and data exfil (HOOKEDGE variants) |

### Tools / Techniques
- New reflective loader (HOOKEDGE variants)
- Credential theft (multiple techniques)
- Persistent SSH tunnels
- Hands-on-keyboard activity over multiple days

## Manchester Airports Group / FulcrumSec
No public C2 IPs or malware hashes widely published in open sources at time of compilation. Focus remains data set (PII from WiFi, parking, lounge, Fast Track).

## Notes
- IPs on cloud/VPS providers may be reassigned. Always corroborate with current network telemetry.
- Additional indicators may appear in future technical reports.
