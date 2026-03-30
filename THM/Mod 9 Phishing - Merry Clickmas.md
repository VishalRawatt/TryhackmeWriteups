
## **Phishing - Merry Clickmas**

```
ls
```

```
cd Rooms/AoC2@25
```

```
./server.py
```

```
http://<Your IP>:8000
```

sign in with username and password

We will use social-engineering-toolkit (SET) here which we just ran

```
setoolkit
```

```
1
```

```
5
```

```
1
```

```
factory@wareville.thm (we have to add email whom we will send this email)
```

```
2
```

```
updates@flyingdeer.thm
```

Flying deer

Press enter twice (no password)

In SMTP email address: target IP

Port default to 25

no

n

n

Email Subject: Alert your google credentials are leaked here

Now in email body type: Dear user, your google credentials are leaked by the boat India server. Please follow the link to change your password from here at 

```
http://<Your IP>:8000
```

Next body line: It would be so nice of you to change these leaked credentials. Thank you for time.

END

Press return or type exit

99

Now we are back now check at your server which we ran ./server.py

Wait for some time and we got username and password of the victim

Now login to the portal with victim’s credentials on target IP

Now we entered and can check our own mail and rest of their email