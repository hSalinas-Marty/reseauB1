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