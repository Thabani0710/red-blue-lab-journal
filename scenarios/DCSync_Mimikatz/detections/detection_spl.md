### Splunk
````spl
index=winlogs EventCode=4662 AND NOT (SubjectUserSid="NT AUTHORITY\LOCAL SERVICE" AND SubjectDomainName = "Window Manager")
(
(ObjectType="%{19195a5b-6da0-11d0-afd3-00c04fd930c9}" OR ObjectType="domainDNS")
  AND
(Properties="*Replicating Directory Changes All*" OR Properties="*{1131f6ad-9c07-11d1-f79f-00c04fc2dcd2}*" OR Properties = "*{9923a32a-3607-11d2-b9be-0000f87a36b2}*" OR Properties = "*{1131f6ac-9c07-11d1-f79f-00c04fc2dcd2}*")
)
| rename _time AS DSTime, SubjectUserSid AS DSUserSid, SubjectDomainName AS DSDomainName, SubjectUserName AS DSUserName, SubjectLogonId AS DSLogonId, ObjectType AS DSObjectType, ObjectName AS DSObjectName, Properties AS DSProperties status AS DSStatus
| join type=left Computer, DSLogonId
[ 
    search index=winlogs AND EventCode=4624 NOT (SubjectUserSid="S-1-5-19" OR SubjectDomainName="Window Manager")
    | rename _time as LogonTime, TargetLogonId AS DSLogonId
]
| convert timeformat="%d/%m/%Y %H:%M:%S" ctime(DSTime), ctime(LogonTime)
| eval IsSuspicious = if(IpAddress != "192.168.1.88", "Yes", "No")
| table DSTime, Computer, DSUserSid, DSDomainName, DSUserName, DSObjectType, DSObjectName, DSProperties, DSStatus, DSLogonId, LogonTime, AuthenticationPackageName, IpAddress, IpPort, IsSuspicious
````
#### Where 192.168.1.88 is a DC IP, Ideally filter for known DCs to minimize noise
