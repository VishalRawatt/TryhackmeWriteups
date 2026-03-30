
## **Anthem**

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

We are hiring page -> Right Click -> View Page Source

##### 2nd Flag

inside- /categories  -> Right Click -> View Page Source

##### 3th Flag

We are hiring -> Author John doe  -> Right Click -> View Page Source

##### 4th Flag

cheers to IT department - page source  -> Right Click -> View Page Source

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

We will find a file in C folder

Unhide files in C folder -> edit permissions

 ```
 xfreerdp3 /v:10.64.144.3 /u:Administrator /p:ChangeMeBaby1MoreTime /cert:ignore +clipboard /dynamic-resolution
 ```

We got out root flag