# 🧪 Scenario: Reverse TCP Shell on Windows VM

This scenario is inspired by and adapted from the *JustHacking – ConDef* course. It covers the complete attack lifecycle:

- 🛠️ Red Team: Execution of a Meterpreter reverse shell using Metasploit
- 🛡️ Blue Team: Detection logic using Splunk (SPL) and Microsoft Sentinel (KQL)

---

## 🔁 Attack–Detection Lifecycle

| Phase           | Details                                          |
|-----------------|--------------------------------------------------|
| Initial Access  | PowerShell-based delivery of `revshell.exe`      |
| Execution       | Payload runs in GUI user context (explorer.exe) |
| Detection       | Sysmon logs + correlation + Splunk + KQL         |
| Future Work     | Integration with Sentinel analytics              |

---

## 📦 Resources

- [🔴 Red Team](./02_red_team.md)
- [🔵 Blue Team](./03_blue_team.md)
- [📊 SPL Detection Query](./detections/detection_spl.spl)
- [📈 KQL Detection Query](./detections/detection_kql.kql)

---

## ⚠️ Legal & Ethical Notice

This scenario was performed in a **controlled lab environment** and is intended **strictly for educational purposes**.  
No real-world systems were harmed or accessed.  
All content is original or adapted with respect for the intellectual property of the *JustHacking – ConDef* training course.
