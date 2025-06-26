# Adversary Emulation & Detection Engineering Lab Series

This repository began as a collection of red and blue team lab scenarios inspired by and adapted from the *JustHacking – ConDef* course.  
It has since evolved into a broader, hands-on portfolio focused on **adversary emulation**, **detection engineering**, and the **full attack-detection-response lifecycle**.

Detection logic is implemented using tools like **Splunk (SPL)** and **Microsoft Sentinel (KQL)**, with scenarios designed to reflect real-world TTPs.


## Scenarios

| Scenario                          | Red Team                          | Blue Team Detection |
|----------------------------------|-----------------------------------|---------------------|
| [Reverse TCP Shell](./scenarios/reverse_tcp_shell) | Payload via Metasploit + PowerShell | Sysmon + SPL/KQL     |
| [Kerberoasting Impacket](./scenarios/kerberoasting_impacket) | Keberoasting via Impacket | Sysmon + SPL/KQL     |
| [DCSync_Impacket](./scenarios/DCSync_Mimikatz) | Keberoasting via Impacket | Sysmon + SPL/KQL     |

---

## Disclaimer

All actions were performed in a **controlled lab environment**. This repository is for **educational purposes only**.  
No proprietary content is shared from the ConDef course.
