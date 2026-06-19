# Project 2: Internal Security Audit (Botium Toys)

## Scenario Background
Botium Toys is a fictional, fast-growing online toy retailer serving both US and EU customers. The company lacks a dedicated security strategy, leaving its expanding digital infrastructure vulnerable. The objective of this project was to conduct a comprehensive internal security audit to align their current business practices with industry standards, mitigate high-risk vulnerabilities, and improve their overall security posture.

## Project Scope & Goals
*   **Scope:** Evaluation of all organizational assets, employee access controls, data processing systems (including point-of-sale and credit card data), and physical facilities.
*   **Goals:** 
    *   Align company practices with the **NIST Cybersecurity Framework (NIST CSF)**.
    *   Enforce the principle of least privilege for user access control.
    *   Ensure compliance with regulatory requirements (**PCI-DSS** for payments and **GDPR** for EU customer privacy).

---

## Risk Assessment & Controls Evaluation

### 1. Administrative Controls
*   **Status:** 🔴 **Critical Gaps**
*   **Findings:** The company lacks formalized security policies, documented incident response plans, and regular employee security awareness training.
*   **Impact:** Higher likelihood of successful phishing attacks and delayed reactions during a live security incident.

### 2. Technical Controls
*   **Status:** 🔴 **Critical Gaps**
*   **Findings:** 
    *   No encryption on customer Personal Identifiable Information (PII) or credit card data at rest or in transit.
    *   All employees possess unrestricted access to sensitive company data.
    *   Lack of an Intrusion Detection System (IDS) or Intrusion Prevention System (IPS).
    *   No centralized logging/SIEM solution and a complete absence of data backup or disaster recovery plans.
*   **Impact:** Massive vulnerability to ransomware, data breaches, and heavy legal penalties.

### 3. Physical Controls
*   **Status:** 🟢 **Sufficient**
*   **Findings:** Physical assets are adequately protected. The facility utilizes active CCTV surveillance, physical door/cabinet locks, and functional fire detection systems.

---

## Compliance Checklist

| Standard / Framework | Status | Requirement & Findings |
| :--- | :---: | :--- |
| **NIST CSF** | ⚠️ Partial | Core pillars (Identify, Protect, Detect) are unfulfilled due to a lack of asset management and technical controls. |
| **PCI-DSS** | ❌ Non-Compliant | Customer credit card information is not encrypted, violating data protection requirements for payment processing. |
| **GDPR** | ❌ Non-Compliant | EU customer data is stored insecurely without encryption or strict access controls, risking heavy compliance fines. |

---

## Actionable Recommendations
1.  **Enforce Least Privilege:** Restrict staff account permissions so employees can only access data mandatory for their immediate job roles.
2.  **Implement Data Encryption:** Immediately deploy cryptographic protections for PII and payment data both at rest and in transit.
3.  **Deploy Monitoring & Defense:** Install an Intrusion Detection System (IDS) and set up routine firewalls and anti-malware definition updates.
4.  **Establish Continuity Plans:** Configure automated off-site backups and draft a formal disaster recovery strategy.
