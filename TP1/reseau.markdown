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