# Scenario: Kerberoasting with Impacket

## Description
This scenario simulates a Kerberoasting attack using the Impacket toolset to request service tickets (TGS) from a domain controller for offline password cracking. The goal is to replicate real-world adversarial behavior and develop effective detection strategies.

## Objective
To detect signs of Kerberoasting activity by identifying multiple service ticket requests (Event ID 4769) where specific encryption types are used (RC4-HMAC and AES256).

## MITRE ATT&CK Mapping
- **Tactic:** Credential Access (TA0006)
- **Technique:** Kerberoasting (T1558.003)
- **Tool:** Impacket (e.g., `GetUserSPNs.py`)
