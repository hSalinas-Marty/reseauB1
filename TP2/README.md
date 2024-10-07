# 1. Quelques pings

### **🌞 Prouvez que votre configuration est effective**

```powershell
PS C:\WINDOWS\system32> Get-NetIPAddress -InterfaceAlias "Ethernet"


IPAddress         : fe80::d8e9:e054:70f9:dc13%10
InterfaceIndex    : 10
InterfaceAlias    : Ethernet
AddressFamily     : IPv6
Type              : Unicast
PrefixLength      : 64
PrefixOrigin      : WellKnown
SuffixOrigin      : Link
AddressState      : Preferred
ValidLifetime     :
PreferredLifetime :
SkipAsSource      : False
PolicyStore       : ActiveStore

IPAddress         : 10.10.10.54
InterfaceIndex    : 10
InterfaceAlias    : Ethernet
AddressFamily     : IPv4
Type              : Unicast
PrefixLength      : 24
PrefixOrigin      : Manual
SuffixOrigin      : Manual
AddressState      : Preferred
ValidLifetime     :
PreferredLifetime :
SkipAsSource      : False
PolicyStore       : ActiveStore
```

### **🌞 Tester que votre LAN + votre adressage IP est fonctionnel**

```powershell
PS C:\WINDOWS\system32> ping 10.10.10.10

Pinging 10.10.10.10 with 32 bytes of data:
Reply from 10.10.10.10: bytes=32 time<1ms TTL=128
Reply from 10.10.10.10: bytes=32 time<1ms TTL=128
Reply from 10.10.10.10: bytes=32 time<1ms TTL=128
Reply from 10.10.10.10: bytes=32 time<1ms TTL=128

Ping statistics for 10.10.10.10:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
```

### **🌞 Capture de ping**

_voir ping.pcap_

# II. Utilisation des ports

### **🌞 Sur le PC client**

```powershell
PS C:\Users\hugos\Downloads\netcat-win32-1.11\netcat-1.11> .\nc.exe 10.10.10.10 8888
```

### **🌞 Echangez-vous des messages**

```powershell
hello
yo bonjour
non
```

### **🌞 Utilisez une commande qui permet de voir la connexion en cours**

```powershell
TCP    10.10.10.54:6611       10.10.10.10:8888       ESTABLISHED
 [nc.exe]
 ```

### **🌞 Faites une capture Wireshark complète d'un échange**

_voir netcat1.pcap_

### **🌞 Inversez les rôles**

### **🌞 Sur le PC serveur**

```powershell
PS C:\Users\hugos\Downloads\netcat-win32-1.11\netcat-1.11> .\nc.exe -l -p 7777
cc
hoo
Tous va bien ?
ouiii
```

### **🌞 Sur le PC serveur toujours**

```powershell
TCP    10.10.10.54:139        0.0.0.0:0              LISTENING
 Can not obtain ownership information
```

### **🌞 Utilisez une commande qui permet de voir la connexion en cours**

```powershell
TCP    10.10.10.54:7777       10.10.10.10:4763       ESTABLISHED
 [nc.exe]
 ```

### **🌞 Faites une capture Wireshark complète d'un échange**

_voir netcat2.pcap_

# III. Analyse de vos applications usuelles

### **1. Serveur web**

_voir http.pcap_

### **2. Autres services**


Spotify (service1.pcap) : 
```powershell
TCP    10.33.77.208:56490     199.232.210.250:443    ESTABLISHED
 [Spotify.exe]
 ```

Discord (service2.pcap) :
```powershell
TCP    10.33.77.208:56162     162.159.135.234:443    ESTABLISHED
 [Discord.exe]
```

Word (service3.pcap) :
```powershell
TCP    192.168.1.17:52775     104.85.28.254:443      ESTABLISHED
 [WINWORD.EXE]
```

Epic Games (service4.pcap) :
```powershell
TCP    192.168.1.17:52930     18.232.239.118:443     ESTABLISHED
 [EpicGamesLauncher.exe]
```
