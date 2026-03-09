The Knife tool provides an interface to manage Chef automation server nodes, cookbooks, recipes, et cetera. Knife usage can be read from manpage. Some examples show that it is possible to edit knife data bags using a text editor. Text editors like vi allow command execution, so if we run knife as root and land in a vi editor, we may be able to fully escalate our privileges. We run the following command to launch the editor:

sudo -l

/usr/bin/knife

```
sudo knife data bag create 1 2 -e vi
```

This opens up the vim editor. We type the below character sequence in the editor to get a shell as root.

```
:!/bin/sh
```