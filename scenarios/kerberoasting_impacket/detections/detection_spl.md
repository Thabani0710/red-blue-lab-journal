## This is the final detection query for my Lab environment

````spl
index=winlogs
| where EventCode = 4769 
      AND TicketEncryptionType IN ("0x17", "0x12")
| eval EncryptionMap = case(
      TicketEncryptionType="0x17", "RC4-HMAC",
      TicketEncryptionType="0x12", "AES256-CTS-HMAC-SHA1-96"
)
| eval src_ip=replace(src_ip, "^::ffff:", "")
| stats dc(ServiceName) as TicketRequestedCount,
        values(ServiceName) as ServicesRequested,
        values(EncryptionMap) as EncryptionTypes,
        values(src_ip) as SourceIPs
        by TargetUserName, _time
| where (EncryptionTypes == "RC4-HMAC" OR EncryptionTypes == "AES256-CTS-HMAC-SHA1-96")
      AND TicketRequestedCount > 5
````
