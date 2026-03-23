
| Port      | Protocol | Common Service / Usage                               | Notes / OSCP Relevance                                                               |
| --------- | -------- | ---------------------------------------------------- | ------------------------------------------------------------------------------------ |
| 20        | TCP      | FTP Data Transfer                                    | FTP active mode; OSCP: brute-force, anonymous login                                  |
| 21        | TCP      | [[21 FTP]] Control                                   | FTP login, banner grabbing                                                           |
| 22        | TCP      | [[22 SSH]]                                           | Remote shell access; OSCP: password/credential attacks                               |
| 23        | TCP      | Telnet                                               | Unencrypted remote login; legacy, useful for practice                                |
| 25        | TCP      | [[SMTP]]                                             | Email transfer; OSCP: mail relay misconfig                                           |
| 53        | TCP/UDP  | DNS                                                  | Domain name resolution; UDP common, TCP for zone transfer                            |
| 67        | UDP      | DHCP Server                                          | Dynamic IP assignment                                                                |
| 68        | UDP      | DHCP Client                                          | Dynamic IP assignment                                                                |
| 69        | UDP      | TFTP                                                 | Trivial File Transfer; unauthenticated uploads possible                              |
| 79        | TCP      | [[79 Finger\|Finger]]                                |                                                                                      |
| 80        | TCP      | [[80 - WEB\|HTTP]]                                   | Web services; OSCP: web app enumeration                                              |
| 88        | TCP      | Kerberos                                             | Kerberos Authen Protocol for secure, ticket-based network authentication (microsoft) |
| 110       | TCP      | [[110 POP3]]                                         | Email retrieval                                                                      |
| 111       | TCP/UDP  | [[111 RPCBind]]                                      | Common on Linux; OSCP: NFS enumeration                                               |
| 123       | UDP      | NTP                                                  | Time synchronization                                                                 |
| 135       | TCP      | RPC                                                  | Microsoft Remote Procedure Call Service                                              |
| 137       | UDP      | NetBIOS Name Service                                 | Windows name resolution; enumeration with nbtscan                                    |
| 138       | UDP      | NetBIOS Datagram                                     | Windows LAN communication                                                            |
| 139       | TCP      | NetBIOS Session [[139 445 SMB\|SMB]]                 | SMB over NetBIOS; OSCP: Windows share enumeration                                    |
| 143       | TCP      | IMAP                                                 | Email retrieval                                                                      |
| 161       | UDP      | [[SNMP Check\|SNMP]]                                 | Network management; OSCP: community string enumeration                               |
| 162       | UDP      | SNMP Trap                                            | Alerts                                                                               |
| 179       | TCP      | BGP                                                  | Border Gateway Protocol (rare for OSCP labs)                                         |
| 389       | TCP/UDP  | [[Synced OSCP Notes/Small Toolkit/Ports/LDAP\|LDAP]] | Directory services; OSCP: user enumeration                                           |
| 443       | TCP      | HTTPS                                                | Secure web; OSCP: web app enumeration, SSL/TLS tests                                 |
| 445       | TCP      | [[139 445 SMB\|SMB]]                                 | Windows file sharing; OSCP: SMB enumeration, exploit                                 |
| 465       | TCP      | [[465 SMTPS\|SMTPS]]                                 | Secure SMTP                                                                          |
| 514       | UDP      | Syslog                                               | Log collection                                                                       |
| 515       | TCP      | [[515 Printer]]                                      | Printer service                                                                      |
| 520       | UDP      | RIP                                                  | Routing Information Protocol                                                         |
| 546       | UDP      | DHCPv6 Client                                        | IPv6 Dynamic IP                                                                      |
| 547       | UDP      | DHCPv6 Server                                        | IPv6 Dynamic IP                                                                      |
| 587       | TCP      | SMTP (Submission)                                    | Outbound mail submission                                                             |
| 631       | TCP/UDP  | IPP / CUPS                                           | Printing service                                                                     |
| 636       | TCP      | LDAPS                                                | Secure LDAP                                                                          |
| 989       | TCP      | FTPS Data                                            | FTP over TLS                                                                         |
| 990       | TCP      | FTPS Control                                         | FTP over TLS                                                                         |
| 993       | TCP      | IMAPS                                                | Secure IMAP                                                                          |
| 995       | TCP      | POP3S                                                | Secure POP3                                                                          |
| 1080      | TCP      | SOCKS Proxy                                          | OSCP: pivoting and tunneling                                                         |
| 1433      | TCP      | Microsoft SQL Server                                 | OSCP: database enumeration/exploitation                                              |
| 1434      | UDP      | MS SQL Monitor                                       | SQL Server discovery                                                                 |
| 1521      | TCP      | Oracle DB                                            | Database enumeration                                                                 |
| 1723      | TCP/UDP  | PPTP VPN                                             | Legacy VPN                                                                           |
| 2049      | TCP/UDP  | NFS                                                  | Linux/Unix file sharing; OSCP: enumeration/exploitation                              |
| 2082      | TCP      | cPanel                                               | Hosting control panel                                                                |
| 2083      | TCP      | cPanel SSL                                           | Secure hosting control panel                                                         |
| 2095      | TCP      | Webmail                                              | Hosting email access                                                                 |
| 2096      | TCP      | Webmail SSL                                          | Secure webmail                                                                       |
| 3000      | TCP      | Node.js Express framework                            |                                                                                      |
| 3128      | TCP      | Squid Proxy                                          | HTTP proxy; pivoting possible                                                        |
| 3306      | TCP      | [[3306 MySQL\|MySQL / MariaDB]]                      | Database enumeration/exploitation                                                    |
| 3389      | TCP      | RDP                                                  | Remote Desktop; OSCP: brute-force if allowed                                         |
| 3690      | TCP      | SVN                                                  | Version control                                                                      |
| 5432      | TCP      | PostgreSQL                                           | Database enumeration/exploitation                                                    |
| 5900      | TCP      | VNC                                                  | Remote GUI access                                                                    |
| 5985      | TCP      | [[Tools/Evil-Winrm\|Evil-Winrm]] (HTTP)              | Windows Remote Management; remote PowerShell access                                  |
| 5986      | TCP      | [[Tools/Evil-Winrm\|Evil-Winrm]] (HTTP)              | Encrypted WinRM; remote PowerShell access                                            |
| 6000–6005 | TCP      | X11 Display                                          | Linux graphical remote access; OSCP rarely needed                                    |
| 6379      | TCP      | Redis                                                | In-memory database; OSCP: misconfig exploitation                                     |
| 6667      | TCP      | IRC                                                  | Chat protocol; OSCP: sometimes pivoting                                              |
| 8000      | TCP      | HTTP Alternate                                       | Web service; OSCP: custom web apps                                                   |
| 8080      | TCP      | HTTP Alternate                                       | Web service; OSCP: often used in labs                                                |
| 8443      | TCP      | HTTPS Alternate                                      | Web service                                                                          |
| 9000      | TCP      | Webmin                                               | Admin panel; OSCP: misconfiguration enumeration                                      |
| 9090      | TCP      | HTTP Alternate                                       | Web service                                                                          |
| 33060     | TCP      | [[3306 MySQL\|MySQL / MariaDB]]                      | Database enumeration/exploitation                                                    |