# Blue Team - Detection Strategy for Kerberoasting

**Log Source:** Windows Security Event Logs  
**Event ID:** 4769 (Kerberos Service Ticket Request)  
**Technique:** T1558.003 - Kerberoasting  
**Tactic:** Credential Access

---

## Detection Focus:

- Monitor Event ID **4769** where the **TicketEncryptionType = 0x17** (RC4-HMAC).
- Flag users or systems generating **high volumes** of TGS-REQs.
- Pay attention to unusual service principal names (SPNs).

---

## Detection Logic (Splunk Overview):

- Filter for 4769 events.
- Focus on RC4-encrypted tickets (0x17), as it is easier to crack but also look for AES encryption.
- Aggregate by source IP, user, and service name.
- Alert if count exceeds normal baseline (e.g., >5 in a short window).

---

## Investigation Tips:

- Look for accounts that typically do not perform SPN requests.
- Investigate source machines generating the requests.
- Correlate with successful logons (Event ID 4624) and account types.

---

## Response Recommendations:

- Disable unused SPNs or rotate service account passwords.
- Enable AES encryption for Kerberos (discourage RC4).
- Implement tiered account management (admin vs. service accounts).
- Consider monitoring tools like ATA, Defender for Identity, or Splunk ESCU.

---

## References:

- https://attack.mitre.org/techniques/T1558/003/
- https://docs.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4769
