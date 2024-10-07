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

### **🌞 Sur le PC serveur**

```powershell
PS C:\Users\hugos\Downloads\netcat-win32-1.11\netcat-1.11> .\nc.exe -l -p 7777
cc
hoo
Tous va bien ?
ouiii
```

```powershell
PS C:\Users\hugos\Downloads\netcat-win32-1.11\netcat-1.11> .\nc.exe 10.10.10.10 7777
hugo
c moi
yooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo
ooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo
Tes sur ?
non
```

### **🌞 Sur le PC serveur toujours**

```powershell
TCP    10.10.10.54:139        0.0.0.0:0              LISTENING
 Can not obtain ownership information
```

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

