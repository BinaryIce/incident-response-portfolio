# Incident Response & Tactical Infrastructure Portfolio

Welcome to my cybersecurity and infrastructure engineering portfolio. This repository serves as a definitive proof-of-work archive documenting real-world, high-stakes incident response operations, bare-metal infrastructure reconstruction, and tactical emergency network deployments executed under critical constraints.

The case studies detailed below demonstrate hands-on experience in mitigating advanced adversary persistence, analyzing zero-day exploits, coordinating with federal law enforcement, and engineering resilient networks under total grid-down conditions.

---

## 🛠️ Featured Case Studies

### 1. 🛡️ Enterprise Defense & Recovery
#### [Infrastructure Reconstruction: Eliminating a $300,000 Ransomware Demand](./Case%20Study%20-%20Ransomware%20Remediation.md)
* **Scenario:** Active production environment fully compromised by an adversarial ransomware payload. The threat actors established persistence, encrypted the core Active Directory domain controller, and issued a $300,000 extortion demand.
* **Core Interventions:** Refused all extortion negotiations. Executed a high-intensity, bare-metal infrastructure reconstruction and secure data extraction strategy over a holiday weekend.
* **Outcome:** 100% operational restoration, complete eradication of adversary persistence, and zero dollars paid to extortionists within a tight 36-hour window.

### 2. 📡 Tactical Field Operations
#### [Disaster Response: Restoring Emergency Communications via Survivalist Fixed-Wireless](./Hurricane%20Harvey%20Tactical%20Network%20Deployment.md)
* **Scenario:** Total regional telecom grid collapse and fiber damage in Corpus Christi following Hurricane Harvey, leaving the American Red Cross without critical coordination data systems.
* **Core Interventions:** Engineered a tactical local network (LAN) utilizing raw field generator power isolated via an online double-conversion UPS. Provisioned high-throughput backhaul via a precision-aligned high-gain directional WISP link using the Gecko Internet network.
* **Outcome:** 100% connectivity uptime for hundreds of disaster relief workers, enforcing strict 5GHz RF isolation and edge QoS traffic shaping to guarantee critical logistics bandwidth.

### 3. 🔍 Threat Intelligence & Digital Forensics
#### [Defeating Edge Infrastructure Compromise and Routing Manipulation via MikroTik Zero-Day](./Case%20Study%20-%20MikroTik%20Zero-Day%20Infrastructure%20Compromise.md)
* **Scenario:** Edge routing and switching infrastructure connected to the Gecko Internet WISP transport network actively compromised by an advanced adversary exploiting an unpatched MikroTik RouterOS zero-day vulnerability.
* **Core Interventions:** Isolated the active C2 beaconing infrastructure out-of-band. Discovered and analyzed a hidden persistence script engineered to silently recreate admin backdoors. Executed a low-level bare-metal firmware flash (Netinstall) and restored verified, historical configurations retrieved from an isolated nightly Google Business email vault.
* **Outcome:** 100% traffic normalization and backdoor eradication. Preserved and packetized full forensic artifacts, malicious source code, and configuration screenshots to submit a formal **IC3 compliance filing to the FBI**.

---
### 4. 🥷 Dark-Target Infrastructure & Cryptographic Segmentation
#### [Engineering High-Anonymity Cryptographic Overlays via ZeroTier Mesh and Tor Onion Services](./Case%20Study%20-%20ZeroTier%20Mesh%20and%20Tor%20Onion%20Services.md)
* **Scenario:** Protecting highly sensitive, internal application servers and staging utilities from automated global zero-day scans, perimeter brute-forcing, and public DNS mapping.
* **Core Interventions:** Architected a zero-trust hidden ecosystem. Bound internal daemons strictly to the host loopback, routed external client access via a cryptographically secure V3 Tor Onion Service, and layered peer-to-peer administrative switching using a private ZeroTier mesh overlay.
* **Outcome:** Eliminated 100% of the public internet attack surface. The environment maintains zero open inbound WAN ports, achieves full location-independence, and registers as completely dark on external Nmap/Shodan scans.

## 🧠 Core Technical Expertise Demonstrated

* **Incident Response & Digital Forensics:** Threat actor persistence removal, blast radius assessment, C2 beaconing identification, evidence preservation, and federal law enforcement coordination (IC3).
* **Tactical Networking & Backhaul:** Fixed-wireless (WISP) Point-to-Point backhaul provisioning, high-density RF spectrum optimization (5GHz isolation), VLAN segmentation, and edge traffic shaping/QoS.
* **Infrastructure Resilience:** Bare-metal system recovery, serial-level firmware flashing (Netinstall), air-gapped configuration deployment, and decoupled backup architecture management.
