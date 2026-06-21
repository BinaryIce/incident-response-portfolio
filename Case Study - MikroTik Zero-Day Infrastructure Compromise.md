# Case Study: Defeating Edge Infrastructure Compromise and Routing Manipulation via MikroTik Zero-Day

## Executive Summary

* **The Threat:** Edge routing and switching infrastructure connected to the Gecko Internet WISP transport network was actively compromised by an advanced adversary exploiting an unpatched MikroTik zero-day vulnerability. The threat actors established external Command and Control (C2) communications, modified production network paths to hijack/reroute traffic, and deployed persistent configuration scripts designed to recreate administrative backdoors upon remediation attempts.
* **The Intervention:** Executed an immediate out-of-band infrastructure isolation strategy. Conducted forensic analysis to identify the attacker's web-based C2 infrastructure, analyzed the persistence scripts, and performed a total bare-metal recovery utilizing secure, historical off-site configuration backups retrieved from an isolated Google Business environment. 
* **The Outcome:** 100% operational remediation and traffic normalization achieved. Full forensic artifacts, including malware configuration scripts, malicious C2 indicators, and system screenshots, were securely packetized and submitted to the FBI via an official IC3 compliance filing. Zero persistent backdoors remained active.

---

## 1. Initial Assessment & Blast Radius Analysis

Anomalous traffic patterns and unauthorized modifications to core network paths indicated a deep compromise of the primary edge routing layers:
* **Vulnerability Vector:** Adversaries leveraged a zero-day exploit targeting the RouterOS management interface, bypassing standard perimeter access controls to gain immediate root-level administrative access.
* **Traffic Hijacking:** Once inside, the threat actors altered routing tables and Layer 2/3 network paths, attempting to intercept, sniff, or redirect traffic flowing across the WISP-connected infrastructure.
* **C2 Communication:** Forensic log review revealed that the compromised MikroTik hardware was actively beaconing out to an external web repository/site used by the actors to convey incoming commands and coordinate downstream actions.

---

## 2. Containment, Forensics & Persistence Analysis

Rather than executing a basic reboot—which would have allowed the adversary to maintain their foothold—a systematic containment and evidence-gathering phase was initiated:

### Persistence Script Analysis
During the forensic audit of the router's scheduler and script files, a hidden malicious script was discovered. The script was engineered to execute automatically on system startup or binary modification, performing the following tasks:
1. Monitoring the user database for the removal of the hacker's access tokens.
2. Silently recreating a hidden administrative account with full privileges if deleted.
3. Automatically re-initiating outbound connection tunnels to bridge the local network back into the adversary's infrastructure.

### Evidence Preservation & Law Enforcement Escalation
Before clearing the devices, all critical forensic evidence was preserved to support a formal criminal investigation:
* Full screenshots of the unauthorized configurations, altered routing paths, and active connections were captured.
* The malicious persistence scripts, local logs, and identified C2 domains/IP addresses were securely packed into an evidence archive.
* A formal **Internet Crime Complaint Center (IC3)** report was filed with the **FBI**, providing law enforcement with the complete packetized payload and forensic artifacts for threat intelligence analysis.

---

## 3. Infrastructure Eradication & Recovery


```

[Isolated Google Business Email] ──(Secure Configuration Sync)──> [Air-Gapped Workstation] ──(Serial Netinstall)──> [Hardened MikroTik Edge]

```

Because the underlying operating system binaries were suspect due to the zero-day exploitation, standard software resets were avoided in favor of a trusted bare-metal rebuild:

1. **Out-of-Band Recovery Access:** Core switches and edge routers were completely isolated from the upstream Gecko Internet transit link to halt active traffic manipulation and terminate C2 beaconing.
2. **Configuration Extraction:** Known-good, uncompromised system configuration backups were securely pulled down from an off-site Google Business email vault, which was automatically updated every night via an encrypted, isolated cron cycle.
3. **Firmware Wipe & Netinstall:** The hardware was flashed at the physical layer using the MikroTik Netinstall utility, completely rewriting the storage sectors to eradicate any low-level rootkits or hidden persistence scripts.
4. **Hardened Restoration:** The verified configuration backups were restored to the clean firmware. All default service ports were disabled, administrative access was restricted strictly to out-of-band management interfaces, and firewall rules were updated to drop all unmapped outbound traffic.

---

## 4. Key Engineering Takeaways

1. **Decouple Backup Infrastructure:** Keeping configuration backups entirely separated from the primary network infrastructure (such as shipping them to a secure, external cloud inbox nightly) ensures recovery capability even during a total domain or infrastructure takeover.
2. **Assume Device Binary Compromise:** When dealing with zero-day exploits, do not trust the device's native operating system to report its own status or handle its own reset. Flash the hardware via lower-level serial/bootloader utilities (like Netinstall) to ensure absolute eradication of persistent scripts.
3. **Document and Escalated Immediately:** Treating a breach as a potential crime scene by documenting artifacts, screenshotting malicious scripts, and handing them to federal authorities (IC3) protects the broader internet ecosystem and builds an unassailable record of institutional response.

```
