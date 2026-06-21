# incident-response-portfolio
Technical post-mortems, secure architecture blueprints, and bare-metal incident response documentation.
# Case Study: Eliminating a $300,000 Ransomware Demand via Infrastructure Reconstruction

## Executive Summary
*   **The Threat:** An organization’s production environment was fully compromised by an adversarial ransomware payload. The threat actors established persistence, encrypted the core active directory domain controller, and issued an extortion demand equivalent to **$300,000 in Bitcoin** for the decryption keys.
*   **The Intervention:** Rather than engaging in negotiation or paying the ransom, a high-intensity bare-metal infrastructure reconstruction and data extraction strategy was executed over the July 4th holiday weekend.
*   **The Outcome:** 100% operational restoration, complete eradication of threat actor persistence, and zero dollars paid to extortionists. The environment was securely verified and handed back to the client fully functional within a tight 36-hour window.

---

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
