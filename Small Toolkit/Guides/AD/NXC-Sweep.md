NetExec Credential Usage Sweep NXC-SWEEP

Upon Entry, Once Creds for unknown usage is obtained, use [[NetExec]]to check across all services, nxc-sweep is used to automatically check all services

nxc-sweep-smb
```
cp ~/Desktop/Tools/Windows/nxc-sweep-smb . && ./nxc-sweep-smb ip.txt -u '[USER]' -p '[PASSWORD]'
```

nxc-sweep-service
```
cp ~/Desktop/Tools/Windows/nxc-sweep-service . && ./nxc-sweep-service ssh ip.txt -u '[USER]' -p '[PASSWORD]' --continue-on-success
```

Custom Details
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `~/Desktop/Tools/Windows/nxc-sweep ${ip} -u '[USER]' -p '[PASSWORD]' --continue-on-success`;

dv.paragraph("```bash\n" + command + "\n```");
```
user and password list
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `~/Desktop/Tools/Windows/nxc-sweep ${ip} -u users -p passwords --continue-on-success`;

dv.paragraph("```bash\n" + command + "\n```");
```
user and NT hash
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `~/Desktop/Tools/Windows/nxc-sweep ${ip} -u users -H [hash]`;

dv.paragraph("```bash\n" + command + "\n```");
```
Custom Details (Kerberos mode)
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `~/Desktop/Tools/Windows/nxc-sweep ${ip} -u '[USER]' -p '[PASSWORD]' -k`;

dv.paragraph("```bash\n" + command + "\n```");
```
-d [domain]

In NetExec (and its predecessor CrackMapExec), seeing (Pwn3d!) next to a set of credentials means that the provided username and password are valid and possess administrative or code execution privileges on that target

#### If untrusted domain / local account suspected
```
nxc mssql <IP> -u <USER> -p '<PASS>' -d <HOSTNAME>
```
#### Alternatively, explicitly try local authentication
```
nxc mssql <IP> -u <USER> -p '<PASS>' --local-auth
```
