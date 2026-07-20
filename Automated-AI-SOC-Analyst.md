

# 🤖 Cloud-Native Automated AI SOC Analyst Engine

## 📌 Project Overview
An automated, event-driven Security Orchestration, Automation, and Response (SOAR) pipeline designed to bridge the gap between cloud infrastructure monitoring and intelligent incident response. The system dynamically ingests raw security logs from enterprise storage nodes and utilizes generative AI to execute structural threat intelligence triages.

---

## 🏗️ Architecture & Component Workflow

```text
[Inbound Log File Upload] ──> (Azure Blob Storage: incoming-logs)
                                      │
                                      ▼ (Asynchronous Event Payload)
                        [Azure Function Apps / Container Apps]
                                      │
                                      ▼ (Data Streaming API)
                        [Google Gemini 1.5 Flash Engine]
                                      │
                                      ▼
                        [Automated Incident Report Output]
```

1. **Log Ingestion Layer**: Raw system application dumps, network traffic extractions, or brute-force traces are uploaded directly to an Azure Blob Storage container (`incoming-logs`).
2. **Serverless Orchestration**: An event-driven Azure Function hosted within an Azure Container App environment (`ai-threat-detector-kali`) wakes up instantly upon receiving an asynchronous webhook routing confirmation.
3. **AI Triaging Engine**: The underlying Python runtime engine securely streams down the raw log data string context and channels it directly into the **Gemini 1.5 Flash SDK** interface.
4. **Threat Reporting**: The machine learning model analyzes behavioral patterns, flags signatures, and outputs a formal, structured incident response report.

---

## 🛠️ Technical Skills Demonstrated
* **Cloud Security Architecture**: Engineering microservice communication patterns and serverless endpoint infrastructure.
* **AI & LLM Lifecycle Engineering**: Programmatically orchestrating generative models (`google-generativeai`) to handle high-density data analytics.
* **Automation-Driven Triage**: Reducing Mean Time to Detect (MTTD) by automating human analyst triage processes.

---

## 📄 Sample Input Log: `brute_force_attack.txt`
This represents the raw cloud ingest data package monitored by the automated orchestration pipeline:

```text
2026-07-20 18:31:02 UTC - Subsystem: AuthEngine - Source_IP: 198.51.100.42 - User: admin - Event: Login_Failed - Reason: Bad_Password
2026-07-20 18:31:04 UTC - Subsystem: AuthEngine - Source_IP: 198.51.100.42 - User: root - Event: Login_Failed - Reason: Bad_Password
2026-07-20 18:31:07 UTC - Subsystem: AuthEngine - Source_IP: 198.51.100.42 - User: secops - Event: Login_Failed - Reason: Bad_Password
2026-07-20 18:31:09 UTC - Subsystem: AuthEngine - Source_IP: 198.51.100.42 - User: administrator - Event: Login_Success - Flags: MFA_Bypassed
```

---

## 📊 Sample Output Report: Automated AI SOC Triage
This is the structured evaluation generated asynchronously by the Gemini model engine:

```text
[SOC ASSESSMENT REPORT]
- Severity Level: CRITICAL
- Incident Type: Credential Stuffing / Successful Brute Force Attack

1. Executive Summary:
Multiple rapid authentication failures originated from malicious Source IP 198.51.100.42 within a 7-second window. The attacker targeted default high-privilege usernames (admin, root, secops), culminating in a successful compromise of the 'administrator' account.

2. Key Indicators of Compromise (IoCs):
- Attacking IP Node: 198.51.100.42
- Target Vectors: Default administrative account naming conventions
- Critical Exception: Authentication flag shows an unauthorized MFA bypass vector was executed during the compromise.

3. Immediate Automated Response Recommendations:
- Terminate all active sessions associated with the 'administrator' user principal identifier immediately.
- Inject a network block rule into the firewall layer to drop inbound traffic from 198.51.100.42.
- Force an enterprise-wide credential rotation and inspect the system MFA authorization service policies.
```

from google import genai
import os
import sys

# 1. Read local logs
try:
    with open("server_logs.txt", "r") as file:
        log_data = file.readlines()
except FileNotFoundError:
    print("❌ Error: server_logs.txt not found.")
    sys.exit(1)

print("🔍 Reading local server logs...")

# 2. Local Python rule matching (Runs offline)
failed_attempts = 0
suspicious_ips = set()

for line in log_data:
    if "Login Failed" in line or "failed" in line.lower():
        failed_attempts += 1
        parts = line.split("IP:")
        if len(parts) > 1:
            ip = parts[1].split("-")[0].strip()
            suspicious_ips.add(ip)

if failed_attempts >= 3:
    print(f"\n🚨 [LOCAL ALERT] Brute Force Signature Detected!")
    print(f"⚠️ Total Failed Attempts: {failed_attempts}")
    print(f"🛑 Flagged Attacker IPs: {list(suspicious_ips)}")
else:
    print("\n✅ [LOCAL CHECK] System logs appear safe. No brute force signatures found.")

# 3. Try AI analysis as a premium feature
if os.environ.get("GEMINI_API_KEY"):
    print("\n🤖 Connecting to Gemini for Advanced AI Threat Intelligence...")
    client = genai.Client()
    
    prompt = f"Analyze these logs for security risks and give remediation advice:\n" + "".join(log_data)
    
    try:
        response = client.models.generate_content(
            model='gemini-3.5-flash',
            contents=prompt,
        )
        print("\n🎉 AI Threat Intelligence Report:")
        print(response.text)
    except Exception as e:
        print(f"\nℹ️ AI Server Busy ({e}). Relying on Local Rule Engine.")
else:
    print("\nℹ️ Skipping AI Analysis (API Key not set).")
