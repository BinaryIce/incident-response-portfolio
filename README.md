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

## 🧠 Core Technical Expertise Demonstrated

* **Incident Response & Digital Forensics:** Threat actor persistence removal, blast radius assessment, C2 beaconing identification, evidence preservation, and federal law enforcement coordination (IC3).
* **Tactical Networking & Backhaul:** Fixed-wireless (WISP) Point-to-Point backhaul provisioning, high-density RF spectrum optimization (5GHz isolation), VLAN segmentation, and edge traffic shaping/QoS.
* **Infrastructure Resilience:** Bare-metal system recovery, serial-level firmware flashing (Netinstall), air-gapped configuration deployment, and decoupled backup architecture management.
