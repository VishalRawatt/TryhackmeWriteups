
## Network Services

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
smbclient //10.48.181.56/secret -U suit -p 445
```

We are trying anonymous login here

```
smbclient -L 10.48.181.56
```

After enumerating we will find a share name called profiles

![enum results](../NPT/Assets/101.png)

```
smbclient //10.48.181.56/profiles -U Anonymous
```

We are logged in

![enum results](../NPT/Assets/102.png)

```
more "Working From Home Information.txt"
```

```
cd .ssh
```

```
ls
```

```
get id_rsa
```

![enum results](../NPT/Assets/103.png)

Now we will use this rsa file to login

```
chmod 600 id_rsa
```

```
ssh -i id_rsa cactus@<IP>
```

![enum results](../NPT/Assets/104.png)

```
ls
```

```
cat smb.txt
```

![enum results](../NPT/Assets/105.png)

#### Task-6 

This one scans a lot of ports so it takes time

```
nmap -p- -vv -T5 10.48.148.51
```

![enum results](../NPT/Assets/106.png)

```
nmap -p8012 -v  10.48.148.51
```

We found a port 8012 

```
telnet 10.48.148.51 8012
```

![enum results](../NPT/Assets/107.png)

#### Task-9

```
nmap -F 10.49.136.137 
```

![enum results](../NPT/Assets/108.png)

