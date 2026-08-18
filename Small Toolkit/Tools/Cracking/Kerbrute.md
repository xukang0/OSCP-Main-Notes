https://github.com/ropnop/kerbrute

```
wget -L https://github.com/ropnop/kerbrute/releases/download/v1.0.3/kerbrute_linux_amd64 -O kerbrute_linux_amd64
```

```
chmod +x ./kerbrute_linux_amd64
```
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `./kerbrute_linux_amd64 userenum --dc ${ip} --domain inlanefreight.local names.txt`;

dv.paragraph("```bash\n" + command + "\n```");
```
