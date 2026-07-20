# Cloud SIEM Honeypot Lab with Automated Incident Triage

## Project Description
This project demonstrates the end-to-end engineering of a cloud-native Security Information and Event Management (SIEM) environment. It features an intentionally exposed Azure Virtual Machine acting as a honeypot to attract global threat actors, integrated log pipelines using the modern Azure Monitor Agent (AMA), custom correlation logic in Microsoft Sentinel, and automated AI incident analysis.

---

## Architecture & Implementation Pipeline

```text
 ┌────────────────────────┐      ┌────────────────────────┐      ┌────────────────────────┐
 │   1. Exposed Azure VM  │ ───> │  2. Data Collection    │ ───> │ 3. Microsoft Sentinel  │
 │   Windows Firewall OFF │      │      Rule (AMA)        │      │    SIEM Workspace      │
 └────────────────────────┘      └────────────────────────┘      └───────────┬────────────┘
                                                                             │
 ┌────────────────────────┐      ┌────────────────────────┐                  │
 │  6. AI Copilot Triage  │ <─── │  5. Analytics Rule     │ <────────────────┘
 │  Incident Mitigation   │      │     Triggered (ID 52)  │
 └────────────────────────┘      └────────────────────────┘
```

### Phase 1: Threat Hunting via KQL
To test the pipeline, an adversarial simulation was conducted from an external Kali Linux environment using `Hydra` to stress-test the RDP interface (Port 3389). A custom Kusto Query Language (KQL) query targeting Event ID 4625 (Failed Logon) was executed to parse the raw database and cleanly map out the attacker's footprint.

<img width="1600" height="900" alt="Screenshot 2026-07-20 235825" src="https://github.com/user-attachments/assets/ed12f616-8227-448c-b7b7-da32238013f2" />



### Phase 2: Detection Engineering & Rule Logic
A scheduled analytics rule was built to continuously monitor the `SecurityEvent` log indexes. The rule was configured to automatically aggregate data and alert the Security Operations Center (SOC) anytime authentication anomalies exceeded a threshold of 5 failures within a rolling 5-minute window.

<img width="893" height="439" alt="image" src="https://github.com/user-attachments/assets/7455e573-9517-48b2-8708-596a9cbac66b" />


### Phase 3: Incident Management & AI Triage
Upon reaching the log threshold, Microsoft Sentinel raised a high-severity alert ticket (**Incident ID 52: Honeypot RDP Brute Force Alert**). Utilizing native platform-integrated AI features, an automated executive summary was generated to map out temporal context, target accounts, and prioritize response.

<img width="1552" height="814" alt="Screenshot 2026-07-21 000934" src="https://github.com/user-attachments/assets/2737639d-7510-40b6-86ca-42a62a57c1eb" />


---

## Core Technical Skills Demonstrated
* **SIEM / Logging Engineering:** Log Analytics Workspace management, Azure Monitor Agent (AMA) configuration, Data Collection Rules (DCR).
* **Threat Hunting:** Querying raw telemetry endpoints using Kusto Query Language (KQL).
* **Detection Engineering:** Creating custom scheduled alert correlation rules inside Microsoft Defender for Cloud.
* **Threat Emulation:** Executing RDP brute-force dictionary attacks via Hydra on Kali Linux.
* **Modern SOC Workflows:** Navigating incident response panels and leveraging cloud-native AI tools.
