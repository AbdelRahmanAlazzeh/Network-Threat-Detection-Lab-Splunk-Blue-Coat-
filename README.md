# Network-Threat-Detection-Lab-Splunk-Blue-Coat-

# Network Threat Detection Lab (Splunk & Blue Coat)

## 📌 Project Overview
A practical simulation of a **Security Operations Center (SOC)** workflow. This project involves deploying **Splunk Enterprise** to ingest, parse, and analyze **Blue Coat Proxy logs**, focusing on detecting network anomalies, policy violations, and performing forensic timeline reconstruction.

## 🛠 Environment & Tools
* **SIEM:** Splunk Enterprise (Local Instance).
* **Data Source:** Blue Coat Proxy Logs (CSV).
* **Key Techniques:** Log Normalization, SPL Scripting, Threat Hunting, Timeline Analysis.

## 🔍 Key Analysis Modules

### 1. Data Ingestion & Parsing
* Configured **Splunk Indexing** for raw CSV data.
* Mapped critical fields: `c_ip`, `cs_username`, `cs_host`, `action`, `category`.
* **Outcome:** Structured data ready for high-speed querying.

### 2. Operational Intelligence (Bandwidth)
* Analyzed `sc_bytes` to identify "Top Talkers".
* Detected potential data exfiltration or misuse of corporate resources.
* **Key Insight:** User `Fahad3315` identified as top consumer (~3GB traffic).

### 3. Threat Detection (Policy Violations)
* Filtered traffic for `action!="allowed"` to spot blocked attempts.
* Correlated `category` fields to identify access to "Hacking" and "Malware" sites.

---

## 🕵️‍♂️ Case Study: The "Zone-H" Incident

**Scenario:** A user attempted to access a known hacking archive website.

**Incident Timeline:**
1.  **Detection:** Splunk triggered an alert for `category="Hacking"` on host `www.zone-h.org`.
2.  **Investigation:**
    * User: `Fahad3315`.
    * Action: `TCP_DENIED` (Blocked by Proxy).
    * Context: User activity showed a pattern of `YouTube` (Learning) → `HaveIBeenPwned` (Recon) → `VirusTotal`.
3.  **Root Cause Analysis:**
    * Analyzed `cs_Referer` field.
    * **Finding:** User did not type the URL directly; access originated from a **Google Search** result.
4.  **Conclusion:** Activity classified as educational/curiosity (Script Kiddie behavior) rather than a sophisticated attack.

**Attack Timeline Visualization:**
> *![Timeline Chart](Screenshot_2026-01-20_040926.png)*
> *(Stacked chart correlating User, Host, and Action)*

---

## 📊 Dashboards & Visualizations
Developed custom Splunk dashboards to provide real-time visibility into:
* **Traffic Volume:** Hourly bandwidth usage.
* **Blocked Requests:** Top blocked domains and categories.
* **User Activity:** Detailed timeline of specific user sessions.

> *![Dashboard Overview](screenshots/image_59e3c3.jpg)*

---

## 📂 Repository Structure
* `queries.txt`: Contains all SPL queries used for detection and analysis.
* `screenshots/`: Visual evidence of dashboards and timeline analysis.
* `README.md`: Project documentation.

## 🚀 Skills Demonstrated
* **SIEM Administration:** Data onboarding and index management.
* **Splunk SPL:** Advanced usage of `stats`, `timechart`, `eval`, `delta`, and `transaction`.
* **Forensics:** Reconstructing incident timelines and analyzing HTTP headers (Referrer).
* **Reporting:** Translating technical logs into actionable security intelligence.
