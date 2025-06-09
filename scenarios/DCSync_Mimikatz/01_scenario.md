# Scenario: DCSync Attack with Mimikatz

**Objective:** Simulate a domain replication attack using Mimikatz to exfiltrate password hashes from Active Directory.

---

## Background

In an Active Directory (AD) environment, domain controllers replicate data (including password hashes) using the Directory Replication Service Remote Protocol (MS-DRSR). This allows domain controllers to stay synchronized and up to date.

Attackers can abuse this process using the `DCSync` feature in tools like **Mimikatz**, which allows them to impersonate a domain controller and request replication data, including sensitive credential material.

---

## Post-Exploitation Context

DCSync is a **post-exploitation attack**. It requires that the attacker has already obtained **valid credentials** for a privileged account — typically a **Domain Admin**, **Enterprise Admin**, or an account with **replication rights**.

With access to this level of privilege, the attacker can extract password hashes for high-value accounts, such as:

- `krbtgt` (used to sign Kerberos tickets)
- `Administrator`
- Any domain user

---

## Impact

One of the most dangerous follow-on actions from a successful DCSync attack is the ability to craft **Golden Tickets** using the stolen `krbtgt` hash.

Golden Tickets enable:
- **Full domain compromise**
- **Impersonation of any user**
- **Unlimited persistence** (until the `krbtgt` password is changed twice)

---

## MITRE ATT&CK Technique

- **Technique ID:** T1003.006  
- **Technique:** OS Credential Dumping: DCSync  
- **Tactic:** Credential Access
