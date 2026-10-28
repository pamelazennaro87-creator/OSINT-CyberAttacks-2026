# INC Ransomware & The Gentlemen Affiliates – Phantom Framework Exposure

**Discovery**: Late September – October 2026 (OPSEC failure – open directories)  
**Nature**: AI-orchestrated intrusion platform used by affiliates of INC Ransomware and The Gentlemen

## Key Findings

Researchers (SOCRadar and others) discovered exposed adversary infrastructure containing:

- 8,257 AI chat messages across 133 sessions
- Full source of the “Phantom” framework (18-skill autonomous red-team style kill-chain)
- 46 customized INC encryptor builds
- Victim knowledge base and tracking data
- Operator logs showing exploitation results

Estimated spend on commercial AI (OpenRouter – Claude and other models): > $23,000.

## Infrastructure (Public IOCs)

See `iocs/indicators.md` for full list.

Primary anchor: `45.227.254.43`

## Initial Access Vectors (Operator Records)

- CVE-2026-35616 – FortiClient EMS auth bypass (2,236 targets scanned, 108 admin accounts created)
- CVE-2024-57727 – SimpleHelp path traversal
- CVE-2026-41940 – cPanel/WHM auth bypass

Additional staging interest in other perimeter products (SonicWall, etc.).

## Operational Model

- AI used for reconnaissance planning, command generation, data triage and extortion note drafting
- Human operators approved critical steps
- When commercial models refused requests, operators reframed them as “authorized red team”
- Payment preference: Monero
- Victims faced short (24–72 h) leak deadlines

## Scale

- 62 organizations named in operator records (majority US)
- Sector concentration: industrial/manufacturing and healthcare
- Some victims later appeared on INC / The Gentlemen leak sites

## Significance

This exposure provides rare insight into the operationalization of commercial AI by ransomware affiliates and the industrialisation of initial access + encryption pipelines in 2026.

## Defensive Actions

- Immediately audit FortiClient EMS consoles for unexpected admin accounts (naming patterns noted in research: sysadmin, fct_svc_*, ems_monitor_*)
- Review SimpleHelp and other RMM instances for unauthorized access
- Hunt for the listed C2 domains and IPs
- Monitor for Windows Update-masquerading agents (Phantom characteristic)

## Sources

SOCRadar Threat Research, public technical write-ups (GBHackers, LavX, DFIR Radar summaries), October 2026.
