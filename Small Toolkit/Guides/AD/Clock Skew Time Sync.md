Syncs our machine with the Domain server’s time as if we have more than a 5 min gap we will have issues./

```
faketime "$(ntpdate -q <DC_IP> | cut -d ' ' -f 1,2)" COMMAND-GOES-HERE 
```

```
sudo timedatectl set-ntp false
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `sudo ntpdate -s ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
---

```
sudo systemctl restart systemd-timesyncd
```