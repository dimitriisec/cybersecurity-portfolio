# 📄 **traffic_analysis.md**

```markdown
# Network Traffic Analysis — TCP SYN Flood Attack

This document analyzes the captured network traffic from the company’s web server during the incident.
The goal is to determine what type of attack occurred, how it affected the server, and which indicators confirm malicious activity.

---

## 1. Overview of Packet Capture

The packet capture contains a mix of:

- Normal TCP three‑way handshakes  
- Legitimate HTTP GET requests  
- A very large number of repeated TCP SYN packets from a single suspicious IP address  

The server’s IP address is: **192.0.2.1**

The suspicious IP address is: **203.0.113.0**

---

## 2. Normal Traffic (Baseline)

Before the attack begins, the log shows normal behavior:

### Example:
```
198.51.100.23 → 192.0.2.1  TCP SYN
192.0.2.1 → 198.51.100.23  TCP SYN/ACK
198.51.100.23 → 192.0.2.1  TCP ACK
HTTP GET /sales.html
HTTP/1.1 200 OK
```

This is a standard TCP three‑way handshake followed by a normal HTTP request and response.

This confirms the server was functioning normally before the attack.

---

## 3. Malicious Traffic Pattern

Shortly after the normal traffic, a **massive flood of SYN packets** begins.

### Key Indicators:

- **Source:** 203.0.113.0  
- **Destination:** 192.0.2.1 (web server)  
- **Protocol:** TCP  
- **Flags:** SYN  
- **Port:** 443 (HTTPS)  
- **Volume:** Hundreds of SYN packets per second  
- **No ACK responses from attacker**  

### Example entries:

```
203.0.113.0 → 192.0.2.1  TCP 54770→443 [SYN]
203.0.113.0 → 192.0.2.1  TCP 54770→443 [SYN]
203.0.113.0 → 192.0.2.1  TCP 54770→443 [SYN]
...
(repeated hundreds of times)
```

This pattern continues for **over 50 seconds**, with no attempt to complete the handshake.

---

## 4. Server Behavior During Attack

The server attempts to respond:

```
192.0.2.1 → 203.0.113.0  TCP [SYN, ACK]
```

But the attacker **never replies with ACK**, leaving the connection half‑open.

Eventually, the server begins sending:

```
192.0.2.1 → 203.0.113.0  TCP [RST, ACK]
```

This indicates:

- The server’s connection queue is full  
- It is dropping connections  
- It is unable to handle new requests  

We also see legitimate clients receiving:

```
HTTP/1.1 504 Gateway Time-out
```

This confirms the attack is impacting real users.

---

## 5. Attack Type Identified

### **TCP SYN Flood Attack**

A SYN flood works by:

1. Sending a massive number of SYN packets  
2. Forcing the server to allocate resources for each half‑open connection  
3. Never completing the handshake  
4. Exhausting the server’s connection table  
5. Preventing legitimate users from connecting  

All indicators in the log match this attack pattern.

---

## 6. Evidence Supporting SYN Flood Conclusion

| Indicator | Evidence from Log |
|----------|-------------------|
| Extremely high SYN volume | Hundreds of SYN packets from 203.0.113.0 |
| No ACK responses | Attacker never completes handshake |
| Server degradation | 504 Gateway Timeout to legitimate clients |
| Server resets | Server sends RST/ACK due to resource exhaustion |
| Single repeated source | 203.0.113.0 sends SYN packets continuously |

This is a textbook SYN flood.

---

## 7. Impact on Web Server

- Server becomes overwhelmed by half‑open TCP connections  
- Connection table fills up  
- Legitimate users cannot access the website  
- Employees cannot search for vacation packages  
- Business operations are disrupted  
- Monitoring system triggers alerts  
- Server eventually becomes unresponsive  

---

## 8. Recommended Mitigations

### **Immediate**
- Block attacking IP (already done)  
- Restart or temporarily take server offline to clear half‑open connections  
- Enable SYN cookies  
- Reduce SYN‑RECEIVED timeout  

### **Long‑Term**
- Deploy DDoS protection (Cloudflare, Akamai, AWS Shield)  
- Implement rate limiting on SYN packets  
- Use a Web Application Firewall (WAF)  
- Add IDS/IPS to detect abnormal SYN patterns  
- Enable anomaly‑based traffic monitoring  
- Consider load balancing or reverse proxying  

---

## 9. Conclusion

The packet capture clearly shows that the company’s web server was targeted by a **TCP SYN flood attack** originating from **203.0.113.0**.
The attack overwhelmed the server, caused service outages, and prevented employees and customers from accessing the website.

Immediate mitigation restored service, but long‑term protections are required to prevent future attacks.

```

Готов продолжать.
