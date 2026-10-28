# Attribution Support & Hunting Guide
## FulcrumSec, Phantom/INC Affiliates and APT28 (HOOKEDGE) – Practical Indicators for Investigators and Defenders

**Independent OSINT Compilation**  
**Date**: 28 October 2026  
**Classification**: TLP:CLEAR  
**Purpose**: Support attribution research and defensive hunting / prevention

---

### 1. Objective

This document consolidates publicly reported indicators, contact points, behavioural patterns and hunting recommendations for three relevant 2026 threat clusters. It is intended to help:

- Researchers performing attribution or infrastructure pivoting
- Defenders hunting for related activity inside their networks
- Incident responders looking for quick, actionable checks

All indicators are derived from open sources. Validate before blocking or using in production detection.

---

### 2. FulcrumSec (aka The Threat Thespians)

**Nature**: Data extortion group. Prefers credential / API-key abuse and cloud misconfigurations over classic encryption ransomware. Active since at least early 2026.

#### Public Contact & Infrastructure Points
| Type | Value | Notes |
|------|-------|-------|
| Email | fulcrumsec@tuta.io | Primary |
| Email | threatspians@fulcrumsec.net | Alternate |
| Telegram | @fulcrumsec | |
| Telegram | @threatspians | |
| Tox | 6A5E9ED3D7D26CAD5E6CA4E229CC80DA3C13AD002F73D4450078284E6C762F6DBDCF1FE9BF44 | |
| Tox | 969F8BE40B09537CD2A5038B9DA4BADE71C5F35DD666CC0D7632A6812D7AF72626D422D22540 | |
| Onion | 4e3p3in2bl67hxchuwza7qvnpe7pyeloyztr5fnh257fxkovfhappjyd.onion | Main leak site (and /shame path) |
| Clearnet | fulcrumsec.vg / fulcrumsec.net | Variable uptime |

#### Operational Pattern Relevant to Attribution
- Strong preference for **abusing exposed or over-privileged API keys and service accounts** rather than deploying encryptors.
- Documented victims include Manchester Airports Group (Iterable keys), PingCAP/TiDB Cloud (stolen service account credentials), Novo Nordisk, Arup Group, and others.
- Claims often include very large data volumes and offers of exclusive sale.

#### Hunting / Prevention Recommendations
- Audit all marketing, CRM and cloud automation platforms for server-side API keys present in client-side JavaScript.
- Monitor for unusual bulk export or high-volume API activity from marketing platforms (Iterable, Segment, Braze, etc.).
- Review cloud service-account usage and key rotation policies, especially for platforms that hold customer or operational data.

---

### 3. Phantom Framework / INC & The Gentlemen Affiliates

**Nature**: Russian-speaking affiliates operating an AI-orchestrated intrusion platform (Phantom). Function both as intruders and as infrastructure / tooling providers for ransomware partners.

#### Key Infrastructure (Public)
| Indicator | Role |
|-----------|------|
| 45.227.254.43 | Main exposed hub (AI logs, knowledge base, Phantom source) |
| 45.227.254.45 | Build / deployment / partner onboarding |
| 45.227.254.84 | Operator VM |
| 179.60.149.68 | Staging / pivot |
| 77.110.109.248 | RevSocks |
| 89.185.83.8 / 138.124.113.210 | Ghost C2 / panel |
| api.iquickline.com / iquickline.com | C2 beaconing |
| system-strategy.org | Redirector / related |
| AS267784 (Flyservers S.A.) | Primary hosting ASN |

#### Behavioural Fingerprints Useful for Attribution
- Operators assessed as **Russian-speaking**.
- Primary activity window observed: **06:00 – 14:00 UTC**.
- Heavy use of commercial AI (Claude via OpenRouter and others) with human approval at each step.
- When models refuse a request, operators reframe it as “authorized red team assessment”.
- FortiClient EMS account naming patterns observed in operator records: `sysadmin`, `fct_svc_*`, `ems_monitor_*`.

#### Hunting Recommendations (High Priority)
1. **FortiClient EMS**  
   Search for unexpected administrator accounts matching the naming patterns above. Review VPN on_connect scripts for unauthorized modifications.
2. **SimpleHelp and other RMM**  
   Audit for unauthorized admin access or unusual remote sessions (CVE-2024-57727 was heavily exploited).
3. **Network**  
   Hunt connections to the listed IPs and to `*.iquickline.com` / `system-strategy.org`.
4. **Endpoint**  
   Look for agents masquerading as Windows Update components and for scheduled tasks named similarly to legitimate audio/video services (e.g. RealtekAudioSvc pattern reported).

---

### 4. APT28 (HOOKEDGE / Swallowtail activity 2026)

**Nature**: Russian state-sponsored (GRU-linked). Espionage focus on NATO defense and government targets.

#### Confirmed Indicators from Public Reporting
| Type | Value | Notes |
|------|-------|-------|
| C2 IP | 185.82.218.119:443 | Dedicated server used for tasking + exfil (replaced earlier webhook.site usage) |
| Loader hash | f1cc91e7427a22027f65d31bbee19c54b602d08d7d93e4745b9cea59fa8132ff | ld.exe reflective loader |
| Technique | Hidden Microsoft Edge window | `--window-size=1,1 --window-position=10000,10000` style |
| Technique | Persistent SSH tunnel | `StrictHostKeyChecking=no`, often port 80, flags `-Nf` |
| Delivery | Macro-enabled Word documents | Spear-phishing |

#### Hunting Recommendations
- Search for unusual `msedge.exe` command lines with extreme window positioning or off-screen parameters.
- Hunt for unexpected SSH tunnels originating from user workstations, especially with `StrictHostKeyChecking=no`.
- Monitor for reflective loading behaviour and the specific loader hash above.
- Review email gateway logs for macro-enabled documents targeting defense, naval or aerospace personnel.

---

### 5. Cross-Cluster Prevention Priorities (Aviation & Critical Infrastructure)

| Priority | Action | Rationale |
|----------|--------|-----------|
| 1 | Eliminate server-side secrets from all public JavaScript | MAG / FulcrumSec vector |
| 2 | Audit and harden FortiClient EMS + all RMM tools | Phantom / INC primary initial access |
| 3 | Monitor for anomalous Edge processes and unexpected SSH tunnels | APT28 HOOKEDGE tradecraft |
| 4 | Retain detailed API and cloud access logs for ≥ 12–24 months | Enables future attribution and exposure-window analysis |
| 5 | Segment marketing / ancillary platforms from operational and identity systems | Reduces blast radius |

---

### 6. How This Helps Attribution Research

- **FulcrumSec**: Contact points and Tox/Telegram identifiers can be monitored for reuse across future claims. Victim selection pattern (API-key rich environments) is a strong behavioural signal.
- **Phantom operators**: Consistent UTC working hours + Russian language + specific ASN + account naming conventions form a multi-factor fingerprint that can be correlated with new infrastructure.
- **APT28**: The shift from webhook.site to dedicated IP, combined with the reflective loader and SSH tunnel technique, provides a clear evolution marker for linking future activity.

Researchers can pivot from any newly observed infrastructure against these patterns to strengthen or refute attribution hypotheses.

---

### Sources

- RansomLook / Breachsense / public leak-site indexing for FulcrumSec contacts and onions
- SOCRadar and subsequent technical reporting on Phantom infrastructure and operator behaviour (Oct 2026)
- Symantec Threat Hunter Team / Recorded Future reporting on APT28 HOOKEDGE and 185.82.218.119
- Public victim disclosures (MAG, PingCAP, etc.)

*Compiled exclusively from open sources for defensive research and attribution support. Always corroborate indicators with current telemetry.*
