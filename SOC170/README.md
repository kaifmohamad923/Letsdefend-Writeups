# SOC170 - Passwd Found in Requested URL - Possible LFI Attack

## Alert Information

| Field | Value |
|---|---|
| Alert ID | 120 |
| Alert Name | SOC170 - Passwd Found in Requested URL - Possible LFI Attack |
| Severity | High |
| Category | Web Attack |
| Detection Time | Mar 01, 2022 - 10:10 AM |

---

## Scenario Overview

This alert was triggered because the requested URL contained references to `/etc/passwd`, which is a strong indicator of a Local File Inclusion (LFI) attack attempt.  
The investigation focused on validating the malicious request, analyzing the attacker IP address, and determining whether the activity was successful or part of a planned test.

---

## Tools Used

- LetsDefend SIEM
- Log Management
- VirusTotal
- Web Traffic Analysis

---

## Alert Detection

The investigation started after a high-severity alert appeared in the LetsDefend monitoring dashboard.  
The alert rule identified suspicious access attempts involving sensitive Linux system files.

![image1](Image/image1.png)

---

## Reviewing Alert Details

The alert details revealed the source IP address, destination server, HTTP method, and suspicious URL request.  
The request attempted to access `/etc/passwd` using directory traversal sequences (`../../../../`), which is commonly associated with LFI attacks.

![image2](Image/image2.png)

---

## Creating The Incident Case

A new investigation case was created to begin the incident response and document all findings related to the alert.

![image3](Image/image3.png)

---

## Incident Information

The incident details confirmed that the event was categorized as a Web Attack linked to Event ID 120.  
This helped organize the investigation workflow and playbook process.

![image4](Image/image4.png)

---

## Investigating Network Traffic

The source IP `106.55.45.162` was identified communicating with the internal web server `172.16.17.13` over HTTPS port 443.  
The traffic timestamp matched the alert generation time.

![image5](Image/image5.png)

---

## Analyzing Raw Logs

The raw logs confirmed an attempt to access the `/etc/passwd` file through the URL parameter.  
The HTTP response status returned `500`, indicating the request failed and the attack was unsuccessful.

![image6](Image/image6.png)

---

## Confirming Malicious Activity

Based on the payload structure and directory traversal technique used in the request, the traffic was classified as malicious.

![image7](Image/image7.png)

---

## Identifying The Attack Type

The attack vector was identified as **LFI/RFI** because the attacker attempted to access local files through manipulated URL parameters.

![image8](Image/image8.png)

---

## Checking For Planned Activity

The investigation included verifying whether the traffic originated from an authorized penetration test or internal simulation activity.  
No evidence of planned testing was found, so the activity was marked as malicious and not planned.

![image9](Image/image9.png)

---

## IP Reputation Analysis

The source IP address was checked using VirusTotal for threat intelligence analysis.  
Although the IP was not flagged by security vendors, the behavior observed in the logs clearly matched LFI attack patterns.

![image10](Image/image10.png)

---

## Determining Traffic Direction

The malicious traffic originated from an external source targeting the internal company server.  
The traffic direction was identified as **Internet → Company Network**.

![image11](Image/image11.png)

---

## Verifying Attack Success

The attack was determined to be unsuccessful because the server returned an HTTP 500 response and no sensitive file contents were exposed.

![image12](Image/image12.png)

---

## Adding Investigation Artifacts

Important artifacts such as the attacker IP address, malicious URL, and victim IP address were added to the incident case for documentation purposes.

![image13](Image/image13.png)

---

## Writing Analyst Notes

An analyst note was added summarizing the investigation findings, including the malicious request, affected target, and failed LFI attempt.

![image14](Image/image14.png)

---

## Completing The Playbook

After completing all investigation steps and documenting the findings, the incident playbook was finalized.

![image15](Image/image15.png)

---

## Playbook Completion Status

The platform confirmed that the investigation playbook was completed successfully and the case was ready for alert closure.

![image16](Image/image16.png)

---

## Closing The Alert

The alert was closed as a **True Positive** because the investigation confirmed a real malicious LFI attack attempt targeting the web server.

![image17](Image/image17.png)

---

## Final Investigation Results

The final investigation summary confirmed that the incident was an unsuccessful Local File Inclusion (LFI) attack attempt against the target system.  
All findings were documented properly within the LetsDefend incident response workflow.

![image18](Image/image18.png)

---

## Conclusion

This investigation confirmed an attempted Local File Inclusion (LFI) attack targeting the web server `172.16.17.13`.  
The attacker attempted to access the sensitive Linux `/etc/passwd` file using directory traversal techniques through the URL request.  
The server responded with an HTTP 500 error, indicating the attack failed and no sensitive data was exposed.  
The incident was classified as a True Positive and documented successfully during the SOC investigation process.

---

## MITRE ATT&CK Mapping

| Technique ID | Description |
|---|---|
| T1006 | Path Traversal |
| T1190 | Exploit Public-Facing Application |

---

## Educational Purpose Disclaimer

This project was created for educational and defensive cybersecurity purposes only.  
All investigations and analysis were performed inside legal training environments provided by LetsDefend.