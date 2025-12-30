# SOC Lab – SSH Log Analysis with Splunk

## Overview

This project demonstrates how **Splunk Enterprise** can be used in a SOC context to analyze **SSH logs** and identify internal hosts generating a high number of SSH connections.

The goal is to simulate a realistic **Blue Team / SOC Analyst** investigation workflow using log analysis and SPL queries.

---

## Objective

Detect potentially abnormal or suspicious behavior such as:

- Excessive SSH connections from internal hosts
- Automated activity or brute-force attempts
- Misconfigured systems generating abnormal traffic

---

## Data Source

- SSH logs (JSON format)
- Splunk Enterprise (Search & Reporting app)

Sample fields used:

- `id.orig_h` – Source IP address
- Timestamp
- SSH connection events

---

## SPL Queries

### 1️⃣ Identify top internal hosts by SSH activity

```spl
source="ssh_logs.json" host="DESKTOP-INIT9SK" sourcetype="_json"
| stats count by id.orig_h
| sort -count
| head 10
```

**Purpose:**

- Identify internal IP addresses generating the highest number of SSH connections
- Quickly spot potential outliers for investigation

---

### 2️⃣ Total number of SSH connections

```spl
source="ssh_logs.json" host="DESKTOP-INIT9SK" sourcetype="_json"
| stats count as total_ssh_connections
```

**Purpose:**

- Measure overall SSH activity
- Provide high-level context before deeper analysis

---

## Results

Several internal hosts were identified as generating a high number of SSH connections.

This behavior may require further investigation, focusing on:

- **Running processes** responsible for the connections
- **Targeted accounts or services**
- **Traffic regularity** (periodic or automated patterns)

Such findings can indicate brute-force attempts, automated scripts, or configuration issues.

---

## SOC Investigation Mindset

This lab follows a SOC-style investigation approach:

1. Start with a high-level view of activity
2. Identify top talkers
3. Prioritize hosts for deeper investigation
4. Reduce noise and focus on anomalies

---

## Skills Demonstrated

- Splunk SPL
- Log analysis
- SSH security monitoring
- SOC / Blue Team investigation mindset
- Detection of abnormal behavior

---

## Screenshots

_(Screenshot available in repository)_

---

## Disclaimer

This project is for **educational and training purposes only**. Logs used are simulated and do not represent real production environments.
