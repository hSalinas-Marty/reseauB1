# I. Récolte d'informations

### **🌞 Adresses IP de ta machine**

```powershell
PS C:\Users\hugos> ipconfig

Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Adresse IPv6 de liaison locale. . . . .: fe80::54fa:110f:881f:356f%7
   Adresse IPv4. . . . . . . . . . . . . .: 10.33.77.208
   Masque de sous-réseau. . . . . . . . . : 255.255.240.0
   Passerelle par défaut. . . . . . . . . : 10.33.79.254
```

```powershell
PS C:\Users\hugos> ipconfig /all

Carte Ethernet Ethernet :

   Statut du média. . . . . . . . . . . . : Média déconnecté
   Suffixe DNS propre à la connexion. . . :
   Description. . . . . . . . . . . . . . : Realtek PCIe GbE Family Controller
   Adresse physique . . . . . . . . . . . : A0-36-BC-6B-BF-62
   DHCP activé. . . . . . . . . . . . . . : Oui
   Configuration automatique activée. . . : Oui

```

### **🌞 Si t'as un accès internet normal, d'autres infos sont forcément dispos...**

```powershell
PS C:\Users\hugos> ipconfig /all

Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Description. . . . . . . . . . . . . . : MediaTek Wi-Fi 6 MT7921 Wireless LAN Card
   Adresse physique . . . . . . . . . . . : 50-5A-65-50-4A-C9
   DHCP activé. . . . . . . . . . . . . . : Oui
   Configuration automatique activée. . . : Oui
   Adresse IPv6 de liaison locale. . . . .: fe80::54fa:110f:881f:356f%7(préféré)
   Adresse IPv4. . . . . . . . . . . . . .: 10.33.77.208(préféré)
   Masque de sous-réseau. . . . . . . . . : 255.255.240.0
   Bail obtenu. . . . . . . . . . . . . . : vendredi 27 septembre 2024 08:42:58
   Bail expirant. . . . . . . . . . . . . : samedi 28 septembre 2024 08:42:58
   Passerelle par défaut. . . . . . . . . : 10.33.79.254
   Serveur DHCP . . . . . . . . . . . . . : 10.33.79.254
   IAID DHCPv6 . . . . . . . . . . . : 122706533
   DUID de client DHCPv6. . . . . . . . : 00-01-00-01-2B-A5-7E-61-A0-36-BC-6B-BF-62
   Serveurs DNS. . .  . . . . . . . . . . : 8.8.8.8
                                       1.1.1.1
   NetBIOS sur Tcpip. . . . . . . . . . . : Activé
```
### **🌟 BONUS : Détermine s'il y a un pare-feu actif sur ta machine**
```powershell
PS C:\Users\hugos> Get-NetFirewallProfile | ft Name,Enabled

Name    Enabled
----    -------
Domain     True
Private    True
Public     True
```

```powershell
PS C:\Users\hugos> Get-NetFirewallRule
Name                          : WFDPRINT-SPOOL-Out-Active
DisplayName                   : Utilisation de spouleur Wi-Fi Direct (Sortie)
Description                   : Règle de trafic sortant relative à l’utilisation d’imprimantes WSD sur des réseaux
                                Wi-Fi Direct.
DisplayGroup                  : Découverte de réseau Wi-Fi Direct
Group                         : @FirewallAPI.dll,-36851
Enabled                       : True
Profile                       : Public
Platform                      : {}
Direction                     : Outbound
Action                        : Allow
EdgeTraversalPolicy           : Block
LooseSourceMapping            : False
LocalOnlyMapping              : False
Owner                         :
PrimaryStatus                 : OK
Status                        : La règle a été analysée à partir de la banque. (65536)
EnforcementStatus             : NotApplicable
PolicyStoreSource             : PersistentStore
PolicyStoreSourceType         : Local
RemoteDynamicKeywordAddresses : {}
PolicyAppId                   :
```

# II. Utiliser le réseau

### **🌞 Envoie un ping vers...**
```powershell
PS C:\Users\hugos> ping 10.33.77.208

Envoi d’une requête 'Ping'  10.33.77.208 avec 32 octets de données :
Réponse de 10.33.77.208 : octets=32 temps<1ms TTL=128
Réponse de 10.33.77.208 : octets=32 temps<1ms TTL=128
Réponse de 10.33.77.208 : octets=32 temps<1ms TTL=128
Réponse de 10.33.77.208 : octets=32 temps<1ms TTL=128

Statistiques Ping pour 10.33.77.208:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms

```
```powershell
PS C:\Users\hugos> ping 127.0.0.1

Envoi d’une requête 'Ping'  127.0.0.1 avec 32 octets de données :
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128

Statistiques Ping pour 127.0.0.1:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms
```

### **🌞 On continue avec ping. Envoie un ping vers...**
```powershell
PS C:\Users\hugos> ping 10.33.79.254

Envoi d’une requête 'Ping'  10.33.79.254 avec 32 octets de données :
Délai d’attente de la demande dépassé.
Délai d’attente de la demande dépassé.
Délai d’attente de la demande dépassé.
Délai d’attente de la demande dépassé.

Statistiques Ping pour 10.33.79.254:
    Paquets : envoyés = 4, reçus = 0, perdus = 4 (perte 100%),
```
```powershell
PS C:\Users\hugos> ping 10.33.77.164

Envoi d’une requête 'Ping'  10.33.77.164 avec 32 octets de données :
Réponse de 10.33.77.164 : octets=32 temps=5 ms TTL=128
Réponse de 10.33.77.164 : octets=32 temps=5 ms TTL=128
Réponse de 10.33.77.164 : octets=32 temps=6 ms TTL=128
Réponse de 10.33.77.164 : octets=32 temps=6 ms TTL=128

Statistiques Ping pour 10.33.77.164:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 5ms, Maximum = 6ms, Moyenne = 5ms
```
```powershell
PS C:\Users\hugos> ping instagram.com

Envoi d’une requête 'ping' sur instagram.com [185.60.219.174] avec 32 octets de données :
Réponse de 185.60.219.174 : octets=32 temps=9 ms TTL=55
Réponse de 185.60.219.174 : octets=32 temps=10 ms TTL=55
Réponse de 185.60.219.174 : octets=32 temps=10 ms TTL=55
Réponse de 185.60.219.174 : octets=32 temps=10 ms TTL=55

Statistiques Ping pour 185.60.219.174:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 9ms, Maximum = 10ms, Moyenne = 9ms
```
### **🌞 Faire une requête DNS à la main**
```powershell
PS C:\Users\hugos> nslookup www.thinkerview.com
Serveur :   dns.google
Address:  8.8.8.8

Réponse ne faisant pas autorité :
Nom :    www.thinkerview.com
Addresses:  2a06:98c1:3121::7
          2a06:98c1:3120::7
          188.114.96.7
          188.114.97.7

PS C:\Users\hugos> nslookup www.wikileaks.org
Serveur :   dns.google
Address:  8.8.8.8

Réponse ne faisant pas autorité :
Nom :    wikileaks.org
Addresses:  51.159.197.136
          80.81.248.21
Aliases:  www.wikileaks.org

PS C:\Users\hugos> nslookup www.torproject.org
Serveur :   dns.google
Address:  8.8.8.8

Réponse ne faisant pas autorité :
Nom :    www.torproject.org
Addresses:  2a01:4f9:c010:19eb::1
          2a01:4f8:fff0:4f:266:37ff:feae:3bbc
          2620:7:6002:0:466:39ff:fe32:e3dd
          2620:7:6002:0:466:39ff:fe7f:1826
          2a01:4f8:fff0:4f:266:37ff:fe2c:5d19
          116.202.120.165
          204.8.99.144
          204.8.99.146
          116.202.120.166
          95.216.163.36
```

# III. Sniffer le réseau

### **🌞 J'attends dans le dépôt git de rendu un fichier ping.pcap**

_voir ping.pcap_

### **🌞 Livrez un deuxième fichier : dns.pcap**

_voir dns.pcap_

# IV. Network scanning et adresses IP

### **🌞 Effectue un scan du réseau auquel tu es connecté**

```powershell
PS C:\Users\hugos> nmap -sn -PR 192.168.1.0/24
Starting Nmap 7.95 ( https://nmap.org ) at 2024-10-06 19:48 Romance Daylight Time
Nmap scan report for lan.home (192.168.1.1)
Host is up (0.012s latency).
MAC Address: 58:1D:D8:28:24:60 (Sagemcom Broadband SAS)
Nmap scan report for 192.168.1.10
Host is up (0.0050s latency).
MAC Address: 58:68:7A:51:9D:C1 (Sagemcom Broadband SAS)
Nmap scan report for iphone-victor.home (192.168.1.13)
Host is up (0.27s latency).
MAC Address: 9E:C9:83:C4:6F:60 (Unknown)
Nmap scan report for repeteurwifi6-56c0.home (192.168.1.16)
Host is up (0.0050s latency).
MAC Address: 2C:93:FB:55:56:C0 (Sercomm France Sarl)
Nmap scan report for pc-9.home (192.168.1.20)
Host is up (0.26s latency).
MAC Address: 6A:3B:B2:98:E5:C4 (Unknown)
Nmap scan report for mini-de-bruno.home (192.168.1.21)
Host is up (0.35s latency).
MAC Address: 6C:96:CF:F1:C3:A6 (Apple)
Nmap scan report for repeteurwifi6.home (192.168.1.22)
Host is up (0.010s latency).
MAC Address: 2C:93:FB:55:45:40 (Sercomm France Sarl)
Nmap scan report for macbooknsempere.home (192.168.1.29)
Host is up (0.28s latency).
MAC Address: A4:5E:60:D2:4C:FF (Apple)
Nmap scan report for macbook-pro-de-maylis.home (192.168.1.33)
Host is up (0.26s latency).
MAC Address: 10:9F:41:C6:74:4F (Apple)
Nmap scan report for pc-de-hugo.home (192.168.1.17)
Host is up.
Nmap done: 256 IP addresses (10 hosts up) scanned in 18.13 seconds
```

