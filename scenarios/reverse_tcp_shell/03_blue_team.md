
# Blue Team – Detection Engineering with Splunk

##  Objective

Detect the execution of a reverse TCP shell using Sysmon logs and Splunk queries.

---

##  Log Sources

- **Sysmon**
  - Event ID 1: Process Creation
  - Event ID 3: Network Connections

---

##  Observables

- Unusual outbound connection to TCP port 4444
- PowerShell initiated the outbound traffic
- Parent process was `explorer.exe` (suggesting user execution)
- File fetched from external HTTP server

---

##  Detection Query Evolution

### Broad Network Scan
```spl
index=sysmon EventCode=3
| stats count by Image, DestinationIp, DestinationPort
````

### Focused on Port 4444
```spl
index=sysmon EventCode=3 DestinationPort=4444
| stats count by Image, DestinationIp
````
