Upon Entry, Once Creds for unknown usage is obtained, use netexec to check across all services, nxc-sweep is used to automatically check all services

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `cd ~/Desktop/Tools/Windows && ./nxc-sweep ${ip} -u '[USER]' -p '[PASSWORD]'`;

dv.paragraph("```bash\n" + command + "\n```");
```




Transfer [[PowerView.ps1]] to target first

Verify commands are loaded
```powershell
Get-Command Get-DomainUser
```
 
 2. Query all active user accounts with an SPN set 

 ```powershell
Get-DomainUser -SPN | Select-Object samaccountname, serviceprincipalname
 ```
 
![[Pasted image 20260817222346.png]]

Kerberoasting is a technique that allows attackers to request a Kerberos ticket for a service associated with a Service Principal Name (SPN)

Transfer [[Rubeus.exe]] into VICTIM TARGET

Once Creds are obtained, use [[Runas]]









