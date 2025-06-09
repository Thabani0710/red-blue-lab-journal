# Scenario: DCSync Attack with Mimikatz

**Objective:** Simulate a domain replication attack using Mimikatz to exfiltrate password hashes from Active Directory.

---

## Background

In an Active Directory (AD) environment, domain controllers replicate data (including password hashes) using the Directory Replication Service Remote Protocol (MS-DRSR). This allows domain controllers to stay synchronized.

Attackers can exploit this by impersonating a domain controller and requesting replication data using the `DCSync` feature in tools like **Mimikatz**.

---

## Why This Matters

The DCSync attack lets an attacker:
- Dump password hashes for **krbtgt**, **Domain Admins**, or **any user**
- Bypass traditional LSASS memory scraping
- Maintain persistence by using the krbtgt hash (Golden Ticket attacks)

---

## MITRE ATT&CK Technique

- **Technique ID:** T1003.006
- **Technique:** OS Credential Dumping: DCSync
- **Tactic:** Credential Access
