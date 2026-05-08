# SOC165 - Possible SQL Injection Payload Detected

## Description
This alert was triggered after the detection of a possible SQL Injection payload targeting a web server.  
The investigation involved analyzing the suspicious request, decoding the payload, checking IP reputation, and validating whether the activity was malicious or part of an authorized test.

---

# Tools Used

- LetsDefend SIEM
- VirusTotal
- URL Decoder

---

# Alert Overview

The investigation started with a high severity alert named:

`SOC165 - Possible SQL Injection Payload Detected`

After opening the alert, I reviewed the event details including the source IP, destination IP, request method, and requested URL.

![Alert Overview](image1.png)

---

# Reviewing the Event Details

The alert reason mentioned that the requested URL contained the pattern `OR 1=1`, which is a well-known SQL Injection payload often used to bypass authentication systems.

The event details also showed:
- Source IP Address: `167.99.169.17`
- Destination IP Address: `172.16.17.18`
- Request Method: `GET`

![Event Details](image2.png)

---

# Creating the Investigation Case

After validating the alert information, I created a case inside LetsDefend to begin the investigation workflow and document the analysis process.

![Create Case](image3.png)

---

# Extracting the Suspicious URL

The requested URL looked URL-encoded, so I copied the payload from the alert details for further analysis.

![Suspicious URL](image4.png)

---

# Decoding the Payload

I used an online URL decoder to decode the suspicious request.

The decoded payload revealed:

```text
" OR 1 = 1 --
```

This is a common SQL Injection technique used to manipulate backend database queries.

![Decoded Payload](image5.png)

---

# Investigating the Source IP

To verify the reputation of the source IP, I searched the address on VirusTotal.

The IP address was flagged by multiple security vendors as malicious or suspicious, increasing confidence that the activity was malicious.

![VirusTotal Analysis](image6.png)

---

# Confirming Malicious Activity

Based on the decoded SQL Injection payload and the malicious IP reputation, I classified the traffic as malicious inside LetsDefend.

![Malicious Traffic](image7.png)

---

# Reviewing Firewall Logs

I checked the related firewall logs to identify additional connections from the same IP address.

Multiple requests were observed targeting the same destination server over HTTPS (port 443).

![Firewall Logs](image8.png)

---

# Analyzing Raw Logs

The raw logs provided additional details about the HTTP request.

The request received an HTTP `200` response, which means the server processed the request successfully.

![Raw Logs](image9.png)

---

# Checking for Planned Activity

As a final verification step, I checked whether the traffic was part of a planned penetration test or attack simulation.

No evidence suggested that the activity was authorized, so the event was marked as `Not Planned`.

![Planned Test Check](image10.png)

---

# Conclusion

The investigation confirmed a malicious SQL Injection attempt against the target web server.

The attacker used a URL-encoded payload containing:

```text
" OR 1 = 1 --
```

The source IP address was also flagged as malicious by multiple vendors on VirusTotal.  
After reviewing the logs and verifying that the activity was not part of an authorized test, the alert was classified as a true positive attack.

---

# Artifacts

| Type | Value |
|------|------|
| Event ID | 115 |
| Source IP | 167.99.169.17 |
| Destination IP | 172.16.17.18 |
| Attack Type | SQL Injection |
| Request Method | GET |

---

# Disclaimer

This writeup is created for educational purposes only and all analysis was performed inside the LetsDefend training platform.