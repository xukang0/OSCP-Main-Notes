[[SSH id_rsa]]
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `GIT_SSH_COMMAND='ssh -i git_id_rsa.clean -p 43022' git clone git@${ip}:/git-server`;

dv.paragraph("```bash\n" + command + "\n```");
```
---

## push the file back to the remote server.

```powershell
┌──(kali㉿kali)-[~/Desktop/git-server]  
└─$ git add .

┌──(kali㉿kali)-[~/Desktop/git-server]  
└─$ git commit -m "oof
```

```
GIT_SSH_COMMAND='ssh -i ../id_rsa -p 43022' git push origin master
```

---

git merge -m 

git checkout b92bdd8

git reflog

git log

git branch

git add .
git commit -m "Work in progress"
git merge <branch-name>

