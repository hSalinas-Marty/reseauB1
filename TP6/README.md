#  I. Le setup

## 2. Marche à suivre

### **☀️ Prouvez que...**

```powershell
[hugo@dhcp ~]$ ping ynov.com
PING ynov.com (172.67.74.226) 56(84) bytes of data.
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=1 ttl=57 time=31.9 ms
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=2 ttl=57 time=31.0 ms
^C
--- ynov.com ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1001ms
rtt min/avg/max/mdev = 31.016/31.450/31.884/0.434 ms
```
```powershell
[hugo@web ~]$ ping ynov.com
PING ynov.com (104.26.10.233) 56(84) bytes of data.
64 bytes from 104.26.10.233 (104.26.10.233): icmp_seq=1 ttl=57 time=20.5 ms
64 bytes from 104.26.10.233 (104.26.10.233): icmp_seq=2 ttl=57 time=29.4 ms
^C
--- ynov.com ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1002ms
rtt min/avg/max/mdev = 20.543/24.966/29.389/4.423 ms
```
```powershell
[hugo@dhcp ~]$ ping 10.6.2.11
PING 10.6.2.11 (10.6.2.11) 56(84) bytes of data.
64 bytes from 10.6.2.11: icmp_seq=1 ttl=63 time=2.83 ms
64 bytes from 10.6.2.11: icmp_seq=2 ttl=63 time=1.52 ms
64 bytes from 10.6.2.11: icmp_seq=3 ttl=63 time=1.70 ms
^C
--- 10.6.2.11 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2004ms
rtt min/avg/max/mdev = 1.517/2.017/2.832/0.581 ms
```
# II. LAN clients

## 2. Client

### **☀️ Prouvez que...**
```powershell
hugo@client1:~$ ip a
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:9f:82:06 brd ff:ff:ff:ff:ff:ff
    inet 10.6.1.37/24 brd 10.6.1.255 scope global dynamic noprefixroute enp0s8
       valid_lft 42587sec preferred_lft 42587sec
    inet6 fe80::a00:27ff:fe9f:8206/64 scope link
       valid_lft forever preferred_lft forever
```
```powershell
hugo@client1:~$ resolvectl
Global
         Protocols: -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
  resolv.conf mode: stub

Link 2 (enp0s8)
    Current Scopes: DNS
         Protocols: +DefaultRoute -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
Current DNS Server: 1.1.1.1
       DNS Servers: 1.1.1.1
```
```powershell
hugo@client1:~$ ip r s
default via 10.6.1.254 dev enp0s8 proto dhcp src 10.6.1.37 metric 100
10.6.1.0/24 dev enp0s8 proto kernel scope link src 10.6.1.37 metric 100
```
```powershell
hugo@client1:~$ ping instagram.com
PING instagram.com (185.60.219.174) 56(84) bytes of data.
64 bytes from instagram-p42-shv-01-cdg4.fbcdn.net (185.60.219.174): icmp_seq=1 ttl=57 time=22.0 ms
64 bytes from instagram-p42-shv-01-cdg4.fbcdn.net (185.60.219.174): icmp_seq=2 ttl=57 time=44.9 ms
^C
--- instagram.com ping statistics ---
3 packets transmitted, 2 received, 33.3333% packet loss, time 2006ms
rtt min/avg/max/mdev = 21.964/33.431/44.898/11.467 ms
```

# III. LAN serveurzzzz

## 3. Analyse et test

### **☀️ Déterminer sur quel port écoute le serveur NGINX**
```powershell
[hugo@web ~]$ sudo ss -lnpt | grep 80
LISTEN 0      511          0.0.0.0:80        0.0.0.0:*    users:(("nginx",pid=1804,fd=6),("nginx",pid=1803,fd=6))
LISTEN 0      511             [::]:80           [::]:*    users:(("nginx",pid=1804,fd=7),("nginx",pid=1803,fd=7))
```

### **☀️ Ouvrir ce port dans le firewall**
```powershell
[hugo@web ~]$ sudo firewall-cmd --permanent --remove-service dhcpv6-client
success
[hugo@web ~]$ sudo firewall-cmd --permanent --remove-service cockpit
success
[hugo@web ~]$ sudo firewall-cmd --reload
success
```

### **☀️ Visitez le site web !**

```powershell
[hugo@web ~]$ curl http://10.6.2.11
<!doctype html>
<html>
  <head>
    <meta charset='utf-8'>
    <meta name='viewport' content='width=device-width, initial-scale=1'>
    <title>HTTP Server Test Page powered by: Rocky Linux</title>
    <style type="text/css">
      /*<![CDATA[*/
```

# III. 2. Serveur DNS
### **☀️ Déterminer sur quel(s) port(s) écoute le service BIND9**
```powershell
[hugo@dns ~]$ sudo ss -lnpt | grep 53
LISTEN 0      10         127.0.0.1:53        0.0.0.0:*    users:(("named",pid=713,fd=22))
LISTEN 0      10         10.6.2.12:53        0.0.0.0:*    users:(("named",pid=713,fd=28))
LISTEN 0      4096       127.0.0.1:953       0.0.0.0:*    users:(("named",pid=713,fd=26))
LISTEN 0      10             [::1]:53           [::]:*    users:(("named",pid=713,fd=25))
LISTEN 0      4096           [::1]:953          [::]:*    users:(("named",pid=713,fd=27))
```
```powershell
[hugo@dns ~]$ sudo ss -lnpu | grep 53
UNCONN 0      0          10.6.2.12:53        0.0.0.0:*    users:(("named",pid=713,fd=6))
UNCONN 0      0          127.0.0.1:53        0.0.0.0:*    users:(("named",pid=713,fd=21))
UNCONN 0      0              [::1]:53           [::]:*    users:(("named",pid=713,fd=24))
```

### **☀️ Ouvrir ce(s) port(s) dans le firewall**
```powershell
[hugo@dns ~]$ sudo firewall-cmd --permanent --add-port=53/tcp
success
[hugo@dns ~]$ sudo firewall-cmd --reload
success
```
```powershell
[hugo@dns ~]$ sudo firewall-cmd --permanent --add-port=53/udp
success
[hugo@dns ~]$ sudo firewall-cmd --reload
success
```
### **☀️ Effectuez des requêtes DNS manuellement depuis le serveur DNS lui-même dans un premier temps**
```powershell
[hugo@dns ~]$ dig web.tp6.b1 @10.6.2.12

; <<>> DiG 9.16.23-RH <<>> web.tp6.b1 @10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 22427
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: cf7cb092f947505801000000671603f6818c330486c0ae7b (good)
;; QUESTION SECTION:
;web.tp6.b1.                    IN      A

;; ANSWER SECTION:
web.tp6.b1.             86400   IN      A       10.6.2.11

;; Query time: 0 msec
;; SERVER: 10.6.2.12#53(10.6.2.12)
;; WHEN: Mon Oct 21 09:34:14 CEST 2024
;; MSG SIZE  rcvd: 83
```
```powershell
[hugo@dns ~]$ dig dns.tp6.b1 @10.6.2.12

; <<>> DiG 9.16.23-RH <<>> dns.tp6.b1 @10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 7900
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: ab147e51df7096c30100000067160404011cf6ae8d8a8796 (good)
;; QUESTION SECTION:
;dns.tp6.b1.                    IN      A

;; ANSWER SECTION:
dns.tp6.b1.             86400   IN      A       10.6.2.12

;; Query time: 0 msec
;; SERVER: 10.6.2.12#53(10.6.2.12)
;; WHEN: Mon Oct 21 09:34:28 CEST 2024
;; MSG SIZE  rcvd: 83
```
```powershell
[hugo@dns ~]$ dig ynov.com @10.6.2.12

; <<>> DiG 9.16.23-RH <<>> ynov.com @10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 45772
;; flags: qr rd ra; QUERY: 1, ANSWER: 3, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: b222debe65674809010000006716040f5e9efc4b68b47fb2 (good)
;; QUESTION SECTION:
;ynov.com.                      IN      A

;; ANSWER SECTION:
ynov.com.               300     IN      A       172.67.74.226
ynov.com.               300     IN      A       104.26.10.233
ynov.com.               300     IN      A       104.26.11.233

;; Query time: 290 msec
;; SERVER: 10.6.2.12#53(10.6.2.12)
;; WHEN: Mon Oct 21 09:34:39 CEST 2024
;; MSG SIZE  rcvd: 113
```
```powershell
[hugo@dns ~]$ dig -x 10.6.2.11 @10.6.2.12

; <<>> DiG 9.16.23-RH <<>> -x 10.6.2.11 @10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 40276
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: 3525650934295f40010000006716042b3e85a516ee194e32 (good)
;; QUESTION SECTION:
;11.2.6.10.in-addr.arpa.                IN      PTR

;; ANSWER SECTION:
11.2.6.10.in-addr.arpa. 86400   IN      PTR     web.tp6.b1.

;; Query time: 0 msec
;; SERVER: 10.6.2.12#53(10.6.2.12)
;; WHEN: Mon Oct 21 09:35:07 CEST 2024
;; MSG SIZE  rcvd: 103
```
```powershell
[hugo@dns ~]$ dig -x 10.6.2.12 @10.6.2.12

; <<>> DiG 9.16.23-RH <<>> -x 10.6.2.12 @10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 44538
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: 06eaecf24345c3ef010000006716043e1468527e4a151a29 (good)
;; QUESTION SECTION:
;12.2.6.10.in-addr.arpa.                IN      PTR

;; ANSWER SECTION:
12.2.6.10.in-addr.arpa. 86400   IN      PTR     dns.tp6.b1.

;; Query time: 0 msec
;; SERVER: 10.6.2.12#53(10.6.2.12)
;; WHEN: Mon Oct 21 09:35:26 CEST 2024
;; MSG SIZE  rcvd: 103
```

### **☀️ Effectuez une requête DNS manuellement depuis client1.tp6.b1**
```powershell 
hugo@client1:~$ dig web.tp6.b1 @10.6.2.12

; <<>> DiG 9.18.28-0ubuntu0.24.04.1-Ubuntu <<>> web.tp6.b1 @10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 26768
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: 09bed5cba0e43cf701000000671605b4631a68db4f3fb062 (good)
;; QUESTION SECTION:
;web.tp6.b1.                    IN      A

;; ANSWER SECTION:
web.tp6.b1.             86400   IN      A       10.6.2.11

;; Query time: 2 msec
;; SERVER: 10.6.2.12#53(10.6.2.12) (UDP)
;; WHEN: Mon Oct 21 09:41:40 CEST 2024
;; MSG SIZE  rcvd: 83
```

### **☀️ Capturez une requête DNS et la réponse de votre serveur**
```powershell
hugo@client1:~$ sudo tcpdump -w tcpdump.pcap -i enp0s8
```
```powershell
hugo@client1:~$ dig web.tp6.b1 @10.6.2.12
```
[tcpdump.pcap](tcpdump.pcap)

### **☀️ Créez un nouveau client client2.tp6.b1 vitefé**
```powershell
hugo@client2:~$ ip a
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:01:80:b2 brd ff:ff:ff:ff:ff:ff
    inet 10.6.1.38/24 brd 10.6.1.255 scope global dynamic noprefixroute enp0s8
       valid_lft 37775sec preferred_lft 37775sec
    inet6 fe80::a00:27ff:fe01:80b2/64 scope link
       valid_lft forever preferred_lft forever
```
```powershell
hugo@client2:~$ resolvectl
Global
         Protocols: -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
  resolv.conf mode: stub

Link 2 (enp0s8)
    Current Scopes: DNS
         Protocols: +DefaultRoute -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
Current DNS Server: 10.6.2.12
       DNS Servers: 10.6.2.12
```
```powershell
hugo@client2:~$ ping web.tp6.b1
PING web.tp6.b1 (10.6.2.11) 56(84) bytes of data.
64 bytes from web.tp6.b1 (10.6.2.11): icmp_seq=1 ttl=63 time=1.96 ms
64 bytes from web.tp6.b1 (10.6.2.11): icmp_seq=2 ttl=63 time=1.74 ms
64 bytes from web.tp6.b1 (10.6.2.11): icmp_seq=3 ttl=63 time=1.62 ms
64 bytes from web.tp6.b1 (10.6.2.11): icmp_seq=4 ttl=63 time=2.24 ms
^C
--- web.tp6.b1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3009ms
rtt min/avg/max/mdev = 1.618/1.890/2.241/0.237 ms
```
