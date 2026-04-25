cctv.htb > cctv.htb/zm

default creds for zoneminder : admin/admin

zoneminder version number seen (v1.37.63)

CVE to dump sqlmap tables
https://github.com/BridgerAlderson/CVE-2024-51482 (trash)
use sql command to slowly dumb

Obtain hash for mark

hashcat the hash and get password

SSH into mark with password

user flag is on sa_mark (inaccesible)

ss -tlpn shows 8765 motioneye running

Chisel port forward motioneye for local access

cd /etc/motioneye/motion.conf shows admin password

spot motioneye version number

find motioneye CVE
https://github.com/gunzf0x/CVE-2025-60787

run the cmd and get root