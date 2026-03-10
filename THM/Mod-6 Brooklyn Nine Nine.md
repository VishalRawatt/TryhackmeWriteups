
## **Brooklyn Nine Nine**

```
nmap -sC -sV -p- 10.48.160.254
```

```
gobuster dir -u http://10.48.160.254 -w dirbuster/wordlists/directory-list-2.3-medium.txt
```

![[134.png]]

We found FTP port open, so let us try anonymous login

```
ftp 10.48.160.254
```

Username and Password both are : anonymous

![[136.png]]

We found a file called note_to_jake.txt, let us transfer this file in our system

```
get note_to_jake.txt
```

We got the file let us open it

```
cat get note_to_jake.txt
```

Found a username called Jake

![[137.png]]




























