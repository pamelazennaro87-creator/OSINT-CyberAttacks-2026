# The Unknowable Exposure Window
## MAG Iterable Keys 2022–2026 and a Practical Methodology for Detecting Client-Side Secrets on Airport Websites

**Independent OSINT Contribution**  
**Date**: 28 October 2026  
**Classification**: TLP:CLEAR  
**Purpose**: Prevention and detection

---

### 1. Why This Is Different

Most reporting on the Manchester Airports Group (MAG) incident stopped at “API keys were in the JavaScript”.  
Scott Helme’s reconstruction using the Wayback Machine established a precise and damning timeline: the same privileged Iterable keys appeared in the public frontend of the three MAG airport websites from **June/July 2022 until August 2026** — more than four continuous years.

This report goes one step further. It treats the incident as a **detection and measurement problem** rather than only a post-incident narrative, and offers a reusable, public methodology that any researcher or airport security team can apply to other European airport websites today.

---

### 2. The Exact Exposure Window (Reconstructed)

| Period | Status |
|--------|--------|
| June – July 2022 | Keys first appear in archived JavaScript of the three MAG airport root domains |
| 2022 – August 2026 | Keys remain present and unchanged |
| Late August 2026 | Keys removed / rotated after the FulcrumSec claim and public scrutiny |
| Duration | ≈ 4 years and 1–2 months |

**Critical implication (Helme):**  
Anyone who viewed the page source on any day in that window could have extracted the keys. There is no public way to know how many other actors did so. MAG itself cannot know without complete Iterable API access logs covering the entire period — logs that may not even exist at full fidelity.

This creates an **unknowable exposure window**: the true number of potential prior compromises is permanently opaque.

---

### 3. Key Privilege Reality

The keys were **not** restricted client-side keys.  
They were server-side privileged keys capable of reaching the large majority of Iterable’s API endpoints (reports indicate access to roughly 98 of 131 endpoints), including:

- Full customer data export
- Individual profile lookup by email
- Bulk update and delete operations

The intended legitimate use was marketing attribution (pageview / click tracking). The privilege level was orders of magnitude higher than required.

Iterable’s own documentation explicitly warns against placing server-side keys in client-side code.

---

### 4. Original Contribution: A Practical Public Detection Methodology

The following methodology can be applied by any independent researcher or internal security team to other airport (or critical infrastructure) websites.

#### Step 1 – Identify marketing / analytics platforms in use
- Load the airport homepage and key booking / parking / lounge pages.
- Open browser developer tools → Network and Sources.
- Search for known marketing domains and SDK names: iterable.com, segment.com, braze.com, salesforce, hubspot, klaviyo, adobe, etc.
- Note any configuration objects or global variables that look like API keys or tokens.

#### Step 2 – Extract candidate secrets
- Search the loaded JavaScript bundles and inline scripts for long alphanumeric strings that match API key patterns.
- Check for objects named `config`, `settings`, `apiKey`, `token`, `iterable`, etc.
- Save the full bundle URLs for historical comparison.

#### Step 3 – Historical validation (Wayback / archive)
- Use the Internet Archive Wayback Machine (or equivalent) on the specific JavaScript file URLs.
- Determine the earliest and latest dates the same key values appear.
- Calculate the continuous exposure window.

#### Step 4 – Privilege assessment (where possible)
- Compare observed key behaviour or documentation against the platform’s published key types (client-side vs server-side).
- If the key can call export, user lookup or destructive endpoints, treat it as critically over-privileged.

#### Step 5 – Document and report
- Record: airport, domain, platform, key type (if known), first/last observed date, estimated window length, and whether the key is still live.
- Responsible disclosure to the operator and, where appropriate, national CSIRT.

This process requires only a browser, the Wayback Machine, and publicly available platform documentation. No authentication or internal access is needed.

---

### 5. Prevention Metrics Derived from the MAG Case

From this single incident we can extract measurable prevention indicators that other operators can adopt:

| Metric | MAG Reality | Target State |
|--------|-------------|--------------|
| Maximum acceptable lifetime of any client-visible credential | > 4 years | 0 (never ship server-side secrets) |
| Time between key introduction and first external discovery | ~4 years | Days / weeks via continuous scanning |
| Ability to answer “who else extracted this key?” | Impossible without full logs | Possible via short-lived, scoped, monitored keys |
| Privilege level vs intended function | Extreme over-privilege | Least privilege, client-side restricted keys only |

---

### 6. Recommended Immediate Actions for Airport Operators

1. Run the methodology above against every public-facing domain and subdomain that serves passenger or booking pages.
2. Treat any server-side key found in JavaScript as already compromised and rotate it immediately.
3. Implement automated secret scanning of frontend assets in the CI/CD pipeline.
4. Move all sensitive marketing API calls behind a backend proxy that holds the real credentials.
5. Retain detailed API access logs for marketing platforms for a minimum of 12–24 months so that future exposure windows can at least be audited.

---

### 7. Closing Observation

The MAG case is not primarily a story about one ransomware group.  
It is a demonstration that a high-value credential can sit in plain sight on major airport websites for more than four years, be harvested by an unknown number of actors, and only become public when one of them decides to monetise it.

The exposure window itself is unknowable.  
The detection methodology above is designed so that the next window does not have to be.

---

### Sources

- Scott Helme analysis (via The Register and subsequent reporting, September 2026)
- FulcrumSec claims and dataset descriptions
- MAG official disclosure (27 August 2026)
- Iterable official documentation on API key types and client-side vs server-side usage
- Wayback Machine historical JavaScript observations as reported by Helme

*This document is published solely for defensive research and prevention purposes.*
