# OSINT Cyber Attacks 2026

**Independent OSINT investigation** – Recent cyber attacks (2026) with focus on aviation, airports, supply-chain and critical infrastructure.

**Author**: Independent OSINT researcher  
**Last update**: 28 October 2026  
**Repository**: Public research portfolio

---

## Overview

This repository collects structured OSINT findings on significant cyber incidents of 2026, with particular attention to:

- Airport and aviation-related breaches
- Supply-chain compromises
- Ransomware groups (INC, FulcrumSec, Storm, etc.)
- State-sponsored activity (APT28)
- Technical IOCs (IPs, domains, TTPs)
- Risk analysis and prevention guidance for critical infrastructure operators

The material is based on open-source reporting, leak-site claims, vendor statements and technical analyses available as of late October 2026.

---

## Structure

```
├── README.md
├── analysis/
│   └── soft-underbelly-aviation-2026.md   ← Deep-dive analysis + prevention
├── reports/
│   ├── 01-manchester-airports-group-fulcrumsec.md
│   ├── 02-apt28-nato-targets.md
│   ├── 03-inc-phantom-infrastructure.md
│   ├── 04-other-2026-incidents.md
│   └── 05-collins-muse-2025-context.md
├── iocs/
│   └── indicators.md
└── risk-analysis.md
```

---

## Key Incidents Covered

| Incident | Date | Type | Impact |
|----------|------|------|--------|
| Manchester Airports Group (FulcrumSec) | Aug 2026 | Data theft / Extortion | 8.7M records, WiFi/parking/lounge data |
| APT28 (Fancy Bear) | Jul–Oct 2026 | Espionage | NATO naval shipbuilder, military aviation engines |
| INC Ransomware + Phantom | Exposed Oct 2026 | Ransomware / AI-assisted | 62+ orgs, FortiClient EMS, SimpleHelp |
| Star Aviation (Storm) | Sep 2026 | Ransomware claim | Boeing/Airbus supplier |
| CyberLogitec maritime cascade | Oct 2026 | Possible supply-chain | 38 companies claimed |
| Collins Aerospace MUSE (context) | Sep 2025 | Ransomware | Major European airport check-in disruption |

---

## Featured Analysis

**[The Soft Underbelly of Aviation](analysis/soft-underbelly-aviation-2026.md)**  

Original analysis of the MAG Iterable client-side keys vector, the multi-year exposure window (2022–2026), systemic risk patterns, Amadeus biometric overlap, risk scorecard for major European airports, technical appendix on Iterable keys, and a concrete prevention checklist.

---

## Disclaimer

This is **open-source intelligence** for research and defensive purposes only.  
Indicators should be validated against current telemetry.  
No classified or non-public information is included.

---

## License

Research material – free to use with attribution.
