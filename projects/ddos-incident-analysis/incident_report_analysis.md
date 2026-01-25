# Incident Report Analysis

This document analyzes a DDoS security event using the NIST Cybersecurity Framework (CSF). It summarizes the incident, identifies root causes, and outlines protection, detection, response, and recovery strategies.

## Summary
The company experienced a security event in which all network services stopped responding due to a distributed denial‑of‑service (DDoS) attack. The cybersecurity team mitigated the issue by blocking incoming ICMP packets, shutting down non‑critical services, and restoring critical network operations.

## Identify
A malicious actor exploited an unconfigured firewall, sending a flood of ICMP ping packets into the network. This vulnerability allowed the attacker to overwhelm internal systems and cause a complete service outage.

## Protect
To prevent similar incidents, the network security team implemented:
- ICMP rate‑limiting firewall rules  
- IDS/IPS filtering for suspicious ICMP traffic  

## Detect
The cybersecurity team enhanced detection capabilities by:
- Deploying network monitoring software  
- Enabling source IP verification  

## Respond
Future response plans include:
- Quarantining compromised systems  
- Prioritizing restoration of essential services  
- Reviewing logs for suspicious activity  
- Documenting incidents and notifying leadership  

## Recover
Recovery steps include:
- Restoring network services  
- Blocking external ICMP flood attempts  
- Re-enabling non‑critical systems after stabilization  

## Reflections / Notes
*(Optional section for personal notes.)*
