# **Windows** `net` **commands cheatsheet**

## **1. User enumeration**

| Command                     | Purpose                       |
| --------------------------- | ----------------------------- |
| `net user`                  | List local users              |
| `net user username`         | Details of a specific user    |
| `net user /domain`          | List domain users             |
| `net user username /domain` | Details of a domain user      |
| `net accounts`              | Password and account policies |
| `net accounts /domain`      | Domain password policy        |

Examples:

```
net user
net user Administrator
net user Administrator /domain
net user /domain
net accounts
net accounts /domain
```

## **2. Group enumeration**

| Command                                 | Purpose                      |
| --------------------------------------- | ---------------------------- |
| `net localgroup`                        | List local groups            |
| `net localgroup "Administrators"`       | Local Administrators members |
| `net localgroup "Remote Desktop Users"` | Local RDP group members      |
| `net group /domain`                     | List domain groups           |
| `net group "Domain Admins" /domain`     | Domain Admins members        |
| `net group "Domain Users" /domain`      | Domain Users members         |

Examples:

```
net localgroup
net localgroup Administrators
net localgroup "Remote Desktop Users"
net group /domain
net group "Domain Admins" /domain
net group "Enterprise Admins" /domain
```

**Remember the distinction:**

- `net localgroup` = local machine groups.
    
- `net group` = domain groups.
    

## **3. User and group modification**

| Command                                | Purpose                                                |
| -------------------------------------- | ------------------------------------------------------ |
| `net user USER PASS /add`              | Create local user                                      |
| `net user USER /delete`                | Delete local user                                      |
| `net user USER PASS /domain`           | Change domain user's password (subject to permissions) |
| `net localgroup GROUP USER /add`       | Add user to local group                                |
| `net localgroup GROUP USER /delete`    | Remove user from local group                           |
| `net group GROUP USER /add /domain`    | Add user to domain group                               |
| `net group GROUP USER /delete /domain` | Remove user from domain group                          |

Examples:

```
net user Retric 'Password123!' /add

net localgroup Administrators Retric /add

net localgroup "Remote Desktop Users" Retric /add

net group "Domain Admins" Retric /add /domain
```

Important: these operations require appropriate permissions. Adding a user to a group does not automatically grant domain privileges unless that group has them.

## **4. Share enumeration**

|Command|Purpose|
|---|---|
|`net share`|List local shared resources|
|`net share SHARE`|Details of a specific share|
|`net view \\HOST`|List remote machine shares|
|`net view /domain`|List visible domains|
|`net view /domain:DOMAIN`|List computers in a domain|

Examples:

```
net share

net view \\MS01

net view /domain

net view /domain:laser.com
```

Create or remove a share:

```
net share ShareName=C:\Share

net share ShareName /delete
```

## **5. Domain and network enumeration**

```
net config workstation
net config server
net statistics workstation
net statistics server
net time /domain
net view
```

|Command|Information|
|---|---|
|`net config workstation`|Computer name, domain/workgroup|
|`net config server`|Server configuration|
|`net statistics workstation`|Workstation statistics|
|`net statistics server`|Server statistics|
|`net time /domain`|Domain controller time|
|`net view`|Visible network computers|

## **6. Sessions and connections**

```
net session
net session \\HOST
net use
net use * /delete
```

|Command|Purpose|
|---|---|
|`net session`|View sessions connected to local server|
|`net session \\HOST`|Inspect a remote session|
|`net use`|List mapped network connections|
|`net use Z: \\HOST\SHARE`|Map network share|
|`net use * /delete`|Remove mapped connections|

## **7. Services**

```
net start
net start SERVICE
net stop SERVICE
```

Examples:

```
net start
net start Spooler
net stop Spooler
```

Useful for checking whether services such as Print Spooler are running.

## **8. Account and password management**

```
net user USERNAME PASSWORD
net user USERNAME /active:yes
net user USERNAME /active:no
net user USERNAME /expires:never
net user USERNAME /passwordchg:no
```

These modify account properties, subject to permissions.

## **9. OSCP quick-reference table**

These are the commands I'd prioritise remembering independently.

|What you want|Command|
|---|---|
|Current local users|`net user`|
|Domain users|`net user /domain`|
|User details|`net user USER`|
|Domain user details|`net user USER /domain`|
|Local groups|`net localgroup`|
|Local administrators|`net localgroup Administrators`|
|Domain groups|`net group /domain`|
|Domain Admins|`net group "Domain Admins" /domain`|
|Password policy|`net accounts /domain`|
|Local shares|`net share`|
|Remote shares|`net view \\HOST`|
|Domain computers|`net view /domain:DOMAIN`|
|Computer/domain information|`net config workstation`|
|Current mapped shares|`net use`|
|Running services|`net start`|

## **10. Important:** `net` **vs other Windows commands**

Don't confuse these:

| Command       | What it is used for                       |
| ------------- | ----------------------------------------- |
| `net`         | Users, groups, shares, sessions, services |
| `whoami`      | Current identity and token privileges     |
| `hostname`    | Computer name                             |
| `systeminfo`  | OS and system information                 |
| `ipconfig`    | Network configuration                     |
| `nltest`      | Domain and domain-controller discovery    |
| `setspn`      | SPN enumeration and management            |
| `dsquery`     | Active Directory object queries           |
| `Get-ADUser`  | PowerShell AD user enumeration            |
| `Get-ADGroup` | PowerShell AD group enumeration           |