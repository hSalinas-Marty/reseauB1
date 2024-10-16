# I. Setup

### **☀️ Uniquement avec des commandes, prouvez-que :**

```powershell
[hugo@routeur ~]$ ip a
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:97:de:8f brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.254/24 brd 10.5.1.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe97:de8f/64 scope link
       valid_lft forever preferred_lft forever
```
```powershell
hugo@client1:~$ ip a
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:6e:57:e7 brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.11/24 brd 10.5.1.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe6e:57e7/64 scope link
       valid_lft forever preferred_lft forever
```
```powershell
hugo@client2:~$ ip a
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:3e:1e:d5 brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.12/24 brd 10.5.1.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe3e:1ed5/64 scope link
       valid_lft forever preferred_lft forever
```
```powershell
PS C:\Users\hugos> ping 10.5.1.254

Pinging 10.5.1.254 with 32 bytes of data:
Reply from 10.5.1.254: bytes=32 time=1ms TTL=64
Reply from 10.5.1.254: bytes=32 time<1ms TTL=64
Reply from 10.5.1.254: bytes=32 time<1ms TTL=64
Reply from 10.5.1.254: bytes=32 time<1ms TTL=64

Ping statistics for 10.5.1.254:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 1ms, Average = 0ms
PS C:\Users\hugos> ping 10.5.1.11

Pinging 10.5.1.11 with 32 bytes of data:
Reply from 10.5.1.11: bytes=32 time=1ms TTL=64
Reply from 10.5.1.11: bytes=32 time<1ms TTL=64
Reply from 10.5.1.11: bytes=32 time<1ms TTL=64
Reply from 10.5.1.11: bytes=32 time<1ms TTL=64

Ping statistics for 10.5.1.11:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 1ms, Average = 0ms
PS C:\Users\hugos> ping 10.5.1.12

Pinging 10.5.1.12 with 32 bytes of data:
Reply from 10.5.1.12: bytes=32 time<1ms TTL=64
Reply from 10.5.1.12: bytes=32 time=1ms TTL=64
Reply from 10.5.1.12: bytes=32 time<1ms TTL=64
Reply from 10.5.1.12: bytes=32 time<1ms TTL=64

Ping statistics for 10.5.1.12:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 1ms, Average = 0ms
```

# II. Accès internet pour tous

## 1. Accès internet routeur

### **☀️ Déjà, prouvez que le routeur a un accès internet**

```powershell
[hugo@routeur ~]$ ping ynov.com
PING ynov.com (172.67.74.226) 56(84) bytes of data.
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=1 ttl=46 time=145 ms
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=2 ttl=46 time=35.2 ms
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=3 ttl=46 time=32.1 ms
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=4 ttl=46 time=31.6 ms
^C
--- ynov.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3006ms
rtt min/avg/max/mdev = 31.645/60.991/145.017/48.531 ms
```

### **☀️ Activez le routage**

```powershell
hugo@client1:~$ ping ynov.com
PING ynov.com (104.26.11.233) 56(84) bytes of data.
64 bytes from 104.26.11.233: icmp_seq=1 ttl=45 time=48.1 ms
64 bytes from 104.26.11.233: icmp_seq=2 ttl=45 time=87.1 ms
64 bytes from 104.26.11.233: icmp_seq=3 ttl=45 time=59.1 ms
64 bytes from 104.26.11.233: icmp_seq=4 ttl=45 time=37.3 ms
^C
--- ynov.com ping statistics ---
5 packets transmitted, 4 received, 20% packet loss, time 4013ms
rtt min/avg/max/mdev = 37.292/57.890/87.064/18.529 ms
```
```powershell
hugo@client2:~$ ping ynov.com
PING ynov.com (172.67.74.226) 56(84) bytes of data.
64 bytes from 172.67.74.226: icmp_seq=1 ttl=45 time=43.7 ms
64 bytes from 172.67.74.226: icmp_seq=2 ttl=45 time=39.6 ms
64 bytes from 172.67.74.226: icmp_seq=3 ttl=45 time=57.0 ms
64 bytes from 172.67.74.226: icmp_seq=4 ttl=45 time=173 ms
^C
--- ynov.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3011ms
rtt min/avg/max/mdev = 39.550/78.244/172.704/54.915 ms
```

## 2. Accès internet clients

### **☀️ Prouvez que les clients ont un accès internet**

```powershell
hugo@client1:~$ ping ynov.com
PING ynov.com (104.26.11.233) 56(84) bytes of data.
64 bytes from 104.26.11.233: icmp_seq=1 ttl=45 time=48.1 ms
64 bytes from 104.26.11.233: icmp_seq=2 ttl=45 time=87.1 ms
64 bytes from 104.26.11.233: icmp_seq=3 ttl=45 time=59.1 ms
64 bytes from 104.26.11.233: icmp_seq=4 ttl=45 time=37.3 ms
^C
--- ynov.com ping statistics ---
5 packets transmitted, 4 received, 20% packet loss, time 4013ms
rtt min/avg/max/mdev = 37.292/57.890/87.064/18.529 ms
```
```powershell
hugo@client2:~$ ping ynov.com
PING ynov.com (172.67.74.226) 56(84) bytes of data.
64 bytes from 172.67.74.226: icmp_seq=1 ttl=45 time=43.7 ms
64 bytes from 172.67.74.226: icmp_seq=2 ttl=45 time=39.6 ms
64 bytes from 172.67.74.226: icmp_seq=3 ttl=45 time=57.0 ms
64 bytes from 172.67.74.226: icmp_seq=4 ttl=45 time=173 ms
^C
--- ynov.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3011ms
rtt min/avg/max/mdev = 39.550/78.244/172.704/54.915 ms
```

### **☀️ Montrez-moi le contenu final du fichier de configuration de l'interface réseau**

```powershell
hugo@client2:~$ cat /etc/netplan/01-netcfg.yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s8:
      dhcp4: no
      addresses: [10.5.1.12/24]
      gateway4: 10.5.1.254
      nameservers:
        addresses: [1.1.1.1]
```

# III. Serveur SSH

### **☀️ Sur routeur.tp5.b1, déterminer sur quel port écoute le serveur SSH**

```powershell
[hugo@routeur ~]$ sudo ss -lnpt | grep 22
LISTEN 0      128          0.0.0.0:22        0.0.0.0:*    users:(("sshd",pid=701,fd=3))
LISTEN 0      128             [::]:22           [::]:*    users:(("sshd",pid=701,fd=4))
```

### **☀️ Sur routeur.tp5.b1, vérifier que ce port est bien ouvert**

```powershell
[hugo@routeur ~]$ sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s3 enp0s8
  sources:
  services: cockpit dhcpv6-client ssh
  ports: 22/tcp
  protocols:
  forward: yes
  masquerade: yes
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
```
# IV. Serveur DHCP

## 3. Rendu attendu

### **☀️ Installez et configurez un serveur DHCP sur la machine routeur.tp5.b1**

```powershell
[root@routeur hugo]# dnf -y install dhcp-server
```
```powershell
[root@routeur hugo]# sudo nano /etc/dhcp/dhcpd.conf
```
```powershell
[root@routeur hugo]# systemctl enable --now dhcpd
```
```powershell
[root@routeur hugo]# cat /etc/dhcp/dhcpd.conf
option domain-name-servers     1.1.1.1;

subnet 10.5.1.0 netmask 255.255.255.0 {
        range dynamic-bootp 10.5.1.137 10.5.1.237;
        option broadcast-address 10.5.1.255;
        option routers 10.5.1.254;
}
``` 
# B. Test avec un nouveau client

### **☀️ Créez une nouvelle machine client client3.tp5.b1**

```powershell
matheo@client3:~$ sudo hostnamectl set-hostname client3.tp5.b1
```
```powershell
root@client3:/home/matheo# sudo nano /etc/netplan/01-netcfg.yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s8:
      dhcp4: yes
```
```powershell
root@client3:/home/matheo# ip a
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:9d:f6:3e brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.137/24 brd 10.5.1.255 scope global dynamic noprefixroute enp0s8
       valid_lft 42768sec preferred_lft 42768sec
    inet6 fe80::a00:27ff:fe9d:f63e/64 scope link
       valid_lft forever preferred_lft forever
```
```powershell
matheo@client3:~$ ping instagram.com
PING instagram.com (157.240.243.174) 56(84) bytes of data.
64 bytes from instagram-p42-shv-01-bcn1.fbcdn.net (157.240.243.174): icmp_seq=1 ttl=50 time=40.7 ms
64 bytes from instagram-p42-shv-01-bcn1.fbcdn.net (157.240.243.174): icmp_seq=2 ttl=50 time=42.0 ms
64 bytes from instagram-p42-shv-01-bcn1.fbcdn.net (157.240.243.174): icmp_seq=3 ttl=50 time=41.2 ms
^C
--- instagram.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2009ms
rtt min/avg/max/mdev = 40.650/41.258/41.971/0.544 ms
```

### **☀️ Consultez le bail DHCP qui a été créé pour notre client**

```powershell
[root@routeur dhcpd]# cat dhcpd.leases
# The format of this file is documented in the dhcpd.leases(5) manual page.
# This lease file was written by isc-dhcp-4.4.2b1

# authoring-byte-order entry is generated, DO NOT DELETE
authoring-byte-order little-endian;

server-duid "\000\001\000\001.\241\003\250\010\000'\227\336\217";

lease 10.5.1.137 {
  starts 2 2024/10/15 10:59:25;
  ends 2 2024/10/15 22:59:25;
  cltt 2 2024/10/15 10:59:25;
  binding state active;
  next binding state free;
  rewind binding state free;
  hardware ethernet 08:00:27:9d:f6:3e;
  uid "\001\010\000'\235\366>";
  client-hostname "client3";
}
```






