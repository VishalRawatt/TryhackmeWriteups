
## **Encryption - Crypto 101**

### **Task-9**

```
ssh2john rsa_file > filename.hash
```

```
john --wordlist=<rockyou.txt path> filename.hash
```

![enum results](../NPT/Assets/131.png)

### **Task-11**

Download task file

```
unzip <filename>
```

```
cat tryhackme.key
```

![enum results](../NPT/Assets/132.png)

File is encrypted

```
gpg --import tryhackme.key
```

```
gpg message.gpg
```

![enum results](../NPT/Assets/133.png)

```
cat message
```















