# Cybersecurity Portfolio

Welcome to my portfolio. This repository documents my hands-on labs, projects, and notes as I complete the Google Cybersecurity Professional Certificate.

---

## Project 1: Incident Response Playbook (Phishing Triage)

### Scenario Background
I created this playbook based on a mock corporate incident scenario. A small medical practice suffered a security breach after an employee interacted with a malicious email. My goal was to outline the exact documentation and operational steps required to investigate the incident securely.

### Phase 1: Preparation & Detection
* **Alert Triage:** Review security alerts to identify the malicious sender address and timestamps.
* **Scope Definition:** Identify which internal systems or employee accounts interacted with the link.

### Phase 2: Containment & Isolation
* **Account Action:** Mandate an immediate password reset for the compromised account.
* **Network Isolation:** Disconnect the affected workstation from the local network to stop potential lateral movement.

### Phase 3: Eradication & Recovery
* **Malware Removal:** Scan the local system for malicious artifacts or persistence mechanisms.
* **Evidence Handling:** Document the chronological steps to maintain a secure chain of custody for legal and insurance requirements.
