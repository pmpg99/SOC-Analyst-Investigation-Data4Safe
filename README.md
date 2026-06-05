# SOC-Analyst-Investigation-Data4Safe

🕵️‍♂️ **A simulated SOC investigation into anomalous SSH traffic, credential brute-forcing, and vulnerability exploitation.**

## 📌 Project Overview
This project simulates a real-world incident response scenario for a fictional company, **Data4Safe**. As the lead investigator, I was tasked with analyzing reports of server latency and suspicious network traffic on an internal Linux server. 

The lab demonstrates an end-to-end Blue Team workflow: from initial detection and traffic analysis to vulnerability correlation and log anonymization for evidence sharing.

---

## 🛠️ Tech Stack & Skills
*   **Environment:** Kali Linux (Attacker VM) ↔ Metasploitable2 (Target VM)
*   **Packet Analysis:** Wireshark, tcpdump
*   **Discovery & OSINT:** Nmap, theHarvester
*   **Credential Testing:** Ncrack
*   **Forensics & Cleanup:** Bash scripting, `sed` (Log anonymization)
*   **Methodology:** Incident Response Lifecycle (Containment, Investigation, Documentation)

---

## 📂 Repository Structure
*   **`/evidence`**: Annotated screenshots proving suspicious activity (Packet captures, Tool outputs).
*   **`/logs`**: Cleaned and anonymized log files demonstrating the simulated attack patterns.
*   **`/scripts`**: Bash scripts used for controlled testing and evidence extraction.
*   **`Incident_Investigation_Technical_Report.pdf`**: Comprehensive technical report documenting the full investigation timeline and remediation steps.

---

## 🚀 Key Investigation Workflow
1.  **Initial Triage:** Captured and analyzed live network traffic (PCAPs) to correlate reports of "server latency" with a high-frequency SSH brute-force attack.
2.  **Service Discovery:** Conducted deep scans (Nmap) to identify exposed services and correlate them with known vulnerabilities (CVEs) in a controlled environment.
3.  **Credential Stress-Testing:** Demonstrated how weak credentials allow for successful intrusion using `Ncrack`, highlighting the need for MFA.
4.  **Forensic Anonymization:** Developed scripts using `sed` to sanitize sensitive system logs, ensuring "Chain of Custody" protocols while protecting PII before sharing evidence.

---

## 📈 Results & Outcomes
*   **Identified** a credential-spraying pattern from the simulated attacker IP.
*   **Mapped** findings to specific exploitable services on the legacy server.
*   **Produced** a remediation plan including SSH hardening (MFA, IP Whitelisting, and Rate Limiting).
*   **Validated** the integrity of forensic evidence through automated log cleaning.

---

## ⚖️ Legal & Ethical Disclaimer
This project was performed in a strictly controlled lab environment for educational purposes. All tools were used against local, authorized virtual machines. **Never use these techniques against systems you do not own.**

---
**Author:** Pedro Gonçalves  
**Target Roles:** SOC Analyst | Blue Team | Incident Responder