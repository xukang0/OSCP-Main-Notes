## **Remote PowerShell — PowerShell Remoting**

This is similar to WinRS, but instead of opening a remote CMD shell, you establish a PowerShell session on the target.

It uses WinRM underneath.

### **Requirements**

- WinRM enabled on the target.
- TCP 5985 or 5986 reachable.
- Valid credentials.
- Permission to access the configured PowerShell remoting endpoint.

### **Step 1 — Check WinRM**

From Windows
```
Test-WSMan MS02.laser.com
```

If it responds with WSMan information, the service is reachable.

From Kali:
```
nxc winrm <TARGET_IP> -u USER -p 'PASSWORD'
```

### **Step 2 — Establish a remote PowerShell session**

```
$cred = Get-Credential
Enter-PSSession -ComputerName MS02.laser.com -Credential $cred
```

Enter your domain credentials when prompted.

You should now see a prompt similar to:
```
[MS02]: PS C:\Users\Eric.Wallows\Documents>
```

You are executing PowerShell commands on MS02, not your local machine.

### **Step 3 — Execute individual remote commands**

You don't always need an interactive session.
```
Invoke-Command -ComputerName MS02.laser.com -Credential $cred -ScriptBlock {
    hostname
    whoami
    ipconfig
}
```

### **Step 4 — Exit**
```
Exit-PSSession
```