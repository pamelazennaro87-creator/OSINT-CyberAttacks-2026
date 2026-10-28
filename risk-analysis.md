# Risk Analysis – Aviation & Critical Infrastructure (October 2026)

## Summary Matrix

| Area | Risk Level | Primary Drivers | Notes |
|------|------------|-----------------|-------|
| Supply-chain vendors (check-in, reservation, RMM) | **Very High** | Single points of failure, credential reuse, shared platforms | Collins 2025, Amadeus, CyberLogitec pattern |
| RMM / FortiClient EMS / SimpleHelp | **High** | Active CVEs exploited at scale (2026) | INC/Phantom campaign |
| Passenger ancillary data (WiFi, parking, lounge) | **Medium-High** | Phishing & social engineering value | MAG / FulcrumSec |
| Operational flight / ATC systems | **Low** (public) | No confirmed 2026 operational disruption of this class | — |
| State-sponsored (APT28) | **High** on defense targets | Custom loaders, persistent SSH tunnels | Military aviation engines, naval |
| AI-assisted ransomware ops | **Rising** | Phantom framework + commercial LLMs | Scalability increase |

## Key Observations

1. **Shift from operational disruption to data extortion**  
   After the high-visibility Collins MUSE ransomware (Sep 2025), 2026 public incidents on airports have been predominantly data-theft / extortion (MAG). Operational check-in blackouts of similar scale have not reappeared in open sources by late October 2026.

2. **Vendor concentration risk**  
   Shared platforms (MUSE, Amadeus, port management software) create systemic exposure. One compromised provider can affect multiple airports or logistics operators simultaneously.

3. **Initial access trends**  
   - Credential-based (valid accounts on third-party systems)
   - RMM and remote management tools (SimpleHelp, FortiClient EMS)
   - Unpatched CVEs on perimeter devices

4. **AI operationalization**  
   INC-related affiliates demonstrated systematic use of commercial AI (Claude via OpenRouter) for reconnaissance, command generation, data triage and extortion drafting. This lowers the skill barrier and increases volume.

5. **Persistence & reinfection patterns**  
   Historical lesson from Collins: attackers re-infiltrated systems during recovery. Credential hygiene and network segmentation remain critical.

## Recommended Defensive Priorities (Aviation / Airport Operators)

- Inventory and hard-segment all third-party passenger processing and RMM systems
- Enforce least-privilege + MFA on any shared vendor access
- Continuous monitoring of FortiClient EMS, SimpleHelp and similar consoles for anomalous admin accounts
- Rapid credential rotation and invalidation after any third-party incident
- Manual fallback procedures tested and staffed (lesson from 2025)
- Dark-web / leak-site monitoring for early claim detection

## Sources

Compiled from public reporting (ENISA references, vendor statements, leak-site claims, technical analyses) as of 28 Oct 2026.
