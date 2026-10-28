# Manchester Airports Group (MAG) – FulcrumSec Breach

**Date**: Late August 2026 (confirmed 27 Aug, leak early September)  
**Actor**: FulcrumSec (also tracked as The Threat Thespians)  
**Type**: Data theft + extortion  
**Affected**: Manchester Airport, London Stansted, East Midlands Airport

## Summary

Unauthorized access to systems holding customer data related to:
- Airport Wi-Fi registrations
- Car park bookings
- Lounge access
- Fast Track services

MAG stated that bank/payment details were **not** present on the affected systems and that airport operations and aviation security remained unaffected.

## Actor Claims

- Initial claim: ~86 GB stolen
- Later leak: approximately half a terabyte of data covering ~8.7 million individuals
- Samples included consolidated customer profiles, booking histories, marketing classifications, browser/IP/geolocation data, vehicle registrations, names, emails, phone numbers

Have I Been Pwned reviewed the dataset.

## Impact Assessment

- **Operational**: None reported on flights or security systems
- **Data**: High volume of PII useful for targeted phishing and travel-related social engineering
- **Financial**: No payment card data confirmed exposed

## Actor Profile

Relatively recent financially motivated extortion group. Active against various sectors (pharma, engineering, data analytics) in 2026. NCC Group data indicated significant activity volume in May 2026.

## Defensive Takeaways

- Ancillary customer systems (WiFi portals, parking, lounges) are attractive targets even when core operational systems are better protected
- Data minimization and segmentation of passenger ancillary data reduce blast radius
- Monitoring of leak sites for early detection of claims remains valuable

## Sources

Public statements by MAG, leak-site claims relayed via media (Computer Weekly, Cybernews, CircleID), Have I Been Pwned confirmation.
