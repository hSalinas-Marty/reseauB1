# II. Serveur Web

## B. Configuration

### **🌞 Lister les ports en écoute sur la machine**
```powershell
[hugo@web ~]$ sudo ss -lnpt | grep 80
LISTEN 0      511          0.0.0.0:80        0.0.0.0:*    users:(("nginx",pid=11395,fd=6),("nginx",pid=11394,fd=6))
LISTEN 0      511             [::]:80           [::]:*    users:(("nginx",pid=11395,fd=7),("nginx",pid=11394,fd=7))
```

### **🌞 Ouvrir le port dans le firewall de la machine**
```powershell
[hugo@web ~]$ sudo firewall-cmd --permanent --add-port=80/tcp
success
[hugo@web ~]$ sudo firewall-cmd --reload
success
```

## C. Tests client

### **🌞 Vérifier que ça a pris effet**
```powershell
root@client1:/home/hugo# ping sitedefou.tp7.b1
PING sitedefou.tp7.b1 (10.7.1.11) 56(84) bytes of data.
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=1 ttl=64 time=1.13 ms
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=2 ttl=64 time=0.781 ms
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=3 ttl=64 time=0.916 ms
^C
--- sitedefou.tp7.b1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2033ms
rtt min/avg/max/mdev = 0.781/0.941/1.128/0.142 ms
```
```powershell
root@client1:/home/hugo# curl http://sitedefou.tp7.b1
meow !
```
# D. Analyze

### **🌞 Capture tcp_http.pcap**

[tcp_http.pcap](tcp_http.pcap)

### **🌞 Voir la connexion établie**
```powershell
root@client1:/home/hugo# sudo ss -npt | grep "10.7.1.11:80"
ESTAB 0      0               10.7.1.101:40666         10.7.1.11:80    users:(("firefox",pid=13910,fd=61))
```

# 2. On rajoute un S

## A. Config

### **🌞 Lister les ports en écoute sur la machine**
```powershell
[hugo@web sitedefou.tp7.b1]$ sudo ss -lnpt | grep 443
LISTEN 0      511        10.7.1.11:443       0.0.0.0:*    users:(("nginx",pid=1419,fd=6),("nginx",pid=1418,fd=6))
```

### **🌞 Gérer le firewall**
```powershell
[hugo@web sitedefou.tp7.b1]$ sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s8
  sources:
  services: cockpit dhcpv6-client ssh
  ports: 443/tcp
  protocols:
  forward: yes
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
```

## B. Test test test analyyyze

```powershell
hugo@client1:~$ curl https://sitedefou.tp7.b1 -k
meow !
```

### **🌞 Capture tcp_https.pcap**

[tcp_https.pcap](tcp_https.pcap)

# 1. Install et conf Wireguard

### **🌞 Prouvez que vous avez bien une nouvelle carte réseau wg0**
```powershell
[hugo@vpn ~]$ ip a
7: wg0: <POINTOPOINT,NOARP,UP,LOWER_UP> mtu 1420 qdisc noqueue state UNKNOWN group default qlen 1000
    link/none
    inet 10.7.200.1/24 scope global wg0
       valid_lft forever preferred_lft forever
```

### **🌞 Déterminer sur quel port écoute Wireguard**
```powershell
[hugo@vpn ~]$ sudo ss -lnpu | grep 51820
UNCONN 0      0            0.0.0.0:51820      0.0.0.0:*

UNCONN 0      0               [::]:51820         [::]:*
```

### **🌞 Ouvrez ce port dans le firewall**
```powershell
[hugo@vpn ~]$ sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s8 enp0s9
  sources:
  services: cockpit dhcpv6-client ssh
  ports: 51820/udp
  protocols:
  forward: yes
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
```

# 3. Proofs

### **🌞 Ping ping ping !**
```powershell
hugo@client1:~$ ping 10.7.200.1
PING 10.7.200.1 (10.7.200.1) 56(84) bytes of data.
64 bytes from 10.7.200.1: icmp_seq=1 ttl=64 time=4.34 ms
64 bytes from 10.7.200.1: icmp_seq=2 ttl=64 time=2.34 ms
^C
--- 10.7.200.1 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1001ms
rtt min/avg/max/mdev = 2.336/3.339/4.342/1.003 ms
```

### **🌞 Capture ping1_vpn.pcap**

[ping1_vpn.pcap](ping1_vpn.pcap)

### **🌞 Capture ping2_vpn.pcap**

[ping2_vpn.pcap](ping2_vpn.pcap)

### **🌞 Prouvez que vous avez toujours un accès internet**
```powershell
matheo@client1:~$ traceroute 1.1.1.1
traceroute to 1.1.1.1 (1.1.1.1), 30 hops max, 60 byte packets
 1  _gateway (10.7.200.1)  4.264 ms  4.206 ms  4.169 ms
 2  * * *
 3  10.0.2.2 (10.0.2.2)  8.367 ms  9.143 ms  10.001 ms
```

# 4. Private service

### **🌞 Visitez le service Web à travers le VPN**
```powershell
matheo@client1:~$ curl https://sitedefou.tp7.b1 -k
meow !
```