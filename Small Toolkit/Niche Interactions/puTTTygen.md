PuTTYgen, which is a key generator tool for creating pairs of public and private SSH keys. PuTTYgen supports various public-key cryptosystems, including the Rivest–Shamir– Adleman (RSA) algorithm. We can use it to generate the private SSH key for the root user. Here, we use the following options in PuttyGen -O to specify the output type, i.e. private-OpenSSH -o to specify the output file.


---

```
echo "[output]" > ssh_key_file
```

Remove extra spaces and formats
```
sed 's/^ *//' ssh_key_file > fixed_key.ppk
```

---

```
puttygen fixed_key.ppk -O private-openssh -o id_rsa 
```

```
cat id_rsa
```

---
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `ssh -i id_rsa root@${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
