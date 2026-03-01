# 🐍 pspy Cheat Sheet – Detecting Root Cron Jobs / Periodic Processes

---

## 1️⃣ What is pspy?

- Lightweight Go binary
- Monitors `ps` output in real-time
- Can see processes **without sudo**
- Perfect for spotting cron jobs, scripts, or processes run by root

---

## 2️⃣ Installation / Setup

No compilation needed — just download:

# 64-bit Linux  

```
wget https://github.com/DominicBreuker/pspy/releases/download/v1.2.1/pspy64  
```
# Make it executable  

```
chmod +x pspy64
```

Optional: move to `$PATH`:

```
sudo mv pspy64 /usr/local/bin/pspy
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