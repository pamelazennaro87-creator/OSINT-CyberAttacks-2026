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
- Risk analysis, attribution support, prevention guidance and original methodological proposals

The material is based on open-source reporting, leak-site claims, vendor statements and technical analyses available as of late October 2026.

---

## Structure

```
├── README.md
├── analysis/
│   ├── soft-underbelly-aviation-2026.md
│   ├── unknowable-exposure-window-mag-2022-2026.md
│   ├── attribution-hunting-guide-2026.md
│   └── open-exposure-ledger-proposal.md   ← Original methodological proposal
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
| Manchester Airports Group (FulcrumSec) | Aug 2026 | Data theft / Extortion | 8.7M records |
| APT28 (Fancy Bear) | Jul–Oct 2026 | Espionage | NATO naval + military aviation |
| INC Ransomware + Phantom | Exposed Oct 2026 | Ransomware / AI-assisted | 62+ orgs |
| Star Aviation (Storm) | Sep 2026 | Ransomware claim | Boeing/Airbus supplier |
| CyberLogitec maritime cascade | Oct 2026 | Possible supply-chain | 38 companies |
| Collins Aerospace MUSE (context) | Sep 2025 | Ransomware | European airport check-in disruption |

---

## Featured Analyses & Proposals

**[The Soft Underbelly of Aviation](analysis/soft-underbelly-aviation-2026.md)**  
Systemic risk, Amadeus overlap, scorecard and prevention checklist.

**[The Unknowable Exposure Window](analysis/unknowable-exposure-window-mag-2022-2026.md)**  
4-year MAG key exposure timeline + public detection methodology.

**[Attribution Support & Hunting Guide](analysis/attribution-hunting-guide-2026.md)**  
Practical indicators and hunting recommendations for FulcrumSec, Phantom/INC and APT28.

**[Open Exposure Ledger (OEL) – Methodological Proposal](analysis/open-exposure-ledger-proposal.md)**  
Original proposal for a public, continuous, cryptographically attested mechanism to measure and record the duration of privileged secret exposure on critical infrastructure public assets. Designed to address the opacity of long exposure windows.

---

## Disclaimer

This is **open-source intelligence** for research and defensive purposes only.  
Indicators should be validated against current telemetry.  
No classified or non-public information is included.  
Methodological proposals are original contributions for discussion and are not claims of existing deployed systems.

---

## License

Research material – free to use with attribution.
