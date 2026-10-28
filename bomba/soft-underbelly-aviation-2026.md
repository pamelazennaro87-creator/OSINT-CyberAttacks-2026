# The Soft Underbelly of Aviation
## Client-Side Secrets, Marketing Platforms and Third-Party Risk in European Airports (2022–2026)

**Independent OSINT Analysis**  
**Date**: 28 October 2026  
**Classification**: TLP:CLEAR  
**Author**: Independent OSINT researcher

---

### Executive Summary

While European airports have significantly hardened core operational systems after the September 2025 Collins Aerospace MUSE ransomware incident, a parallel and largely unaddressed risk surface remains wide open: **client-side secrets and third-party marketing / passenger ancillary platforms**.

The August 2026 Manchester Airports Group (MAG) breach provides the clearest public case study. FulcrumSec gained access through **admin-level Iterable API keys that had been hardcoded in the frontend JavaScript of the three MAG airport websites (Manchester, Stansted, East Midlands) since at least 2022** — nearly four years of continuous exposure.

This report reconstructs the vector, analyses the systemic pattern, and connects it to the concurrent expansion of Amadeus biometric systems across the same UK airports.

---

### 1. The MAG Breach Vector – Reconstructed

**Confirmed public elements:**

- MAG disclosed unauthorized access on 27 August 2026 affecting customer data from Wi-Fi registrations, car park, lounge and Fast Track bookings.
- FulcrumSec claimed responsibility and later leaked ~550 GB (claimed) covering approximately 8.7–8.8 million records.
- Multiple independent sources (SecurityWeek, The Register, Scott Helme analysis, Have I Been Pwned) confirmed that the initial access vector was **admin keys for the Iterable marketing automation platform left in plaintext inside the public JavaScript of the three airport root domains**.

**Key technical insight:**

These were not temporary debug keys. They remained present and functional for years. Iterable keys of this type typically allow broad read (and in some configurations write) access to customer profiles, event streams, purchase history, messaging logs and marketing configuration.

This is a classic **client-side secret anti-pattern**: credentials that belong exclusively on the server side were shipped to every visitor’s browser.

**Impact summary:**
- 8.7M+ customer profiles
- Purchase and booking histories
- Vehicle registration plates
- Browser / device / geolocation data
- SMS and engagement event logs
- No confirmed payment card data or operational flight systems compromised

---

### 2. Why This Matters More Than the Data Leak Itself

The operational systems (check-in, boarding, baggage, ATC interfaces) of major European airports have received intense attention and investment after Collins MUSE. The MAG case demonstrates that the real residual risk has migrated to the **ancillary layer**:

| Layer | Hardening Level (2026) | Attractiveness to Attackers | Example |
|-------|------------------------|-----------------------------|---------|
| Core operational (MUSE, DCS, AODB) | High | High impact, high difficulty | Collins 2025 |
| Border / biometric | Rising rapidly | High value identity data | Amadeus Seamless Gates |
| Marketing & CRM platforms | Low–Medium | High volume PII, low difficulty | Iterable at MAG |
| Passenger ancillary (WiFi, parking, lounge) | Medium | Medium–High | MAG systems |
| RMM / remote management | Variable | Very High (initial access) | SimpleHelp, FortiClient EMS |

Attackers have rationally shifted toward the soft underbelly.

---

### 3. The Amadeus Overlap – An Emerging Convergence Risk

As of October 2026, Amadeus is rolling out **Seamless Gates** biometric border technology across 13 UK international airports, including:

- Manchester
- London Stansted
- East Midlands

(plus Heathrow, Gatwick, Birmingham, Edinburgh, etc.)

These are exactly the same airports whose marketing platforms were compromised months earlier via client-side keys.

While the biometric systems themselves are separate, the **passenger identity and travel data ecosystems are converging**. Marketing platforms already hold rich behavioural and identity-linked data. Biometric systems add high-assurance identity anchors. The combination creates a high-value target surface if the ancillary systems remain weakly protected.

---

### 4. Systemic Pattern Across 2025–2026

Three distinct but related failure modes appear repeatedly:

1. **Shared operational platforms** (Collins MUSE) → single point of failure for multiple airports.
2. **Long-lived client-side secrets** (MAG Iterable keys) → trivial initial access lasting years.
3. **Exposed RMM and management tools** (SimpleHelp, FortiClient EMS in the Phantom/INC campaign) → scalable initial access for ransomware affiliates.

In all three cases the core flight operations were either not reached or only indirectly affected. The damage occurred in the supporting digital infrastructure that airports treat as secondary.

---

### 5. Innovative Contribution of This Analysis

Previous public reporting on MAG stopped at “data leaked after ransom refusal” or “keys found in JavaScript”.  
This report adds:

- Explicit reconstruction of the multi-year exposure window (2022–2026).
- Framing of the incident as a **structural class of risk** rather than an isolated event.
- Direct linkage to the concurrent Amadeus biometric expansion on the identical airport set.
- A risk layering model that separates operational, identity, marketing and remote-management surfaces.
- Forward-looking warning: as airports push biometric and seamless travel, the unprotected marketing and ancillary data layers become the highest-ROI target for both criminal and state actors.

---

### 6. Defensive Recommendations (Actionable)

For airport operators and their technology partners:

1. **Immediate audit** of all public JavaScript bundles for API keys, tokens, and secrets (Iterable, Segment, Braze, Salesforce Marketing Cloud, custom analytics, etc.).
2. Treat marketing automation platforms with the same credential hygiene and network controls applied to operational systems.
3. Implement strict Content Security Policy and subresource integrity where possible; move all sensitive API interaction server-side.
4. Maintain an inventory of every third-party platform that processes passenger data (even “non-critical” ones).
5. Assume that any key ever shipped to the browser is compromised and rotate accordingly.
6. Segment marketing and ancillary data environments from both operational and biometric identity systems.

---

### 7. Conclusion

The Collins Aerospace incident of 2025 forced European aviation to confront the danger of shared operational platforms.  
The MAG breach of 2026 should force a second, quieter but equally important realisation: **the soft underbelly is no longer the check-in desk — it is the JavaScript on the airport website and the marketing cloud behind it**.

Until airports apply the same rigour to their ancillary and customer-data platforms that they now apply to passenger processing systems, high-volume, low-difficulty breaches of this type will continue.

---

### Sources & References

- MAG official disclosure (27 Aug 2026)
- FulcrumSec leak-site claims and media relay (SecurityWeek, Computer Weekly, Hackread, Breached.Company)
- Scott Helme / The Register analysis of Iterable keys in frontend JS
- Have I Been Pwned confirmation of dataset contents
- Amadeus Seamless Gates rollout announcements (October 2026) covering the 13 UK airports including MAG sites
- Prior Collins Aerospace MUSE incident reporting (ENISA, RTX, NCA)
- SOCRadar Phantom/INC infrastructure research (for RMM parallel)

*This analysis is based exclusively on publicly available information and is intended for defensive research purposes.*
