# SOC165 - Possible SQL Injection Payload Detected

## Room Link
https://app.letsdefend.io/

## Description
In this alert, a possible SQL Injection payload was detected targeting the web server.  
The investigation focused on analyzing the suspicious URL, decoding the payload, checking the source IP reputation, and validating whether the traffic was malicious or part of a planned test.

---

# Tools Used

- LetsDefend SIEM
- URL Decoder
- VirusTotal

---

# Investigation Steps

## Step 1: Open the Alert

The alert `SOC165 - Possible SQL Injection Payload Detected` was triggered with High severity.  
I started the investigation by opening the alert details and reviewing the basic event information.

![image](images/image1.png)

---

## Step 2: Review Event Details

I checked the hostname, source IP address, destination IP address, request method, and requested URL.  
The alert reason mentioned that the requested URL contained `OR 1=1`, which is commonly used in SQL Injection attacks.

![image](images/image2.png)

---

## Step 3: Create a Case

After reviewing the alert details, I created a case to begin the investigation process officially.  
This helps track the alert investigation workflow inside LetsDefend.

![image](images/image3.png)

---

## Step 4: Copy the Suspicious URL

I copied the encoded URL from the alert details for further analysis.  
The payload looked URL-encoded and required decoding to understand the actual request.

![image](images/image4.png)

---

## Step 5: Decode the URL

Using an online URL decoder, I decoded the suspicious request.  
The decoded payload revealed the SQL Injection attempt:

```text
" OR 1 = 1 --
```

This payload is commonly used to bypass authentication or manipulate database queries.

![image](images/image5.png)

---

## Step 6: Investigate Source IP Reputation

I searched the source IP address `167.99.169.17` on VirusTotal.  
Multiple security vendors flagged the IP address as malicious and related to phishing/suspicious activity.

![image](images/image6.png)

---

## Step 7: Determine If Traffic Is Malicious

Based on the SQL Injection payload and malicious IP reputation, I concluded that the traffic was malicious.  
I selected the `Malicious` option in LetsDefend.

![image](images/image7.png)

---

## Step 8: Review Firewall Logs

I checked related firewall logs to identify additional traffic from the same source IP.  
Multiple requests were observed targeting the destination server over port 443.

![image](images/image8.png)

---

## Step 9: Analyze Raw Logs

I opened the raw log details to review the HTTP request information.  
The request used the GET method and received an HTTP 200 response, meaning the server processed the request successfully.

![image](images/image9.png)

---

## Step 10: Check for Planned Activity

Finally, I verified whether the activity was part of a planned penetration test or attack simulation.  
No evidence suggested that the traffic was authorized, so I marked it as `Not Planned`.

![image](images/image10.png)

---

# Conclusion

The investigation confirmed a malicious SQL Injection attempt targeting the web server.  
The attacker used a URL-encoded SQL payload containing `OR 1=1`, and the source IP was flagged as malicious by multiple security vendors.  
After analyzing logs and verifying the activity was not planned, the alert was classified as a true positive attack.

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

This writeup is created for educational and documentation purposes only.  
All investigations were performed inside the LetsDefend training platform.