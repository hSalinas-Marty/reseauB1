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