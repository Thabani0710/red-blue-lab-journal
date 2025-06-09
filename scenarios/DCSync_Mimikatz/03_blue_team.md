# Blue Team - Detection Strategy for DCSync Attack

**Log Source:** Windows Security Event Logs  
**Event IDs:**  
- 4662 (Object Operation Audit)  
- 4624 (Logon Success)  

---

## Key Detection Focus

### 1. Look for Event ID 4662 with DRS Replication GUID

```text
Object Type: DS-Replication-Get-Changes
Object Type: DS-Replication-Get-Changes-All
Object Type: DS-Replication-Get-Changes-In-Filtered-Set
````

```spl
index=winlogs EventCode=4662 
AND NOT (SubjectUserSid="NT AUTHORITY\\LOCAL SERVICE" AND SubjectDomainName = "Window Manager")
(
(ObjectType="%{19195a5b-6da0-11d0-afd3-00c04fd930c9}" OR ObjectType="domainDNS")
  AND
(Properties="*Replicating Directory Changes All*" 
 OR Properties="*{1131f6ad-9c07-11d1-f79f-00c04fc2dcd2}*" 
 OR Properties="*{9923a32a-3607-11d2-b9be-0000f87a36b2}*" 
 OR Properties="*{1131f6ac-9c07-11d1-f79f-00c04fc2dcd2}*")
)
| table SubjectDomainName, SubjectUserName, SubjectUserSid, ObjectType, Properties, Logon_ID

````

#### Notes
````text
DS-Replication-Get-Changes → {1131f6ac-9c07-11d1-f79f-00c04fc2dcd2}
DS-Replication-Get-Changes-All → {1131f6ad-9c07-11d1-f79f-00c04fc2dcd2}
DS-Replication-Get-Changes-In-Filtered-Set → {9923a32a-3607-11d2-b9be-0000f87a36b2}
