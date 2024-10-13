# 1. Les mains dans le capot

### **☀️ Capturez un échange DHCP complet**

[dhcp.pcap](dhcp.pcap)

### **☀️ Directement dans Wireshark, vous pouvez voir toutes les infos que vous donne  le serveur DHCP**

adresse IP proposée :

```Wireshark
Option: (50) Requested IP Adress (192.168.1.17)
    Length: 4
    Requested IP Adress: 192.168.1.17
```

serveur DNS indiqué :

```Wireshark
Option: (6) Domain Name Server
    Length: 4
    Domain Name Server: 192.168.1.1
```

passerelle du réseau : 
```Wireshark
Option: (54) DHCP Server Identifier (192.168.1.1)
    Length: 4
    DHCP Server Identifier: 192.168.1.1
```