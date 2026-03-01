#### Show Available NFS Shares

  NFS
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `showmount -e ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
```
Export list for 10.129.14.128:
/mnt/nfs 10.129.14.0/24
```



```
mkdir target-NFS
```
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `sudo mount -t nfs ${ip}:/ ./target-NFS/ -o nolock`;

dv.paragraph("```bash\n" + command + "\n```");
```

```
sudo ls -lah target-NFS
```

```
cd target-NFS
```

```
tree .
```

```
.
└── mnt
    └── nfs
        ├── id_rsa
        ├── id_rsa.pub
        └── nfs.share

2 directories, 3 files
```


#### Unmounting

  NFS

```shell-session
Retric@htb[/htb]$ cd ..
Retric@htb[/htb]$ sudo umount ./target-NFS
```

There we will have the opportunity to access the rights and the usernames and groups to whom the shown and viewable files belong. Because once we have the usernames, group names, UIDs, and GUIDs, we can create them on our system and adapt them to the NFS share to view and modify the files.

#### List Contents with Usernames & Group Names

  NFS

```shell-session
Retric@htb[/htb]$ ls -l mnt/nfs/

total 16
-rw-r--r-- 1 cry0l1t3 cry0l1t3 1872 Sep 25 00:55 cry0l1t3.priv
-rw-r--r-- 1 cry0l1t3 cry0l1t3  348 Sep 25 00:55 cry0l1t3.pub
-rw-r--r-- 1 root     root     1872 Sep 19 17:27 id_rsa
-rw-r--r-- 1 root     root      348 Sep 19 17:28 id_rsa.pub
-rw-r--r-- 1 root     root        0 Sep 19 17:22 nfs.share
```