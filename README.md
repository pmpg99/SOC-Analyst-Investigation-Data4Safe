# SOC Incident Investigation Lab — Data4Safe Simulation

 - The full technical report is available in Portuguese; an English Executive Summary is provided below / in the repository. - 

Hi, I'm Pedro. This is a hands-on project I built to simulate a real-world SOC incident investigation — from detecting suspicious network behavior to remediating risks in a controlled environment.


### What I Did
- Investigated latency alerts on a legacy Linux server
- Captured and analyzed live SSH brute-force attempts
- Discovered vulnerable services and tested credential weakness
- Collected and sanitized forensic logs for safe sharing
- Proposed hardening actions for production environments
- 

### Why I Built This
I wanted to practice core SOC/Blue Team skills like:
- Traffic analysis (tcpdump/Wireshark)
- Service reconnaissance (Nmap)
- Vulnerability correlation (searchsploit)
- Log anonymization and evidence handling
- Reporting and mitigation planning


All work was done in my own isolated lab. No unauthorized systems were accessed.

---

## 🏬 Project Context (The Scenario)
This investigation centers on a fictional logistics company, **Data4Safe**. As the lead investigator, I was alerted to significant server latency and reports of "sluggish" performance on a core Linux server. 

The goal was not just to stop the lag, but to find the root cause: Was it a misconfiguration, or an active intrusion?

## 🏗️ Lab Infrastructure
I chose to use a mix of physical and virtual hardware to replicate a realistic "Legacy Server" scenario where old, unpatched systems still exist in the corporate perimeter.

### The Setup:
- **Attacker Machine:** Kali Linux (Run on a dedicated physical machine for performance).
- **Target Machine:** A legacy Ubuntu 12.04.3 LTS (Metasploitable 2) instance. I chose this version specifically because it is intentionally unpatched, allowing for a wide range of vulnerability exploration.
- **Network Environment:** An isolated local lab (Bridged/NAT) simulating a segmented DMZ to ensure all traffic remained under my control.

### Investigated Risk:
The focus was on the **External Perimeter**, specifically attacking and defending exposed services like SSH, Apache, and VSFTPD.

---

## 🛠️ Technical Toolkit
I used a combination of industry-standard tools to carry out the investigation. Each tool was selected for a specific phase of the incident response lifecycle.

| Phase | Tools Used | Skills Demonstrated |
| :--- | :--- | :--- |
| **Detection & Triage** | `tcpdump`, Wireshark | Packet capture, protocol filtering, traffic analysis. |
| **Recon & Discovery** | `Nmap`, `theHarvester` | Service versioning, OSINT, mapping the attack surface. |
| **Validation** | `Ncrack`, `Hydra` | Credential stress-testing, validating weak auth policies. |
| **Correlation** | `searchsploit` | Mapping identified services to known CVEs/exploits. |
| **Forensics & Sharing** | Bash, `sed` | Log anonymization, evidence preservation (PII masking). |

### Key Skills Applied:
- **Incident Response Lifecycle:** Discovery -> Analysis -> Containment -> Remediation.
- **Protocol Analysis:** Deep-diving into SSH (port 22) and TCP handshakes.
- **Scripting for SOC:** Automating tedious tasks (like cleaning 10,000 log lines) using Bash.
- **Reporting:** Translating technical findings into a professional PDF summary.

---

## 🔍 Investigation Workflow (Step-by-Step)

### 1. Initial Triage & Packet Capture
Following reports of server latency, I initiated a live packet capture using `tcpdump`. I then moved the PCAP to **Wireshark** for deep analysis. 
- **Finding:** I identified a massive volume of SYN packets and failed login attempts targeting port 22. This confirmed the latency was caused by an active **SSH Brute-Force/Credential Spraying** attack.

### 2. Attack Surface Mapping
Once the attack vector was identified, I performed a version-intensity scan using `Nmap` to see what else was exposed.
- **Finding:** The scans revealed several legacy services (Apache, VSFTPD) running outdated versions with multiple known vulnerabilities. I used `searchsploit` to correlate these services with specific CVEs.

### 3. Impact Validation (Controlled Lab)
To prove the risk of weak passwords to the "client," I used `Ncrack` and `Hydra` within my authorized lab environment to test the server’s resistance.
- **Result:** Within minutes, I achieved a successful login. This provided the "Proof of Concept" needed to justify immediate hardening of the authentication policies.

### 4. Forensic Log Handling
Following the "Chain of Custody" principle, I needed to share the evidence without exposing sensitive data (PII). I developed a **Bash script using `sed`** to automate the anonymization of system logs.
- **Process:** The script masks IPs and usernames while keeping the timestamps and error codes intact, making the logs safe for external reporting or stakeholder review.

---

## 📉 Key Findings & Remediation Plan

Based on the investigation, I identified several critical security gaps. Below are the findings and the proposed hardening steps to secure the infrastructure.

### 🚩 Critical Findings:
*   **Authentication Weakness:** The server allowed unlimited SSH login attempts with no lockout policy, making it highly susceptible to brute-force attacks.
*   **Technical Debt:** The use of a legacy, unpatched Ubuntu instance (12.04) left the system exposed to well-known exploits in Apache and VSFTPD.
*   **Lack of Monitoring:** The attack was only discovered due to "latency" reports from users, indicating a lack of proactive alerting/SIEM integration.

### ✅ Recommended Mitigations:
1.  **SSH Hardening:** 
    *   Disable password-based authentication and enforce **SSH Key-Pair** authentication.
    *   Implement **Fail2Ban** to automatically block IPs after 3-5 failed attempts.
    *   Change the default SSH port to reduce noise from automated bots.
2.  **Access Control:** Implement **Multi-Factor Authentication (MFA)** for all administrative access.
3.  **Vulnerability Management:** Decommission or immediately patch legacy services. If the legacy system is mission-critical, isolate it within a strictly firewalled **VLAN**.
4.  **Logging & Alerting:** Centralize system logs and configure automated alerts for "High-Frequency Failed Logins" to catch attacks before they consume server resources.

---

## 📁 Repository Structure
To help you navigate my work, the repository is organized as follows:
*   **`/evidence`**: Annotated screenshots and PCAPs of the investigation process.
*   **`/logs`**: A comparison of raw vs. sanitized (anonymized) log files.
*   **`/scripts`**: The Bash scripts I wrote for log anonymization and capture.
*   📄 **[Incident_Investigation_Technical_Report.pdf](./Incident_Investigation_Technical_Report.pdf)**: My full, detailed technical report (Final Project).

---

## ⚖️ Legal & Ethical Disclaimer
This project was performed in a **strictly controlled lab environment** for educational purposes. All tools and techniques were used against local, authorized virtual machines that I own and manage. I do not condone or support the use of these techniques against unauthorized systems.

## 🤝 Let's Connect
I am currently transitioning into a full-time **SOC Analyst / Blue Team** role and am open to remote opportunities worldwide. If you have questions about this lab or want to discuss cybersecurity, feel free to reach out!

- **LinkedIn:** [linkedin.com/in/pedro-goncalves-infosecurity](https://linkedin.com/in/pedro-goncalves-infosecurity)
- **Portfolio/GitHub:** [github.com/pmpg99](https://github.com/pmpg99)
- **Email:** pmpg99@gmail.com

---
*Finished in October 2025 as part of the Cybersecurity Specialist Course.*
