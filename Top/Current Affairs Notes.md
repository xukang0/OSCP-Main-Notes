
[[Current Affairs Notes Template]]

# Steps to User flag

135 RPCclient nothing

445 SMB enum4linux-ng finds domain information and OS info

after fuzzing web page port 50000, there is a /askjeeves page

Its a jenkies control panel

at logs page there are interesting historical commands

following my jenkins priv esc guide, 

https://github.com/godylockz/CVE-2024-23897

this cve recorded in the past works as i tried to read /etc/hosts file of windows machine

use [[Jenkins Priv Esc]] to get RCE through groovy script

able to access C:\Users\Administrator\.jenkins but not cd .. into administrator desktop

I am shell as jeeves\kohsuke

I realize SeImpersonatePrivilege is enabled so its easy priv esc [[SeImpersonatePrivilege]]

Since its windows 10 and x64 bit I choose to use godpotato.exe

---

stopped at trying to priv esc into admin account

how to regain shell : 

groovy script , peneloper listener port 8044.

Figure out how to use WES.py through gemini






