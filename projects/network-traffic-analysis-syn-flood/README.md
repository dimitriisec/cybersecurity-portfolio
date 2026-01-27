# Network Traffic Analysis — TCP SYN Flood Attack

This project analyzes a real-world network incident affecting a travel agency’s public-facing web server. 
Employees rely on the company’s sales webpage to search for vacation packages for customers. 
One afternoon, the monitoring system generated an alert indicating abnormal server behavior. 
Employees reported connection timeout errors when attempting to access the website.

A packet capture revealed a large number of TCP SYN packets originating from an unfamiliar IP address. 
The server became overwhelmed by these half-open connections, preventing it from responding to legitimate traffic. 
This behavior is consistent with a **TCP SYN flood attack**, a type of Denial-of-Service (DoS) attack.

The project includes a scenario description, a detailed incident report, and a full traffic analysis based on the captured packets.

---

## 📄 Included Documents

- **scenario.md** — description of the business scenario and initial symptoms  
- **incident_report.md** — full incident analysis, impact assessment, and remediation recommendations  
- **traffic_analysis.md** — detailed breakdown of the packet capture and identification of the SYN flood attack
- **Cybersecurity_incident_report.pdf**
- **Wireshark_TCP_HTTP log_-_TCP _log.pdf**

---

## 🎯 Objectives

- Analyze captured network traffic using packet-sniffing tools  
- Identify abnormal TCP behavior and DoS attack patterns  
- Document the incident using professional reporting standards  
- Explain the impact of a SYN flood attack on server availability  
- Recommend both short-term and long-term mitigation strategies  

---

## 🧩 Skills Demonstrated

- Network traffic analysis (TCP, HTTP, SYN/ACK patterns)  
- Identification of DoS attack indicators  
- Use of packet-sniffing tools (e.g., Wireshark, tcpdump)  
- Incident response documentation  
- Root cause analysis  
- Communication of technical findings to non-technical stakeholders  

---

## 🛡️ Summary of Findings

The packet capture revealed:

- A massive volume of TCP SYN packets from **203.0.113.0**  
- No corresponding ACK responses from the attacker  
- The server repeatedly sending SYN/ACK and eventually RST packets  
- Legitimate clients receiving **504 Gateway Timeout** errors  
- Server resource exhaustion due to half-open TCP connections  

These indicators confirm a **TCP SYN flood attack**, which overwhelmed the server and prevented employees and customers from accessing the sales webpage.

---

## 🚀 Recommended Mitigation

### **Immediate Actions**
- Block attacking IP address  
- Restart or temporarily take the server offline to clear half-open connections  
- Enable SYN cookies  
- Reduce SYN-RECEIVED timeout values  

### **Long-Term Solutions**
- Deploy DDoS protection services (Cloudflare, Akamai, AWS Shield)  
- Implement rate limiting for SYN packets  
- Use a Web Application Firewall (WAF)  
- Deploy IDS/IPS for anomaly detection  
- Improve network monitoring and alerting  
- Consider load balancing or reverse proxying  

---
