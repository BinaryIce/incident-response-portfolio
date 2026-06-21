# incident-response-portfolio
Technical post-mortems, secure architecture blueprints, and bare-metal incident response documentation.
# Case Study: Eliminating a $300,000 Ransomware Demand via Infrastructure Reconstruction

## Executive Summary
*   **The Threat:** An organization’s production environment was fully compromised by an adversarial ransomware payload. The threat actors established persistence, encrypted the core active directory domain controller, and issued an extortion demand equivalent to **$300,000 in Bitcoin** for the decryption keys.
*   **The Intervention:** Rather than engaging in negotiation or paying the ransom, a high-intensity bare-metal infrastructure reconstruction and data extraction strategy was executed over the July 4th holiday weekend.
*   **The Outcome:** 100% operational restoration, complete eradication of threat actor persistence, and zero dollars paid to extortionists. The environment was securely verified and handed back to the client fully functional within a tight 36-hour window.

---

. Initial Assessment & Blast Radius Analysis

An emergency post-incident audit was conducted to map the compromise vectors and locate surviving assets while the primary network was entirely locked down.

    Compromise Vector: An internal user (Accounting) initiated a remote connection to the corporate server through a traditional client-side VPN. The endpoint device had been compromised via a phishing vector or a drive-by malicious download, allowing the payload to pass directly through the encrypted VPN tunnel.

    Lateral Movement: Exploiting a lack of internal network microsegmentation, the malware moved horizontally from the compromised VPN endpoint straight to the core infrastructure. The payload targeted a Windows Server 2012 Domain Controller, executing encryption routines across all visible operating system paths and local shares.

    The Critical Discovery: During a physical asset and disk topology audit, a hidden hardware asset was identified: an external storage drive connected directly to the server. The primary host OS had been configured such that the drive volume structure was invisible to standard Windows explorer paths, inadvertently creating an air-gapped security layer that protected it from the automated ransomware script.

2. Emergency Response & Recovery Timeline
Phase 1: Zero-Hour Perimeter Blackout & Triage (Holiday Weekend Deployment)

The immediate priority was to contain the blast radius and verify the integrity of the hidden storage device without exposing it to potential re-infection vectors.

    Action: Severed the compromised VPN gateway and terminated all active network states on Thursday, July 3rd, to kill any active Command and Control (C2) persistence.

    Action: Safely unmounted the hidden external storage drive from the infected physical machine to prevent any delayed or reactive execution routines from touching it.

Phase 2: Sandboxed Forensics & Disk Mounting

Because the external drive had been physically attached to a compromised host, treating it as natively safe was a high-risk path.

    Action: Provisioned an isolated, non-networked Linux Virtual Machine (VM) to act as a secure forensic sandbox.

    Action: Attached the raw external storage drive to the Linux VM layer. Deep-level partition analysis revealed an unencrypted virtual disk container (Image Format: .vmdk) containing the organization's complete system and database backups.

    Action: Safely mounted the virtual disk filesystem inside the Linux sandbox, verified the data block integrity, and performed a thorough signature scan to ensure no dormant malware payloads were embedded within the backup tree.

    Action: Bit-stream copied the verified corporate data structures cleanly onto a secondary, sterile external storage target.

Phase 3: Bare-Metal Purification and Re-deployment

With the verified data safely isolated on a clean medium, the tainted infrastructure was systematically purged over the course of Friday, July 4th.

    Action: Executed a low-level format on the compromised Windows Server 2012 physical machine and all verified local client endpoints, completely destroying the compromised OS footprints, partition tables, and potential rootkits.

    Action: Installed a fresh, hardened instance of the Windows Server OS directly onto the clean bare-metal hardware.

    Action: Securely transferred the recovered data from the sterile backup drive back onto the newly provisioned server volumes, running an aggressive post-migration file integrity and virus sweep to finalize verification by Friday night.

3. Business Metrics & Deliverables

    Ransom Paid: $0.00 (Threat actors denied all leverage)

    Data Recovery Rate: 100% Structural Integrity Retained

    Time to Operational Baseline: Under 36 Hours (Fully operational prior to the conclusion of the holiday weekend)

Architectural Takeaway

Traditional perimeter security and standard corporate VPNs are no longer sufficient containment barriers; an infected remote endpoint can easily tunnel a payload directly into core directories. True security relies on an engineer's ability to maintain absolute situational awareness over bare-metal hardware, leverage multi-platform environments (like using Linux forensic sandboxing to safely handle Windows images), and execute rapid, automated bare-metal purges when a production kernel is compromised.


## Technical Architecture & Lifecycle Map

```mermaid
graph TD
    %% Define Styles
    classDef compromised fill:#ffcccc,stroke:#cc0000,stroke-width:2px,color:#000;
    classDef isolate fill:#fff2cc,stroke:#d6b656,stroke-width:2px,color:#000;
    classDef secure fill:#d5e8d4,stroke:#82b366,stroke-width:2px,color:#000;

    %% Threat Vector Layer
    subgraph Incident_Origin [Incident Origin: Thursday, July 3rd]
        A[Compromised Accounting Endpoint] -->|Infected Client VPN Tunnel| B[Windows Server 2012 Domain Controller]
        B -->|Automated Ransomware Script| C[Primary Datastores Encrypted]
    end
    class A,B,C compromised;

    %% Isolation & Triage Layer
    subgraph Containment_Actions [Immediate Containment & Air-Gap Execution]
        D[Sever VPN Gateway & Kill Public WAN Link] -.->|Isolate C2 Persistence| B
        E[Identify Hidden External Backup Drive] -->|Physical Extraction from Host OS| F[Host Storage Isolation]
    end
    class D,E,F isolate;

    %% Hardened Forensic Layer
    subgraph Forensic_Purification [Hardened Clean Room Environment]
        F --> G[Attach Raw Drive to Non-Networked Host]
        G --> H[Provision Isolated Linux Forensic VM]
        H -->|Safely Mount Extracted .vmdk Container| I[Scan File Tree & Verify Data Integrity]
        I -->|Bit-Stream Copy Data Structures| J[Sterile Secondary Backup Target]
    end
    class G,H,I,J secure;

    %% Infrastructure Restoration Layer
    subgraph Bare_Metal_Rebuild [Production Environment Re-Deployment: Friday, July 4th]
        K[Execute Low-Level Format on Physical Server Hardware] --> L[Fresh Bare-Metal OS Installation]
        L --> M[Migrate 100% Verified Clean Data from Sterile Target]
        M --> N[Aggressive Post-Incident Signature Sweep]
        N --> O[100% Operational Baseline Restored & Hardened]
    end
    class K,L,M,N,O secure;


