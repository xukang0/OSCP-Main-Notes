When you see `SeDebugPrivilege` **enabled**, think:

1. **Target:** LSASS (`lsass.exe`).
2. **Tool:** [[Synced OSCP Notes/Small Toolkit/Guides/AD/Mimikatz|Mimikatz]].
3. **Attempt:**

    ```
    privilege::debug
    sekurlsa::logonpasswords
    ```
    
4. **If blocked:** Check whether LSASS PPL, Credential Guard, or endpoint protection is preventing access.

One caveat: `SeDebugPrivilege` is an opportunity to access privileged processes, not a guarantee that LSASS credentials can be extracted.

## **When would Mimikatz fail?**

|Reason|What happens|
|---|---|
|Defender / EDR|Mimikatz is detected or blocked|
|LSASS PPL|Direct LSASS access is restricted|
|Credential Guard|Certain credentials are isolated and unavailable in LSASS|
|Insufficient access|You cannot obtain the required process handle|
|No useful credentials in memory|Mimikatz runs, but finds nothing useful|

**2. ProcDump — know the workflow**

```
procdump.exe -accepteula -ma lsass.exe lsass.dmp
```

Creates a dump of LSASS. You can subsequently analyse that dump with Mimikatz:

```
sekurlsa::minidump lsass.dmp
sekurlsa::logonpasswords
```

**3. comsvcs.dll — know it exists**

Uses Windows' built-in MiniDump functionality to create a process dump. It is another way to obtain an LSASS dump, not a way around PPL or Credential Guard.

**4. Rubeus — separate category**

Kerberos ticket manipulation and extraction. Not an alternative LSASS dumper.