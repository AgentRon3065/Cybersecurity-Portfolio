# 🛡️ Project: Endpoint Security Auditing & Network Telemetry Analysis Lab

## 📝 Executive Summary
Designed and deployed a localized, resource-lean defensive security micro-lab inside an isolated virtual environment using Kali Linux. The objective of this project was to establish a foundational understanding of blue-team operations by generating network and application traffic, configuring host-based defensive barriers, and threat hunting through modern system security logs.

---

## 🛠️ Tools & Technologies Used
*   **Hypervisor:** Oracle VM VirtualBox (Isolated Host-Only Virtual Networking)
*   **Operating System:** Kali Linux (Rolling Architecture)
*   **Network Analysis:** Wireshark Packet Analyzer
*   **Host Firewall:** Uncomplicated Firewall (UFW)
*   **Security Auditing:** `systemd-journald` (`journalctl`)
*   **Services:** Python3 HTTP Server Module

---

## 🚀 Lab Implementation Steps & Methodology

### Phase 1: Network Telemetry & Packet Isolation
*   Initialized a live promiscuous-mode packet capture using **Wireshark** on the primary interface (`eth0`).
*   Generated standard ICMP network discovery packets using the host terminal (`ping -c 4`).
*   Applied low-level display filters (`icmp`) to strip away background network noise (ARP/NTP) and isolate exact threat vectors.
*   Inspected raw packet hex/ASCII payloads to differentiate between legitimate network baseline traffic and data exfiltration techniques (such as ICMP Tunneling).

### Phase 2: Host Hardening & Network Whitelisting
*   Provisioned and initialized the Linux kernel firewall architecture (**UFW**).
*   Configured a strict structural security policy: **Default Deny (Incoming)** to drop unauthenticated scanning attempts, paired with **Default Allow (Outgoing)**.
*   Crafted custom transport-layer rule exceptions (`sudo ufw allow 80/tcp`) to safely expose an authorized listening web gateway while dropping adjacent port probes.

### Phase 3: Application Log Monitoring
*   Spawned a live listener service using Python's raw HTTP module on administrative port 80.
*   Audited open transport sockets locally via network statistics utilities (`sudo ss -tulpn`) to track active Process IDs (PIDs) running on the machine.
*   Simulated user and scanner interactions using `curl`, successfully reading incoming client `GET` request headers and tracking transactional response statuses (`HTTP 200 OK`).

### Phase 4: Threat Hunting via System Journals
*   Leveraged modern `journalctl` utility filters to bypass missing legacy flat text log constraints (`/var/log/auth.log`).
*   Executed structural parameter queries (`sudo journalctl _COMM=sudo -n 20`) to map administrative account accountability.
*   Isolated exact security events, including historical timestamps, targeted system binaries, and **intentional credential authentication failures** matching malicious user behavior profile models.

---

## 📸 Technical Evidence
<img width="1026" height="484" alt="image" src="https://github.com/user-attachments/assets/74607e85-3f74-405e-a15f-13203be0e646" />




---

## 🎯 Key Takeaways & Security Competencies
*   **Log Familiarity:** Learned to read raw, unstructured authentication strings and parse specific security codes like `authentication failure`.
*   **Defense-in-Depth:** Proven capability to enforce local network access control lists (ACLs) directly via the command line interface.
*   **Analytical Pivot:** Developed the investigative mindset required to capture a symptom in network traffic (Wireshark) and successfully pivot to system logs (`journalctl`) to verify the root cause.
