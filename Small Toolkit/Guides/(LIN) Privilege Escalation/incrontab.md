View global incron tables
```
cat /etc/incron.d/*
```

View user-specific tables
```
incrontab -l
```

Check if user is permitted to use incrontab by verifying

```
/etc/incron.allow
```

or

```
/etc/incron.deny
```


This means when incron is written into, sysadmin_manager is triggered and $# is replaced by the filename of incron directory
```powershell
/usr/local/asterisk/incron IN_CLOSE_WRITE /usr/bin/sysadmin_manager --local $#
```