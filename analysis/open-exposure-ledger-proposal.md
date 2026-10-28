# Open Exposure Ledger (OEL)
## A Proposed Accountability Mechanism for Public Secret Exposure on Critical Infrastructure Assets

**Independent Methodological Proposal**  
**Date**: 28 October 2026  
**Classification**: TLP:CLEAR  
**Status**: Original proposal – not an existing system

---

### 1. Problem Statement

The Manchester Airports Group incident (2026) demonstrated a structural failure mode:

- Privileged API keys remained in public JavaScript for more than four years.
- The duration of exposure was opaque to external observers.
- Even the operator cannot reliably determine how many third parties may have extracted the credentials during that window.

Current defensive approaches (internal secret scanning, attack surface management, CSP, key rotation policies) remain largely **internal and private**. They do not create continuous, externally verifiable visibility into how long high-privilege secrets have been present on public-facing assets.

This opacity is the core problem OEL is designed to address.

---

### 2. Core Proposal

**Open Exposure Ledger (OEL)** is a proposed public accountability mechanism with three defining properties:

1. **External measurement** – Observations of public web assets are performed by independent parties (researchers, specialised services, automated scanners), not solely by the operator.
2. **Continuous tracking of exposure age** – The system focuses specifically on the *duration* that credential-like objects remain present in public assets.
3. **Cryptographic attestation** – Each measurement is digitally signed, creating a non-repudiable record that can be independently verified.

The resulting ledger (or set of attestations) is publicly queryable. The operator does not control the historical record.

---

### 3. What an Attestation Contains

A signed measurement attestation would include at minimum:

- Target domain / asset identifier
- Cryptographic hash of the observed JavaScript bundle or configuration object (the secret itself is never published)
- Classification of the object (e.g. high-privilege API key pattern, marketing platform credential, low-risk token)
- Timestamp of observation
- Estimated age relative to previous observations of the same object
- Digital signature of the measuring party
- Optional: measurement methodology identifier and software version

Chaining these attestations over time produces a verifiable history of exposure duration.

---

### 4. Why This Differs from Existing Approaches

| Existing Practice | OEL |
|-------------------|-----|
| Internal secret scanning | External, independent measurement |
| Private attack-surface reports | Public, queryable record |
| Binary “key found / not found” | Focus on *duration* of exposure |
| Operator-controlled disclosure | Operator cannot erase or rewrite history |
| No cryptographic proof of measurement | Digitally signed, verifiable attestations |

OEL does not replace internal controls. It adds a layer of **external, time-aware accountability** that currently does not exist for this class of risk.

---

### 5. Intended Effects

- Transforms the “unknowable exposure window” into a measurable and publicly visible quantity.
- Creates continuous reputational, regulatory and insurance pressure against long-lived public secrets.
- Enables researchers and defenders to detect systemic hygiene failures before they become incidents.
- Provides a new language for discussing risk (“the Exposure Clock has been elevated for 11 months”) that is harder to neutralise with post-incident statements.

---

### 6. Implementation Considerations (High Level)

- Measurement must avoid publishing the secrets themselves; only hashes, classifications and temporal metadata.
- False-positive handling for credential-like strings is a non-trivial technical challenge.
- Governance of the ledger (who may submit attestations, how disputes are handled, retention policy) requires careful design.
- Adoption path is most realistic through a combination of sector initiatives (aviation, critical infrastructure), insurance underwriting criteria, and eventual regulatory recognition.

---

### 7. Relationship to the 2026 Aviation Cases

Had an Open Exposure Ledger existed and been populated for major European airport websites:

- The multi-year presence of privileged Iterable keys on the MAG domains would have been externally visible long before August 2026.
- The duration itself would have become a public fact rather than a post-incident reconstruction via the Wayback Machine.
- Incentives to remove or properly scope such credentials would have operated continuously instead of only after extortion.

---

### 8. Status of This Document

This is an **original methodological proposal**. It is not a description of an existing product, standard or deployed system. It is offered as a contribution to the discussion on how to reduce the opacity of public secret exposure in critical digital assets.

Feedback, critique and refinement are expected and welcome.

---

### 9. Summary Principle

> The duration for which privileged secrets remain present on public-facing assets of critical operators should be externally observable, historically recorded, and cryptographically attested.

This is the defining claim of Open Exposure Ledger.

---

*Published for defensive research and methodological discussion. No operational system is claimed to exist under this name at the time of writing.*
