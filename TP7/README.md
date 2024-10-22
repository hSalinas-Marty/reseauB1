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

##

