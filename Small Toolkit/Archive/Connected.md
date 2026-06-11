[[Active Notes Template]]
## Provided Credentials
---

```

```

```

```

---
## Open Ports

| Port | Service | Notes |
| ---- | ------- | ----- |
|      |         |       |

```powershell
22/tcp  open  ssh       OpenSSH 7.4 (protocol 2.0)
| ssh-hostkey: 
|   2048 4e:60:38:6f:e7:78:6c:ca:58:62:a1:f1:56:ae:8d:30 (RSA)
|   256 12:41:55:26:9d:ad:3d:e8:bf:4e:31:aa:d7:d1:a5:d2 (ECDSA)
|_  256 8e:b6:96:e0:21:83:5d:1d:ce:8d:e2:6a:dd:38:c6:75 (ED25519)

80/tcp  open  http      Apache httpd 2.4.6 ((CentOS) OpenSSL/1.0.2k-fips PHP/7.4.16)
|_http-title: Did not follow redirect to http://connected.htb/
|_http-server-header: Apache/2.4.6 (CentOS) OpenSSL/1.0.2k-fips PHP/7.4.16

443/tcp open  ssl/https Apache/2.4.6 (CentOS) OpenSSL/1.0.2k-fips PHP/7.4.16
|_http-server-header: Apache/2.4.6 (CentOS) OpenSSL/1.0.2k-fips PHP/7.4.16
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=pbxconnect/organizationName=SomeOrganization/stateOrProvinceName=SomeState/countryName=--
| Not valid before: 2025-11-30T14:07:27
|_Not valid after:  2026-11-30T14:07:27
|_http-title: 400 Bad Request

```


---
## Software Versions

```powershell
redis_version:3.2.12
```


---
## Discovered Subdomains




---
## Discovered Credentials


| Username | Password | Notes |
| -------- | -------- | ----- |
|          |          |       |

---
## Attack Angles

```powershell
[asterisk@connected incron.d]$ cat legacy

/var/spool/asterisk/sysadmin/vpnget IN_CLOSE_WRITE /usr/sbin/sysadmin_openvpn -d
/var/spool/asterisk/sysadmin/intrusion_detection_stop IN_CLOSE_WRITE /etc/init.d/fail2ban stop
/var/spool/asterisk/sysadmin/update_system_cron IN_CLOSE_WRITE /usr/sbin/sysadmin_update_set_cron
/var/spool/asterisk/sysadmin/portmgmt_setup IN_CLOSE_WRITE /usr/sbin/sysadmin_portmgmt
/var/spool/asterisk/sysadmin/wanrouter_restart IN_CLOSE_WRITE /usr/sbin/sysadmin_wanrouter_restart
/var/spool/asterisk/sysadmin/dahdi_restart IN_CLOSE_WRITE /usr/sbin/sysadmin_dahdi_restart
/usr/local/asterisk/ha_trigger IN_CLOSE_WRITE /usr/sbin/sysadmin_ha


[asterisk@connected incron.d]$ cat local

/usr/local/asterisk/incron IN_CLOSE_WRITE /usr/bin/sysadmin_manager --local $#

[asterisk@connected incron.d]$ cat sysadmin

/var/spool/asterisk/incron IN_MODIFY,IN_ATTRIB,IN_CLOSE_WRITE /usr/bin/sysadmin_manager $#
```

/usr/bin/lsmd -d

/usr/sbin/incrond

/usr/sbin/smartd -n -q never

/usr/bin/redis-server 127.0.0.1:6379

/usr/sbin/asterisk -f -vvvg -c

/usr/bin/python /usr/local/bin/pnp_server

!grep -iE "mysql|db|password" /etc/asterisk/*.conf

/usr/local/bin/dialplan-exec PBX_SECRET_2025 id

username=>freepbxuser
password=>mZzDpAGKTmPJ
database=>asteriskcdrdb

admin    |       |           | 05c689686a4fad5ce3ec76e7ae5708b1fe2da43a 

```
*7¡Vamos!
```



---
## Steps to User.txt

This script to get access to user asterisk reverse shell

https://github.com/watchtowrlabs/watchTowr-vs-FreePBX-CVE-2025-57819



---
## Steps to root.txt


---

## User Flag

```

```

## Root Flag

```

```