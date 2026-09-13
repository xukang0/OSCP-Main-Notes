Mimikatz on windows, Pypykatz on KALI ATTACKER

| **Storage File** | **Scope**                   | **What it Contains**                                                                         |
| ---------------- | --------------------------- | -------------------------------------------------------------------------------------------- |
| **`SAM` Hive**   | **Local Machine**           | Local accounts only (e.g., local `Administrator`, `Guest`, local service accounts).          |
| **`ntds.dit`**   | **Active Directory Domain** | All Domain accounts (e.g., Domain `Administrator`, Domain Users, Kerberos service accounts). |

```shell-session
pypykatz lsa minidump lsass.DMP 
```

```
hashcat -m 1000 hash /usr/share/wordlists/rockyou.txt
```