# Case Study: Restoring Emergency Communications via Survivalist Fixed-Wireless Architecture

## Executive Summary

* **The Threat:** Following the catastrophic landfall of Hurricane Harvey in the Corpus Christi region, complete grid failure and widespread subterranean fiber cuts rendered traditional telecom infrastructure entirely offline. Regional cellular networks were heavily saturated or non-functional, cutting off critical data systems required by the American Red Cross for logistics, supply lines, and medical coordination.
* **The Intervention:** Rather than relying on standard commercial carriers or waiting for public infrastructure restoration, a rapid-deployment field operation was executed to leverage an independent, high-altitude Fixed Wireless Internet Service Provider (WISP) network that survived the storm surge. A tactical local area network (LAN) was built on-site using conditioned generator power and isolated distribution arrays.
* **The Outcome:** 100% operational data connectivity restored to the emergency field operations center and megashelter. The network safely handled high-density tactical traffic for hundreds of disaster relief workers without a single hour of downstream downtime, ensuring uninterrupted emergency services to the local community.

---

## 1. Initial Assessment & Environmental Constraints

Upon arriving at the designated Corpus Christi relief site, a rapid physical and RF assessment was conducted to establish the operational baseline:
* **Infrastructure Collapse:** Local underground fiber backhauls were completely compromised by uprooted trees and severe localized flooding. Cellular towers lacked stable auxiliary power or suffered from extreme backhaul congestion.
* **Power Quality Degradation:** The site relied entirely on auxiliary portable field generators. Raw generator output exhibited significant voltage sags and frequency fluctuations capable of destroying sensitive microwave or routing hardware.
* **RF Spectrum Over-Saturation:** The concentration of emergency radios and personal consumer devices in a confined metal-frame shelter structure created a highly destructive co-channel interference environment in the 2.4GHz spectrum.

---

## 2. Infrastructure Reconstruction & Deployment Phases

### Tactical Backhaul Engineering
The independent local WISP, **Gecko Internet**, was identified as the sole functioning commercial internet infrastructure remaining in the sector due to their high-altitude line-of-sight tower positioning. 
* A heavy-duty temporary mast mount was rigged on the facility roof, braced mechanically to withstand residual high-velocity coastal winds.
* A high-gain directional subscriber dish was mounted and manually aligned to the nearest surviving Gecko Internet sector tower.
* Azimuth and elevation were precision-tuned while tracking RSSI (Received Signal Strength Indicator) and CINR (Carrier-to-Interference-plus-Noise Ratio) until a stable, low-latency symmetric link was locked.

### Power Conditioning Layer
To protect the core network stack from dirty generator power, the generator feed was routed into an **online double-conversion UPS**. This architecture ensured that incoming erratic AC power was constantly converted to DC, and then regenerated into a pristine, stable AC sine wave to feed the PoE injectors and security gateway.

### Access & Distribution Layer
* High-density, ruggedized Wireless Access Points (WAPs) were deployed across the operational floor.
* The local network was completely segmented via VLANs to isolate corporate operational data from public or volunteer traffic.
* The 2.4GHz band was disabled entirely on operational SSIDs, forcing all critical logistics tablets and laptops onto cleaner 5GHz channels configured with narrow 20MHz channel widths to prioritize link resilience over theoretical raw throughput.

---

## 3. Traffic Micro-Management & Edge Policies

To prevent the fixed-wireless backhaul from being choked by automated background OS updates or non-essential data syncs, aggressive Quality of Service (QoS) queues were enforced at the firewall edge:

| Priority Level | Traffic Classification | Allocation Strategy |
| :--- | :--- | :--- |
| **Priority 1 (Critical)** | National Disaster Data Systems, VoIP, Radio-over-IP | Guaranteed bandwidth allocation; absolute queue priority. |
| **Priority 2 (Operational)** | Standard operational email, logistical coordination spreadsheets | Best-effort allocation; capped during peak operational hours. |
| **Priority 3 (Restricted)** | Video streaming, social media uploads, background OS updates | Aggressively throttled or dropped at the security gateway. |

---

## 4. Key Engineering Takeaways

1. **Leverage Regional Sovereignty:** Maintaining up-to-date documentation on independent, regional WISPs is invaluable for disaster recovery. Local wireless operators can re-route sector capacity or manually adjust tower settings to prioritize a critical emergency hub far faster than a major nationwide telecom provider.
2. **Mandatory Shielded Cabling:** Deploying high-gain outdoor antennas in stormy coastal conditions requires shielded twisted pair (STP) cabling with grounded RJ45 connectors. This prevents static electricity buildup from high winds from blowing out the physical Ethernet ports on internal switching hardware.
3. **Power Isolation is Non-Negotiable:** Field networking equipment should never be connected directly to a standard standby UPS on generator lines. Online double-conversion topology is a mandatory requirement to isolate delicate microwave radios from devastating voltage fluctuations.
