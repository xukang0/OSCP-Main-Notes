```
python3 -m http.server
```

Other computer

```
ip a
```

Find your kali IP

[[IP]]

Visit this website to download uploaded files
```dataviewjs
const page = dv.page("Templater/IP");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `http://${KaliIP}:8000`;

dv.paragraph("```bash\n" + command + "\n```");
```

or


```dataviewjs
const page = dv.page("Templater/IP");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `wget http://${KaliIP}:8000/[filename]`;

dv.paragraph("```bash\n" + command + "\n```");
```


