# I. ARP basics

### **☀️ Avant de continuer...**

```powershell
PS C:\Users\hugos> ipconfig /all
Wireless LAN adapter Wi-Fi:

   Connection-specific DNS Suffix  . :
   Description . . . . . . . . . . . : MediaTek Wi-Fi 6 MT7921 Wireless LAN Card
   Physical Address. . . . . . . . . : 50-5A-65-50-4A-C9
   DHCP Enabled. . . . . . . . . . . : Yes
   Autoconfiguration Enabled . . . . : Yes
   Link-local IPv6 Address . . . . . : fe80::54fa:110f:881f:356f%7(Preferred)
   IPv4 Address. . . . . . . . . . . : 10.33.77.208(Preferred)
   Subnet Mask . . . . . . . . . . . : 255.255.240.0
   Lease Obtained. . . . . . . . . . : Tuesday, October 8, 2024 8:45:40 AM
   Lease Expires . . . . . . . . . . : Wednesday, October 9, 2024 8:45:40 AM
   Default Gateway . . . . . . . . . : 10.33.79.254
   DHCP Server . . . . . . . . . . . : 10.33.79.254
   DHCPv6 IAID . . . . . . . . . . . : 122706533
   DHCPv6 Client DUID. . . . . . . . : 00-01-00-01-2B-A5-7E-61-A0-36-BC-6B-BF-62
   DNS Servers . . . . . . . . . . . : 8.8.8.8
                                       1.1.1.1
   NetBIOS over Tcpip. . . . . . . . : Enabled
```

### **☀️ Affichez votre table ARP**

PS C:\Users\hugos> arp -a
```powershell
Interface: 10.33.77.208 --- 0x7
  Internet Address      Physical Address      Type
  10.33.65.63           44-af-28-c3-6a-9f     dynamic
  10.33.66.78           e4-b3-18-48-36-68     dynamic
  10.33.73.77           98-8d-46-c4-fa-e5     dynamic
  10.33.77.160          c8-94-02-f8-ab-97     dynamic
  10.33.79.254          7c-5a-1c-d3-d8-76     dynamic
  10.33.79.255          ff-ff-ff-ff-ff-ff     static
  224.0.0.22            01-00-5e-00-00-16     static
  224.0.0.251           01-00-5e-00-00-fb     static
  224.0.0.252           01-00-5e-00-00-fc     static
  239.255.255.250       01-00-5e-7f-ff-fa     static
  255.255.255.255       ff-ff-ff-ff-ff-ff     static

Interface: 192.168.56.1 --- 0x9
  Internet Address      Physical Address      Type
  192.168.56.255        ff-ff-ff-ff-ff-ff     static
  224.0.0.22            01-00-5e-00-00-16     static
  224.0.0.251           01-00-5e-00-00-fb     static
  224.0.0.252           01-00-5e-00-00-fc     static
  239.255.255.250       01-00-5e-7f-ff-fa     static
  255.255.255.255       ff-ff-ff-ff-ff-ff     static
```

### **☀️ Déterminez l'adresse MAC de la passerelle du réseau de l'école**
```powershell
10.33.79.254          7c-5a-1c-d3-d8-76     dynamic
```

### **☀️ Supprimez la ligne qui concerne la passerelle**
```powershell
PS C:\WINDOWS\system32> arp -d 10.33.79.254
```

### **☀️ Prouvez que vous avez supprimé la ligne dans la table ARP**
```powershell
PS C:\WINDOWS\system32> arp -a

Interface: 10.33.77.208 --- 0x7
  Internet Address      Physical Address      Type
  224.0.0.22            01-00-5e-00-00-16     static
  224.0.0.251           01-00-5e-00-00-fb     static
  224.0.0.252           01-00-5e-00-00-fc     static
  239.255.255.250       01-00-5e-7f-ff-fa     static
  255.255.255.255       ff-ff-ff-ff-ff-ff     static

Interface: 192.168.56.1 --- 0x9
  Internet Address      Physical Address      Type
  192.168.56.255        ff-ff-ff-ff-ff-ff     static
  224.0.0.22            01-00-5e-00-00-16     static
  224.0.0.251           01-00-5e-00-00-fb     static
  224.0.0.252           01-00-5e-00-00-fc     static
  239.255.255.250       01-00-5e-7f-ff-fa     static
  255.255.255.255       ff-ff-ff-ff-ff-ff     static
```
### **☀️ Wireshark**

[arp1.pcap](arp1.pcap)

# II. ARP dans un réseau local

### **1. Basics**
```powershell
PS C:\WINDOWS\system32> ipconfig /all

Wireless LAN adapter Wi-Fi:
 IPv4 Address. . . . . . . . . . . : 172.20.10.6(Preferred)
 Physical Address. . . . . . . . . : 50-5A-65-50-4A-C9
```

### **☀️ DIY**
```powershell
PS C:\Users\hugos\Downloads> ipconfig

Wireless LAN adapter Wi-Fi:

   Connection-specific DNS Suffix  . :
   IPv6 Address. . . . . . . . . . . : 2a02:8440:6300:309e:e53e:21c5:3846:1562
   Temporary IPv6 Address. . . . . . : 2a02:8440:6300:309e:64b1:d660:436e:bca6
   Link-local IPv6 Address . . . . . : fe80::54fa:110f:881f:356f%7
   IPv4 Address. . . . . . . . . . . : 172.20.10.11
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : fe80::cdb:eaff:fe5b:1364%7
                                       172.20.10.1
```

### **☀️ Pingz !**
Ulysse
```powershell
PS C:\Users\hugos\Downloads> ping 172.20.10.9 

Pinging 172.20.10.9 with 32 bytes of data:
Reply from 172.20.10.9: bytes=32 time=88ms TTL=128
Reply from 172.20.10.9: bytes=32 time=107ms TTL=128
Reply from 172.20.10.9: bytes=32 time=13ms TTL=128
Reply from 172.20.10.9: bytes=32 time=123ms TTL=128

Ping statistics for 172.20.10.9:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 13ms, Maximum = 123ms, Average = 82ms
```
Teddy
```powershell
PS C:\Users\hugos\Downloads> ping 172.20.10.10

Pinging 172.20.10.10 with 32 bytes of data:
Reply from 172.20.10.10: bytes=32 time=3ms TTL=128
Reply from 172.20.10.10: bytes=32 time=4ms TTL=128
Reply from 172.20.10.10: bytes=32 time=56ms TTL=128
Reply from 172.20.10.10: bytes=32 time=7ms TTL=128

Ping statistics for 172.20.10.10:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 3ms, Maximum = 56ms, Average = 17ms
```
Victoria
```powershell
PS C:\Users\hugos\Downloads> ping 172.20.10.8

Pinging 172.20.10.8 with 32 bytes of data:
Reply from 172.20.10.8: bytes=32 time=222ms TTL=128
Reply from 172.20.10.8: bytes=32 time=14ms TTL=128
Reply from 172.20.10.8: bytes=32 time=115ms TTL=128
Reply from 172.20.10.8: bytes=32 time=26ms TTL=128

Ping statistics for 172.20.10.8:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 14ms, Maximum = 222ms, Average = 94ms
```
insta
```powershell
PS C:\Users\hugos\Downloads> ping www.instagram.com

Pinging z-p42-instagram.c10r.instagram.com [2a03:2880:f27b:1e4:face:b00c:0:4420] with 32 bytes of data:
Reply from 2a03:2880:f27b:1e4:face:b00c:0:4420: time=51ms
Reply from 2a03:2880:f27b:1e4:face:b00c:0:4420: time=62ms
Reply from 2a03:2880:f27b:1e4:face:b00c:0:4420: time=43ms
Reply from 2a03:2880:f27b:1e4:face:b00c:0:4420: time=33ms

Ping statistics for 2a03:2880:f27b:1e4:face:b00c:0:4420:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 33ms, Maximum = 62ms, Average = 47ms
```
# 2. ARP

```powershell
PS C:\Users\hugos\Downloads> arp -a

Interface: 172.20.10.11 --- 0x7
  Internet Address      Physical Address      Type
  172.20.10.1           0e-db-ea-5b-13-64     dynamic
  172.20.10.8           10-63-c8-68-8c-21     dynamic
  172.20.10.9           90-09-df-a4-67-21     dynamic
  172.20.10.10          d4-3b-04-ff-44-7a     dynamic
  172.20.10.255         ff-ff-ff-ff-ff-ff     static
  224.0.0.22            01-00-5e-00-00-16     static
  224.0.0.251           01-00-5e-00-00-fb     static
  239.255.255.250       01-00-5e-7f-ff-fa     static

Interface: 192.168.56.1 --- 0x9
  Internet Address      Physical Address      Type
  192.168.56.255        ff-ff-ff-ff-ff-ff     static
  224.0.0.22            01-00-5e-00-00-16     static
  224.0.0.251           01-00-5e-00-00-fb     static
  224.0.0.252           01-00-5e-00-00-fc     static
  239.255.255.250       01-00-5e-7f-ff-fa     static
  255.255.255.255       ff-ff-ff-ff-ff-ff     static
```

### **☀️ Capture arp2.pcap**

[arp2.pcapng](arp2.pcapng)

# 3. Bonus : ARP poisoning

### **⭐ Empoisonner la table ARP de l'un des membres de votre réseau**

