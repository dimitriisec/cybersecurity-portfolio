# Scenario

This project analyzes a fictional distributed denial of service (DDoS) attack targeting a multimedia company that provides web design, graphic design, and social media marketing services. The attack disrupted internal network operations for two hours by overwhelming the network with a flood of ICMP packets.

During the incident, internal network services stopped responding, preventing normal traffic from accessing critical resources. The incident response team mitigated the attack by blocking incoming ICMP packets, shutting down non‑critical services, and restoring essential operations.

A post‑incident investigation revealed that the attacker exploited an unconfigured firewall, allowing ICMP traffic to enter the network unchecked. This vulnerability enabled the malicious actor to launch a successful DDoS attack.

To prevent future incidents, the network security team implemented:

- Firewall rate‑limiting for incoming ICMP packets  
- Source IP verification to detect spoofed addresses  
- Network monitoring tools to identify abnormal traffic patterns  
- IDS/IPS filtering for suspicious ICMP traffic  

As a cybersecurity analyst, your task is to evaluate this incident using the NIST Cybersecurity Framework (CSF) and develop a comprehensive plan to improve the company’s network security posture. The analysis follows the five NIST CSF functions:

- **Identify** — Assess risks, assets, and vulnerabilities  
- **Protect** — Implement safeguards to reduce attack surface  
- **Detect** — Improve monitoring and detection capabilities  
- **Respond** — Contain and mitigate security incidents  
- **Recover** — Restore affected systems and strengthen resilience  
