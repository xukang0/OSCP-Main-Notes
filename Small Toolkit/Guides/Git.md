```
git status
```


---


```
git log
```

Example output
```powershell
root@websrv1:/srv/www/wordpress# git log
commit 612ff5783cc5dbd1e0e008523dba83374a84aaf1 (HEAD -> master)
Author: root <root@websrv1>
Date:   Tue Sep 27 14:26:15 2022 +0000

    Removed staging script and internal network access

commit f82147bb0877fa6b5d8e80cf33da7b8f757d11dd
Author: root <root@websrv1>
Date:   Tue Sep 27 14:24:28 2022 +0000

    initial commit
```

---

**git show**, which shows differences between commits. In our case, we'll supply the commit hash of the latest commit to the command as we are interested in the changes after the first commit.

Show first commit
```
git show 612ff5783cc5dbd1e0e008523dba83374a84aaf1
```

---


