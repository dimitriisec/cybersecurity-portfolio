# Incident Report — TCP SYN Flood Attack on Web Server

## 1. Overview

On the afternoon of the incident, the company’s monitoring system generated an automated alert indicating abnormal behavior on the public-facing web server. Employees reported that they were unable to access the company’s sales webpage, receiving connection timeout errors.

A packet capture revealed a large number of TCP SYN packets originating from an unfamiliar IP address. The volume of SYN requests overwhelmed the server’s ability to respond, causing service degradation and preventing legitimate users from accessing the website.

The evidence indicates that the server was targeted by a **TCP SYN flood attack**, a type of Denial-of-Service (DoS) attack.

---

## 2. Impact

- Employees were unable to access the sales webpage  
- Customers could not view promotions or vacation packages  
- Business operations were disrupted  
- The web server became unresponsive due to resource exhaustion  
- Potential loss of revenue during downtime  

---

## 3. Technical Analysis

### 3.1 Symptoms Observed
- Connection timeout errors in browser  
- Automated monitoring alert  
- Server unresponsive to legitimate traffic  
- Packet capture showed:
  - Extremely high volume of TCP SYN packets  
  - All originating from a single unfamiliar IP address  
  - No corresponding ACK responses  

### 3.2 Attack Type Identified
**TCP SYN Flood Attack**

This attack works by:

1. Sending a massive number of SYN packets  
2. Forcing the server to allocate resources for half-open TCP connections  
3. Exhausting the server’s connection table  
4. Preventing legitimate users from establishing connections  

### 3.3 Immediate Actions Taken
- Server temporarily taken offline to recover  
- Firewall configured to block the attacking IP address  
- Monitoring enabled to detect further anomalies  

---

## 4. Root Cause

The attacker exploited the TCP handshake process by sending a flood of SYN packets without completing the connection. The server attempted to respond to each SYN request, eventually running out of resources.

The root cause is the server’s inability to handle large volumes of half-open TCP connections.

---

## 5. Recommendations

### **Short-Term Mitigation**
- Enable SYN cookies  
- Reduce SYN-RECEIVED timeout values  
- Rate-limit SYN packets  
- Block attacking IPs (temporary measure only)

### **Long-Term Prevention**
- Deploy a Web Application Firewall (WAF)  
- Use a DDoS protection service (Cloudflare, Akamai, AWS Shield, etc.)  
- Implement network-level filtering and anomaly detection  
- Configure intrusion detection/prevention systems (IDS/IPS)  
- Monitor for spoofed IP traffic  
- Increase server capacity or use load balancing  

---

## 6. Conclusion

The company’s web server was targeted by a TCP SYN flood attack, causing service disruption and preventing employees and customers from accessing the sales webpage. Immediate mitigation steps restored service, but long-term protections are required to prevent future attacks.

A follow-up meeting with management is recommended to discuss permanent DDoS mitigation strategies.
