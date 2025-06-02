
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
- Unusual .exe file initiated the outbound traffic
- Parent process was not `explorer.exe` (suggesting user non-standard execution)
- File fetched from external HTTP server

---

##  Detection Query Evolution

### Broad Network Scan
```spl
index=sysmon EventCode=3
| stats count by Image, DestinationIp, DestinationPort
````
#### Found a connection on port 8080 and looking further into the communication there is another connection on port 4444 

### Focused on Port 4444
```spl
index=sysmon EventCode=3 DestinationPort=4444
| stats count by Image, DestinationIp
````

### Process that created the connection

Looking for events that run the whoami command, we can see the same Image detected above executing commands suggesting a remote shell.

````spl
index=sysmon whoami
| dedup ParentProcessGuid
| table _time,ParentProcessGuid,CommandLine,ParentImage
````

Next step is to match this to the ParentCommandLine

```spl
index=sysmon 
| where EventCode = 1
| where ProcessGuid IN ("{72b2a473-06e5-683e-fe00-000000004b01}","{72b2a473-00e0-683e-d601-000000004a01}")
| table _time,ProcessGuid,CommandLine,ParentCommandLine
````
