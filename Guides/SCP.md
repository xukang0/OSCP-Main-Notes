Nice and simple one 👍 — `scp` is basically **`cp` over SSH**.

I’ll give you the **90% use cases first**, then a couple of pro tips.

---

## 🔹 Basic syntax (remember this)

`scp [options] source destination`

---

## 📤 Copy **from your local machine → remote**

`scp file.txt user@10.10.10.10:/home/user/`

Example (HTB-style):

`scp linpeas.sh htb-student@10.10.10.10:/tmp/`

➡️ Copies `linpeas.sh` to `/tmp` on the target.

---

## 📥 Copy **from remote → your local machine**

`scp user@10.10.10.10:/etc/passwd .`

➡️ Downloads `/etc/passwd` into your current directory.

---

## 📁 Copy an **entire directory** (very common)

Use `-r` (recursive):

`scp -r tools/ user@10.10.10.10:/tmp/tools/`

Or download a directory:

`scp -r user@10.10.10.10:/var/www/html .`

---

## 🔑 Using an SSH key

`scp -i id_rsa file.txt user@10.10.10.10:/home/user/`

HTB often needs this 👆

---

## 🚪 Custom SSH port

`scp -P 2222 file.txt user@10.10.10.10:/tmp/`

⚠️ Capital **`-P`**, not `-p`.

---

## 🧪 Quiet but useful flags

`scp -r -C -v file.txt user@10.10.10.10:/tmp/`

- `-C` → compression (slow links)
    
- `-v` → verbose (debug auth issues)
    
- `-r` → directories
    

---

## 🧠 Pro tips (pentest mindset)

### 🔹 Preserve permissions/timestamps

`scp -p file.txt user@10.10.10.10:/tmp/`

### 🔹 Transfer from target A → target B (from your box)

`scp user1@hostA:/tmp/file user2@hostB:/tmp/`

### 🔹 When SCP is blocked

Use:

`rsync -avz -e ssh file user@host:/tmp/`

---

## 🚨 Common mistakes

❌ Forgetting `-r` for directories  
❌ Using `-p` instead of `-P` for port  
❌ No write permissions on destination

---

## TL;DR cheat sheet

`# Upload scp file user@ip:/path/  # Download scp user@ip:/path/file .  # Directory scp -r dir user@ip:/path/  # SSH key scp -i key file user@ip:/path/  # Custom port scp -P 2222 file user@ip:/path/`

If you want, tell me:

- Linux ↔ Linux?
    
- Windows ↔ Linux?
    
- HTB / OSCP exam constraints?
    

I’ll tailor it exactly to your scenario 🔥