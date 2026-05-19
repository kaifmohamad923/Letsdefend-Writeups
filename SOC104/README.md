# SOC104 - Malware Detected | LetsDefend Writeup

## Room Information

- **Platform:** :contentReference[oaicite:0]{index=0}
- **Alert Name:** SOC104 - Malware Detected
- **Event ID:** 36
- **Category:** Malware Investigation
- **Difficulty:** Medium

---

## Scenario

A malware alert was triggered after a suspicious executable file was downloaded on an endpoint inside the environment. During the investigation, multiple indicators including malicious network communication, ransomware-related hashes, and suspicious outbound traffic were identified.

---

# Tools Used

- SIEM Dashboard
- VirusTotal
- Endpoint Security
- Proxy Logs
- Threat Intelligence Sources

---

# Initial Alert Investigation

The investigation started from the monitoring dashboard where a high severity malware alert was triggered on the host `AdamPRD`.

<p align="center">
  <img src="Images/image1.png" width="900"/>
</p>

After opening the alert details, important artifacts such as hostname, source IP, file name, hash value, and device action were identified. The suspicious file was `Invoice.exe`.

<p align="center">
  <img src="Images/image2.png" width="900"/>
</p>

---

# Creating the Incident Case

A new incident case was created from the alert to begin the investigation and launch the malware response playbook.

<p align="center">
  <img src="Images/image3.png" width="500"/>
</p>

The case information confirmed that the alert was categorized as a malware incident.

<p align="center">
  <img src="Images/image4.png" width="900"/>
</p>

---

# Defining the Threat Indicator

During the playbook execution, the malware-related threat indicator was selected based on the suspicious executable behavior and network activity observed during the investigation.

<p align="center">
  <img src="Images/image5.png" width="700"/>
</p>

---

# Reviewing Network Activity

The next step involved reviewing proxy and network logs associated with the infected endpoint. Suspicious outbound traffic was identified from `10.15.15.18` communicating with the external IP `92.63.8.47` over port `443`.

<p align="center">
  <img src="Images/image6.png" width="900"/>
</p>

The raw event logs confirmed the exact malicious URL accessed by the endpoint.

<p align="center">
  <img src="Images/image7.png" width="500"/>
</p>

---

# VirusTotal Analysis

The suspicious IP address was analyzed on VirusTotal. Multiple security vendors flagged the IP as malicious and associated it with malware infrastructure activity.

<p align="center">
  <img src="Images/image8.png" width="900"/>
</p>

The downloaded executable hash was also checked on VirusTotal. The file was detected by many vendors and linked with ransomware behavior, specifically Maze ransomware indicators.

<p align="center">
  <img src="Images/image9.png" width="900"/>
</p>

---

# Malware Validation

Additional malware analysis confirmed that the executable was malicious. Based on the indicators and VirusTotal detections, the malware classification was validated successfully.

<p align="center">
  <img src="Images/image11.png" width="700"/>
</p>

---

# Checking C2 Communication

The investigation then focused on identifying Command and Control (C2) communication attempts. Log analysis confirmed that the infected endpoint had accessed the malicious C2 infrastructure.

<p align="center">
  <img src="Images/image12.png" width="700"/>
</p>

---

# Endpoint Containment

The infected machine was isolated through the EDR platform to prevent further communication with external malicious infrastructure.

<p align="center">
  <img src="Images/image13.png" width="700"/>
</p>

The endpoint containment status later confirmed that the host was successfully isolated.

<p align="center">
  <img src="Images/image14.png" width="900"/>
</p>

---

# Adding Investigation Artifacts

Important investigation artifacts including victim IP, C2 IP address, malicious URL, and malware hash were documented inside the incident case for future reference and tracking.

<p align="center">
  <img src="Images/image15.png" width="700"/>
</p>

---

# Analyst Notes

An analyst note was added to summarize the malware detection findings, affected host information, and timeline of the incident.

<p align="center">
  <img src="Images/image16.png" width="700"/>
</p>

---

# Completing the Playbook

After validating all indicators and containment actions, the malware response playbook was completed successfully.

<p align="center">
  <img src="Images/image17.png" width="600"/>
</p>

---

# Closing the Alert

The alert was marked as a True Positive because the investigation confirmed active malware behavior and malicious communication from the endpoint.

<p align="center">
  <img src="Images/image18.png" width="700"/>
</p>

The final alert summary displayed all completed investigation actions and playbook responses.

<p align="center">
  <img src="Images/image19.png" width="900"/>
</p>

---

# Conclusion

This investigation confirmed the presence of a malicious executable on the endpoint `AdamPRD`. The malware established communication with a malicious external IP and showed ransomware-related indicators associated with Maze ransomware. After validating the threat through VirusTotal and log analysis, the infected host was successfully contained to prevent further compromise.

---

# Artifacts Identified

| Type | Value |
|------|------|
| Victim IP | `10.15.15.18` |
| Hostname | `AdamPRD` |
| Malicious IP | `92.63.8.47` |
| Malicious URL | `hxxp://92.63.8.47/` |
| File Name | `Invoice.exe` |
| File Hash | `f83fb9ce6a83da58b20685c1d7e1e546` |

---

# MITRE ATT&CK Mapping

| Technique | Description |
|------|------|
| T1105 | Ingress Tool Transfer |
| T1071 | Application Layer Protocol |
| T1041 | Exfiltration Over C2 Channel |
| T1486 | Data Encrypted for Impact |

---

# Disclaimer

This writeup was created for educational and defensive cybersecurity learning purposes only.