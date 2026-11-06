
[[Current Affairs Notes Template]]

# Steps to User flag

Run rust scan, ports 80 and 3306 open

3306 doesnt have anything interesting so far, focus on 80

visiting webpage shows a default slick page.

Decide to directory fuzz against ip address

/bugtracker is revealed, showing a mantis bug tracker page

http://192.168.228.204/bugtracker/admin/install.php shows that webpage can interact with sql database

Updating Configuration File (config/config_inc.php)

Google search vaguely suggests that the creds to the sql database is in this file

The goal now is to try to read this file

Search for Mantis arbitrary file read

https://mantisbt.org/bugs/view.php?id=23173

links to 

https://github.com/allyshka/Rogue-MySql-Server/blob/master/roguemysql.php

